---
layout: "default"
description: ""
id: "laatusaannot"
status: "Keskeneräinen"
---
{% include common/important.html content="Sisältö ei vielä ajantasalla UML-kaavion kanssa" %}
# Laatusäännöt
{:.no_toc}

1. 
{:toc}

## Johdanto

## Yhteiset laatusäännöt

### UML-mallin mukaisuus
{% include common/clause_start.html type="req" id="laatu/vaat-uml-mukaisuus" %}
Kaavatietomallin loogisen tietomallin toteutusten tulee noudattaa tietomallin [UML-kielisen luokkakaavion](./uml/) määrityksiä luokkien attribuuttien ja assosiaatioiden kardinaliteetin ja tyypin suhteen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-uml-toteutus" %}
Kunkin fyysisen tietomallin kuvauksessa tulee määritellä minkälaista rakennetta ja tietotyyppiä kukin loogisen tietomallin luokka ja attribuutin tyyppi vastaa fyysisessä mallissa. Attribuutit ja assosiaatiot, joiden kardinaliteetti on loogisessa tietomallissa ```0..1``` tai ```0..*``` voivat puuttua fyysisen tietomallin mukaisista objekteista.
{% include common/clause_end.html %}

### Tunnisteet ja sisäisten viittausten eheys
{% include common/clause_start.html type="req" id="laatu/vaat-tunnukset-viittaukset" %}
Kaavatietomallin versioitavilla tietokohteilla tulee olla yksilöivät tunnukset, joiden luomisessa ja käyttämisessä viittaamiseen toisiin tietokohteisiin tulee noudattaa elinkaarisääntöjen luvun [Tunnukset ja niiden hallinta](elinkaarisaannot.html#tunnukset-ja-niiden-hallinta) vaatimuksia.
{% include common/clause_end.html %}

### Elinkaarisääntöjen mukaisuus
{% include common/clause_start.html type="req" id="laatu/vaat-elinkaarisaannot" %}
Kaavatietomallin mukaisten aineistojen tulee noudattaa Kaavatietomallin [elinkaarisääntöjen](elinkaarisaannot.html) vaatimuksia, ja niiden on suositeltavaa noudattaa elinkaarisääntöjen suosituksia. Vaatimukset ja suositukset on erotettu selkeästi elinkaarisääntöjen muusta sisällöstä.
{% include common/clause_end.html %}

### Soveltamisohjeiden mukaisuus
{% include common/clause_start.html type="req" id="laatu/vaat-soveltamisohjeet" %}
Kaavatietomallin mukaisten aineistojen tulee noudattaa niiden kaavalajikohtaisten soveltamisprofiilien ([Asemakaava](../soveltamisohjeet/asemakaava/), [Yleiskaava](../soveltamisohjeet/yleiskaava/)) vaatimuksia, ja niiden on suositeltavaa noudattaa soveltamisprofiilien suosituksia. Vaatimukset ja suositukset on erotettu selkeästi soveltamisprofiilien muusta sisällöstä.
{% include common/clause_end.html %}

### Merkkijonojen käyttö
#### Merkistöt
{% include common/clause_start.html type="req" id="laatu/vaat-merkisto-utf8" %}
Kaikki Kaavatietomallin tekstimuotoiset sisällöt on tiedonsiirtoa varten koodattava käyttäen UTF-8 -merkistökoodausta.
{% include common/clause_end.html %}

#### Monikielinen sisältö ja kielikoodit
Kaikki kaavatietomallin tekstimuotoinen sisältö ilmaistaan ISO 19103 -standardin määrittelemän [LanguageString](dokumentaatio/#languagestring)-luokan avulla.

{% include common/clause_start.html type="req" id="laatu/vaat-monikielisyys-kielikoodi" %}
Kunkin LanguageString-luokan objektin tulee toteuttaa ```language```-attribuutti, jonka arvona on ISO 639-2 -standardin mukainen terminologinen, kolmekirjaiminen kielikoodi code (ISO 639-2/T).
{% include common/clause_end.html %}

{% include common/note.html content="ISO 639-2/T koodilistan mukaiset koodit Suomen virallisille kielille ovat ```fin``` (suomi), ```swe``` (ruotsi), ```smn``` (inarinsaami), ```sms```(koltansaami) ja ```sme``` (pohjoissaami). Muita Suomessa paljon puhuttujen kielten ISO 639-2/T -koodeja: ```rus``` (venäjä), ```est``` (viro), ```ara```(arabia),  ```eng``` (englanti), ```som``` (somali), ```kur``` (kurdi)." %}

Tekstimuotoiset attribuutit on määritelty siten, että ne sisältävät nolla tai enemmän LanguageString-tyyppisiä arvoja.

{% include common/clause_start.html type="req" id="laatu/vaat-yksi-teksti-per-kieli" %}
Kunkin tekstimuotoista sisältöä kuvaavan attribuutin arvoina tulee olla enintään yksi LanguageString-tyyppinen arvo kutakin kielikoodia (```language```-attribuutti) kohti.
{% include common/clause_end.html %}

#### Enimmäispituudet
{% include common/clause_start.html type="req" id="laatu/vaat-merkijono-pituus" %}
Kunkin yhdellä kielellä annetun LanguageString-tyyppisen merkkijonon enimmäispituus on 2048 merkkiä.
{% include common/clause_end.html %}

{% include common/note.html content="Valittu 2048 merkin raja perustuu arvioon yksittäisten kaavamäräystekstien tyypillisistä pituuksista. Merkkijonojen enimmäispituuden määrääminen loogisen tietomallin tasolla on jossain määrin kajoamista mallin tekniseen toteutukseen, mutta yhteentoimivuuden takaamisen näkökulmasta on tärkeää, että kaikkissa fyysisissä tietomalleissa varataan yhtä suuri maksimimäärä merkkejä tekstisisältöjen tallentamiseen. Muutoin on riskinä oikeusvaikuttteisen tiedon katoaminen tiedonsiirrossa tai -käsittelyproseseissa." %}

#### Tekstiarvojen käyttö

Tekstimuotoisina annettujen kaavamääräysten koneellinen tulkittavuus on monimutkaisempaa kuin kuvattaessa sama ohjausvaikutus koodistojen arvojen tai numeeristen arvojen avulla. Tekstimuotoiset arvot ovat kuitenkin usein tarpeen, koska kaikkia mahdollisia yksityiskohtaisia kaavamääräyksiä ei ole mielekästä tai edes mahdollista koodittaa. Ihmisen tulee todennäköisesti aina tarkistaa tekstimuotoisten kaavamääräysten tulkinta, mikä heikentää kaavatiedon koneellista tulkintaa. Tämän vuoksi tekstimuotoisia kaavamääräysten ja niiden lisätietojen arvoja tulee käyttää kuvaamaan vain näitä täydentävää tai täsmentävää sisältöä.

{% include common/clause_start.html type="rec" id="laatu/suos-vain-tarpeelliset-tekstiarvot" %}
Mikäli [Kaavamaarays](dokumentaatio/#kaavamaarays)- tai [Lisatieto](dokumentaatio/#lisatieto)-luokkien ```arvo```-attribuuteille on annettu nollasta poikkeava määrä [TekstiArvo](dokumentaatio/#tekstiarvo)-tyyppisiä arvoja, tulee niitä käyttää lähtökohtaisesti täydentämään tai täsmentämään kaavamääräyksen tai lisätiedon muiden attribuuttien avulla kuvattua merkitystä.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-tekstiarvot-luokittelu" %}
Mikäli [Kaavamaarays](dokumentaatio/#kaavamaarays)-luokan ```arvo```-attribuutille on annettu nollasta poikkeava määrä [TekstiArvo](dokumentaatio/#tekstiarvo)-tyyppisiä arvoja, tulee [SanallinenMääräys](dokumentaatio/#sanallinenmaarays)-luokan koodistoarvon tai -arvojen avulla annotoida eli luokitella määräyksen sisältö.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-otsikointi-nimi" %}
[Kaavamaarays](dokumentaatio/#kaavamaarays)-, [Kaavasuositus](dokumentaatio/#kaavasuositus)- ja [Kaavakohde](dokumentaatio/#kaavakohde)-luokkien instanssien mahdolliseen ei-oikeusvaikutteiseen otsikointiin tulee käyttää niiden ```nimi```-attribuutteja.
{% include common/clause_end.html %}

### Geometriat

#### Geometriatyypit
{% include common/clause_start.html type="req" id="laatu/vaat-geom-piste-maar" %}
Pistemäiset geometriat toteuttavat ISO 19107 -standardin määrittelemän ```Point```-rajapinnan.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-geom-viiva-maar" %}
Viivamaiset geometriat toteuttavat ISO 19107 -standardin määrittelemän ```Curve```-rajapinnan.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-geom-2d-alue-maar" %}
Aluemaiset geometriat toteuttavat ISO 19107 -standardin määrittelemän ```Surface```-rajapinnan.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-geom-3d-kappale-maar" %}
3-ulotteiset kappalegeometriat toteuttavat joko ISO 19107 -standardin määrittelemän ```Solid```-rajapinnan.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-geom-kokoelmat-maar" %}
Geometriakokoelmat toteuttavat ISO 19107 -standardin määrittelemän ```Collection```-rajapinnan. Monipiste (multipoint) -geometriat rakentuvat ```Point```-rajapinnan, moniviiva (multicurve) -geometriat ```Curve```-rajapinnan, monialue (multisurface) -geometriat ```Surface```-rajapinnan ja monikappale (multisolid) -geometriat ```Solid```-rajapinnan toteuttavista osista (```element```-attribuutti).
{% include common/clause_end.html %}

{% include common/note.html content="Kaavatietomalli ei vaadi kaikkien ISO 19107 -standardin mukaisten geometriatyyppien tukemista. Kaavatietomallin mukaiset fyysiset tietomallit voivat rajoittaa mahdollisia geometriatyyppejä ja niiden ominaisuuksia." %}

#### Sallitut koordinaatistot ja koordinaattijärjestys

Rakennetun ympäristön tietojärjestelmä tukee seuraavia koordinaatistoja:

Tiedon luovutuksen koordinaatistot
* EPSG:4326, WGS84
  * Käytössä myös IFC-mallissa 
* EPSG:3857, Google Web Mercator
* Tiedon luovutusrajapinnan käyttäjä voi pyytää vastauksen haluamassaan tuetussa koordinaatistossa, jolloin tietojärjestelmä muuntaa tarvittaessa varannossa olevan tiedon haluttuun kohdekoordinaatistoon.

Tiedon luovutuksen ja vastaanoton koordinaatistot
* EPSG:3067, valtakunnallinen koordinaatisto.
* EPSG:3873-3885 koordinaatistot tiedon luovutuksessa / tiedon vastaanotossa
* Tiedon toimituksen yhteydessä tulee tallentaa tieto koordinaattijärjestelmästä ja korkeusjärjestelmästä (N2000), jossa tieto toimitettu.

{% include common/clause_start.html type="req" id="laatu/vaat-koord-jarjestys" %}
Geometrioiden ilmaisemisessa tulee noudattaa kunkin koordinaatiston määritelmässä annettua virallista koordinaattijärjestystä.
{% include common/clause_end.html %}

#### Geometrinen ja topologinen eheys

{% include common/clause_start.html type="req" id="laatu/vaat-suljetut-ringit" %}
Mikäli viiva on osa aluemaisen geometrian reunaviivaa, on sen oltava suljettu, eli sen alku- ja loppuppisteiden on oltava samat.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-viiva-kielletyt-leikkaukset" %}
Viivamainen geometria ei saa leikata itseään.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-alue-kielletyt-leikkaukset" %}
Aluemaisen geometrian ulkoreunan ja reikien reunaviivat eivät saa leikata itseään tai toisiaan. Kukin reunaviiva saa koskettaa alueen ulkoreunaa tai reiän reunaa, mukaanlukien se itse, vain yksittäisissä pisteissä.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-yhteneva-alue" %}
Aluemaisen geometrian sisäosan on oltava yhtenevä, eli minkä tahansa kahden alueen sisäpisteen välillä on voitava muodostaa yhtenäinen käyrä, joka kulkee kokonaan alueen sisällä.
{% include common/clause_end.html %}

Aluemaisen geometrian sisäosan pinta-ala on oltava mitattavissa, eli alueeseen tulee sisältyä pisteitä, jotka eivät ole osa alueen ulkoreunaa.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-pinnan-orientaatio" %}
Aluemaisten geometrioiden kiertosuuntien tulee noudattaa ISO 19107 -standardin määritelmää: Geometrioiden reunojen kiertosuunnat tulee valita siten, että pinnan yläpuolelta katsottuna ulkorajan reunan kiertosuunta on vastapäivään ja pinnan mahdollisten reikien reunojen kiertosuunnat ovat myötäpäivään. Mikäli pinta on osa 3-ulotteisten geometrian ulkorajaa, ulkopuoli vastaa yläpuolta.
{% include common/clause_end.html %}


#### Paikkatietokohteiden geometrioiden sisäkkäisyys ja päällekkäisyys

{% include common/clause_start.html type="req" id="laatu/vaat-kaavakohteet-kaavan-sisalla" %}
[Kaava](dokumentaatio/#kaava)-luokan objektin ```aluerajaus```-attribuutin ilmaiseman kaava-alueen tulee pitää sisällään kaikki kaavaan sisältyvien [AbstraktiKaavakohde](dokumentaatio/#abstraktikaavakohde)-luokan objektien geometriat, poislukien sellaiset [Kaavakohde](dokumentaatio/#kaavakohde)-luokan objektit, joiden kaikki kaavamääräykset ja kaavasuositukset ovat kumottuja.
{% include common/clause_end.html %}



### Päivämäärät ja kelloanajat
Kaavatietomallin yksittäisiä ajanhetkiä kuvaavat attribuutit ovat ISO 19108 -standardin määrittämää tyyppiä [TM_Instant](dokumentaatio/#tm_instant) ja aikavälejä kuvaavat attribuutit tyyppiä [TM_Period](dokumentaatio/#tm_period). Päivämäärät annetaan käyttäen Gregoriaanista kalenteria ja kellonajat käyttäen 24 tunnin kelloaikamuotoa alkaen kellonajasta 00:00:00.000  ja päättyen ajanhetkeen 23:59:59.999 (tunti, minuutti, sekunti, millisekunti).

{% include common/clause_start.html type="req" id="laatu/vaat-ajanhetki-tarkkuus" %}
Yksittäisiä ajanhetkiä kuvaavat attribuutit ilmaistaan joko pelkän päivämäärän tai päivämäärän ja kelloajan avulla. Päivämäärät ilmaistaan antamalla vuoden, kuukauden ja kuukauden päivän numeeriset arvot. Kellonajat ilmaistaan vähintään yhden minuutin ja enintään yhden millisekunnin tarkkuudella antamalla tunnin, minuutin, sekunnin ja millisekunnin numeeriset arvot.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-aikavyohykkeet" %}
Päivämäärien ja kellonaikojen yhteydessä voidaan antaa myös tieto aikavyöhykkeestä tai aikojen poikkeamasta UTC-ajasta. Mikäli muuta ei tietoa ei anneta, tulee ajanhetkitiedot tulkita siten, että ne kuvaavat Suomen aikaa noudattaen kyseisellä ajanhetkellä voimassaolleita asetuksia kesäaikaan liittyen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="rec" id="laatu/suos-ajanhetki-muoto" %}
Mikäli fyysinen tietomalli ei aseta ajanhetken muodolle rajoituksia, on suositeltavaa käyttää [IETF RFC 3339 Date and Time on the Internet: Timestamps](https://tools.ietf.org/html/rfc3339)-standardin määrittelemää syntaksia.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-aikavali-maar" %}
Aikavälejä kuvaavat attribuutit voidaan antaa joko sekä alku- että loppuajanhetken avulla tai vain joko alku- tai loppuajanhetken avulla. Mikäli alkuajanhetkeä ei anneta, tulkitaan aikavälin sisältävän minkä tahansa ajanhetken loppuajanhetkeen saakka. Vastaavasti mikäli loppuajanhetkeä ei anneta, tulkitaan aikavälin sisältävän minkä tahansa ajanhetken alkujanhetkestä lähtien.
{% include common/clause_end.html %}

## Luokkakohtaiset säännöt

### AbstraktiMaankayttoasia
{% include common/clause_start.html type="req" id="laatu/vaat-mkp-aluerajaus-geometria" %}
[AbstraktiMaankayttoasia](dokumentaatio/#abstraktimaankayttoasia)-luokan objektien ```aluerajaus```-attribuutin arvon tulee kuvata kaavan suunnittelualue joko [aluemaisena geometriana](#laatu-vaat-geom-2d-alue-maar) tai [monialueena](#laatu-vaat-geom-kokoelmat-maar).
{% include common/clause_end.html %}

### Lahtotietoaineisto
{% include common/clause_start.html type="req" id="laatu/vaat-lahtotietoaineisto-aluerajaus-geometria" %}
[Lahtotietoaineito](dokumentaatio/#lahtotietoaineisto)-luokan objektien ```aluerajaus```-attribuutin arvon tulee kuvata aineiston maantieteellinen kattavuus joko [aluemaisena geometriana](#laatu-vaat-geom-2d-alue-maar) tai [monialueena](#laatu-vaat-geom-kokoelmat-maar).
{% include common/clause_end.html %}

### KaavanKumoamistieto
{% include common/clause_start.html type="req" id="laatu/vaat-lahtotietoaineisto-aluerajaus-geometria" %}
[KaavanKumoamistieto](dokumentaatio/#kaavankumoamistieto)-luokan objektien ```kumottavanKaavanAlue```-attribuutin arvon tulee kuvata kumottava alue joko [aluemaisena geometriana](#laatu-vaat-geom-2d-alue-maar) tai [monialueena](#laatu-vaat-geom-kokoelmat-maar).
{% include common/clause_end.html %}

### Kaava
{% include common/clause_start.html type="req" id="laatu/vaat-kaava-paallekkaiset-aluerajaukset" %}
Kaavatietovarastossa ei tule olla kahta [Kaava](dokumentaatio/#kaava)-luokan objektia, joiden 
* ```laji```-attribuutin arvot ovat samat,
* ```voimassaoloAika```-attribuutin arvojen kuvaamat aikavälit ovat sisäkkäisiä tai lomittain, ja
* ```aluerajaus```-attribuuttien kuvaavat geometriat leikaavat toisiaan tai ovat sisäkkäisiä.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-kaava-aluerajaus-annettava" %}
[Kaava](dokumentaatio/#kaava)-luokan objektilla, jonka [elinkaatila](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaaritila) on kaavaehdotus tai myöhempi (koodi 04, 05, 06, 07, 08, 09, 10, 11 tai 12) tulee olla ei-tyhjä ```aluerajaus```-attribuutin arvo. 
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-kaava-virelletuloaika-annettava" %}
[Kaava](dokumentaatio/#kaava)-luokan objektilla, jonka [elinkaatila](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaaritila) on virelletullut tai myöhempi (koodi 02, 03, 04, 05, 06, 07, 08, 09, 10, 11 tai 12), tulee olla ei-tyhjä ```virelletuloAika```-attribuutin arvo. 
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-kaava-hyvaksymistuloaika-annettava" %}
[Kaava](dokumentaatio/#kaava)-luokan objektilla, jonka [elinkaatila](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaaritila) on hyväksytty kaava tai myöhempi (koodi 06, 07, 08, 09, 10, 11 tai 12), tulee olla ei-tyhjä ```hyvaksymisAika```-attribuutin arvo.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-kaava-voimassaolo-alku" %}
[Kaava](dokumentaatio/#kaava)-luokan objektilla, jonka [elinkaatila](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaaritila) on osittain voimassa, voimassa, tai niitä myöhempi (koodi 09, 10, 11 tai 12) tulee olla ei-tyhjä ```voimassaAika```-attribuutin alkuajanhetken arvo.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-kaava-voimassaolo-loppu" %}
[Kaava](dokumentaatio/#kaava)-luokan objektilla, jonka [elinkaatila](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaaritila) on  kumottu tai kumoutunut (koodi 11 tai 12), tulee olla annettu ei-tyhjä ```voimassaAika```-attribuutin loppuajanhetken arvo.
{% include common/clause_end.html %}

### Kaavakohde

{% include common/clause_start.html type="req" id="laatu/vaat-kaavakohde-geometria" %}
[Kaavakohde](dokumentaatio/#kaavakohde)-luokan objektin ```geometria```-attribuutin arvon tulee olla [piste](#laatu-vaat-geom-piste-maar), [viiva](#laatu-vaat-geom-viiva-maar), [alue](#laatu-vaat-geom-2d-alue-maar), [3-ulotteinen kappale](#laatu-vaat-geom-3d-kappale-maar), [moniviiva, monialue tai monikappale](#laatu-vaat-geom-kokoelmat-maar).
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-kaavakohde-3d-konsistenssi" %}
Mikäli [Kaavakohde](dokumentaatio/#kaavakohde)-luokan objektin ```geometria```-attribuutin arvo on [3-ulotteinen kappale](#laatu-vaat-geom-3d-kappale-maar) tai [monikappale](#laatu-vaat-geom-kokoelmat-maar), ja sille on annettu ```pystysuuntainenRajaus```-attribuutti, tulee ```geometria```-attribuutin arvon sijaita pystysuuntaisen rajauksen määrittämien korkeuksien ala- ja ylärajojen väleissä. 
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="laatu/vaat-paallekkaiset-kaavakohteet" %}
Kaavatietovarastossa ei tule olla kahta [Kaavakohde](dokumentaatio/#kaavakohde)-luokan objektia, joiden
* ```kaava```-attribuutin arvo viittaavat eri kaavoihin, 
* ```voimassaoloAika```-attribuutin arvojen kuvaamat aikavälit ovat sisäkkäisiä tai lomittain, ja
* ```geometria```- ja ```pystysuuntainenRajaus```-attribuuttien yhdessä kuvaavat geometriat leikaavat toisiaan tai ovat sisäkkäisiä.
{% include common/clause_end.html %}

