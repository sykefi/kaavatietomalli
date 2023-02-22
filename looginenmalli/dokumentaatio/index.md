---
layout: "default"
description: ""
id: "dokumentaatio"
status: "Keskeneräinen"
---
{% include common/important.html content="Sisältö ei vielä ajantasalla UML-kaavion kanssa" %}

# Loogisen tason kaavatietomalli
{:.no_toc}

1. 
{:toc}

## Yleistä
Loogisen tason Kaavatietomalli määrittelee kaikille kaavalajeille yhteiset tietorakenteet, joita sovelletaan kaavatiedon ilmaisemiseen kullekin kaavalajille laadittujen soveltamisohjeiden ([asemakaava](../../soveltamisohjeet/asemakaava/), [yleiskaava](../../soveltamisohjeet/yleiskaava/)) ja niissä kiinnitettyjen koodistojen sekä [elinkaari](../elinkaarisaannot.html)- ja [laatusääntöjen](../laatusaannot.html) mukaisesti. Looginen tietomalli pyrkii olemaan mahdollisimman riippumaton tietystä toteutusteknologiasta tai tiedon fyysisestä esitystavasta (esim. relaatiotietokanta, tietyn ohjelmointikielen tietorakenteet, XML, JSON).

## Normatiiviset viittaukset
Seuraavat dokumentit ovat välttämättömiä tämän dokumentin täysipainoisessa soveltamisessa:

* [ISO 639-2:1998 Codes for the representation of names of languages — Part 2: Alpha-3 code][ISO-639-2]
* [ISO 8601-1:2019 Date and time — Representations for information interchange — Part 1: Basic rules][ISO-8601-1]
* [ISO 19103:2015 Geographic information — Conceptual schema language][ISO-19103]
* [ISO 19107:2019 Geographic information — Spatial schema][ISO-19107]
* [ISO 19108:2002 Geographic information — Temporal schema][ISO-19108]
* [ISO 19109:2015 Geographic information — Rules for application schema][ISO-19109]
* [ISO 19505-2:ISO/IEC 19505-2:2012, Information technology — Object Management Group Unified Modeling Language (OMG UML) — Part 2: Superstructure][ISO-19505-2]

## Standardienmukaisuus
Looginen kaavatietomalli perustuu [ISO 19109][ISO-19109]-standardin yleinen kohdetietomalliin (General Feature Model, GFM), joka määrittelee rakennuspalikat paikkatiedon ISO-standardiperheen mukaisten sovellusskeemojen määrittelyyn. GFM kuvaa muun muassa metaluokat ```FeatureType```, ```AttributeType``` ja ```FeatureAssociationType```. Kaavatietomallissa kaikki tietokohteet, joilla on tunnus ja jota voivat esiintyä erillään toisista kohteista on määritelty kohdetyypeinä (stereotyyppi ```FeatureType```. Sellaiset tietokohteet, joilla ei ole omaa tunnusta ja jotka voivat esiintyä vain kohdetyyppien attribuuttien arvoina on määritelty [ISO 19103][ISO-19103]-standardin ```DataType```-stereotyypin avulla. Lisäksi [HallinnollinenAlue](#hallinnollinenalue) ja [Organisaatio](#organisaatio) on mallinnettu vain rajapintojen (```Interface```) avulla, koska on niitä ei ole tarpeen kuvata kaavatietomallissa yksityiskohtaisesti, ja on todennäköistä, että kaavatietovarastoja ylläpitävät tietojärjestelmät tarjovat niille konkreettiset toteuttavat luokat.

[ISO 19109][ISO-19109] -standardin lisäksi Kaavatietomalli perustuu muihin paikkatiedon ISO-standardeihin, joista keskeisimpiä ovat [ISO 19103][ISO-19103] (UML-kielen käyttö paikkatietojen mallinnuksessa), [ISO 19107][ISO-19107] (sijaintitiedon mallintaminen) ja [ISO 19108][ISO-19108] (aikaan sidotun tiedon mallintaminen).

### Muulla määritellyt luokat ja tietotyypit

#### CharacterString

Kuvaa yleisen merkkijonon, joka koostuu 0..* merkistä, merkkijonon pituudesta, merkistökoodista ja maksimipituudesta. Määritelty rajapinta-tyyppisenä [ISO 19103][ISO-19103]-standardissa.

#### LanguageString

Kuvaa kielikohtaisen merkkijonon. Laajentaa [CharacterString](#characterstring)-rajapintaa lisäämällä siihen ```language```-attribuutin, jonka arvo on ```LanguageCode```-koodiston arvo. Kielikoodi voi [ISO 19103][ISO-19103]-standardin määritelmän mukaan olla mikä tahansa ISO 639 -standardin osa.

#### Number

Kuvaa yleisen numeroarvon, joka voi olla kokonaisluku, desimaaliluku tai liukuluku. Määritelty rajapintana [ISO 19103][ISO-19103]-standardissa.

#### Integer

Laajentaa [Number](#number)-rajapintaa kuvaamaan numeron, joka on kokonaisluku ilman murto- tai desimaaliosaa. Määritelty rajapintana [ISO 19103][ISO-19103]-standardissa.

#### Decimal

Laajentaa [Number](#number)-rajapintaa kuvaamaan numeron, joka on desimaaliluku. Decimal-rajapinnan toteuttava numero voidaan ilmaista virheettä yhden kymmenysosan tarkkuudella. Määritelty rajapintana [ISO 19103][ISO-19103]-standardissa. Decimal-numeroita käytetään, kun desimaalien käsittelyn tulee olla tarkkaa, esim. rahaan liityvissä tehtävissä.

#### Real

Laajentaa [Number](#number)-rajapintaa kuvaamaan numeron, joka on tarkkudeltaan rajoitettu liukuluku. Real-rajapinnan numero voi ilmaista tarkasti vain luvut, jotka ovat 1/2:n (puolen) potensseja. Määritelty rajapintana [ISO 19103][ISO-19103]-standardissa. Käytännössä esitystarkkuus riippuu numeron tallentamiseen varattujen bittien määrästä, esim. ```float (32-bittinen)``` (tarkkuus 7 desimaalia) ja ```double (64-bittinen)``` (tarkkuus 15 desimaalia).

#### TM_Object

Aikamääreiden yhteinen yläluokka, käytetään, mikäli arvo voi olla joko yksittäinen ajanhetki tai aikaväli. Määritelty luokkana [ISO 19108][ISO-19108]-standardissa. 

#### TM_Instant

Kuvaa yksittäisen ajanhetken 0-ulotteisena ajan geometriana, joka vastaa pistettä avaruudessa. Määritelty luokkana [ISO 19108][ISO-19108]-standardissa. Aikapisteen arvo on määritelty ```TM_Position```-luokalla yhdistelmänä [ISO 8601][ISO-8601-1]-standin mukaisia päivämäärä- tai kellonaika-kenttiä tai näiden yhdistelmää, tai muuta ```TM_TemporalPosition```-luokan avulla kuvattua aikapistettä. Viimeksi mainitun luokan attribuutti ```indeterminatePosition``` mahdollistaa ei-täsmällisen ajanhetken ilmaisemisen liittämällä mahdolliseen arvoon luokittelun tuntematon, nyt, ennen, jälkeen tai nimi.

#### TM_Period

Kuvaa aikavälin [TM_Instant](#tm_instant)-tyyppisten ```begin```- ja ```end```-attribuuttien avulla. Molemmat attribuutit ovat pakollisia, mutta voivat sisältää tuntemattoman arvon  ```indeterminatePosition = unknown``` -attribuutin arvon avulla annettuna. Määritelty luokkana [ISO 19108][ISO-19108]-standardissa.

#### URI

Määrittää merkkijonomuotoisen Uniform Resource Identifier (URI) -tunnuksen [ISO 19103][ISO-19103]-standardissa. URIa voi käyttää joko pelkkänä tunnuksena tai resurssin paikantimena (Uniform Resource Locator, URL).

#### Geometry

Kaikkien geometria-tyyppien yhteinen rajapinta [ISO 19107][ISO-19107]-standardissa. Tyypillisimpiä [ISO 19107][ISO-19107]-standardin Geometry-rajapintaa laajentavia rajapintoja ovat ```Point```, ```Curve```, ```Surface``` ja ```Solid``` sekä ```Collection```, jota käyttämällä voidaan kuvata geometriakokoelmia (multipoint, multicurve, multisurface, multisolid).

#### Point
Täsmälleen yhdestä pisteestä koostuva geometriatyyppi. Määritelty rajapintana [ISO 19107][ISO-19107]-standardissa.

## Kaavatietomallin yleispiirteet

Tietomalli on jaettu kahteen UML-pakettiin: [MKP-ydin](#mkp-ydin) kuvaa maankäyttöpäätösten tietomallintamisessa yleiskäyttöisiksi suunnitellut luokat ja niihin liittyvät koodistot, ja [Kaavatiedot](#kaavatiedot) kuvaa kaavojen mallinukseen tarkoitetut, ydinpakettia hyödyntävät luokat ja niiden koodistot. Myös muita maankäyttöpäätöksiä kuin kaavoja voidaan tulevaisuudessa mallintaa laajentamalla MKP-ydin -paketin luokkia.

UML-mallin suunnittelussa on kiinnitetty erityistä huomiota siihen, että malli tarjoaa hyvän yhteentoimivuuskehikon tulevaisuuden kaavatietojen tietomallipohjaiseen kuvaamiseen erilaisissa tietojärjestelmissä. Malliin on tarkoituksellisesti jätetty useita laajennusmahdollisuuksia käyttäen abstrakteja luokkia ja koodistoja. Käyttämällä yhteistä luokkarakennetta ja erikoistamala koodistoja kaavalajikohtaisesti on saatu aikaan malli, joka mahdollistaa eri kaavalajien käsittelyn, tiedonsiirron ja tallentamisen samojen tietojärjestelmien ja -rakenteiden avulla, mutta tarjoaa kuitenkin riittävät mahdollisuudet eri kaavalajien erityispiirteiden huomioimiseen niiden tietosisällön ja merkityksen osalta.

Kaavatietomallin UML-luokkakaaviot ovat saatavilla erillisellä [UML-kaaviot](../uml/)-sivulla.

## Kaavatiedot

### Kaava
Englanninkielinen nimi: **SpatialPlan**

Kuvaa käsitteen [Kaava](../../kasitemalli/#kaava), erikoistaa luokkaa [VersioituObjekti](https://tietomallit.ymparisto.fi/ry-yhteiset/v1.0/looginenmalli/dokumentaatio/#versioituobjekti), stereotyyppi: FeatureType (kohdetyyppi)

**Ominaisuudet**

Nimi             | Name               | Tyyppi                       | Kardinaliteetti | Kuvaus
-----------------|--------------------|------------------------------|-----------------|------------------------------------
kaavalaji             | type               | [Kaavalaji](#kaavalaji)      | 1               | kaavan tyyppi
kaavaTunnus      | planId             | [URI](#uri)                  | 1               | kaavan yksilöivä ja pysyvä tunnus
elinkaaritila    | lifecycleStatus    | [KaavanElinkaaritila](#kaavanelinkaaritila) | 1 | kaavan elinkaaren tila
kaavaKuvaus      | planDescription    | [CharacterString](#characterstring) |0..1| sanallinen kuvaus kaavasta
maanalaisuus     | groundRelativePosition | [MaanalaisuudenLaji](#maanalaisuudenlaji) | 0..1 | luokittelu maanalaista ja maanpäällistä maankäyttöä koskeviin kaavoihin
mittakaava       | scale   | [Int](#integer) | 0..1 | kertoo kaavan mittakaavan
kaavakartta    | planMap   | [Kaavakartta](#kaavakartta) | 0..* | viittaus kaavatietomallin mukaiseen kaavatiedostoon (geotiff)
aluerajaus    | boundary   | [Geometry](#geometry) | 0..* | kuvaa kaavan suunnittelualueen
yleiskaavanOikeusvaikutus    | legalEffectOfLocalMasterPlan |   | [YleiskaavanOikeusvaikutukset](#yleiskaavanoikeusvaikutukset) | 0..* | luokittelu yleiskaavan oikeusvaikutuksista
kumoamistieto    | cancellationInfo   | [KaavanKumoamistieto](#kaavanakumoamistieto) | 0..* | kaava tai sen osa, jonka tämä kaava kumoaa


**Assosiaatiot**

Roolinimi        | Role name          | Kohde               | Kardinaliteetti | Kuvaus
-----------------|--------------------|---------------------|-----------------|------------------------------------
osallistumisJaArvointisuunnitelma | participationAndEvaluationPlan | [OsallistumisJaArviontiSuunnitelma](#osallistumisjaarviointisuunnitelma) | 0..1 | kaavan osallistumis- ja arviointisuunnitelma
selostus         | spatialPlanCommentary | [Kaavaselostus](#kaavaselostus) | 0..1          | kaavaselostus
laatija          | planner            | [KaavanLaatija]() | 0..* | kaavan laatimiseen tietyssä roolissa osallistunut suunnittelija
muuKaavaAineisto | otherPlanMaterial  | [MuuKaavaAineisto](#muukaavaaineisto) | 0..* | ei-asiakirjaksi luokiteltavat muut kaava-aineistot mm. videot, vaikutusten arvioinnit jne..
kaavakohde       | planObject         | [Kaavakohde](#kaavakohde) | 0..*       | paikkatietokohde, johon kohdistuu kaavamääräyksiä tai -suosituksia
kaavamääräys     | generalRegulation  | [Kaavamaarays](#kaavamaarays) | 0..*   | kaavamääräys, joka koskee koko kaavan aluetta
yleisMääräysJaSuositus    | generalRegulationAndGuidance    | [Kaavamääräysryhmä](#kaavamääräysryhmä) | 0..* | kaavan yleismääräys, yleissuositus tai niiden muodostama ryhmä, joka koskee koko kaavaan aluetta

### Kaavaselostus

Englanninkielinen nimi: **SpatialPlanCommentary**

Kuvaa käsitteen [Kaavaselostus](../../kasitemalli/#kaavaselostus), erikoistaa luokkaa [VersioituObjekti](https://tietomallit.ymparisto.fi/ry-yhteiset/v1.0/looginenmalli/dokumentaatio/#versioituobjekti), stereotyyppi: FeatureType (kohdetyyppi)

Kaavaselostus on on Kaavatietomallin tässä versiossa kuvattu vain viittauksena kaavaselostuksen muodostaviin asiakirjoihin. Tulevissa tietomallin kehitysversiossa kaavaselostusta voidaan rakenteistaa pidemmälle tämän luokan avulla.

**Assosiaatiot**

Roolinimi        | Role name          | Kohde               | Kardinaliteetti | Kuvaus
-----------------|--------------------|---------------------|-----------------|------------------------------------
tiedosto        | file           | [Liiteasiakirja](https://tietomallit.ymparisto.fi/ry-yhteiset/dev/looginenmalli/dokumentaatio/#liiteasiakirja) | 0..*        | liiteasiakirja, joka on osa kaavaselostusta.


### OsallistumisJaArviointisuunnitelma

Englanninkielinen nimi: **ParticipationAndEvalutionPlan**

Kuvaa käsitteen [Osallistumis- ja arviointisuunnitelma](../../kasitemalli/#osallistumis--ja-arviointisuunnitelma), erikoistaa luokkaa [VersioituObjekti](https://tietomallit.ymparisto.fi/ry-yhteiset/v1.0/looginenmalli/dokumentaatio/#versioituobjekti), stereotyyppi: FeatureType (kohdetyyppi)

Osallistumis- ja arviointisuunnitelma on on Kaavatietomallin tässä versiossa kuvattu vain viittauksena suunnitelman muodostaviin asiakirjoihin. Tulevissa tietomallin kehitysversiossa osallistumis- ja arviointisuunnitelmaa voidaan rakenteistaa pidemmälle tämän luokan avulla.

**Assosiaatiot**

Roolinimi        | Role name          | Kohde               | Kardinaliteetti | Kuvaus
-----------------|--------------------|---------------------|-----------------|------------------------------------
tiedosto        | file           | [Liiteasiakirja](https://tietomallit.ymparisto.fi/ry-yhteiset/dev/looginenmalli/dokumentaatio/#liiteasiakirja) | 0..*        | asiakirja, joka on osa kaavaselostusta. 


### Kaavakohde
Englanninkielinen nimi: **PlanObject**

Kuvaa käsitteen [Kaavakohde](../../kasitemalli/#kaavakohde), erikoistaa luokkaa [RakennetunYmpäristönKohde](#rakennetunympäristönkohde), stereotyyppi: FeatureType (kohdetyyppi)

**Ominaisuudet**

Nimi             | Name               | Tyyppi                       | Kardinaliteetti | Kuvaus
-----------------|--------------------|------------------------------|-----------------|------------------------------------
laji             | type               | [RakennetunYmpäristönKohdelaji](#rakennetunympäristönkohdelaji) | 0..1 | varattu tulevaisuuden käyttöön
sijainninSitovuus | bindingnessOflocation | [Sitovuuslaji](#sitovuuslaji) | 0..1       | kaavakohteeseen liitettyjen kaavamääräysten ja -suositusten sijainnin tulkinta
elinkaaritila    | lifecycleStatus    | [KaavanElinkaaritila](#kaavanelinkaaritila) | 1 | kaavakohteen elinkaaren tila
liittyvanLahtotietokohteenTunnus | relatedInputDatasetObjectId | [URI](#uri) | 0..*    | viittaus kaavan lähtötietoaineistoon sisältyvään tietokohteeseen, joka liittyy kaavakohteeseen. Esim. pohjavesialue
voimassaoloaika  | validityTime       | [TM_Period](#tm_period) | 0..1        | maankäyttöasiasssa tehdyn päätöksen voimassaoloaika
maanalaisuus     | groundRelativePosition | [MaanalaisuudenLaji](#maanalaisuudenlaji) | 0..1 | luokittelu maanalaista ja maanpäällistä maankäyttöä koskeviin kaavakohteisiin
värikoodi        | colorCode | [CharacterString](#characterstring) | 0..1 | kunnan antama kaavakohteen värikoodi

**Assosiaatiot**

Roolinimi        | Role name          | Kohde               | Kardinaliteetti | Kuvaus
-----------------|--------------------|---------------------|-----------------|------------------------------------
määräysJaSuositus       | regulationAndGuidance         | [Kaavamaaraysryhmä](#kaavamaarays) | 0..*  | kaavamääräys, suositus tai niiden muodostama ryhmä, joka kohdistuu tämän kaavakohteen alueelle


### Kaavamaaraysryhmä

Englanninkielinen nimi: **PlanRegulationGroup**

Kuvaa käsitteen [Kaavamääräysryhmä](../../kasitemalli/#kaavamääräysryhmä), erikoistaa luokkaa [VersioituObjekti](https://tietomallit.ymparisto.fi/ry-yhteiset/v1.0/looginenmalli/dokumentaatio/#versioituobjekti), stereotyyppi: FeatureType (kohdetyyppi)

**Ominaisuudet**

Nimi             | Name               | Tyyppi                       | Kardinaliteetti | Kuvaus
-----------------|--------------------|------------------------------|-----------------|------------------------------------
kaavamääräyksenOtsikko  | titleOfPlanRegulation | [CharacterString](#characterstring) | 0..1 | kaavamääräyksen otsikko
kirjainTunnus  | letterIdentifier | [CharacterString](#characterstring) | 0..1 | kaavamääräyksen kirjaintunnus


### Kaavamaarays

Englanninkielinen nimi: **PlanRegulation**

Kuvaa käsitteen [Kaavamääräys](../../kasitemalli/#kaavamääräys), erikoistaa luokkaa [Tietoyksikko](https://tietomallit.ymparisto.fi/ry-yhteiset/dev/looginenmalli/dokumentaatio/#tietoyksikk%C3%B6), stereotyyppi: FeatureType (kohdetyyppi)

**Ominaisuudet**

Nimi             | Name               | Tyyppi                       | Kardinaliteetti | Kuvaus
-----------------|--------------------|------------------------------|-----------------|------------------------------------
laji             | type               | [AbstraktiKaavamaaraysLaji](#abstraktikaavamaarayslaji) | 1 | kaavamääräyksen luokittelu
elinkaaritila    | lifecycleStatus    | [KaavanElinkaaritila](#kaavanelinkaaritila) | 1 | kaavamääräyksen elinkaaren tila
teema            | theme              | [AbstraktiKaavoitusteema](#abstraktikaaavoitusteema) | 0..* | kaavamääräyksen teemoittelu
lisatieto        | additionalInformation | [Lisatieto](#lisatieto)   | 0..*            | tarkentaa tai rajaa kaavamääräystä
voimassaoloAika  | validityTime       | [TM_Period](#tm_period)      | 0..1            | kaavamääräyksen lainvoimaisuusaika
aihetunniste  | subjectIdentifier | [CharacterString](#characterstring) | 0..* | kaavamääräyksen aihetunniste
sanallinenMääräys  | verbalRegulation              | [SanallisenMääräyksenLaji](#sanallisenmääräyksenlaji) | 0..* | kaavamääräyksen teemoittelu

**Assosiaatiot**

Roolinimi        | Role name          | Kohde               | Kardinaliteetti | Kuvaus
-----------------|--------------------|---------------------|-----------------|------------------------------------
liittyvaAsiakirja | relatedDocument   | [Asiakirja](#asiakirja) | 0..*        | asiakirja, joka on perustelee kaavamääräystä tai liittyy siihen muulla tavalla. Kukin assosiaatio voi sisältää ```rooli```-määreen tyyppiä [LanguageString](#languagestring), joka kuvaa liittymistavan.

### Kaavasuositus

Englanninkielinen nimi: **PlanGuidance**

Kuvaa käsitteen [Kaavasuositus](../../kasitemalli/#kaavasuositus), erikoistaa luokkaa [AbstraktiTietoyksikko](#abstraktitietoyksikko), stereotyyppi: FeatureType (kohdetyyppi)

**Ominaisuudet**

Nimi             | Name               | Tyyppi                       | Kardinaliteetti | Kuvaus
-----------------|--------------------|------------------------------|-----------------|------------------------------------
kuvaus             | name               | [LanguageString](#languagestring) | 0..*       | kaavasuosituksen sanallinen kuvaus
elinkaaritila    | lifecycleStatus    | [KaavanElinkaaritila](#kaavanelinkaaritila) | 1 | kaavasuosituksen elinkaaren tila
teema            | theme              | [AbstraktiKaavoitusteema](#abstraktikaaavoitusteema) | 0..* | kaavasuosituksen teemoittelu
voimassaoloAika  | validityTime       | [TM_Period](#tm_period)      | 0..1            | kaavasuosituksen lainvoimaisuusaika
liittyväAsiakirja        | relatedDocument   | [Liiteasiakirja](https://tietomallit.ymparisto.fi/ry-yhteiset/dev/looginenmalli/dokumentaatio/#liiteasiakirja) | 0..*        | liiteasiakirja, joka on perustelee kaavasuositusta tai liittyy siihen muulla tavalla.

### Lisatieto

Englanninkielinen nimi: **SupplementaryInformation**

Kuvaa käsitteen [Lisätieto](../../kasitemalli/#lisätieto), stereotyyppi: DataType (tietotyyppi)

**Ominaisuudet**

Nimi             | Name               | Tyyppi                       | Kardinaliteetti | Kuvaus
-----------------|--------------------|------------------------------|-----------------|------------------------------------
laji             | type               | [LisatiedonLaji](#abstraktilisatiedonlaji) | 1 | lisätiedon luokittelu
nimi             | name               | [LanguageString](#languagestring) | 0..*       | lisätiedon tunnistamiseen käytettävä nimi. Huom: kaavan oikeusvaikutteiset nimeämiset (mm. katujen, teiden ja yleisten alueiden nimet ja korttelinumerot) kuvataan kaavamääräysten arvojen avulla.
arvo             | value              | [OminaisuudenArvo](#ominaisuudenarvo) | 0..*         | lisätiedon lajia tarkentava arvo


### KaavanKumoamistieto
Englanninkielinen nimi: **CancellationInfo**

Stereotyyppi: DataType (tietotyyppi)

Kumoamistieto yksilöi mitä kaavoja tai niiden osia kaava kumoaa lainvoimaiseksi tullessaan.

**Ominaisuudet**

Nimi             | Name               | Tyyppi                       | Kardinaliteetti | Kuvaus
-----------------|--------------------|------------------------------|-----------------|------------------------------------
kumottavanKaavanTunnus | cancelledPlanId | [URI](#uri)               | 1               | kaava, johon kumoaminen kohdistuu
kumoaaKaavanKokonaan | cancelsEntirePlan | boolean                   | 1               | jos arvo on ```true```, kumoaa kaavan kokonaisuudessaan, muuten muiden ominaisuuksien yksilöimällä tavalla
kumottavaKaavanAlue | areaToCancel    | [Geometry](#geometry)        | 0..1            | alue, jonka sisällä kokonaan olevia kaavamääräyksiä ja -suosituksia kumoaminen koskee
kumottavanKohteenTunnus | cancelledPlanObjectId | [URI](#uri)        | 0..*            | kaavakohteen ```viittausTunnus```, jota kumoaminen koskee
kumottavanMaarayksenTunnus | cancelledRegulationId | [URI](#uri)     | 0..*            | kaavamääräyksen ```viittausTunnus```, jota kumoaminen koskee
kumottavanSuosituksenTunnus | cancelledGuidanceId | [URI](#uri)      | 0..*            | kaavasuosituksen ```viittausTunnus```, jota kumoaminen koskee

### Koodistot

#### Kaavalaji
Englanninkielinen nimi: **SpatialPlanKind**

Stereotyyppi: CodeList (koodisto)

Laajennettavuus: [Ei laajennettavissa](http://inspire.ec.europa.eu/registry/extensibility/none)

{% include common/codelistref.html registry="rytj" id="RY_Kaavalaji" name="Kaavalajit (maakunta-, yleis- ja asemakaava)" %}


#### KaavanElinkaaritila
Englanninkielinen nimi: **SpatialPlanLifecycleStatus**

Stereotyyppi: CodeList (koodisto)

Laajennettavuus: [Ei laajennettavissa](http://inspire.ec.europa.eu/registry/extensibility/none)

{% include common/codelistref.html registry="rytj" id="RY_KaavanElinkaaritila" name="Elinkaaren tila (yleis- ja asemakaava)" %}

#### Sitovuuslaji
Englanninkielinen nimi: **BindingnessKind**

Stereotyyppi: CodeList (koodisto)

Laajennettavuus: [Ei laajennettavissa](http://inspire.ec.europa.eu/registry/extensibility/none)

{% include common/codelistref.html registry="rytj" id="RY_Sitovuuslaji" name="Sijainnin sitovuuden laji" %}

#### MaanalaisuudenLaji
Englanninkielinen nimi: **GroundRelativenessKind**

Stereotyyppi: CodeList (koodisto)

Laajennettavuus: [Ei laajennettavissa](http://inspire.ec.europa.eu/registry/extensibility/none)

{% include common/codelistref.html registry="rytj" id="RY_MaanalaisuudenLaji" name="Maanalaisuuden laji" %}

#### AbstraktiKaavoitusteema
Englanninkielinen nimi: **AbstractSpatialPlanTheme**

Stereotyyppi: CodeList (koodisto)

Laajennettavuus: [Laajennettavissa kaikilla tasoilla](http://inspire.ec.europa.eu/registry/extensibility/open)

#### KaavoitusteemaAsemakaava
Englanninkielinen nimi: **DetailPlanTheme**

Erikoistaa luokkaa [AbstraktiKaavoitusteema](#abstraktikaavoitusteema), stereotyyppi: CodeList (koodisto)

Laajennettavuus: [Laajennettavissa kaikilla tasoilla](http://inspire.ec.europa.eu/registry/extensibility/open)

{% include common/codelistref.html registry="rytj" id="RY_Kaavoitusteema_AK" name="Kaavoitusteema (asemakaava)" %}

#### KaavoitusteemaYleiskaava
Englanninkielinen nimi: **MasterPlanTheme**

Erikoistaa luokkaa [AbstraktiKaavoitusteema](#abstraktikaavoitusteema), stereotyyppi: CodeList (koodisto)

Laajennettavuus: [Laajennettavissa kaikilla tasoilla](http://inspire.ec.europa.eu/registry/extensibility/open)

{% include common/codelistref.html registry="rytj" id="RY_Kaavoitusteema_YK" name="Kaavoitusteema (yleiskaava)" %}

#### Kaavamaarayslaji
Englanninkielinen nimi: **PlanRegulationKind**

Stereotyyppi: CodeList (koodisto)

Laajennettavuus: [Ei laajennettavissa](http://inspire.ec.europa.eu/registry/extensibility/none)

#### LisatiedonLaji
Englanninkielinen nimi: **AdditionInformationKind**

Stereotyyppi: CodeList (koodisto)

Laajennettavuus: [Laajennettavissa kaikilla tasoilla](http://inspire.ec.europa.eu/registry/extensibility/open)

#### SanallisenMääräyksenLaji
Englanninkielinen nimi: **typeOfVerbalRegulation**

Laajennettavuus: [Ei laajennettavissa](http://inspire.ec.europa.eu/registry/extensibility/none)

{% include common/codelistref.html registry="rytj" id="" name="Sanallisen määräyksen lji (yleis- ja asemakaava)" %}

#### YleiskaavanOikeusvaikutukset
Englanninkielinen nimi: **legalEffectOfLocalMasterPlan**

Laajennettavuus: [Ei laajennettavissa](http://inspire.ec.europa.eu/registry/extensibility/none)

{% include common/codelistref.html registry="rytj" id="oikeusvaik_YK" name="Elinkaaren tila (yleis- ja asemakaava)" %}

[ISO-8601-1]: https://www.iso.org/standard/70907.html "ISO 8601-1:2019 Date and time — Representations for information interchange — Part 1: Basic rules"
[ISO-639-2]: https://www.iso.org/standard/4767.html "ISO 639-2:1998 Codes for the representation of names of languages — Part 2: Alpha-3 code"
[ISO-19103]: https://www.iso.org/standard/56734.html "ISO 19103:2015 Geographic information — Conceptual schema language"
[ISO-19107]: https://www.iso.org/standard/66175.html "ISO 19107:2019 Geographic information — Spatial schema"
[ISO-19108]: https://www.iso.org/standard/26013.html "ISO 19108:2002 Geographic information — Temporal schema"
[ISO-19109]: https://www.iso.org/standard/59193.html "ISO 19109:2015 Geographic information — Rules for application schema"
[ISO-19505-2]: https://www.iso.org/standard/52854.html "ISO/IEC 19505-2:2012, Information technology — Object Management Group Unified Modeling Language (OMG UML) — Part 2: Superstructure"