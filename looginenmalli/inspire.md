---
layout: "default"
description: ""
id: "inspire"
status: "Keskeneräinen"
---
# Inspire-yhteensopivuus
{:.no_toc}

1. 
{:toc}

## Inspire Planned Land Use -sovellusskeema

Maankäytön suunnitteluun liittyvät kaavatietoaineistot julkaistaan Inspire-tietoaineistoina käyttäen Inspire-direktiivin liiteen 3 piiriin kuuluvan [Land Use (LU)](https://inspire.ec.europa.eu/Themes/129/2892) -teeman Planned Land Use -sovellusskeemaa (PLU). 

Kaikki Land Use -teeman sovellusskeemat on kuvattu dokumentissa [Data Specification on Land Use – Technical Guidelines, v. 3.0](https://inspire.ec.europa.eu/id/document/tg/lu). Skeeman ydin koostuu neljästä kohdetyyppi-stereotyypin (feature type) luokasta ja niiden välisistä assosiaatiosta: SpatialPlan, ZoningElement, SupplementaryRegulation ja OfficialDocumentation. 

![Planned Land Use -sovellusskeeman kohdetyypit](inspire-plu-luokkakaavio.png "Planned Land Use -sovellusskeeman kohdetyypit")

PLU-sovellusskeemassa määritellään myös seitsemän tietotyyppi-stereotyypin (data type) luokkaa: BackgroundMapValue, OrdinanceValue, DimensioningIndicationValue, DimensioningIndicationRealValue, DimensioningIndicationIntegerValue, DimensioningIndicationCharacterValue ja DimensioningIndicationMeasureValue.

![Planned Land Use -sovellusskeeman tietotyypit](inspire-plu-luokkakaavio-datatypes.png "Planned Land Use -sovellusskeeman tietotyypit")

Koodistojen osalta PLU-skeemassa määritellään seuraavat: [PlanTypeNameValue](https://inspire.ec.europa.eu/codelist/PlanTypeNameValue), [SpecificSupplementaryRegulationValue](https://inspire.ec.europa.eu/codelist/SpecificSupplementaryRegulationValue), [SupplementaryRegulationValue](https://inspire.ec.europa.eu/codelist/SupplementaryRegulationValue), [LevelOfSpatialPlanValue](https://inspire.ec.europa.eu/codelist/LevelOfSpatialPlanValue), [ProcessStepGeneralValue](https://inspire.ec.europa.eu/codelist/LevelOfSpatialPlanValue) ja [RegulationNatureValue](https://inspire.ec.europa.eu/codelist/RegulationNatureValue). Näiden lisäksi PLU-skeeman luokissa käytetään skeemasta Land Use Nomenclature koodistoja [LandUseClassificationValue](https://inspire.ec.europa.eu/codelist/LandUseClassificationValue) ja [HILUCSValue](https://inspire.ec.europa.eu/codelist/LandUseClassificationValue) sekä olemassaolevaa maankäyttöä kuvaavia SpecificPresence- ja HILUCSPresence -union-tyyppisiä luokkia.

Tässä dokumentissa kuvataan miten loogisen tason Kaavatietomallin tiedoista voidaan tuottaa Inspire PLU -sovellusskeeman mukaisia tietoaineistoja. Kaikkea Kaavatietomallin mahdollistamaa tietosisältöä ei kuitenkaan voida muuntaa Inspire PLU-mallin muotoon, sillä PLU-malli ei sisällä kaikki vastaavia tietosisältöjä ja -rakenteita. Erityisesti [Lisatieto](dokumentaatio/#lisatieto)-luokan tiedot jäävät kokonaan pois Inspire-muunnoksessa.

## Luokka- ja ominaisuustason vastaavuudet

### SpatialPlan

Inspire Planned Land Use -skeeman ```SpatialPlan```-luokan tiedot johdetaan loogisen tason Kaavatietomallin [Kaava](dokumentaatio/#kaava)-luokan ja siihen liittyvien [Lahtotietoaineisto](dokumentaatio/#lahtotietoaineisto)- ja [Asiakirja](dokumentaatio/#asiakirja)-luokkien tiedoista alla esitettyjen taulukoiden mukaisesti. Kukin Kaavatietomallin ```Kaava```-luokan instanssi vastaa yhtä Inspire Planned Land Use -skeeman ```SpatialPlan```-luokan instanssia.

| Attribuutti                   |  Johtaminen Kaavatietomallin tiedoista        | Huomautukset
------------------------------- | --------------------------------------------- | -------------------------------
| inspireId: Identifier [1]     |  ks. seuraavat rivit                          |
|                               | ```localId```: Kaava.identiteettiTunnus       |
|                               | ```version```: Kaava.paikallinenTunnus ilman identiteettiTunnus -alkuosaa |
|                               | ```namespace```: <http://paikkatiedot.fi/so/{aineistotunnus}/LU/SpatialPlan>, jossa {aineistotunnus} on Maanmittauslaitoksen myöntämä
| extent: GM_MultiSurface [1]   | Kaava.aluerajaus                              |
| beginLifeSpanVersion: DateTime [1] (voidable) | Kaava.viimeisinMuutos                    | 
| officialTitle: CharacterString [1] | Kaava.nimi                               | valitaan yksi kieli käyttäjän preferessin perusteella
| levelOfSpatialPlan: LevelOfSpatialPlanValue [1] | <https://inspire.ec.europa.eu/codelist/LevelOfSpatialPlanValue/regional>
| endLifeSpanVersion: DateTime [1] (voidable) | Kaava.korvattuKohteella.tallennusAika      |
| validFrom: Date [0..1] (voidable) | Kaava.voimassaoloAika.begin               |
| validTo: Date [0..1] (voidable) | Kaava.voimassaoloAika.end                   |
| alternativeTitle: CharacterString [1] (voidable) | ei anneta
| planTypeName: PlanTypeName [1] | Kaava.laji                                   | [RY_Kaavalaji](http://uri.suomi.fi/codelist/rytj/RY_Kaavalaji)-koodisto tulisi määritellä laajentamaan Inspire:n [PlanTypeName](https://inspire.ec.europa.eu/codelist/PlanTypeNameValue)-koodistoa
| processStepGeneral: ProcessStepGeneralValue [1] (voidable) | Kaava.elinkaaritila | ks. [ProcessStepGeneralValue](#processstepgeneralvalue)
| backgroundMap: BackgroundMapValue [1] (voidable) | Kaava.hyodynnettyAineisto[laji = [Pohjakartta](http://uri.suomi.fi/codelist/rytj/RY_LahtotietoaineistonLaji/code/11)], ks. seuraavat rivit |
|                               | ```backgroundMapDate```: Lahtotietoaineisto.viimeisinMuutos |
|                               | ```backgroundMapReference```: Lahtotietoaineisto.nimi |
|                               | ```backgroundMapURI```: Lahtotietoaineisto.lisatietolinkki |
| ordinance: OrdinanceValue [1..*] (voidable) | ks. seuraavat rivit
|                                | ```ordinanceReference```: Kasittelytapahtuma[liittyvaAsia = Kaava.paikallinenTunnus JA (laji = [Kaavan hyväksyminen](http://uri.suomi.fi/codelist/rytj/RY_KaavanKasittelytapahtumanLaji/code/09) TAI laji = [Kaavan hyväksyminen oikaisukehotuksen johdosta](http://uri.suomi.fi/codelist/rytj/RY_KaavanKasittelytapahtumanLaji/code/10) TAI laji = [Kaavan kumoaminen](http://uri.suomi.fi/codelist/rytj/RY_KaavanKasittelytapahtumanLaji/code/11))].liittyvaAsiakirja[laji = [Päätös](http://uri.suomi.fi/codelist/rytj/RY_AsiakirjanLaji_YKAK/code/12)].asiakirjanTunnus
|                                | ```ordinanceDate```: Kasittelytapahtuma[liittyvaAsia = Kaava.paikallinenTunnus JA (laji = [Kaavan hyväksyminen](http://uri.suomi.fi/codelist/rytj/RY_KaavanKasittelytapahtumanLaji/code/09) TAI laji = [Kaavan hyväksyminen oikaisukehotuksen johdosta](http://uri.suomi.fi/codelist/rytj/RY_KaavanKasittelytapahtumanLaji/code/10) TAI laji = [Kaavan kumoaminen](http://uri.suomi.fi/codelist/rytj/RY_KaavanKasittelytapahtumanLaji/code/11))].tapahtumanAika

| Assosiaatio-rooli             | Johtaminen Kaavatietomallin tiedoista        | Huomautukset
| ----------------------------- | -------------------------------------------- | ---------------------------------
| officialDocument: OfficialDocumentation [1..*] (voidable) | Kaava.asianLiite | ks. [OfficialDocumentation](#officialdocumentation)
| member: ZoningElement [0..*]  | Kaava.kaavaKohde[maarays.laji = alakoodi([Alueen käyttötarkoitus (asemakaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01)) TAI maarays.laji = alakoodi([Alueen käyttötarkoitus (yleiskaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_YK/code/01))] | ks. [ZoningElement](#zoningelement)
| restriction: SupplementaryRegulation [0..*] | Kaava.kaavaKohde[maarays.laji != alakoodi([Alueen käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01))] | ks. [SupplementaryRegulation (yleismääräykset)](#supplementaryregulation-yleismääräykset) ja [SupplementaryRegulation](#supplementaryregulation)


### ZoningElement

Inspire Planned Land Use -skeeman ```ZoningElement```-luokan tiedot johdetaan loogisen tason Kaavatietomallin [Kaavakohde](dokumentaatio/#kaavakohde)-luokan ja siihen liittyvän [Kaavamaarays](dokumentaatio/#kaavamaarays)-luokan tiedoista alla esitettyjen taulukoiden mukaisesti. Syötteeksi valitaan ne Kaavakohde-luokkien instanssit, jotka ovat joko [asemakaavan käyttötarkoitusalue](../soveltamisohjeet/asemakaava/#sov-ak-vaat-kayttotarkoitusalue-maar)- tai [yleiskaavan aluevaraus](../soveltamisohjeet/yleiskaava/#sov-yk-vaat-aluevaraus-maar) -tyyppisiä, eli joihin liittyy vähintään yksi alueen käyttötarkoitus -tyyppinen kaavamääräys.

| Attribuutti                   |  Johtaminen Kaavatietomallin tiedoista        | Huomautukset
------------------------------- | --------------------------------------------- | -------------------------------
| inspireId: Identifier [1]     |  ks. seuraavat rivit                          |
|                               | ```localId```: Kaavakohde.identiteettiTunnus       |
|                               | ```version```: Kaavakohde.paikallinenTunnus ilman identiteettiTunnus -alkuosaa |
|                               | ```namespace```: <http://paikkatiedot.fi/so/{aineistotunnus}/LU/ZoningElement>, jossa {aineistotunnus} on Maanmittauslaitoksen myöntämä
| geometry: GM_MultiSurface [1]    | Kaavakohde.geometria                           | geometria on aina aluemainen, ks. Soveltamisohjeet [asemakaava, vaatimus ```vaat-aluemainen-kayttotarkoitusalue```](../soveltamisohjeet/asemakaava/##sov-ak-vaat-aluemainen-kayttotarkoitusalue) ja [yleiskaava, vaatimus ```vaat-aluemainen-aluevaraus```](../soveltamisohjeet/yleiskaava/#sov-yk-vaat-aluemainen-aluevaraus)
| validFrom: Date [0..1] (voidable) | Kaavakohde.maarays[laji = alakoodi([Alueen käyttötarkoitus (asemakaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01)) TAI maarays.laji = alakoodi([Alueen käyttötarkoitus (yleiskaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_YK/code/01))][1].voimassaoloAika.begin               |
| validTo: Date [0..1] (voidable) | Kaavakohde.maarays[laji = alakoodi([Alueen käyttötarkoitus (asemakaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01)) TAI maarays.laji = alakoodi([Alueen käyttötarkoitus (yleiskaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_YK/code/01))][1].voimassaoloAika.end                 |
| hilucsLandUse: HILUCSValue [1..*] | Kaavakohde.maarays[laji = alakoodi([Alueen käyttötarkoitus (asemakaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01)) TAI maarays.laji = alakoodi([Alueen käyttötarkoitus (yleiskaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_YK/code/01))].laji | ks. [HILUCSValue (asemakaava)](#hilucsvalue-asemakaava) ja [HILUCSValue (yleiskaava)](#hilucsvalue-yleiskaava)
| beginLifeSpanVersion: DateTime [1] (voidable) | Kaavakohde.viimeisinMuutos                    |
| hilucsPresence: HILUCSPresence [1] (voidable) | ei anneta, [VoidReasonValue: Unknown](https://inspire.ec.europa.eu/codelist/VoidReasonValue/Unknown)              |
| specificLandUse: LandUseClassificationValue [1..*] (voidable) | Kaavakohde.maarays[laji = alakoodi([Alueen käyttötarkoitus (asemakaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01)) TAI maarays.laji = alakoodi([Alueen käyttötarkoitus (yleiskaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_YK/code/01))].laji       | Tulisi johtaa alueen käyttötarkoitus -koodistot, alijoukkoina [Kaavamääräyslaji (asemakaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK)- ja [Kaavamääräyslaji (yleiskaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_YK)-koodistojen ```Alueen käyttötarkoitus```-koodin alikoodeista siten, että ne laajentavat Inspire:n [LandUseClassificationValue](https://inspire.ec.europa.eu/codelist/LandUseClassificationValue)-koodistoja.
| specificPresence: SpecificPresence [1] (voidable) | ei anneta, [VoidReasonValue: Unknown](https://inspire.ec.europa.eu/codelist/VoidReasonValue/Unknown)              |
| regulationNature: RegulationNatureValue [1] | <https://inspire.ec.europa.eu/codelist/RegulationNatureValue/generallyBinding>
| endLifeSpanVersion: DateTime [1] (voidable) | Kaavakohde.korvattuKohteella.tallennusAika      |
| processStepGeneral: ProcessStepGeneralValue [1] (voidable) | Kaavakohde.maarays[laji = alakoodi([Alueen käyttötarkoitus (asemakaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01)) TAI maarays.laji = alakoodi([Alueen käyttötarkoitus (yleiskaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_YK/code/01))].elinkaaritila | ks. [ProcessStepGeneralValue](#processstepgeneralvalue)
| backgroundMap: BackgroundMapValue [1] (voidable) | Kaavakohde.kaava.hyodynnettyAineisto[laji = [Pohjakartta](http://uri.suomi.fi/codelist/rytj/RY_LahtotietoaineistonLaji/code/11)], ks. seuraavat rivit |
|                               | ```backgroundMapDate```: Lahtotietoaineisto.viimeisinMuutos |
|                               | ```backgroundMapReference```: Lahtotietoaineisto.nimi |
|                               | ```backgroundMapURI```: Lahtotietoaineisto.lisatietolinkki |
| dimensioningIndication: DimensioningIndicationValue [0..*] (voidable) | Kaavakohde.maarays | ks. [DimensioningIndicationValue](#dimensioningindicationvalue)

| Assosiaatio-rooli             | Johtaminen Kaavatietomallin tiedoista        | Huomautukset
| ----------------------------- | -------------------------------------------- | ---------------------------------
| plan: SpatialPlan [1]         | Kaavakohde.kaava                             |
| officialDocument: OfficialDocumentation [1..*] (voidable) | ei annetta, [VoidReasonValue: Unpopulated](https://inspire.ec.europa.eu/codelist/VoidReasonValue/Unpopulated)


### SupplementaryRegulation

Inspire Planned Land Use -skeeman ```SupplementaryRegulation```-luokan tiedot johdetaan loogisen tason Kaavatietomallin [Kaavakohde](dokumentaatio/#kaavakohde)-luokan ja siihen liittyvän [Kaavamaarays](dokumentaatio/#kaavamaarays)-luokan tiedoista alla esitettyjen taulukoiden mukaisesti. Syötteeksi valitaan ne Kaavakohde-luokkien instanssit, jotka eivät ole [asemakaavan käyttötarkoitusalue](../soveltamisohjeet/asemakaava/#sov-ak-vaat-kayttotarkoitusalue-maar)- tai [yleiskaavan aluevaraus](../soveltamisohjeet/yleiskaava/#sov-yk-vaat-aluevaraus-maar) -tyyppisiä, eli joihin ei liity yhtään alueen käyttötarkoitus -tyyppistä kaavamääräystä.


| Attribuutti                   |  Johtaminen Kaavatietomallin tiedoista        | Huomautukset
------------------------------- | --------------------------------------------- | -------------------------------
| validFrom: Date [0..1] (voidable) | Kaavakohde.maarays[1].voimassaoloAika.begin        | 
| validTo: Date [0..1] (voidable) | Kaavakohde.maarays[1].voimassaoloAika.begin            | 
| specificSupplementaryRegulation: SpecificSupplementaryRegulationValue [1..*] (voidable) | Kaavakohde.maarays.laji | Tulisi määritellä [Kaavamääräyslaji (asemakaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK)- ja [Kaavamääräyslaji (yleiskaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_YK) -koodistot laajentamaan Inspire:n [SpecificSupplementaryRegulationValue](https://inspire.ec.europa.eu/codelist/SpecificSupplementaryRegulationValue)-koodistoa
| processStepGeneral: ProcessStepGeneralValue [1] (voidable) | Kaavakohde.maarays[1].elinkaaritila | ks. [ProcessStepGeneralValue](#processstepgeneralvalue)
| backgroundMap: BackgroundMapValue [1] (voidable) | Kaavakohde.kaava.hyodynnettyAineisto[laji = [Pohjakartta](http://uri.suomi.fi/codelist/rytj/RY_LahtotietoaineistonLaji/code/11)], ks. seuraavat rivit |
|                               | ```backgroundMapDate```: Lahtotietoaineisto.viimeisinMuutos |
|                               | ```backgroundMapReference```: Lahtotietoaineisto.nimi |
|                               | ```backgroundMapURI```: Lahtotietoaineisto.lisatietolinkki |
| beginLifeSpanVersion: DateTime [1] (voidable) | Kaavakohde.viimeisinMuutos                    |
| dimensioningIndication: DimensioningIndicationValue [0..*] (voidable) | Kaavakohde.maarays | ks. [DimensioningIndicationValue](#dimensioningindicationvalue)
| inspireId: Identifier [1]     |  ks. seuraavat rivit                          |
|                               | ```localId```: Kaavakohde.identiteettiTunnus       | 
|                               | ```version```: Kaavakohde.paikallinenTunnus ilman identiteettiTunnus -alkuosaa |
|                               | ```namespace```: <http://paikkatiedot.fi/so/{aineistotunnus}/LU/SupplementaryRegulation>, jossa {aineistotunnus} on Maanmittauslaitoksen myöntämä
| endLifeSpanVersion: DateTime [1] (voidable) | Kaavakohde.korvattuKohteella.tallennusAika      |
| geometry: GM_Object [1]       | Kaavakohde.geometria |
| inheritedFromOtherPlans: Boolean [1] (voidable) | ei anneta, [VoidReasonValue: Unpopulated](https://inspire.ec.europa.eu/codelist/VoidReasonValue/Unpopulated)  |
| specificRegulationNature: CharacterString [1] (voidable) | ei anneta, [VoidReasonValue: Unpopulated](https://inspire.ec.europa.eu/codelist/VoidReasonValue/Unpopulated)
| name: CharacterString [0..*] (voidable) | Kaavakohde.maarays.nimi                  | valitaan yksi kieli käyttäjän preferessin perusteella
| regulationNature: RegulationNatureValue [1] | <https://inspire.ec.europa.eu/codelist/RegulationNatureValue/generallyBinding>
| supplementaryRegulation: SupplementaryRegulationValue [1..*] | Kaavakohde.maarays.laji | ks. [SupplementaryRegulationValue (asemakaava)](#supplementaryregulationvalue-asemakaava) ja [SupplementaryRegulationValue (yleiskaava)](#supplementaryregulationvalue-yleiskaava)

| Assosiaatio-rooli             | Johtaminen Kaavatietomallin tiedoista        | Huomautukset
| ----------------------------- | -------------------------------------------- | ---------------------------------
| plan: SpatialPlan [1]         | Kaavakohde.kaava                             |
| officialDocument: OfficialDocumentation [1..*] (voidable) | ei annetta, [VoidReasonValue: Unpopulated](https://inspire.ec.europa.eu/codelist/VoidReasonValue/Unpopulated)

### SupplementaryRegulation (yleismääräykset)

Inspire Planned Land Use -skeeman ```SupplementaryRegulation```-luokan tiedot johdetaan kaavan yleismääräysten tapauksessa loogisen tason Kaavatietomallin [Kaava](dokumentaatio/#kaava)-luokan ja siihen liittyvän [Kaavamaarays](dokumentaatio/#kaavamaarays)-luokan tiedoista alla esitettyjen taulukoiden mukaisesti. Kutakin kaavaa kohden luodaan enintään yksi SupplementaryRegulation-luokan instanssi.


| Attribuutti                   |  Johtaminen Kaavatietomallin tiedoista        | Huomautukset
------------------------------- | --------------------------------------------- | -------------------------------
| validFrom: Date [0..1] (voidable) | Kaava.yleismaarays[1].voimassaoloAika.begin        | 
| validTo: Date [0..1] (voidable) | Kaava.yleismaarays[1].voimassaoloAika.begin            | 
| specificSupplementaryRegulation: SpecificSupplementaryRegulationValue [1..*] (voidable) | Kaava.yleismaarays.laji | 
| processStepGeneral: ProcessStepGeneralValue [1] (voidable) | Kaava.yleismaarays[1].elinkaaritila | ks. [ProcessStepGeneralValue](#processstepgeneralvalue)
| backgroundMap: BackgroundMapValue [1] (voidable) | Kaava.hyodynnettyAineisto[laji = [Pohjakartta](http://uri.suomi.fi/codelist/rytj/RY_LahtotietoaineistonLaji/code/11)], ks. seuraavat rivit |
|                               | ```backgroundMapDate```: Lahtotietoaineisto.viimeisinMuutos |
|                               | ```backgroundMapReference```: Lahtotietoaineisto.nimi |
|                               | ```backgroundMapURI```: Lahtotietoaineisto.lisatietolinkki |
| beginLifeSpanVersion: DateTime [1] (voidable) | Kaava.viimeisinMuutos                    |
| dimensioningIndication: DimensioningIndicationValue [0..*] (voidable) | Kaava.yleismaarays | ks. [DimensioningIndicationValue](#dimensioningindicationvalue)
| inspireId: Identifier [1]     |  ks. seuraavat rivit                          |
|                               | ```localId```: Kaava.identiteettiTunnus       | 
|                               | ```version```: Kaava.paikallinenTunnus ilman identiteettiTunnus -alkuosaa |
|                               | ```namespace```: <http://paikkatiedot.fi/so/{aineistotunnus}/LU/SupplementaryRegulation>, jossa {aineistotunnus} on Maanmittauslaitoksen myöntämä
| endLifeSpanVersion: DateTime [1] (voidable) | Kaava.korvattuKohteella.tallennusAika      |
| geometry: GM_Object [1]       | Kaava.aluerajaus |
| inheritedFromOtherPlans: Boolean [1] (voidable) | ei anneta, [VoidReasonValue: Unpopulated](https://inspire.ec.europa.eu/codelist/VoidReasonValue/Unpopulated)  |
| specificRegulationNature: CharacterString [1] (voidable) | ei anneta, [VoidReasonValue: Unpopulated](https://inspire.ec.europa.eu/codelist/VoidReasonValue/Unpopulated)
| name: CharacterString [0..*] (voidable) | Kaava.yleismaarays.nimi                  | valitaan yksi kieli käyttäjän preferessin perusteella
| regulationNature: RegulationNatureValue [1] | <https://inspire.ec.europa.eu/codelist/RegulationNatureValue/generallyBinding>
| supplementaryRegulation: SupplementaryRegulationValue [1..*] | Kaava.yleismaarays.laji | ks. [SupplementaryRegulationValue (asemakaava)](#supplementaryregulationvalue-asemakaava) ja [SupplementaryRegulationValue (yleiskaava)](#supplementaryregulationvalue-yleiskaava)

| Assosiaatio-rooli             | Johtaminen Kaavatietomallin tiedoista        | Huomautukset
| ----------------------------- | -------------------------------------------- | ---------------------------------
| plan: SpatialPlan [1]         | Kaava                                        |
| officialDocument: OfficialDocumentation [1..*] (voidable) | ei annetta, [VoidReasonValue: Unpopulated](https://inspire.ec.europa.eu/codelist/VoidReasonValue/Unpopulated)

### OfficialDocumentation

Inspire Planned Land Use -skeeman ```OfficialDocument```-luokan tiedot johdetaan [Asiakirja](dokumentaatio/#asiakirja)-luokan tiedoista alla esitetyn taulukon mukaisesti. 
Syötteeksi valitaan kaikki kaavan Asiakirja-instanssit, joihin viitataan jollain seuraavista tavoista:
* [Kaava](dokumentaatio/#kaava)-luokan instansseista assosiaation ```asianLiite``` avulla,
* [Kaava](dokumentaatio/#kaava)-luokan instansseista assosiaation ```selostus``` ja edelleen [Kaavaselostus](dokumentaatio/#kaavaselostus)-luokan assosiaation ```asiakirja``` avulla, tai
* [Kaava](dokumentaatio/#kaava)-luokan instansseista assosiaation ```osallistumisJaArviointisuunnitelma``` ja edelleen [OsallistumisJaArviointisuunnitelma](dokumentaatio/#osallistumisjaarviointisuunnitelma)-luokan assosiaation ```asiakirja``` avulla.

| Attribuutti                   |  Johtaminen Kaavatietomallin tiedoista        | Huomautukset
------------------------------- | --------------------------------------------- | -------------------------------
| inspireId: Identifier [1]     |  ks. seuraavat rivit                          |
|                               | ```localId```: Asiakirja.identiteettiTunnus   | 
|                               | ```version```: Asiakirja.paikallinenTunnus ilman identiteettiTunnus -alkuosaa |
|                               | ```namespace```: <http://paikkatiedot.fi/so/{aineistotunnus}/LU/OfficialDocumentation>, jossa {aineistotunnus} on Maanmittauslaitoksen myöntämä
| legislationCitation: LegislationCitation[0..1] (voidable) | ei tuoteta        |
| regulationText: CharacterString[0..1] (voidable) | ei tuoteta                 |
| planDocument: DocumentCitation[0..1] (voidable) | ks. seuraavat rivit         |
|                               | ```name```: Asiakirja.nimi                    | valitaan yksi kieli käyttäjän preferessin perusteella
|                               | ```date```: Asiakirja.viimeisinMuutos         | Poimitaan vain päivämäärä
|                               | ```link```: Asiakirja.viittausTunnus          |
|                               | ```specificReference```: ei tuoteta           |

### DimensioningIndicationValue

Riippuen Kaavamaarays-luokan instanssin ```arvo```-attribuuttien luokista tuotetaan yksi tai useampi [DimensioningIndicationRealValue](#dimensioningindicationrealvalue)-, [DimensioningIndicationMeasureValue](#dimensioningindicationmeasurevalue)- tai [DimensioningIndicationCharacterValue](#dimensioningindicationcharactervalue)-luokan instanssi.

{% include common/note.html content="PLU-mallin DimensioningIndicationValue -luokan käyttäminen kaikkien kaavamääräysten arvojen koodaamiseen laventaa todennäköisesti ko. luokan alkuperäistä käyttöä jonkin verran, sillä nimensä perusteella sitä voisi kuvitella tarkoitettavan käyttää vain 'mitoitustiedon' ilmaisemiseen. Toisaalta [Data Specification on Land Use – Technical Guidelines, v. 3.0](https://inspire.ec.europa.eu/id/document/tg/lu) kuvaa DimensioningIndicationValue:n käytön vain hyvin ylimalkaisesti." %}

{% include common/note.html content="Kaavamääräysten arvot, jotka ovat tyyppiä [GeometriaArvo](dokumentaatio/#geometriaarvo), ei muunneta Inspire-muotoon, koska käyttökelpoista kohdetyyppiä ei ole PLU-skeemassa määritelty." %}

{% include common/note.html content="Kaavamääräysten lisätietoja ei muunneta Inspire-muotoon, koska käyttökelpoista kohdetyyppiä ei ole PLU-skeemassa määritelty. " %}

### DimensioningIndicationRealValue

Inspire Planned Land Use -skeeman ```DimensioningIndicationRealValue``` tiedot johdetaan loogisen tason Kaavatietomallin [Kaavamaarays](dokumentaatio/#kaavamaarays)-luokan ja siihen liittyvän [Arvo](dokumentaatio/#arvo)-luokan tiedoista alla esitetyn taulukon mukaisesti. Syötteeksi valitaan ne Kaavamaarays-luokan instanssit, joiden ```arvo```-attribuutilla on vähintään yksi sellainen [NumeerinenArvo](dokumentaatio/#numeerinenarvo)- tai [NumeerinenArvovali](dokumentaatio/#numeerinenarvovali)-luokan instanssi, jonka ```yksikko```-attribuuttia ei ole annettu, ja jonka ```arvo```-attribuutin tyyppi toteuttaa [Real](dokumentaatio/#real)-rajapinnan. Kutakin NumeerinenArvo-luokan instanssia kohden luodaan yksi ja kutakin NumeerinenArvovali-luokan instanssia kohden kaksi DimensioningIndicationRealValue-instanssia (nimeäminen ks. indicationReference).

| Attribuutti                   |  Johtaminen Kaavatietomallin tiedoista        | Huomautukset
------------------------------- | --------------------------------------------- | -------------------------------
| indicationReference: CharacterString [1] | Kaavamaarays.arvo[luokka = NumeerinenArvo TAI NumeerinenArvovali].laji | Mikäli kyseessä on arvoväli, luodaan kaksi instanssia, joiden indicationReference-arvot ovat NumeerinenArvovali.laji + '#minimiarvo' ja NumeerinenArvovali.laji + '#maksimiarvo'
| value: Real[1]                | Kaavamaarays.arvo[luokka = NumeerinenArvo].arvo TAI Kaavamaarays.arvo[luokka = NumeerinenArvovali].minimiarvo ja maksimiarvo | Mikäli kyseessä on arvoväli, luodaan kaksi instanssia, joiden value-arvot ovat NumeerinenArvovali.minimiarvo ja NumeerinenArvovali.maksimiarvo

### DimensioningIndicationIntegerValue

Inspire Planned Land Use -skeeman ```DimensioningIndicationIntegerValue``` tiedot johdetaan loogisen tason Kaavatietomallin [Kaavamaarays](dokumentaatio/#kaavamaarays)-luokan ja siihen liittyvän [Arvo](dokumentaatio/#arvo)-luokan tiedoista alla esitetyn taulukon mukaisesti. Syötteeksi valitaan ne Kaavamaarays-luokan instanssit, joiden ```arvo```-attribuutilla on vähintään yksi sellainen [NumeerinenArvo](dokumentaatio/#numeerinenarvo)- tai [NumeerinenArvovali](dokumentaatio/#numeerinenarvovali)-luokan instanssi, jonka ```yksikko```-attribuuttia ei ole annettu, ja jonka ```arvo```-attribuutin tyyppi toteuttaa [Integer](dokumentaatio/#integer)-rajapinnan. Kutakin NumeerinenArvo-luokan instanssia kohden luodaan yksi ja kutakin NumeerinenArvovali-luokan instanssia kohden kaksi DimensioningIndicationRealValue-instanssia (nimeäminen ks. indicationReference).

| Attribuutti                   |  Johtaminen Kaavatietomallin tiedoista        | Huomautukset
------------------------------- | --------------------------------------------- | -------------------------------
| indicationReference: CharacterString [1] | Kaavamaarays.arvo[luokka = NumeerinenArvo TAI NumeerinenArvovali].laji | Mikäli kyseessä on arvoväli, luodaan kaksi instanssia, joiden indicationReference-arvot ovat NumeerinenArvovali.laji + '#minimiarvo' ja NumeerinenArvovali.laji + '#maksimiarvo'
| value: Integer[1]                | Kaavamaarays.arvo[luokka = NumeerinenArvo].arvo TAI Kaavamaarays.arvo[luokka = NumeerinenArvovali].minimiarvo ja maksimiarvo | Mikäli kyseessä on arvoväli, luodaan kaksi instanssia, joiden value-arvot ovat NumeerinenArvovali.minimiarvo ja NumeerinenArvovali.maksimiarvo

### DimensioningIndicationMeasureValue

Inspire Planned Land Use -skeeman ```DimensioningIndicationMeasureValue``` tiedot johdetaan loogisen tason Kaavatietomallin [Kaavamaarays](dokumentaatio/#kaavamaarays)-luokan ja siihen liittyvän [Arvo](dokumentaatio/#arvo)-luokan tiedoista alla esitetyn taulukon mukaisesti. Syötteeksi valitaan ne Kaavamaarays-luokan instanssit, joiden ```arvo```-attribuutilla on vähintään yksi sellainen [NumeerinenArvo](dokumentaatio/#numeerinenarvo)- tai [NumeerinenArvovali](dokumentaatio/#numeerinenarvovali)-luokan instanssi, jonka ```yksikko```-attribuutti on annettu. Kutakin NumeerinenArvo-luokan instanssia kohden luodaan yksi ja kutakin NumeerinenArvovali-luokan instanssia kohden kaksi DimensioningIndicationMeasureValue-instanssia (nimeäminen ks. indicationReference).

| Attribuutti                   |  Johtaminen Kaavatietomallin tiedoista        | Huomautukset
------------------------------- | --------------------------------------------- | -------------------------------
| indicationReference: CharacterString [1] | Kaavamaarays.arvo[luokka = NumeerinenArvo TAI NumeerinenArvovali].laji | Mikäli kyseessä on arvoväli, luodaan kaksi instanssia, joiden indicationReference-arvot ovat NumeerinenArvovali.laji + '#minimiarvo' ja NumeerinenArvovali.laji + '#maksimiarvo'
| value: Measure[1]                | ks. seuraavat rivit                        |
|                                  | ```value```: Kaavamaarays.arvo[luokka = NumeerinenArvo].arvo TAI Kaavamaarays.arvo[luokka = NumeerinenArvovali].minimiarvo ja maksimiarvo | Mikäli kyseessä on arvoväli, luodaan kaksi instanssia, joiden value-arvot ovat NumeerinenArvovali.minimiarvo ja NumeerinenArvovali.maksimiarvo
|                                  | ```unitOfMeasure```: Kaavamaarays .arvo[luokka = NumeerinenArvo].yksikko TAI Kaavamaarays.arvo[luokka = NumeerinenArvovali].yksikko |

### DimensioningIndicationCharacterValue

Inspire Planned Land Use -skeeman ```DimensioningIndicationCharacterValue``` tiedot johdetaan loogisen tason Kaavatietomallin [Kaavamaarays](dokumentaatio/#kaavamaarays)-luokan ja siihen liittyvän [Arvo](dokumentaatio/#arvo)-luokan tiedoista alla esitetyn taulukon mukaisesti. Syötteeksi valitaan ne Kaavamaarays-luokan instanssit, joiden ```arvo```-attribuutilla on vähintään yksi [TekstiArvo](dokumentaatio/#tekstiarvo)-, [KoodiArvo](dokumentaatio/#koodiarvo)-, [TunnusArvo](dokumentaatio/#tunnusarvo)-, [Ajanhetkiarvo](dokumentaatio/#ajanhetkiarvo)- tai [Aikavaliarvo](dokumentaatio/#aikavaliarvo)-luokan instanssi. Kutakin Arvo-luokan instanssia luodaan kohden yksi DimensioningIndicationCharacterValue-instanssi.

| Attribuutti                   |  Johtaminen Kaavatietomallin tiedoista        | Huomautukset
------------------------------- | --------------------------------------------- | -------------------------------
| indicationReference: CharacterString [1] | Kaavamaarays.arvo[luokka = TekstiArvo TAI luokka = KoodiArvo TAI luokka = TunnusArvo TAI luokka = Ajanhetkiarvo TAI luokka = Aikavaliarvo].laji |
| value: CharacterString[1]     | ks. seuraavat rivit                           | valitaan yksi seuraavien rivien vaihtoehdoista
|                               | Kaavamaarays.arvo[luokka = TekstiArvo].arvo   | valitaan yksi kieli käyttäjän preferessin perusteella
|                               | Kaavamaarays.arvo[luokka = KoodiArvo].arvo    | URI-arvo koodataan merkkijonona
|                               | Kaavamaarays.arvo[luokka = TunnusArvo].arvo   | URI-arvo koodataan merkkijonona
|                               | Kaavamaarays.arvo[luokka = Ajanhetkiarvo].arvo| Koodataan ajanhetki [IETF RFC 3339](https://tools.ietf.org/html/rfc3339)-standardin mukaisena päivämäärä tai päivämäärä + kelloaika -yhdistelmänä
|                               | Kaavamaarays.arvo[luokka = Aikavaliarvo].arvo | Koodataan aikaväli kahtena [IETF RFC 3339](https://tools.ietf.org/html/rfc3339)-standardin mukaisena päivämäärä tai päivämäärä + kelloaika -yhdistelmänä erotettuna väliviivalla (```-```). Jos alku tai loppu puuttuu (indeterminatePosition = unknown), ei ko. arvoa tuoteta väliviivan kyseiselle puolelle.

## Koodistojen vastaavuudet

### ProcessStepGeneralValue

[Elinkaaren tila (yleis- ja asemakaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaaritila)-koodiston arvo kuvataan Inspire:n [Process Step General](https://inspire.ec.europa.eu/codelist/ProcessStepGeneralValue)-koodiston arvoiksi alla olevan taulukon mukaisesti.

Elinkaaren tila                                                                            | Process Step General               |
------------------------------------------------------------------------------------------ | -----------------------------------|
[Kaavoitusaloite](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/01)        | [luonnnos (elaboration)](https://inspire.ec.europa.eu/codelist/ProcessStepGeneralValue/elaboration)
[Vireilletullut](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/02)         | [luonnnos (elaboration)](https://inspire.ec.europa.eu/codelist/ProcessStepGeneralValue/elaboration)
[Valmistelu](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/03)             | [luonnnos (elaboration)](https://inspire.ec.europa.eu/codelist/ProcessStepGeneralValue/elaboration)
[Kaavaehdotus](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/04)           | [ehdotus (in the process of adoption)](https://inspire.ec.europa.eu/codelist/ProcessStepGeneralValue/adoption)
[Tarkistettu kaavaehdotus](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/05) | [ehdotus (in the process of adoption)](https://inspire.ec.europa.eu/codelist/ProcessStepGeneralValue/adoption)
[Hyväksytty kaava](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/06)       | [ehdotus (in the process of adoption)](https://inspire.ec.europa.eu/codelist/ProcessStepGeneralValue/adoption)
[Oikaisukehotuksen alainen](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/07) | [ehdotus (in the process of adoption)](https://inspire.ec.europa.eu/codelist/ProcessStepGeneralValue/adoption)
[Valituksen alainen](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/08)     | [ehdotus (in the process of adoption)](https://inspire.ec.europa.eu/codelist/ProcessStepGeneralValue/adoption) 
[Osittain voimassa](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/09)      | [laillisesti sitova tai voimassa (legally binding or active)](https://inspire.ec.europa.eu/codelist/ProcessStepGeneralValue/legalForce)
[Voimassa](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/10)               | [laillisesti sitova tai voimassa (legally binding or active)](https://inspire.ec.europa.eu/codelist/ProcessStepGeneralValue/legalForce)
[Kumottu](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/11)                | [kumottu (obsolete)](https://inspire.ec.europa.eu/codelist/ProcessStepGeneralValue/obsolete)
[Kumoutunut](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/12)             | [kumottu (obsolete)](https://inspire.ec.europa.eu/codelist/ProcessStepGeneralValue/obsolete)
[Rauennut](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/13)               | [kumottu (obsolete)](https://inspire.ec.europa.eu/codelist/ProcessStepGeneralValue/obsolete)
[Hylätty](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/14)                | [kumottu (obsolete)](https://inspire.ec.europa.eu/codelist/ProcessStepGeneralValue/obsolete)

### HILUCSValue (asemakaava)

Kaavamääräyslaji (asemakaava) -koodiston koodin [Alueen käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01) alikoodit kuvautuvat Inspire [HILUCSValue](https://inspire.ec.europa.eu/codelist/HILUCSValue)-koodiston arvoiksi alla olevien taulukkojen mukaisesti.

#### Asuminen

Kaavamääräyslaji (asemakaava)                                                                         | HILUCSValue                       | Huomautukset
------------------------------------------------------------------------------------------------------|-----------------------------------|-----------------|
[Asuminen](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0101)                        | [asuinalueet (residential use)](https://inspire.ec.europa.eu/codelist/HILUCSValue/5_ResidentialUse) |
[Asuinkerrostaloalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010101)           | |
[Asuinpientaloalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010102)             | |
[Rivitalojen ja muiden kytkettyjen asuinrakennusten alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010103)           | |
[Erillispientaloalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010104)           | |
[Asumista palveleva yhteiskäyttöinen alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010105)           | |
[Maatilan talouskeskuksen alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010106)           | |
[Kyläalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010107)           | |
[Erityisryhmien palveluasuminen](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010108)           | |
[Muu asuminen](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010109)           | |


#### Keskustatoiminnot

Kaavamääräyslaji (asemakaava)                                                                         | HILUCSValue                       | Huomautukset
------------------------------------------------------------------------------------------------------|-----------------------------------|-----------------|
[Keskustatoiminnot](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0102)               | ?                                 | |
[Keskustatoimintojen alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010201)      | [asuinalueet (residential use)](https://inspire.ec.europa.eu/codelist/HILUCSValue/5_ResidentialUse) | HILUCSValue-koodin määritelmässä: "Tähän luokkaan kuuluvat myös asuinalueet, joita käytetään yhdessä muiden soveltuvien käyttötarkoitusten kanssa (keskusta-alueet)..." |
[Keskustatoimintojen alakeskus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010202) | | |
[Muut keskustatoiminnot](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010203)        | | |

{% include question.html content="Ei ole selvää, onko päätason koodia 'Keskustatoiminnot' tarkoitus voida käyttää sellaisenaan, vai vain ryhmittelyotsikkona? Jos tarkoitus olla yleiskoodi kaikille keskustatoiminnoille, niin tulisiko koodi '010201 Keskustatoimintojen' alue olla 'Keskustatoimintojen pääkeskus' tms.?" %}


#### Liike- ja toimistorakentaminen

Kaavamääräyslaji (asemakaava)                                                                         | HILUCSValue                       | Huomautukset
------------------------------------------------------------------------------------------------------|-----------------------------------|-----------------|
[Liike- ja toimistorakentaminen](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0103)  | | |
[Liikerakennusten alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010301)         | | |
[Toimistorakennusten alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010302)      | | |
[Toimitilarakennusten alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010303)     | | |
[Kaupallisten palvelujen alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010304)  | | |
[Muu liike- ja toimistorakentaminen](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010305) | | |


#### Palvelut

Kaavamääräyslaji (asemakaava)                                                                         | HILUCSValue                       | Huomautukset
------------------------------------------------------------------------------------------------------|-----------------------------------|-----------------|
[Palvelut](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0104)                        | | |
[Palvelurakennusten alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010401)       | | |
[Lähipalvelujen alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010402)           | | |
[Huvi- ja viihdepalvelujen alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010403) | | |
[Muut palvelut](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010404)                 | | |

#### Julkiset palvelut

Kaavamääräyslaji (asemakaava)                                                                         | HILUCSValue                       | Huomautukset
------------------------------------------------------------------------------------------------------|-----------------------------------|-----------------|
[Julkiset palvelut](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0105)               | | |
[Julkiset palvelut](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010501)             | | |
[Yleisten rakennusten alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010502)     | | |
[Julkisten lähipalvelujen alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010503) | | |
[Hallinto- ja virastorakennusten alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010504) | | |
[Opetustoimintaa palvelevien rakennusten alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010505) | | |
[Sosiaalitointa ja terveydenhuoltoa palvelevien rakennusten alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010506) | | |
[Kulttuuritoimintaa palvelevien rakennusten alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010507) | | |
[Museorakennusten alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010508)         | | |
[Kirkkojen ja muiden seurakunnallisten rakennusten alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010509) | | |
[Urheilutoimintaa palvelevien rakennusten alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010510) | | |
[Julkisten palvelujen ja hallinnon alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010511) | | Miten eroaa koodista 010510 Julkiset palvelut ?|
[Muut julkiset palvelut](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010501)        | | |

{% include question.html content="Ei ole selvää, onko päätason koodia 'Julkiset palvelut (0105)' tarkoitus voida käyttää sellaisenaan, vai vain ryhmittelyotsikkona? Jos tarkoitus olla yleiskoodi kaikille julkisille palveluille, niin tulisiko koodi '010501 Julkiset palvelut' poistaa?" %}

#### Työ ja tuotanto

Kaavamääräyslaji (asemakaava)                                                                         | HILUCSValue                       | Huomautukset
------------------------------------------------------------------------------------------------------|-----------------------------------|-----------------|
[Työ ja tuotanto](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0106)                 | | |
[Työpaikka-alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010601)                | | |
[Teollisuusalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010602)                | | |
[Varastorakennusten alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010603)       | | |
[Alue, jolle saa sijoittaa merkittävän, vaarallisia kemikaaleja valmistavan tai varastoivan laitoksen](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010604) | | |
[Ympäristövaikutuksiltaan merkittävien teollisuustoimintojen alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010605) | | |
[Kiertotalous](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010606)                 | | |
[Ympäristöhäiriötä aiheuttava teollisuustoiminta](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010607) | | |
[Muu työpaikka tai tuotantoalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010608) | | |

{% include bug.html content="Koodistossa 'Muu työpaikka tai tuontantoalue', tulisi olla 'Muu työpaikka tai tuotantoalue'" %}

#### Virkistys

Kaavamääräyslaji (asemakaava)                                                                         | HILUCSValue                       | Huomautukset
------------------------------------------------------------------------------------------------------|-----------------------------------|-----------------|
[Virkistys](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0107)                       | | |
[Virkistyalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010701)                  | | |
[Puisto](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010702)                        | | |
[Lähivirkistysalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010703)             | | |
[Leikkipuisto](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010704)                  | | |
[Urheilupalvelujen alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010705)        | | |
[Retkeily- ja ulkoilualue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010706)      | | |
[Uimaranta-alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010707)                | | |
[Lähimetsä](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010708)                     | | |
[Muu virkistysalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010709)             | | |

{% include question.html content="Ei ole selvää, onko päätason koodia 'Virkistys (0107)' tarkoitus voida käyttää sellaisenaan, vai vain ryhmittelyotsikkona? Jos tarkoitus olla yleiskoodi kaikille virkistysalueille, niin tulisiko koodi '010701 Virkistysalue' poistaa?" %}

#### Loma-asuminen ja matkailu

Kaavamääräyslaji (asemakaava)                                                                         | HILUCSValue                       | Huomautukset
------------------------------------------------------------------------------------------------------|-----------------------------------|-----------------|
[Loma-asuminen ja matkailu](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0108)       | | |
[Loma-asuntojen alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010801)           | | |
[Matkailua palvelevien rakennusten alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010802) | | |
[Leirintäalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010803)                  | | |
[Asuntovaunualue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010804)               | | |
[Siirtolapuutarha-/palstaviljelyalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010805) | | |
[Muu loma-asumisen tai matkailun alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010806) | | |

#### Liikenne

Kaavamääräyslaji (asemakaava)                                                                         | HILUCSValue                       | Huomautukset
------------------------------------------------------------------------------------------------------|-----------------------------------|-----------------|
[Liikenne](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0109)                        | | |
[Liikennealue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010901)                  | | |
[Yleisen tien alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010902)             | | |
[Rautatieliikenteen alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010903)       | | |
[Lentoliikenteen alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010904)          | | |
[Satama-alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010905)                   | | |
[Kanava-alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010906)                   | | |
[Venesatama/venevalkama](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010907)        | | |
[Yleinen pysäköintialue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010908)        | | |
[Huoltoasema-alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010909)              | | |
[Henkilöliikenteen terminaalialue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010910) | | |
[Tavaraliikenteen terminaalialue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010911) | | |
[Yleisten pysäköintilaitosten alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010912) | | |
[Autopaikkojen alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010913)            | | |
[Katualue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010914)                      | | |
[Muu liikennealue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010915)              | | |

{% include question.html content="Ei ole selvää, onko päätason koodia 'Liikenne (0109)' tarkoitus voida käyttää sellaisenaan, vai vain ryhmittelyotsikkona? Jos tarkoitus olla yleiskoodi kaikille liikennealueille, niin tulisiko koodi '010901 Liikennealue' poistaa?" %}

#### Erityisalueet

Kaavamääräyslaji (asemakaava)                                                                         | HILUCSValue                       | Huomautukset
------------------------------------------------------------------------------------------------------|-----------------------------------|-----------------|
[Erityisalueet](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0110)                   | | |
[Erityisalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011001)                   | | |
[Yhdyskuntateknisen huollon alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011002) | | |
[Energiahuollon alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011003)           | | |
[Jätteenkäsittelyalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011004)          | | |
[Maa-ainesten ottoalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011005)         | | |
[Kaivoisalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011006)                   | | |
[Mastoalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011007)                     | | |
[Ampumarata-alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011008)               | | |
[Puolustusvoimien alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011009)         | | |
[Hautausmaa-alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011010)               | | |
[Suojaviheralue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011011)                | | |
[Tuulivoimaloiden alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011012)         | | |
[Moottorirata](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011013)                  | | |
[Maa-ainesten vastaanotto- tai läjitysalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011014) | | |
[Vankila-alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011015)                  | | |
[Muu erityisalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011016)               | | |

{% include question.html content="Ei ole selvää, onko päätason koodia 'Erityisalueet (0110)' tarkoitus voida käyttää sellaisenaan, vai vain ryhmittelyotsikkona? Jos tarkoitus olla yleiskoodi kaikille erityisalueille, niin tulisiko koodi '011001 Erityisalue' poistaa?" %}

#### Suojelu

Kaavamääräyslaji (asemakaava)                                                                         | HILUCSValue                       | Huomautukset
------------------------------------------------------------------------------------------------------|-----------------------------------|-----------------|
[Suojelu](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0111)                         | | |
[Suojelualue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011101)                   | | |
[Luonnonsuojelualue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011102)            | | |
[Muinaismuistoalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011103)             | | |
[Rakennuslainsäädännön nojalla suojeltava alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011104)  | | |
[Rakennussuojelulakien nojalla suojeltu alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011105) | | |
[Muu suojelualue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011106)               | | |

{% include question.html content="Ei ole selvää, onko päätason koodia 'Suojelu (0111)' tarkoitus voida käyttää sellaisenaan, vai vain ryhmittelyotsikkona? Jos tarkoitus olla yleiskoodi kaikille suojelualueille, niin tulisiko koodi '011101 Suojelualue' poistaa?" %}

{% include question.html content="Ilmausten 'Rakennuslainsäädännön nojalla' ja 'Rakennussuojelulakien nojalla' ero?" %}

{% include question.html content="Mitkä näistä ovat todellisuudessa asemakaavassa päätettäviä, mitkä lähtötietoaineistoja?" %}

#### Maa- ja metsätalous

Kaavamääräyslaji (asemakaava)                                                                         | HILUCSValue                       | Huomautukset
------------------------------------------------------------------------------------------------------|-----------------------------------|-----------------|
[Maa- ja metsätalous](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0112)             | | |
[Maa- ja metsätalousalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011201)       | | |
[Maatalousalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011202)                  | | |
[Kotieläintalouden suuryksikön alue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011203) | | |
[Puutarha- ja kasvihuonealue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011204)   | | |
[Maisemallisesti arvokas peltoalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011205) | | |
[Poronhoitovaltainen maa- ja metsätalousalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011206) | | |
[Muu maa- ja metsätalousalue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011207)   | | |

{% include question.html content="Ei ole selvää, onko päätason koodia 'Maa- ja metsätalous (0112)' tarkoitus voida käyttää sellaisenaan, vai vain ryhmittelyotsikkona? Jos tarkoitus olla yleiskoodi kaikille maa- ja metsätalousalueille, niin tulisiko koodi '011201 Maa- ja metsätalousalue' poistaa?" %}

{% include question.html content="Koodi 'Poronhoitovaltainen maa- ja metsätalousalue' on koko koodiston ainoa, jossa esiintyy '-valtainen', tulisiko olla vain 'Poronhoitoalue', kun käyttötarkoituksia voidaan antaa useita?" %}

#### Vesialueet

Kaavamääräyslaji (asemakaava)                                                                         | HILUCSValue                       | Huomautukset
------------------------------------------------------------------------------------------------------|-----------------------------------|-----------------|
[Vesialueet](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0113)                      | | |
[Vesialue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011301)                      | | |
[Muu vesialue](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/011302)                  | | |


{% include question.html content="Ei ole selvää, onko päätason koodia 'Vesialueet (0113)' tarkoitus voida käyttää sellaisenaan, vai vain ryhmittelyotsikkona? Jos tarkoitus olla yleiskoodi kaikillevesialueille, niin tulisiko koodi '011301 Vesialue' poistaa?" %}

{% include question.html content="'Muu vesialue' ei ole mielekäs, kun vesialuetyyppejä on vain yleinen vesialue. Muu kuin mikä?" %}

### HILUCSValue (yleiskaava)

Kaavamääräyslaji (yleiskaava) -koodiston koodin [Alueen käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_YK/code/01) alikoodit kuvautuvat Inspire [HILUCSValue](https://inspire.ec.europa.eu/codelist/HILUCSValue)-koodiston arvoiksi alla olevien taulukojen mukaisesti.

### SupplementaryRegulationValue (asemakaava)

[Kaavamääräyslaji (asemakaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/) -koodiston koodit, poislukien koodin [Alueen käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01) alikoodit, kuvautuvat Inspire [SupplementaryRegulationValue](https://inspire.ec.europa.eu/codelist/SupplementaryRegulationValue)-koodiston arvoiksi alla olevan taulukon mukaisesti.

### SupplementaryRegulationValue (yleiskaava)

[Kaavamääräyslaji (yleiskaava)](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_YK/) -koodiston koodit, poislukien koodin [Alueen käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_YK/code/01) alikoodit, kuvautuvat Inspire [SupplementaryRegulationValue](https://inspire.ec.europa.eu/codelist/SupplementaryRegulationValue)-koodiston arvoiksi alla olevan taulukon mukaisesti.





