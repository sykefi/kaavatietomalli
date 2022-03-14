---
layout: "default"
title: "Kaavatietomalli - Kaava-JSON"
description: ""
id: "kaava-json"
status: "Ehdotus"
---
# Kaava-JSON
{:.no_toc}

1. 
{:toc}

## Mallinnusperiaatteet
Kaava-JSON on [loogisen tason Kaavatietomallin](../../looginenmalli/dokumentaatio/) toteuttava [GeoJSON](https://tools.ietf.org/html/rfc7946)-formaattiin perustuva fyysinen tietomalli.

Kohdetyypit kuvataan GeoJSON Feature -objekteiksi. GeoJSON-objektin ominaisuuden "properties" alle tulevat kaikki muut tietokohteen loogisen mallin mukaiset ominaisuudet paitsi ```paikallinenTunnus``` (GeoJSON Feature-objektin ```id```) ja geometria-ominaisuudet. Paikkatietokohteiden ensisijainen geometriatieto ilmaistaa GeoJSON-objektin "geometry"-omainaisuutena, ja sen koordinaatisto "crs"-ominaisuutena (ks. [NamedCooodinateReferenceSystem](##namedcooodinatereferencesystem)). Kohteilla, jolla ei ole geometriatietoa "geometry"-ominaisuuden arvoksi tulee aina ```coordinates```-taulukoltaan tyhjä Polygon, jolla ei ole "crs" ominaisuutta.

Kaava-JSON -formaatti ei rajoita koordinaatistojen käyttöä, mutta on hyvä tietää, että GeoJSON-spesifikaation ([IETF RFC 7946](https://www.rfc-editor.org/info/rfc7946)) mukaan GeoJSON-kohteiden koordinaatisto on aina WGS84 (urn:ogc:def:crs:OGC::CRS84), longitudi, latitudi -järjestyksessä. Tuottajien ja käyttäjien yhteisellä ennakkosopimuksella tästä  voidaan spesifikaation mukaan kuitenkin poiketa. Koordinaatistotieto on mallinnettu korvatun GeoJSON draft version 6:n "Named CRS" -rakenteen mukaisesti, ks. <http://wiki.geojson.org/GeoJSON_draft_version_6> (crs-ominaisuus on poistettu uudemmista GeoJSON-spesifikaatioista).


## Kohdetyypit (FeatureType)

### SpatialPlan (Kaava)

Toteuttaa loogisen tietomallin luokan [Kaava](../../looginenmalli/dokumentaatio/#kaava)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type
--------------|-------------------------|-----------------------|------------
[GeoJSON-tyyppi] |                      | type = "Feature"      | string
paikallinenTunnus | CharacterString [0..1]  | id                | string
aluerajaus    | Surface [0..*]          | geometry              |  object (GeoJSON MultiPolygon)
[luokan nimi] |                         | properties.featureType = "SpatialPlan" | string
nimiavaruus   | URI [0..1]              | properties.namespace  | string (uri)
viittausTunnus | URI [0..1]           | properties.referenceId  | string (uri)
identiteettiTunnus | CharacterString [0..1] | properties.identityId   | string
tuottajakohtainenTunnus | CharacterString [0..1]  | properties.producerSpecificId | string
viimeisinMuutos | TM_Instant [0..1]     | properties.latestChange | string (date-time)
tallennusAika | TM_Instant [0..1]       | properties.storageTime | string (date-time)
nimi             | LanguageString [0..*]| properties.name                  | object (LanguageString)
kuvaus           | LanguageString [0..*] | properties.description           | object (LanguageString)
oikeusvaikutteisuus | OikeusvaikutteisuudenLaji [0..1] | properties.legalEffectiveness | object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_OikeusvaikutteisuudenLaji>
metatietokuvaus | URI [0..1]            | properties.metadata              | string (uri)
voimassaoloAika | TM_Period [0..1]      | properties.validFrom, properties.validTo | string (date-time)
laji            | Kaavalaji             | properties.type          | object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_Kaavalaji>
kaavatunnus     | URI                   | properties.spatialPlanId | string (uri)
elinkaaritila   | KaavanElinkaaritila   | properties.lifecycleStatus | object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaaritila>
kumoamistieto   | KaavanKumoamistieto [0..*] | properties.cancellations | object (CancellationInfo)
maanalaisuus    | MaanalaisuudenLaji [0..1] | properties.groundRelativePosition | object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_MaanalaisuudenLaji>
virelletuloaika | TM_Instant [0..1]     | properties.initiationTime | string (date)
hyvaksymisaika  | TM_Instant [0..1]     | properties.approvalTime | string (date)
digitaalinenAlkupera | DigitaalinenAlkupera [0..1] | properties.digitalOrigin | object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_DigitaalinenAlkupera>

**Assosiaatiot**

Nimi          | UML tyyppi              | JSON property name    | JSON type
--------------|-------------------------|-----------------------|------------
korvaaObjektin | AbstraktiVersioituObjekti[0..*] | properties.replacesObjects | array of object (FeatureLink)
korvattuObjektilla | AbstraktiVersioituObjekti[0..*] | properties.replacedByObjects | array of object (FeatureLink)
vastuullinenOrganisaatio | Organisaatio[0..1] | properties.responsibleOrganisation | object (FeatureLink)
koskeeHallinnollistaAluetta | HallinnollinenAlue [0..*] | properties.administrativeAreas | array of object (FeatureLink)
asianLiite    | Dokumentti [0..*]       | properties.attachments | array of object (FeatureLink)
hyodynnettyAineisto | Lahtotietoaineisto [0..*] | properties.usedInputDatasets | array of object (FeatureLink)
liittyvaAsia  | AbstraktiMaankayttoasia [0..*]  | properties.relatedMatters | array of object (FeatureLink)
selostus      | Kaavaselostus [0..1]    | properties.spatialPlanCommentary | object (FeatureLink)
osallistumisJaArviointisuunnitelma      | OsallistumisJaArviontisuunnitelma [0..1]    | properties.participationAndEvalutionPlan | object (FeatureLink)
laatija       | KaavanLaatija [0..*]    | properties.planners   | array of object (FeatureLink)
kaavakohde | Kaavakohde [0..*] | properties.planObjects | array of object (FeatureLink)
yleismaarays  | Kaavamaarays [0..*]     | properties.generalRegulations | array of object (FeatureLink)
yleissuositus  | Kaavasuositus [0..*]     | properties.generalGuidances | array of object (FeatureLink)

**Esimerkki**

```json
{
        "id" : "9c97e469-083d-4284-90a9-3dbebdfe5622.23",
        "type" : "Feature",
        "geometry" : {
            "type" : "MultiPolygon",
            "coordinates" : [ ]
        },
        "crs" : {
            "type" : "name",
            "properties" : {
                "name" : "http://www.opengis.net/def/crs/EPSG/0/3067"
            }
        },
        "properties" : {
            "featureType": "SpatialPlan",
            "identityId": "9c97e469-083d-4284-90a9-3dbebdfe5622",
            "namespace": "http://uri.suomi.fi/object/rytj/kaava",
            "referenceId": "http://uri.suomi.fi/object/rytj/kaava/SpatialPlan/9c97e469-083d-4284-90a9-3dbebdfe5622.23",
            "producerSpecificId": "somelocalstuff-id123445",
            "latestChange": "2020-01-01T13:00:00Z",
            "storageTime": "2020-01-01T13:00:00Z",
            "planId": "http://uri.suomi.fi/object/rytj/kaava/SpatialPlan/9c97e469-083d-4284-90a9-3dbebdfe5622",
            "planType": {
                "code": "http://uri.suomi.fi/codelist/rytj/RY_Kaavalaji/code/31",
                "title": {
                    "fin": "Asemakaava"
                }
            },
            "name": {
                "fin": "Asemakaava X"
            },
            "description": {
                "fin": "Kuvaustekstiä"
            },
            "administrativeAreas": [
                 {
                    "linkedFeatureType": "AdministrativeArea",
                    "linkedFeatureId": "ee30bab5-ff5f-44b1-bb64-cede4fcde85e.1",
                    "href": "https://rytj.fi/api/yleinen/AdministrativeArea/ee30bab5-ff5f-44b1-bb64-cede4fcde85e.1",
                    "title": {
                        "fin": "Kaupunki X"
                    }
                }
            ],
            "legalEffectiveness": {
                "code": "http://uri.suomi.fi/codelist/rytj/RY_OikeusvaikutteisuudenLaji/code/01",
                "title": {
                    "fin": "Oikeusvaikutteinen"
                }
            },
            "usedInputDatasets": [
                {
                    "linkedFeatureType": "InputDataset",
                    "linkedFeatureId": "c4cee4eb-c4da-4441-88a3-20239f513f19.5",
                    "href": "https://rytj.fi/api/kaava/InputDataset/c4cee4eb-c4da-4441-88a3-20239f513f19.5",
                    "title": {
                        "fin": "Kaupungin X kantakartta-aineisto"
                    }
                }
            ],
            "responsibleOrganisation": {
                 "linkedFeatureType": "Organisation",
                 "linkedFeatureId": "e0fb82f9-be21-44f7-9caf-f565270c7f90/.34",
                 "href": "https://rytj.fi/api/yleinen/Organisation/e0fb82f9-be21-44f7-9caf-f565270c7f90.34",
                 "title": {
                     "fin": "Kaupunki X"
                }
            },
            "groundRelativePosition": {
                "code": "http://uri.suomi.fi/codelist/rytj/RY_MaanalaisuudenLaji/code/02",
                "title": {
                    "fin": "Maanpäällinen"
                }
            },
            "planners": [
                {
                    "linkedFeatureType": "Planner",
                    "linkedFeatureId": "391debf8-3d07-4a31-9854-17b90c86abb5.64",
                    "href": "https://rytj.fi/api/kaava/Planner/391debf8-3d07-4a31-9854-17b90c86abb5.64"
                }
            ],
            "planCommentary": {
                "linkedFeatureType": "SpatialPlanCommentary",
                "linkedFeatureId": "52b9cb68-7e00-4e09-976e-5be94730fb81.5",
                "href": "https://rytj.fi/api/kaava/SpatialPlanCommentary/52b9cb68-7e00-4e09-976e-5be94730fb81.5"
            },
             "participationAndEvaluationPlan": {
                "linkedFeatureType": "ParticipationAndEvaluationPlan",
                "linkedFeatureId": "3298d1ce-8486-4d83-89b0-e2e44d786d09.12",
                "href": "https://rytj.fi/api/kaava/ParticipationAndEvaluationPlan/3298d1ce-8486-4d83-89b0-e2e44d786d09.12"
            },
            "attachments": [
                {
                    "linkedFeatureType": "Document",
                    "linkedFeatureId": "640bff6b-c16a-4947-af8d-d86f89106be1.1",
                    "href": "https://rytj.fi/api/kaava/Document/640bff6b-c16a-4947-af8d-d86f89106be1.1",
                    "title": {
                        "fin": "Kaavakartta"
                    }
                }
            ],
            "planObjects": [
                {
                    "linkedFeatureType": "PlanObject",
                    "linkedFeatureId": "6d32ca64-9a8d-44bb-9702-e46c228add64.76",
                    "href": "https://rytj.fi/api/kaava/PlanObject/6d32ca64-9a8d-44bb-9702-e46c228add64.76"
                }
            ],
            "generalRegulations": [
                {
                    "linkedFeatureType": "PlanRegulation",
                    "linkedFeatureId": "5615b954-e8fc-4996-9d7a-caef5d495ef3.1",
                    "href": "https://rytj.fi/api/kaava/PlanRegulation/5615b954-e8fc-4996-9d7a-caef5d495ef3.1"
                }
            ],
             "generalGuidance": [
                {
                    "linkedFeatureType": "PlanGuidance",
                    "linkedFeatureId": "a7e688ad-4352-4a1e-b22b-b0db1797165d.32",
                    "href": "https://rytj.fi/api/kaava/PlanGuidance/a7e688ad-4352-4a1e-b22b-b0db1797165d.32"
                }
            ],
            "lifecycleStatus": {
                "code": "http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaaritila/code/06",
                "title": {
                    "fin": "Hyväksytty kaava"
                }
            },
            "digitalOrigin": {
                "code": "http://uri.suomi.fi/codelist/rytj/RY_DigitaalinenAlkupera/code/01",
                "title": {
                    "fin": "Tietomallin mukaan laadittu"
                }
            },
            "metadata": "",
            "initiationTime": "2018-03-01",
            "approvalTime": "2020-03-02",
            "validFrom": "2020-05-01T00:00:00Z",
        }
    }
```

### Document (Asiakirja)
Toteuttaa loogisen tietomallin luokan [Asiakirja](../../looginenmalli/dokumentaatio/#asiakirja).

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type
--------------|-------------------------|-----------------------|------------
[GeoJSON-tyyppi] |                      | type = "Feature"      | string
paikallinenTunnus | CharacterString [0..1]  | id                | string
              |                         | geometry              | object (tyhjä GeoJSON Polygon)
[luokan nimi] |                         | properties.featureType = "Document" | string
nimiavaruus   | URI [0..1]              | properties.namespace  | string (uri)
viittausTunnus | URI [0..1]           | properties.referenceId  | string (uri)
identiteettiTunnus | CharacterString [0..1] | properties.identityId   | string
tuottajakohtainenTunnus | CharacterString [0..1]  | properties.producerSpecificId | string
viimeisinMuutos | TM_Instant [0..1]     | properties.latestChange | string (date-time)
tallennusAika | TM_Instant [0..1]       | properties.storageTime | string (date-time)
asiakirjanTunnus | URI [0..*]           | properties.documentId            | array of string (uri)
nimi             | LanguageString [0..*]| properties.name                  | object (LanguageString)
laji             | AsiakirjanLaji       | properties.type                  | object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_AsiakirjanLaji_YKAK>
lisatietolinkki  | URI [0..1]           | properties.externalInformationLink | string (uri)
metadatakuvaus   | URI [0..1]           | properties.metadata              | string (uri)

*Assosiaatiot**

Nimi          | UML tyyppi              | JSON property name    | JSON type
--------------|-------------------------|-----------------------|------------
korvaaObjektin | AbstraktiVersioituObjekti[0..*] | properties.replacesObjects | array of object (FeatureLink)
korvattuObjektilla | AbstraktiVersioituObjekti[0..*] | properties.replacedByObjects | array of object (FeatureLink)
liittyvaAsiakirja | Document[0..*]      | properties.relatedDocuments | array of object (FeatureLink)

**Esimerkki**

```json
    {
        "id" : "640bff6b-c16a-4947-af8d-d86f89106be1.1",
        "type" : "Feature",
        "geometry" : {
            "type" : "Polygon",
            "coordinates" : [ ]
        },
        "properties": {
            "featureType": "Document",
            "identityId": "640bff6b-c16a-4947-af8d-d86f89106be1",
            "namespace": "http://uri.suomi.fi/object/rytj/kaava",
            "referenceId": "http://uri.suomi.fi/object/rytj/kaava/Document/640bff6b-c16a-4947-af8d-d86f89106be1.1",
            "producerSpecificId": "somelocalstuff-idjojodafg9we5794t7",
            "latestChange": "2020-11-06T12:05:00Z",
            "storageTime": "2020-11-06T12:05:00Z",
            "documentId": "",
            "name": { 
                "fin": "Kaavakartta, LAANILAN KAUP,OSAN LIIKENNEAL. JA HINTAN KAUP.OSAN KORTT. 6, 7 JA 39 SEKÄ URH.YM. AL.KOSKEVA AK.MUUTOS SEKÄ AK OSILLE LAANILAN JA HINTAN KAUP.OSIA."
            },
            "type": {
                "code": "http://uri.suomi.fi/codelist/rytj/RY_AsiakirjanLaji_YKAK/code/03",
                "title": {
                    "fin": "Kaavakartta"
                }
            },
            "externalInformationLink": "https://kartta.ouka.fi/viralliset_asemakaavat/ak1643.pdf",
            "metadata": ""
        } 
    }
```

### InputDataset (Lahtotietoaineisto)
Toteuttaa loogisen tietomallin luokan [Lahtotietoaineisto](../../looginenmalli/dokumentaatio/#lahtotietoaineisto)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type
--------------|-------------------------|-----------------------|------------
[GeoJSON-tyyppi] |                      | type = "Feature"      | string
paikallinenTunnus | CharacterString [0..1]  | id                | string
aluerajaus    | Surface[0..*]           | geometry              | object (GeoJSON MultiPolygon)
[luokan nimi] |                         | properties.featureType = "InputDataset" | string
nimiavaruus   | URI [0..1]              | properties.namespace  | string (uri)
viittausTunnus | URI [0..1]           | properties.referenceId  | string (uri)
identiteettiTunnus | CharacterString [0..1] | properties.identityId   | string
tuottajakohtainenTunnus | CharacterString [0..1]  | properties.producerSpecificId | string
viimeisinMuutos | TM_Instant [0..1]     | properties.latestChange | string (date-time)
tallennusAika | TM_Instant [0..1]       | properties.storageTime | string (date-time)
aineistoTunnus   | URI [0..1]           | properties.datasetId             | string (uri)
nimi             | LanguageString [0..*]| properties.name                  | object (LanguageString)
laji             | LahtietoaineistonLaji | properties.type                  | object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_LahtotietoaineistonLaji>
lisatietolinkki  | URI [0..1]           | properties.externalInformationLink | string (uri)
metadatakuvaus   | URI [0..1]           | properties.metadata              | string (uri)

**Assosiaatiot**

Nimi          | UML tyyppi              | JSON property name    | JSON type
--------------|-------------------------|-----------------------|------------
korvaaObjektin | AbstraktiVersioituObjekti[0..*] | properties.replacesObjects | array of object (FeatureLink)
korvattuObjektilla | AbstraktiVersioituObjekti[0..*] | properties.replacedByObjects | array of object (FeatureLink)

**Esimerkki**

```json
{
        "id" : "c4cee4eb-c4da-4441-88a3-20239f513f19.5",
        "type" : "Feature",
        "geometry" : {
            "type" : "MultiPolygon",
            "coordinates" : [ ]
        },
        "crs" : {
            "type" : "name",
            "properties" : {
                "name" : "http://www.opengis.net/def/crs/EPSG/0/3067"
            }
        },
        "properties": {
            "featureType": "InputDataset",
            "identityId": "c4cee4eb-c4da-4441-88a3-20239f513f19",
            "namespace": "http://uri.suomi.fi/object/rytj/kaava",
            "referenceId": "http://uri.suomi.fi/object/rytj/kaava/InputDataset/c4cee4eb-c4da-4441-88a3-20239f513f19.5",
            "producerSpaecificId": "somelocalstuff-id66652385275",
            "latestChange": "2020-01-01T13:00:00Z",
            "storageTime": "2020-01-01T13:00:00Z",
            "datasetId": "",
            "name": {
                "fin": "Kaupungin X kantakartta-aineisto"
            },
            "type": {
                "code": "http://uri.suomi.fi/codelist/rytj/RY_LahtotietoaineistonLaji/code/11",
                "title": {
                    "fin": "Pohjakartta"
                }
            },
            "externalInformationLink": "",
            "metadata": ""
        }  
    }
```
### HandlingEvent (Kasittelytapahtuma)

Toteuttaa loogisen tietomallin luokan [Kasittelytapahtuma](../../looginenmalli/dokumentaatio/#kasittelytapahtuma)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type
--------------|-------------------------|-----------------------|------------
[GeoJSON-tyyppi] |                      | type = "Feature"      | string
paikallinenTunnus | CharacterString [0..1]  | id                | string
sijainti      | Point [0..1]            | geometry              | object (GeoJSON Point)
[luokan nimi] |                         | properties.featureType = "HandlingEvent" | string
nimiavaruus   | URI [0..1]              | properties.namespace  | string (uri)
viittausTunnus | URI [0..1]           | properties.referenceId  | string (uri)
identiteettiTunnus | CharacterString [0..1] | properties.identityId   | string
tuottajakohtainenTunnus | CharacterString [0..1]  | properties.producerSpecificId | string
viimeisinMuutos | TM_Instant [0..1]     | properties.latestChange | string (date-time)
tallennusAika | TM_Instant [0..1]       | properties.storageTime | string (date-time)
nimi             | LanguageString [0..*]| properties.name    | object (LanguageString)
kuvaus           | LanguageString [0..*]| properties.description  | object (LanguageString)
tapahtumaAika    | TM_Object [0..1]     | properties.eventTime, properties.eventTime_start, properties.eventTime_end | string (date-time)
laji             | AbstraktiKasittelytapahtumanLaji | properties.type  | object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_KaavanKasittelytapahtumanLaji>
lisatietolinkki | URI [0..1]            | properties.additionalInformationLink | string (uri)
peruttu       | boolean = false         | cancelled             | boolean

**Assosiaatiot**

Nimi          | UML tyyppi              | JSON property name    | JSON type
--------------|-------------------------|-----------------------|------------
korvaaObjektin | AbstraktiVersioituObjekti[0..*] | properties.replacesObjects | array of object (FeatureLink)
korvattuObjektilla | AbstraktiVersioituObjekti[0..*] | properties.replacedByObjects | array of object (FeatureLink)
liittyvaAsia   | AbstraktiMaankayttoasia[0..*] | properties.relatedMatters    | array of object (FeatureLink)
liittyvaAsiakirja | Asiakirja [0..*]  | properties.relatedDocuments    | array of object (FeatureLink)
kasittelija   | Organisaatio [0..1]     | properties.handler    | object (FeatureLink)

**Esimerkki**

```json
 {
        "id" : "c5e9b3ff-fdfe-4939-8c27-35d4491ffcf6.5",
        "type" : "Feature",
        "geometry" : {
            "type" : "Polygon",
            "coordinates" : [ ]
        },
        "properties": {
            "featureType": "HandlingEvent",
            "identityId": "c5e9b3ff-fdfe-4939-8c27-35d4491ffcf6",
            "namespace": "http://uri.suomi.fi/object/rytj/kaava",
            "referenceId": "http://uri.suomi.fi/object/rytj/kaava/HandlingProcessingEvent/c5e9b3ff-fdfe-4939-8c27-35d4491ffcf6.5",
            "producerSpecificId": "somelocalstuff-idwpi8045jhgi5",
            "latestChange": "2020-01-01T13:00:00Z",
            "storageTime": "2020-01-01T13:00:00Z",
            "type": {
                "code": "http://uri.suomi.fi/codelist/rytj/RY_KaavanKasittelytapahtumanLaji/code/09",
                "title": {
                    "fin": "Kaavan hyväksyminen"
                }
            },
            "name": {
                "fin": "Hyväksyminen kunnanvaltuuston kokouksessa"
            },
            "description": {
                 "fin": "Asemakaava hyväksyttiin esityksen mukaisesti"
            },
            "eventTime": "2020-06-23",
            "relatedMatters": [
                {
                    "linkedFeatureType": "SpatialPlan",
                    "linkedFeatureId": "9c97e469-083d-4284-90a9-3dbebdfe5622.23",
                    "href": "https://rytj.fi/api/kaava/SpatialPlan/9c97e469-083d-4284-90a9-3dbebdfe5622.23",
                    "title": {
                        "fin": "Asemakaava Y"
                    }
                }
            ],
            "handler": {
                "linkedFeatureType": "Organisation",
                "linkedFeatureId": "f2bae809-a8e3-4550-b4a0-71bfad95968a.1",
                "href": "https://rytj.fi/api/kaava/Organisation/f2bae809-a8e3-4550-b4a0-71bfad95968a/1",
                "title": {
                    "fin": "Kunnan X kunnanvaltuusto"
                }
            },
            "relatedDocuments": [
                {
                    "linkedFeatureType": "Document",
                    "linkedFeatureId": "2f0e91bd-bced-4eec-8151-6bd700ebac0e.1",
                    "href": "https://rytj.fi/api/kaava/Document/2f0e91bd-bced-4eec-8151-6bd700ebac0e/1",
                    "title": {
                        "fin": "Valtuuston kokouksen pöytäkirja"
                    }
                }
            ]
        }
    }
```

### InteractionEvent (Vuorovaikutustapahtuma)

Toteuttaa loogisen tietomallin luokan [Vuorovaikutustapahtuma](../../looginenmalli/dokumentaatio/#vuorovaikutustapahtuma)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type
--------------|-------------------------|-----------------------|------------
[GeoJSON-tyyppi] |                      | type = "Feature"      | string
paikallinenTunnus | CharacterString [0..1]  | id                | string
sijainti      | Point [0..1]            | geometry              | object (GeoJSON Point)
[luokan nimi] |                         | properties.featureType = "InteractionEvent" | string
nimiavaruus   | URI [0..1]              | properties.namespace  | string (uri)
viittausTunnus | URI [0..1]           | properties.referenceId  | string (uri)
identiteettiTunnus | CharacterString [0..1] | properties.identityId   | string
tuottajakohtainenTunnus | CharacterString [0..1]  | properties.producerSpecificId | string
viimeisinMuutos | TM_Instant [0..1]     | properties.latestChange | string (date-time)
tallennusAika | TM_Instant [0..1]       | properties.storageTime | string (date-time)
nimi             | LanguageString [0..*]| properties.name    | object (LanguageString)
kuvaus           | LanguageString [0..*]| properties.description  | object (LanguageString)
tapahtumaAika    | TM_Object [0..1]      | properties.eventTime, properties.eventTime_start, properties.eventTime_end | string (date-time)
laji             | AbstraktiVuorovaikutustapahtumaLaji | properties.type  | object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_KaavanVuorovaikutustapahtumanLaji>

lisatietolinkki | URI [0..1]            | properties.additionInformationLink | string (uri)
peruttu       | boolean = false         | cancelled             | boolean
 
**Assosiaatiot**

Nimi          | UML tyyppi              | JSON property name    | JSON type
--------------|-------------------------|-----------------------|------------
korvaaObjektin | AbstraktiVersioituObjekti[0..*] | properties.replacesObjects | array of object (FeatureLink)
korvattuObjektilla | AbstraktiVersioituObjekti[0..*] | properties.replacedByObjects | array of object (FeatureLink)
liittyvaAsia   | AbstraktiMaankayttoasia[0..*] | properties.relatedMatters    | array of object (FeatureLink)
liittyvaAsiakirja | Asiakirja [0..*]  | properties.relatedDocuments    | array of object (FeatureLink)

**Esimerkki**

```json
{
        "id" : "c2001929-6810-4ea4-9b75-4dbde014b358.2",
        "type" : "Feature",
        "geometry" : {
            "type" : "Point",
            "coordinates" : [ 23.0, 65.0 ]
        },
        "properties": {
            "featureType": "InteractionEvent",
            "identityId": "c2001929-6810-4ea4-9b75-4dbde014b358",
            "namespace": "http://uri.suomi.fi/object/rytj/kaava",
            "referenceId": "http://uri.suomi.fi/object/rytj/kaava/InteractionEvent/c2001929-6810-4ea4-9b75-4dbde014b358.2",
            "producerSpecificId": "somelocalstuff-idwpi8045jhgi5",
            "latestChange": "2020-01-01T13:00:00Z",
            "storageTime": "2020-01-01T13:00:00Z",
            "type": {
                "code": "http://uri.suomi.fi/codelist/rytj/RY_KaavanVuorovaikutustapahtumanLaji/code/01",
                "title": {
                    "fin": "Nähtävilläolo"
                }
            },
            "name": {
                "fin": "Asemakaava nähtävillä"
            },
            "description": {
                 "fin": "Asemakaava on nähtävillä Kohtauspaikassa 1.7. - 15.7.2019"
            },
            "eventTime_start": "2019-07-01T00:00:00Z",
            "eventTime_end": "2019-07-15T00:00:00Z",
            "additionInformationLink": "https://kunta.fi/tapahtumakalenteri/iqoergqoergoi",
            "relatedMatters": [
                {
                    "linkedFeatureType": "SpatialPlan",
                    "linkedFeatureId": "9c97e469-083d-4284-90a9-3dbebdfe5622.23",
                    "href": "https://rytj.fi/api/kaava/SpatialPlan/9c97e469-083d-4284-90a9-3dbebdfe5622.23",
                    "title": {
                        "fin": "Asemakaava Y"
                    }
                }
            ],
            "relatedDocuments": [
                {
                    "linkedFeatureType": "Document",
                    "linkedFeatureId": "cdee8a56-c573-4514-8cc4-a6ff1536ac62.1",
                    "href": "https://rytj.fi/api/kaava/Document/cdee8a56-c573-4514-8cc4-a6ff1536ac62.1",
                    "title": {
                        "fin": "Huomautus asema-aukion pohjoiseen rajaukseen"
                    },
                    "role": {
                        "fin": "Mielipide"
                    }
                }
            ]
        }  
    }
```


###  SpatialPlanCommentary (Kaavaselostus)

Toteuttaa loogisen tietomallin luokan [Kaavaselostus](../../looginenmalli/dokumentaatio/#kaavaselostus)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   |
--------------|-------------------------|-----------------------|-------------|
[GeoJSON-tyyppi] |                      | type = "Feature"      | string
paikallinenTunnus | CharacterString [0..1]  | id                | string
              |                         | geometry              | object (tyhjä GeoJSON Polygon)
[luokan nimi] |                         | properties.featureType = "SpatialPlanCommentary" | string
nimiavaruus   | URI [0..1]              | properties.namespace  | string (uri)
viittausTunnus | URI [0..1]           | properties.referenceId  | string (uri)
identiteettiTunnus | CharacterString [0..1] | properties.identityId   | string
tuottajakohtainenTunnus | CharacterString [0..1]  | properties.producerSpecificId | string
viimeisinMuutos | TM_Instant [0..1]     | properties.latestChange | string (date-time)
tallennusAika | TM_Instant [0..1]       | properties.storageTime | string (date-time)



**Assosiaatiot**

Nimi          | UML tyyppi              | JSON property name    | JSON type
--------------|-------------------------|-----------------------|------------
korvaaObjektin | AbstraktiVersioituObjekti[0..*] | properties.replacesObjects | array of object (FeatureLink)
korvattuObjektilla | AbstraktiVersioituObjekti[0..*] | properties.replacedByObjects | array of object (FeatureLink)
asiakirja     | Asiakirja [0..1]        | properties.document   | object (FeatureLink)

**Esimerkki**

```json
{
        "id" : "52b9cb68-7e00-4e09-976e-5be94730fb81.5",
        "type" : "Feature",
        "geometry" : {
            "type" : "Polygon",
            "coordinates" : [ ]
        },
        "properties": {
            "featureType": "SpatialPlanCommentary",
            "identityId": "52b9cb68-7e00-4e09-976e-5be94730fb81",
            "namespace": "http://uri.suomi.fi/object/rytj/kaava",
            "referenceId": "http://uri.suomi.fi/object/rytj/kaava/SpatialPlanCommentary/52b9cb68-7e00-4e09-976e-5be94730fb81.5",
            "producerSpecificId": "somelocalstuff-id9983890",
            "latestChange": "2020-01-01T13:00:00Z",
            "storageTime": "2020-01-01T13:00:00Z",
            "document": {
                "linkedFeatureType": "Document",
                "linkedFeatureId": "640bff6b-c16a-4947-af8d-d86f89106be1.1",
                "href": "https://rytj.fi/api/kaava/Document/640bff6b-c16a-4947-af8d-d86f89106be1.1"
            }
        }
    }
```


###  ParticipationAndEvaluationPlan (OsallistumisJaArviointisuunnitelma)

Toteuttaa loogisen tietomallin luokan [OsallistumisJaArviointisuunnitelma](../../looginenmalli/dokumentaatio/#osallistumisjaarviointisuunnitelma)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   |
--------------|-------------------------|-----------------------|-------------|
[GeoJSON-tyyppi] |                      | type = "Feature"      | string
paikallinenTunnus | CharacterString [0..1]  | id                | string
              |                         | geometry              | object (tyhjä GeoJSON Polygon)
[luokan nimi] |                         | properties.featureType = "ParticipationAndEvaluationPlan" | string
nimiavaruus   | URI [0..1]              | properties.namespace  | string (uri)
viittausTunnus | URI [0..1]           | properties.referenceId  | string (uri)
identiteettiTunnus | CharacterString [0..1] | properties.identityId   | string
tuottajakohtainenTunnus | CharacterString [0..1]  | properties.producerSpecificId | string
viimeisinMuutos | TM_Instant [0..1]     | properties.latestChange | string (date-time)
tallennusAika | TM_Instant [0..1]       | properties.storageTime | string (date-time)

**Assosiaatiot**

Nimi          | UML tyyppi              | JSON property name    | JSON type
--------------|-------------------------|-----------------------|------------
korvaaObjektin | AbstraktiVersioituObjekti[0..*] | properties.replacesObjects | array of object (FeatureLink)
korvattuObjektilla | AbstraktiVersioituObjekti[0..*] | properties.replacedByObjects | array of object (FeatureLink)
asiakirja     | Asiakirja [0..1]        | properties.document   | object (FeatureLink)

**Esimerkki**

```json
{
        "id" : "3298d1ce-8486-4d83-89b0-e2e44d786d09.12",
        "type" : "Feature",
        "geometry" : {
            "type" : "Polygon",
            "coordinates" : [ ]
        },
        "properties": {
            "featureType": "ParticipationAndEvaluationPlan",
            "identityId": "3298d1ce-8486-4d83-89b0-e2e44d786d09",
            "namespace": "http://uri.suomi.fi/object/rytj/kaava",
            "referenceId": "http://uri.suomi.fi/object/rytj/kaava/ParticipationAndEvaluationPlan/3298d1ce-8486-4d83-89b0-e2e44d786d09.12",
            "producerSpecificId": "somelocalstuff-id9983890",
            "latestChange": "2020-01-01T13:00:00Z",
            "storageTime": "2020-01-01T13:00:00Z",
            "document": {
                "linkedFeatureType": "Document",
                "linkedFeatureId": "53eca1bb-f573-4c12-ab81-8248738c0d0c.1",
                "href": "https://rytj.fi/api/kaava/Document/53eca1bb-f573-4c12-ab81-8248738c0d0c.1"
            }
        }
    }
```

### Planner (KaavanLaatija)

Toteuttaa loogisen tietomallin luokan [KaavanLaatija](../../looginenmalli/dokumentaatio/#kaavanlaatija)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   |
--------------|-------------------------|-----------------------|-------------|
[GeoJSON-tyyppi] |                      | type = "Feature"      | string
paikallinenTunnus | CharacterString [0..1]  | id                | string
              |                         | geometry              | object (tyhjä GeoJSON Polygon)
[luokan nimi] |                         | properties.featureType = "Planner" | string
nimiavaruus   | URI [0..1]              | properties.namespace  | string (uri)
viittausTunnus | URI [0..1]           | properties.referenceId  | string (uri)
identiteettiTunnus | CharacterString [0..1] | properties.identityId   | string
tuottajakohtainenTunnus | CharacterString [0..1]  | properties.producerSpecificId | string
viimeisinMuutos | TM_Instant [0..1]     | properties.latestChange | string (date-time)
tallennusAika | TM_Instant [0..1]       | properties.storageTime | string (date-time)
nimi          | CharacterString         | properties.personName | string
nimike        | LanguageString [0..*]   | properties.professionTitle | object (LanguageString)
rooli         | LanguageString [0..*]   | properties.role       | object (LanguageString)

**Assosiaatiot**

Nimi          | UML tyyppi              | JSON property name    | JSON type
--------------|-------------------------|-----------------------|------------
korvaaObjektin | AbstraktiVersioituObjekti[0..*] | properties.replacesObjects | array of object (FeatureLink)
korvattuObjektilla | AbstraktiVersioituObjekti[0..*] | properties.replacedByObjects | array of object (FeatureLink)

**Esimerkki**

```json
    {
        "id" : "391debf8-3d07-4a31-9854-17b90c86abb5.64",
        "type" : "Feature",
        "geometry" : {
            "type" : "Polygon",
            "coordinates" : [ ]
        },
        "properties": {
            "featureType": "Planner",
            "identityId": "391debf8-3d07-4a31-9854-17b90c86abb5",
            "namespace": "http://uri.suomi.fi/object/rytj/kaava",
            "referenceId": "http://uri.suomi.fi/object/rytj/kaava/Planner/391debf8-3d07-4a31-9854-17b90c86abb5.64",
            "producerSpecificId": "somelocalstuff-id0892459077094",
            "latestChange": "2020-01-01T13:00:00Z",
            "stotageTime": "2020-01-01T13:00:00Z",
            "personName": "John Doe",
            "professionalTitle": {
                "fin": "Kaupunginarkkitehti"
            },
            "role": {
                 "fin": "Vastuullinen laatija"
            }
        }
    }
```

### PlanObject (Kaavakohde)

Toteuttaa loogisen tietomallin luokan [Kaavakohde](../../looginenmalli/dokumentaatio/#kaavakohde)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   |
--------------|-------------------------|-----------------------|-------------|
[GeoJSON-tyyppi] |                      | type = "Feature"      | string
paikallinenTunnus | CharacterString [0..1]  | id                | string
geometria     | Geometry                | geometry              | object (GeoJSON Geometry)
[luokan nimi] |                         | properties.featureType = "PlanObject" | string
nimiavaruus   | URI [0..1]              | properties.namespace  | string (uri)
viittausTunnus | URI [0..1]           | properties.referenceId  | string (uri)
identiteettiTunnus | CharacterString [0..1] | properties.identityId   | string
tuottajakohtainenTunnus | CharacterString [0..1]  | properties.producerSpecificId | string
viimeisinMuutos | TM_Instant [0..1]     | properties.latestChange | string (date-time)
tallennusAika | TM_Instant [0..1]       | properties.storageTime | string (date-time)
nimi            | LanguageString [0..*] | properties.name                  | object (LanguageString)
pystysuuntainenRajaus | Korkeusvali [0..*] | properties.verticalLimits | array of object (ElevationRange)
laji          | AbstraktiKaavamaarayskohdeLaji [0..1] | properties.type       | object (CodelistValue), ei arvoja toistaiseksi
sijainninSitovuus | Sitovuuslaji [0..1] | properties.bindingnessOfLocation | object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_Sitovuuslaji>
liittyvanLahtotietokohteenTunnnus | URI [0..*] | properties.relatedInputDatasetObjectIds | array of string (uri)
maanalaisuus    | MaanalaisuudenLaji [0..1] | properties.groundRelativePosition | object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_MaanalaisuudenLaji>
ymparistomuutoksenLaji | AbstraktiYmparistomuutoksenLaji | properties.environmentalChangeNature | object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_ymparistomuutoksenLaji_YK> (vain yleiskaava)

**Assosiaatiot**

Nimi          | UML tyyppi              | JSON property name    | JSON type
--------------|-------------------------|-----------------------|------------
korvaaObjektin | AbstraktiVersioituObjekti[0..*] | properties.replacesObjects | array of object (FeatureLink)
korvattuObjektilla | AbstraktiVersioituObjekti[0..*] | properties.replacedByObjects | array of object (FeatureLink)
kaava         | Kaava                   | properties.spatialPlan | object (FeatureLink)
liittyvaKohde | AbstraktiKaavakohde [0..*] | properties.relatedPlanObjects | array of object (FeatureLink)
maarays       | Kaavamaarays [0..*]     | properties.regulations | array of object (FeatureLink)
suositus      | Kaavasuositus [0..*]     | properties.guidances  | array of object (FeatureLink)

**Esimerkki**

```json
    {
        
        "id" : "6d32ca64-9a8d-44bb-9702-e46c228add64.76",
        "type" : "Feature",
        "geometry" : {
            "type" : "Polygon",
            "coordinates" : [ ]
        },
        "crs" : {
            "type" : "name",
            "properties" : {
                "name" : "http://www.opengis.net/def/crs/EPSG/0/3067"
            }
        },
        "properties": {
            "featureType": "PlanObject",
            "identityId": "6d32ca64-9a8d-44bb-9702-e46c228add64",
            "namespace": "http://uri.suomi.fi/object/rytj/kaava",
            "referenceId": "http://uri.suomi.fi/object/rytj/kaava/PlanObject/6d32ca64-9a8d-44bb-9702-e46c228add64.76",
            "producerSpecificId": "somelocalstuff-idgj40895425",
            "latestChange": "2020-01-01T13:00:00Z",
            "storageTime": "2020-01-01T13:00:00Z",
            "spatialPlan": {
                    "linkedFeatureType": "SpatialPlan",
                    "linkedFeatureId": "9c97e469-083d-4284-90a9-3dbebdfe5622.23",
                    "href": "https://rytj.fi/api/kaava/SpatialPlan/9c97e469-083d-4284-90a9-3dbebdfe5622.23"
            },
            "verticalLimits": [
                {
                    "valueType": "ElevationRange",
                    "minValue": 0.0,
                    "maxValue": 1.5,
                    "unitOfMeasure": "m",
                    "referencePoint": {
                        "crs": {
                            "type" : "name",
                            "properties" : {
                                "name" : "http://www.opengis.net/def/crs/EPSG/0/3900"
                            }
                        }, 
                        "type" : "Point",
                        "coordinates" : [ 40.1 ]
                    }
                }
            ],
            "bindingnessOfLocation": {
                "code": "http://uri.suomi.fi/codelist/rytj/RY_Sitovuuslaji/code/01",
                "title": {
                    "fin": "Sitova"
                }
            },
            "groundRelativePosition": {
                "code": "http://uri.suomi.fi/codelist/rytj/RY_MaanalaisuudenLaji/code/02",
                "title": {
                    "fin": "Maanpäällinen"
                }
            },
            "regulations": [
                {
                    "linkedFeatureType": "PlanRegulation",
                    "linkedFeatureId": "f207c8b7-ed57-4e2e-8150-64fc229e17d3.3",
                    "href": "https://rytj.fi/api/kaava/PlanRegulation/f207c8b7-ed57-4e2e-8150-64fc229e17d3.3"
                }
            ],
            "guidances": [
                {
                    "linkedFeatureType": "PlanGuidance",
                    "linkedFeatureId": "ff451636-8747-4148-b290-b5d96b21b2c3.3",
                    "href": "https://rytj.fi/api/kaava/PlanGuidance/ff451636-8747-4148-b290-b5d96b21b2c3.3"
                }
            ],
            "validFrom": "2020-05-01T00:00:00Z"
        }
    }
```

### PlanRegulation (Kaavamaarays)

Toteuttaa loogisen tietomallin luokan [Kaavamaarays](../../looginenmalli/dokumentaatio/#kaavamaarays)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   |
--------------|-------------------------|-----------------------|-------------|
[GeoJSON-tyyppi] |                      | type = "Feature"      | string
paikallinenTunnus | CharacterString [0..1]  | id                | string
              |                         | geometry              | object (GeoJSON Geometry)
[luokan nimi] |                         | properties.featureType = "PlanRegulation" | string
nimiavaruus   | URI [0..1]              | properties.namespace  | string (uri)
viittausTunnus | URI [0..1]           | properties.referenceId  | string (uri)
identiteettiTunnus | CharacterString [0..1] | properties.identityId   | string
tuottajakohtainenTunnus | CharacterString [0..1]  | properties.producerSpecificId | string
viimeisinMuutos | TM_Instant [0..1]     | properties.latestChange | string (date-time)
tallennusAika | TM_Instant [0..1]       | properties.storageTime | string (date-time)
nimi          | LanguageString [0..*]   | properties.name       | object (LanguageString)
arvo          | AbstraktiArvo [0..*]    | properties.values      | array of object (TimeInstantValue, TimePeriodValue, GeometryValue, CodeValue, IntegerValue, IntegerRange, NumberValue, NumberRange, ElevationPosition, ElevationRange, TextValue tai IdentifierValue)
laji          | AbstraktiKaavamaaraysLaji | properties.type       | object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK>, <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_YK>
elinkaaritila   | KaavanElinkaaritila   | properties.lifecycleStatus | object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila>
teema         | AbstraktiKaavoitusteema [0..*] | properties.themes     | array of object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_Kaavoitusteema_AK>, <http://uri.suomi.fi/codelist/rytj/RY_Kaavoitusteema_YK>
lisatieto     | Lisatieto [0..*]        | properties.supplementaryInfo | array of object (SupplementaryInformation)
voimassaoloAika | TM_Period [0..1]      | properties.validFrom, properties.validTo | string (date-time)

**Assosiaatiot**

Nimi          | UML tyyppi              | JSON property name    | JSON type
--------------|-------------------------|-----------------------|------------
korvaaObjektin | AbstraktiVersioituObjekti[0..*] | properties.replacesObjects | array of object (FeatureLink)
korvattuObjektilla | AbstraktiVersioituObjekti[0..*] | properties.replacedByObjects | array of object (FeatureLink)
kaava         | Kaava                   | properties.spatialPlan | object (FeatureLink)
kohdistus     | AbstraktiKaavakohde [0..1] | properties.target  | object (FeatureLink)
liittyvaAsiakirja | Dokumentti [0..*] | properties.relatedDocuments | array of object (FeatureLink)

**Esimerkki**

```json
    {
        "id" : "f207c8b7-ed57-4e2e-8150-64fc229e17d3.3",
        "type" : "Feature",
        "geometry" : {
            "type" : "Polygon",
            "coordinates" : [ ]
        },
        "properties": {
            "featureType": "PlanRegulation",
            "identityId": "f207c8b7-ed57-4e2e-8150-64fc229e17d3",
            "namespace": "http://uri.suomi.fi/object/rytj/kaava",
            "referenceId": "http://uri.suomi.fi/object/rytj/kaava/PlanRegulation/f207c8b7-ed57-4e2e-8150-64fc229e17d3.3",
            "latestChange": "2020-01-01T13:00:00Z",
            "storageTime": "2020-01-01T13:00:00Z",
            "producerSpecificId": "idfr00834790",
            "spatialPlan": {
                    "linkedFeatureType": "SpatialPlan",
                    "linkedFeatureId": "9c97e469-083d-4284-90a9-3dbebdfe5622.23",
                    "href": "https://rytj.fi/api/kaava/SpatialPlan/9c97e469-083d-4284-90a9-3dbebdfe5622.23"
            },
            "target": {
                    "linkedFeatureType": "PlanObject",
                    "linkedFeatureId": "6d32ca64-9a8d-44bb-9702-e46c228add64.76",
                    "href": "https://rytj.fi/api/kaava/PlanObject/6d32ca64-9a8d-44bb-9702-e46c228add64.76"
            },
            "type": {
                "code": "http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010301",
                "title": {
                    "fin": "Liikerakennusten alue"
                }
            },
            "lifecycleStatus": {
                "code": "http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/06",
                "title": {
                    "fin": "Hyväksytty kaava"
                }
            },
            "validFrom": "2020-05-01T00:00:00Z"
        }
    }
```

### PlanGuidance (Kaavasuositus)

Toteuttaa loogisen tietomallin luokan [Kaavasuositus](../../looginenmalli/dokumentaatio/#kaavasuositus)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   |
--------------|-------------------------|-----------------------|-------------|
[GeoJSON-tyyppi] |                      | type = "Feature"      | string
paikallinenTunnus | CharacterString [0..1]  | id                | string
              |                         | geometry              | object (GeoJSON Geometry)
[luokan nimi] |                         | properties.featureType = "PlanGuidance" | string
nimiavaruus   | URI [0..1]              | properties.namespace  | string (uri)
viittausTunnus | URI [0..1]           | properties.referenceId  | string (uri)
identiteettiTunnus | CharacterString [0..1] | properties.identityId   | string
tuottajakohtainenTunnus | CharacterString [0..1]  | properties.producerSpecificId | string
viimeisinMuutos | TM_Instant [0..1]     | properties.latestChange | string (date-time)
tallennusAika | TM_Instant [0..1]       | properties.storageTime | string (date-time)
nimi          | LanguageString [0..*]   | properties.name       | object (LanguageString)
arvo          | AbstraktiArvo [0..*]    | properties.values      | array of object (TextValue)
elinkaaritila   | KaavanElinkaaritila   | properties.lifecycleStatus | object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila>
teema         | AbstraktiKaavoitusteema [0..*] | properties.themes     | array of object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_Kaavoitusteema_AK>, <http://uri.suomi.fi/codelist/rytj/RY_Kaavoitusteema_YK>
voimassaoloAika | TM_Period [0..1]      | properties.validFrom, properties.validTo | string (date-time)

**Assosiaatiot**

Nimi          | UML tyyppi              | JSON property name    | JSON type
--------------|-------------------------|-----------------------|------------
korvaaObjektin | AbstraktiVersioituObjekti[0..*] | properties.replacesObjects | array of object (FeatureLink)
korvattuObjektilla | AbstraktiVersioituObjekti[0..*] | properties.replacedByObjects | array of object (FeatureLink)
kaava         | Kaava                   | properties.spatialPlan | object (FeatureLink)
kohdistus     | AbstraktiKaavakohde [0..1] | properties.target  | object (FeatureLink)
liittyvaAsiakirja | Dokumentti [0..*] | properties.relatedDocuments | array of object (FeatureLink)

**Esimerkki**

```json
    {
        "id" : "ff451636-8747-4148-b290-b5d96b21b2c3.3",
        "type" : "Feature",
        "geometry" : {
            "type" : "Polygon",
            "coordinates" : [ ]
        },
        "properties": {
            "featureType": "PlanGuidance",
            "identityId": "ff451636-8747-4148-b290-b5d96b21b2c3",
            "namespace": "http://uri.suomi.fi/object/rytj/kaava",
            "referenceId": "http://uri.suomi.fi/object/rytj/kaava/PlanGuidance/ff451636-8747-4148-b290-b5d96b21b2c3.3",
            "latestChange": "2020-01-01T13:00:00Z",
            "storageTime": "2020-01-01T13:00:00Z",
            "producerSpecificId": "idfr0083450",
            "spatialPlan": {
                    "linkedFeatureType": "SpatialPlan",
                    "linkedFeatureId": "9c97e469-083d-4284-90a9-3dbebdfe5622.23",
                    "href": "https://rytj.fi/api/kaava/SpatialPlan/9c97e469-083d-4284-90a9-3dbebdfe5622.23"
            },
            "target": {
                    "linkedFeatureType": "PlanObject",
                    "linkedFeatureId": "6d32ca64-9a8d-44bb-9702-e46c228add64.76",
                    "href": "https://rytj.fi/api/kaava/PlanObject/6d32ca64-9a8d-44bb-9702-e46c228add64.76"
            },
            "values": [
                {
                    "valueType": "TextValue",
                    "value": {
                        "fin": "Peltojen avoimina säilyttämisen tukeminen ja mahdolliset ympäristönhoitotoimenpiteet ovat perusteltuja"
                    }
                }
            ],
            "lifecycleStatus": {
                "code": "http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/06",
                "title": {
                    "fin": "Hyväksytty kaava"
                }
            },
            "validFrom": "2020-05-01T00:00:00Z"
        }
    }
```

## Tietotyypit (DataType)

Tietotyypit eivät kuvaudu omiksi GeoJSON-kohteikseen, vaan kohdetyyppien tai toisten tietotyyppien rakenteisiksi ominaisuuksiksi. Tietotyypin instanssilla ei ole tunnusta, eikä se voi esiintyä irrallaan sen sisältävästä kohteesta.

### CancellationInfo (KaavanKumoamistieto)

Toteuttaa loogisen tietomallin luokan [KaavanKumoamistieto](../../looginenmalli/dokumentaatio/#kaavankumoamistieto)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   | huomioita
--------------|-------------------------|-----------------------|-------------|--------------
kumottavanKaavanTunnus | URI            |  cancelledPlanId | string (uri) | viittaa kaavatunnus-kenttään (SpatialPlan, properties.spatialPlanId)
kumoaaKaavanKokonaan | boolean          | cancelsEntirePlan     | boolean | sama kuin jos ko. kaavan kaikki kohteet ja määräykset kumottaisiin
kumottavaKaavanAlue  | Surface [0..*]   | areaToCancel         | object (GeoJSON MultiPolygon) | aluerajaukset, joiden sisältämät kohteet ja niiden määräykset kumotaan
kumottavanMaarayksenTunnus | URI [0..*] | planningRegulationIdsToCancel | array of string (uri)
kumottavanSuosituksenTunnus | URI [0..*]    | planningGuidanceIdsToCancel | array of string (uri)

**Esimerkki**

```json
{
    "cancelledPlanId": "",
    "cancelsEntirePlan": false,
    "areaToCancel": {
        "type" : "MultiPolygon",
        "coordinates" : [ ]
    },
    "planningRegulationIdsToCancel": [
        ""
    ],
    "planningGuidanceIdsToCancel": [
        ""
    ],
}
```

### SupplementaryInformation (Lisatieto)

Toteuttaa loogisen tietomallin luokan [Lisatieto](../../looginenmalli/dokumentaatio/#lisatieto)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   | huomioita
--------------|-------------------------|-----------------------|-------------|--------------
laji          | AbstraktiLisatiedonLaji | type                  | object (CodelistValue), <http://uri.suomi.fi/codelist/rytj/RY_LisatiedonLaji_AK>, <http://uri.suomi.fi/codelist/rytj/RY_LisatiedonLaji_YK>
nimi          | LanguageString [0..*]   | name       | object (LanguageString)
arvo          | AbstraktiArvo [0..*]    | values      | array of object (TimeInstantValue, TimePeriodValue, GeometryValue, CodeValue, IntegerValue, IntegerRange, NumberValue, NumberRange, ElevationPosition, ElevationRange, TextValue tai IdentifierValue)

**Esimerkki**

```json
{
    "type": {
        "code": "http://uri.suomi.fi/codelist/rytj/RY_LisatiedonLaji_AK/code/01",
        "title": {
            "fin": "Käyttötarkoituksen osuus kerrosalasta"
        }   
    },
    "values": [
        {
            "valueType": "CodeValue",
            "value": "http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010301",
            "title": {
                "fin": "Liikerakennusten alue"
            }
        }, 
        {
            "valueType": "NumberRange",
            "minValue": 200.0,
            "maxValue": 1000.0,
            "unitOfMeasure": "m2"
        }
    ]
}
```

### TimeInstantValue (Ajanhetkiarvo)

Toteuttaa loogisen tietomallin luokan [Ajanhetkiarvo](../../looginenmalli/dokumentaatio/#ajanhetkiarvo)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   | huomioita
--------------|-------------------------|-----------------------|-------------|--------------
[luokan nimi] |                         | valueType="TimeInstantValue" | string | 
arvo          | TM_Instant              | value                  | string (date-time)

**Esimerkki**

```json
    {
        "valueType": "TimeInstantValue",
        "value": "2020-11-06T10:00:05Z"
    }
```

### TimePeriodValue (Aikavaliarvo)

Toteuttaa loogisen tietomallin luokan [Aikavaliarvo](../../looginenmalli/dokumentaatio/#aikavaliarvo)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   | huomioita
--------------|-------------------------|-----------------------|-------------|--------------
[luokan nimi] |                         | valueType="TimePeriodValue" | string | 
arvo          | TM_Period               | value_start, value_end  | string (date-time) | jompi kumpi voi puuttua

**Esimerkki**

```json
    {
        "valueType": "TimePeriodValue",
        "value_start": "2020-11-06T00:00:00Z",
        "value_end": "2020-12-06T00:00:00Z"
    }
```

```json
    {
        "valueType": "TimePeriodValue",
        "value_start": "2020-11-06T00:00:00Z"
    }
```

### GeometryValue (GeometriaArvo)

Toteuttaa loogisen tietomallin luokan [GeometriaArvo](../../looginenmalli/dokumentaatio/#geometriaarvo)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   | huomioita
--------------|-------------------------|-----------------------|-------------|--------------
[luokan nimi] |                         | valueType="GeometryValue" | string | 
arvo          | Geometry                | value              | object (GeoJSON Geometry) |

**Esimerkki**

```json
    {
        "valueType": "GeometryValue",
        "value": {
            "type" : "LineString",
            "coordinates" : [ ]
        }
    }
```

### CodeValue (Koodiarvo)

Toteuttaa loogisen tietomallin luokan [Koodiarvo](../../looginenmalli/dokumentaatio/#koodiarvo)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   | huomioita
--------------|-------------------------|-----------------------|-------------|--------------
[luokan nimi] |                         | valueType="CodeValue" | string | 
arvo          | URI                     | value                  | string (uri) |
koodistonTunnnus | URI [0..1]           | codeList              | string (uri) |
otsikko       | LanguageString [0..*]   | title                 | object (LanguageString) |

**Esimerkki**

```json
    {
        "valueType": "CodeValue",
        "value": "http://uri.suomi.fi/codelist/rytj/RY_Sitovuuslaji/code/01",
        "codeList": "http://uri.suomi.fi/codelist/rytj/RY_Sitovuuslaji",
        "title": {
            "fin": "Sitova"
        }
    }
```


### IntegerValue (NumeerinenArvo)

Toteuttaa loogisen tietomallin luokan [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) siten, että ```arvo```-attribuutin tyyppi toteuttaa [Integer](../../looginenmalli/dokumentaatio/#integer)-rajapinnan.


**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   | huomioita
--------------|-------------------------|-----------------------|-------------|--------------
[luokan nimi] |                         | valueType="IntegerValue" | string |
arvo          | Number                  | value                | integer      |
mittayksikko  | CharacterString [0..1]  | unitOfMeasure     | string      |

**Esimerkki**

```json
{
    "valueType": "IntegerValue",
    "value": 20
}
```

### IntegerRange (NumeerinenArvovali)

Toteuttaa loogisen tietomallin luokan [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali) siten, että ```minimiarvo```- ja ```maksimiarvo```-attribuuttien tyypit toteuttavat [Integer](../../looginenmalli/dokumentaatio/#integer)-rajapinnan.

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   | huomioita
--------------|-------------------------|-----------------------|-------------|--------------
[luokan nimi] |                         | valueType="IntegerRange" | string   |
nimimiarvo    | Number [0..1]           | minValue              | integer     |
maksimiarvo   | Number [0..1]           | maxValue              | integer     |
mittayksikko  | CharacterString [0..1]  | unitOfMeasure         | string      |

**Esimerkki**

```json
{
    "valueType": "IntegerRange",
    "minValue": 20,
    "maxValue": 30,
}
```

### NumberValue (NumeerinenArvo)

Toteuttaa loogisen tietomallin luokan [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) siten, että ```arvo```-attribuutin tyyppi toteuttaa [Real](../../looginenmalli/dokumentaatio/#real)-rajapinnan.


**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   | huomioita
--------------|-------------------------|-----------------------|-------------|--------------
[luokan nimi] |                         | valueType="NumberValue" | string    |
arvo          | Number                  | value                 | number      |
mittayksikko  | CharacterString [0..1]  | unitOfMeasure         | string      |

**Esimerkki**

```json
{
    "valueType": "NumberValue",
    "value": 20.0,
    "unitOfMeasure": "dB"
}
```

### NumberRange (NumeerinenArvovali)

Toteuttaa loogisen tietomallin luokan [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali) siten, että ```minimiarvo```- ja ```maksimiarvo```-attribuuttien tyypit toteuttavat [Real](../../looginenmalli/dokumentaatio/#real)-rajapinnan.

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   | huomioita
--------------|-------------------------|-----------------------|-------------|--------------
[luokan nimi] |                         | valueType="NumberRange" | string    |
nimimiarvo    | Number [0..1]           | minValue              | number      |
maksimiarvo   | Number [0..1]           | maxValue              | number      |
mittayksikko  | CharacterString [0..1]  | unitOfMeasure         | string      |

**Esimerkki**

```json
{
    "valueType": "NumberRange",
    "minValue": 1000.0,
    "maxValue": 2500.0,
    "unitOfMeasure": "m2"
}
```

### ElevationPosition (Korkeuspiste)

Toteuttaa loogisen tietomallin luokan [Korkeuspiste](../../looginenmalli/dokumentaatio/#korkeuspiste)

**Attribuutit**


Nimi          | UML tyyppi              | JSON property name    | JSON type   | huomioita
--------------|-------------------------|-----------------------|-------------|--------------
[luokan nimi] |                         | valueType="ElevationPosition" | string |
arvo          | double                  | value                | number      |
mittayksikko  | CharacterString [0..1]  | unitOfMeasure    | string      |
referenssipiste | Point [0..1]          | referencePoint        | object (CoordinateReferencePoint) |

**Esimerkki**

```json
{
    "valueType": "ElevationPosition",
    "value": 10.2,
    "unitOfMeasure": "m",
    "referencePoint": {
        "crs": {
            "type" : "name",
            "properties" : {
                "name" : "http://www.opengis.net/def/crs/EPSG/0/3900"
            }
        }, 
        "type" : "Point",
        "coordinates" : [ 40.1 ]
    }
}
```

### ElevationRange (Korkeusvali)

Toteuttaa loogisen tietomallin luokan [Korkeusvali](../../looginenmalli/dokumentaatio/#korkeusvali)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   | huomioita
--------------|-------------------------|-----------------------|-------------|--------------
[luokan nimi] |                         | valueType="ElevationRange" | string |
nimimiarvo    | double [0..1]           | minValue              | number      |
maksimiarvo   | double [0..1]           | maxValue              | number      |
mittayksikko  | CharacterString [0..1]  | unitOfMeasure   | string      |
referenssipiste | Point [0..1]          | referencePoint        | object (CoordinateReferencePoint) |

**Esimerkki**

```json
{
    "valueType": "ElevationRange",
    "minValue": 10.0,
    "maxValue": 15.0,
    "unitOfMeasure": "m",
    "referencePoint": {
        "crs": {
            "type" : "name",
            "properties" : {
                "name" : "http://www.opengis.net/def/crs/EPSG/0/3900"
            }
        }, 
        "type" : "Point",
        "coordinates" : [ 40.1 ]
    }
}
```

### TextValue (Tekstiarvo)

Toteuttaa loogisen tietomallin luokan [Tekstiarvo](../../looginenmalli/dokumentaatio/#tekstiarvo)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   | huomioita
--------------|-------------------------|-----------------------|-------------|--------------
[luokan nimi] |                         | valueType="TextValue" | string |
arvo          | LanguageString [1..*]   | value                 | object (LanguageString)  |
syntaksi      | CharacterString [0..1]  | syntax                | string      |

**Esimerkki**

```json
{
    "valueType": "TextValue",
    "value": {
        "fin": "Aluetta kehitetään asumisen sekä sitä palvelevien toimintojen ja lähipalvelujen sekä ympäristöhäiriötä aiheuttamattomien elinkeinotoimintojen alueena."
    },
    "syntax": "naturalLanguage"
}
```


### IdentifierValue (Tunnusarvo)

Toteuttaa loogisen tietomallin luokan [Tunnusarvo](../../looginenmalli/dokumentaatio/#tunnusarvo)

**Attribuutit**

Nimi          | UML tyyppi              | JSON property name    | JSON type   | huomioita
--------------|-------------------------|-----------------------|-------------|--------------
[luokan nimi] |                         | valueType="IdentifierValue" | string |
arvo          | CharacterString         | value                 | string (uri)| tunnuksen arvo
rekisterinTunnus | URI  [0..1]          | registerId            | string (uri)|
rekisterinNimi | LanguageString [0..*]  | registerName          | object (LanguageString)

**Esimerkki**

```json
{
    "valueType": "IdentifierValue",
    "value": "86-413-1-124",
    "registerId": "http://maanmittauslaitos.fi/kiinteistorekisteri",
    "registerName": {
        "fin": "Kiinteistörekisteri"
    }
}
```

## Yleiskäyttöiset rakenteiset aputyypit

### LanguageString

Ominaisuus       | tyyppi      | pakollinen  | huomiot 
-----------------|-------------|-------------|-----------
[kielikoodi]     | string      | k           | ominaisuuden nimenä ISO 639-2 (kolme merkkiä) -koodi, arvona kielikohtainen teksti


### CodelistValue

Ominaisuus       | tyyppi                   | pakollinen | huomiot
-----------------|--------------------------|------------|-------------
code             | string (uri)             | k         | mieluiten koko URL, jos resolvautuu
codelist         | string (uri)             | e         | ei yleensä tarvita, jos koodi resolvautuu
title            | object (LanguageString)  | e         | informatiivinen, vain tietoa tarjottaessa


### FeatureLink 

Ominaisuus       | tyyppi                   | pakollinen | huomiot
-----------------|--------------------------|------------|-------------
linkedFeatureId  | string (uri)             | k          | kohteen id-kentän arvo
linkedFeatureType | string                  | e          | kohteen featureType-kentän arvo, auttaa päättelemään linkatun tietorakenteen
href             | string (uri-reference)   | e          | suora URL viitattuun kohteeseen, API populoi, ei käytetä tallennustiedostossa
role             | object (LanguageString)  | e          | roolitieto (miten liittyy) mikäli tarvitaan assosiaatiossa
title            | object (LanguageString)  | e          | viitatun kohteen selväkielinen nimi, mikäli tarpeen  

### CoordinateReferencePoint 

Ominaisuus       | tyyppi                   | pakollinen | huomiot
-----------------|--------------------------|------------|-------------
crs              | object (NamedCooodinateReferenceSystem) | e | GeoJSON-spesifikaation ([IETF RFC 7946](https://www.rfc-editor.org/info/rfc7946)) mukaan GeoJSON-kohteiden koordinaatisto on aina WGS84 (urn:ogc:def:crs:OGC::CRS84), longitudi, latitudi -järjestyksessä. Tuottajien ja käyttäjien yhteisellä ennakkosopimuksella tästä voidaan kuitenkin poiketa.   
type             | string = "Point"         | k          |
coordinates      | array of number          | k          | koordinaatiston koordinaattien mukainen määrä numeroita


### NamedCooodinateReferenceSystem 

Sama kuin deprekoidun GeoJSON draft version 6:n "Named CRS", ks. http://wiki.geojson.org/GeoJSON_draft_version_6

Ominaisuus       | tyyppi                   | pakollinen | huomiot
-----------------|--------------------------|------------|-------------
type             | string = "name"          | k          | 
properties.name  | string (uri)             | k          | Koordinaatiston URI-muotoinen tunnus, esim. "http://www.opengis.net/def/crs/EPSG/0/4326", "http://www.opengis.net/def/crs/EPSG/0/3067" tai "http://www.opengis.net/def/crs/EPSG/0/3900"
      