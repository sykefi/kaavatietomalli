---
layout: "default"
title: "Kaavatietomalli - PostgreSQL-tietokanta"
description: ""
id: "kaava-postgre"
status: "Ehdotus"
---
# PostgreSQL/PostGIS -tietokanta

[Yleis- ja asemakaavan tietomallit -projektissa](../../../projektit/ak-yk-tietomallit/) laadittiin 
[loogisen tason Kaavatietomallin](../../looginenmalli/dokumentaatio/) mukainen PostgreSQL-tietokanta [Kaava-JSON](../json/)-formaatissa olevien kaavojen testaamiseksi. Testauksessa käytettiin PostgreSQL-tietokannanhallintajärjestelmän versiota 13. Valittu tietokantarakenne perustui siihen, että kaavatiedot tallennetaan GeoJSON-formaatissa, ja siinä hyödynnettiin PostgreSQL:n [PostGIS](https://postgis.net/)-geometriatukea ja JSON-tukea. Testauksessa käytetty aineisto on kuvattu [omalla sivullaan](../../../projektit/ak-yk-tietomallit/aineistot/).

Tietokantauluina mallinnettiin seuraavat loogisen tietomallin luokat:
* [Kaavatiedot::Kaava](../../looginenmalli/dokumentaatio/#kaava): ```spatial_plan```,
* [Kaavakohde](../../looginenmalli/dokumentaatio/#kaavakohde): ```plan_regulation_object``` ja
* [Kaavamaarays](../../looginenmalli/dokumentaatio/#kaavamaarays): ```plan_regulation```.

Lisäksi kantaan luotiin taulu ```feature_collection```, johon tallennettiin kokonainen kaava kaikkine kaavakohteineen ja -määräyksineen.

Tietokantaan ei mallinnettu seuraavia testauksen ulkopuolelle jätettyjä loogisen tietomallin luokkia:
* [MKP-ydin::Asiakirja](../../looginenmalli/dokumentaatio/#asiakirja)
* [MKP-ydin::Lahtotietoaineisto](../../looginenmalli/dokumentaatio/#lahtotietoaineisto)
* [MKP-ydin::Kasittelytapahtuma](../../looginenmalli/dokumentaatio/#kasittelytapahtuma)
* [MKP-ydin::Vuorovaikutustapahtuma](../../looginenmalli/dokumentaatio/#vuorovaikutustapahtuma)
* [MKP-ydin::HallinnollinenAlue](../../looginenmalli/dokumentaatio/#hallinnollinenalue)
* [MKP-ydin::Organisaatio](../../looginenmalli/dokumentaatio/#organisaatio)
* [Kaavatiedot::Kaavaselostus](../../looginenmalli/dokumentaatio/#kaavaselostus)
* [Kaavatiedot::OsallistumisJaArviointisuunnitelma](../../looginenmalli/dokumentaatio/#osallistumisjaarviointisuunnitelma)
* [Kaavatiedot::KaavanLaatija](../../looginenmalli/dokumentaatio/#kaavanlaatija)
* [Kaavatiedot::Kaavasuositus](../../looginenmalli/dokumentaatio/#kaavasuositus)

Pois jätettyjen luokkien mallintamisessa ei nähdä mitään erityisiä haasteita, mutta niiden mukaisten testausaineistojen tuottaminen käsin käytössä olleista kaava-aineistoista ei ollut mahdollista projektin aikataulun puitteissa. Loogisen tietomallin tietotyypit (DataType-stereotyyppi) mallinnettiin osana luokkia, jota sisältävät niihin kohdistuvia assosiaatioita.


Tietokannan, taulujen ja näkymien luomiseen käytetyn [luontiskriptin](https://github.com/YM-rakennettu-ymparisto/kaavatietomalli/blob/8a98b21e848c0208de9c384f49f30d3cf664ab73/testaus/postgre/init-user-db.sh) avulla voidaan alustaa PostgreSQL-tietokanta tauluineen ja näkymineen.

{% include common/note.html content="Tietokantamallinnuksessa ei kiinnitetty erityistä huomiota rakenteiden hakutehokkuuteen ja tietojen indeksointiin, koska ensisijaisena tavoitteena oli testata loogisen tietomallin mallinnettavuutta tietokantarakenteena. Mikäli tässä kuvatun tietokantaratkaisun pohjalta luotaisiin operatiiviseen käyttöön soveltuva tietokanta, tulee sen suunnittelussa ottaa huomioon myös ratkaisun suorituskyky." %} 

## Luokkien mallinnus relaatioina
Kaikki neljä tietokantataulua mallinnettiin täsmälleen samalla tavalla: taulujen sarakkeiksi valittiin
* ```id VARCHAR(255) PRIMARY KEY```: taulun pääavain,
* ```created_time TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP```: latausaika,
* ```properties JSONB NOT NULL```: koko kohteen GeoJSON-properties -objekti
* ```geom geometry NOT NULL```: kohteen geometria

Geometriatietoa lukuunottamatta kaikki loogisen tietomallin mukainen tietosisältö kuvattiin siis suoraan [JSONB](https://www.postgresql.org/docs/current/datatype-json.html)-saraketyypin avulla, jolloin kunkin kohteen tietorakennetta ja sisältötyyppejä ei tarvitse kuvata taulurakenteessa yksityiskohtaisesti, vaan JSON-sisältö tallennetaan sellaisenaan sarakkeen arvoksi. Tämä vastaa karkeasti JSON-tiedon tallentamista ns. NoSQL-tietokannoissa (esim. MongoDB), mutta tarjoaa PostGIS:n tehokkaan geometriakäsittelyn.

## JSON-kyselyihin perustuvat näkymät
PostgreSQL:n [JSON-kyselyfuntiot](https://www.postgresql.org/docs/current/functions-json.html) mahdollistavat tietokantakyselyt myös JSONB-sarakkeiden sisärakenteeseen, mitä hyödynnettiin nostamalla kunkin kohdetyypin Kaava-JSON -tietorakennettava vastaavat tiedot näkymien sarakkeiksi seuraavasti:

```sql
CREATE VIEW public.v_spatial_plan AS
        SELECT
            id,
            created_time AS "_createdTime",
            properties::jsonb->>'identityId' AS "identityId",
            properties::jsonb->>'versionId' AS "versionId",
            properties::jsonb->>'localId' AS "localId",
            properties::jsonb->>'latestChange' AS "latestChange",
            properties::jsonb->>'planId' AS "planId",
            properties::jsonb->'planType'->>'code' AS "planTypeCode",
            properties::jsonb->'planType'->'title'->>'fin' AS "planTypeTitle",
            properties::jsonb->'name'->>'fin' AS "name",
            properties::jsonb->'description'->>'fin' AS "description",
            properties::jsonb->'planObjects' AS "planObjects",
            properties::jsonb->'generalRegulations' AS "generalRegulations",
            properties::jsonb->'administrativeAreaIds' AS "administrativeAreaIds",
            properties::jsonb->'legalEffectiveness'->>'code' AS "legalEffectivenessCode",
            properties::jsonb->'legalEffectiveness'->'title'->>'fin' AS "legalEffectivenessTitle",
            properties::jsonb->'usedInputDatasets' AS "usedInputDatasets",
            properties::jsonb->'responsibleOrganisation'->>'linkedFeatureType' AS "responsibleOrganisationLinkedFeatureType",
            properties::jsonb->'responsibleOrganisation'->>'linkedFeatureId' AS "responsibleOrganisationLinkedFeatureId",
            properties::jsonb->'responsibleOrganisation'->>'href' AS "responsibleOrganisationHref",
            properties::jsonb->'responsibleOrganisation'->'title'->>'fin' AS "responsibleOrganisationTitle",
            properties::jsonb->'undergroundness'->>'code' AS "undergroundnessCode",
            properties::jsonb->'undergroundness'->'title'->>'fin' AS "undergroundnessTitle",
            properties::jsonb->'planners' AS "planners",
            properties::jsonb->'planCommentary'->>'linkedFeatureType' AS "planCommentaryLinkedFeatureType",
            properties::jsonb->'planCommentary'->>'linkedFeatureId' AS "planCommentaryLinkedFeatureId",
            properties::jsonb->'planCommentary'->>'href' AS "planCommentaryHref",
            properties::jsonb->'attachments' AS "attachments",
            properties::jsonb->'cancellations' AS "cancellations",
            properties::jsonb->'lifecycleStatus'->>'code' AS "lifecycleStatusCode",
            properties::jsonb->'lifecycleStatus'->'title'->>'fin' AS "lifecycleStatusTitle",
            properties::jsonb->'digitalOrigin'->>'code' AS "digitalOriginCode",
            properties::jsonb->'digitalOrigin'->'title'->>'fin' AS "digitalOriginTitle",
            properties::jsonb->>'metadata' AS "metadata",
            properties::jsonb->>'initiationTime' AS "initiationTime",
            properties::jsonb->>'approvalTime' AS "approvalTime",
            properties::jsonb->>'validFrom' AS "validFrom",
            geom
        FROM data.spatial_plan;
```

```sql
CREATE VIEW public.v_plan_regulation_object AS
        SELECT
            id,
            created_time AS "_createdTime",
            properties::jsonb->>'identityId' AS "identityId",
            properties::jsonb->>'versionId' AS "versionId",
            properties::jsonb->>'localId' AS "localId",
            properties::jsonb->>'latestChange' AS "latestChange",
            properties::jsonb->'spatialPlan'->>'linkedFeatureType' AS "spatialPlanLinkedFeatureType",
            properties::jsonb->'spatialPlan'->>'linkedFeatureId' AS "spatialPlanLinkedFeatureId",
            properties::jsonb->'spatialPlan'->>'href' AS "spatialPlanHref",
            properties::jsonb->'verticalLimits' AS "verticalLimits",
            properties::jsonb->'bindingnessOfLocation'->>'code' AS "bindingnessOfLocationCode",
            properties::jsonb->'bindingnessOfLocation'->'title'->>'fin' AS "bindingnessOfLocationTitle",
            properties::jsonb->'undergroundness'->>'code' AS "undergroundnessCode",
            properties::jsonb->'undergroundness'->'title'->>'fin' AS "undergroundnessTitle",
            properties::jsonb->'regulations' AS "regulations",
            properties::jsonb->'lifecycleStatus'->>'code' AS "lifecycleStatusCode",
            properties::jsonb->'lifecycleStatus'->'title'->>'fin' AS "lifecycleStatusTitle",
            properties::jsonb->>'validFrom' AS "validFrom",
            properties::jsonb->'groundRelativePosition'->>'code' AS "groundRelativePositionCode",
            properties::jsonb->'groundRelativePosition'->'title'->>'fin' AS "groundRelativePositionTitle",
            geom
        FROM data.plan_regulation_object;
```

```sql
CREATE VIEW public.v_plan_regulation AS
        SELECT
            id,
            created_time AS "_createdTime",
            properties::jsonb->>'identityId' AS "identityId",
            properties::jsonb->>'versionId' AS "versionId",
            properties::jsonb->>'localId' AS "localId",
            properties::jsonb->>'latestChange' AS "latestChange",
            properties::jsonb->'spatialPlan'->>'linkedFeatureType' AS "spatialPlanLinkedFeatureType",
            properties::jsonb->'spatialPlan'->>'linkedFeatureId' AS "spatialPlanLinkedFeatureId",
            properties::jsonb->'spatialPlan'->>'href' AS "spatialPlanHref",
            properties::jsonb->'targetObject'->>'linkedFeatureType' AS "targetObjectLinkedFeatureType",
            properties::jsonb->'targetObject'->>'linkedFeatureId' AS "targetObjectLinkedFeatureId",
            properties::jsonb->'targetObject'->>'href' AS "targetObjectHref",
            properties::jsonb->'type'->> 'code' AS "typeCode",
            properties::jsonb->'type'->'title'->> 'fin' AS "typeTitle",
            properties::jsonb->'themes' AS "themes",
            properties::jsonb->'values' AS "values",
            properties::jsonb->'lifecycleStatus'->>'code' AS "lifecycleStatusCode",
            properties::jsonb->'lifecycleStatus'->'title'->>'fin' AS "lifecycleStatusTitle",
            properties::jsonb->>'validFrom' AS "validFrom",
            geom
        FROM data.plan_regulation;
```





