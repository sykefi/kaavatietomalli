---
layout: "default"
description: ""
id: "elinkaarisaannot"
status: "Ehdotus"
---
# Elinkaarisäännöt
{:.no_toc}

1. 
{:toc}

## Johdanto

Kaavoilla, niiden kaavamääräyksillä ja -suosituksilla on Kaavatietomallissa elinkaari, joka määrää miten kyseiset tietokohteet syntyvät, miten ja voivat muuttua kaavaprosessin aikana ennen niiden voimassaolon alkua, ja miten ne kumoutuvat johtaen niiden voimassaolon päättymiseen. Elinkaarisääntöjen määrittely liittyy olennaisesti tietokohteiden versionhallintaan, eli miten yksittäisten tietokohteiden niiden elinkaaren aikana muodotettavat versiot voidaan tallentaa ja yksilöidä viittauskelpoisten pysyvien tunnusten avulla. Tässä annetut säännöt pohjautuvat paikkatietokohteiden yksilöivien tunnusten ja elinkaarisääntöjen periaatteisiin, jotka on kuvattu jukishallinnon suosituksessa [JHS 193 - Paikkatiedon yksilöivät tunnukset](http://www.jhs-suositukset.fi/suomi/jhs193).

### HTTP URI -tunnukset

HTTP URI -muotoiset tunnukset ovat [RFC 3986 -standardiin](https://tools.ietf.org/html/rfc3986) perustuvia HTTP(S) -protokollan mukaisia URI-osoitteita (Uniform Resource Identifier), joiden globaali yksilöivyys varmistetaan Internetin DNS-nimipalveluun rekisteröityjen domain-nimien avulla. Kullakin DNS-palveluun rekisteröidyllä domain-nimellä (esim. ```uri.suomi.fi```) on yksiselitteinen omistaja, joka on suoraan tai välillisesti vastuussa ko. domain-nimen alla julkaistavasta sisällöstä. Nimen omistaja on myös ainoa taho, joka voi päättää ko. domain-nimeä käyttävien osoitteiden ohjautumisesta haluttuihin resursseihin, mikä tekee siitä luontevan perustan yksilöivien tunnusten nimiavaruuksille (esim. <http://uri.suomi.fi/object/rytj/kaava>). HTTP URI -muotoisen tunnuksen yksilöivyys perustuu siis domain-nimien ja siten niihin perustuvien nimiavaruuksien keskitettyyn hallintaprosessiin.

URI-tunnuksen ei tarvitse viitata konkreettiseen sijaintiin internetissä, vaan se voi olla abstraktimpi tunnus. [JHS 193 Paikkatiedon yksilöivät tunnukset](http://www.jhs-suositukset.fi/suomi/jhs193) määrittelee paikkatiedon yksilöiville tunnuksille muodon <http://paikkatiedot.fi/{tunnustyyppi}/{aineistotunnus}/{paikallinen tunnus}>, jossa paikkatietokohteiden ```tunnustyyppi``` on ```so```. Kaavatietomallissa on esimerkkinä käytetty tunnusmuotoa 
<http://uri.suomi.fi/object/rytj/{aineistotyyppi}/{TietotyypinNimi}/{paikallinenTunnus}>. HTTP URI -muotoisen tunnuksen etuna on luettavuus sekä DNS- ja HTTP-protokollien tarjoama kyky ratkaista (resolve) tunnus ja ohjata kysyjä sitä kuvaavaan Internet-resurssiin ilman tarvetta erityiselle keskitetylle tunnusrekisterille ja siihen perustuvalle ratkaisupalvelulle.

Kaavatietomallissa HTTP URI -muotoa käytetään [viittaustunnus](#viittaustunnus)-attribuutissa, jonka avulla viitataan tiettyyn versioon tietokohteesta kaavan ulkopuolelta.

### UUID-tunnukset
UUID (Universally Unique Identifier) on OSF:n (Open Software Foundation) määrittelemä standardoitu tunnusmuoto, jonka avulla voidaan luoda vakiokokoisia, hyvin suurella todennäköisyydellä yksilöiviä tunnuksia ilman keskitettyä hallintajärjestelmää. UUID-tunnukset voivat perustua satunnaislukuihin, aikaleimoihin, tietokoneiden verkkokorttien MAC-osoitteisiin tai merkkijonomuotoisiin nimiavaruuksiin eri yhdistelmissä. UUID-tunnukset erityisen hyvin tietojärjestelmissä, joissa uusia globaalisti pysyviä ja yksilöiviä tunnuksia on tarpeen luoda hajautetusti ilman keskitettyä tunnusrekisteriä.

Kaavatietomallissa UUID-muotoisia tunnuksia suositellaan käytettäväksi [identiteettitunnus](#identiteettitunnus)-, [kaavatunnus](#kaavatunnus)- ja [tuottajakohtainen tunnus](#tuottajakohtainen-tunnus)-attribuuttien arvoina.


## Kaavatietomallin kohteiden elinkaaren hallinnan periaatteet
Kaavatietomallin elinkaarisäännöt mahdollistavat tietomallin tietokohteiden käsittelyn, tallentamisen ja muuttamisen hallitusti sekä niiden laatimis- että voimassaolovaiheissa. Kaavatietomallin mukaiset tietosisällöt ovat merkittäviä oikeusvaikutuksia aiheuttavia, juridisesti päteviä aineistoja, joita käsitellään hajautetusti eri toimijoiden tietojärjestelmissä. Tämän vuoksi niiden tunnusten, viittausten ja versionnin hallintaan on syytä kiinnittää erityistä huomiota.

Seuraavat keskeiset periaatteet ohjaavat kaavatietomallin elinkaaren hallintaa:
* Kukin kaavatietovarastoon tallennettu versio kaavasta ja sen sisältämistä yksittäisistä tietokohteista saa pysyvän, versiokohtaisen tunnuksen.
* Kuhinkin kaavatietovarastoon tallennettun tietokohteen versioon voidaan viitata sen pysyvän tunnuksen avulla.
* Kaavatietomallin tietokohteiden väliset viittaukset toteutetaan hallitusti sekä kaavatietoa tuottavissa tietojärjestelmissä että yhteisissä kaavatietovarastoissa.
* Kaavatietovarasto vastaa pysyvien tunnusten luomisesta ja antamisesta tallennettaville tietokohteille.
* Lainvoiman saaneita kaavoja ei voi muuttaa kaavatietovarastossa muilta osin kuin niiden tai niiden osien kumoamiseen liittyen.

Kaavatietomallin mukaisten aineistojen tallentamisessa erotetaan toisistaan tietojen tuottaminen ja muokkaus sisäisesti niiden tuottamiseen ja muokkaamiseen käytettävissä tietojärjestelmissä ja niiden hallinta yhteisessä versiohallitussa kaavatietovarastossa. Kaavatietomallin ei ole mielekästä asettaa vaatimuksia kaavatietoa tuottavien tietojärjestelmien tunnusten ja versioden hallintaan, vaan tietomallissa tulee varautua siihen, että yhteiseen tietovarastoon tallennettavia tietoja on muokattu ja tallennettu sisäisesti tuntematon määrä kertoja ennen ensimmäistä viemistä yhteiseen tietovarastoon, ja samoin tuntematon määrä kertoja kunkin yhteiseen varastoon vietävän version välillä. Näin ollen on mahdollista, että kaavasta voi olla joissain tietojärjestelmissä tallennettuna paikallisia versiota, joita ei ole koskaan viety yhteiseen kaavatietovarastoon.

## Tunnukset ja niiden hallinta

### Identiteettitunnus
Identiteettitunnus yhdistää saman tunnistettavan kaavan tietokohteen kehitysversiot toisiinsa.

{% include common/clause_start.html type="req" id="elinkaari/vaat-identiteettitunnus-maar" %}
Kaavatietomallin tietokohteissa identiteettitunnus kuvataan attribuutilla ```identiteettiTunnus```. Kahdella kaavatietomallin versioitavalla objektilla voi olla sama ```identiteettiTunnus```-attribuutin arvo ainoastaan, mikäli kaikki seuraavista ehdoista ovat tosia:
* Molemmat objektit kuvaavat saman kaavan tai sen sisältämän, nimettävissä olevan tietokohteen kehityskaaren eri tiloja.
* Molemmat objektit liittyvät samaan kaavaan.
* Molemmat objektit ovat saman loogisen tietomallin luokan edustajia.
{% include common/clause_end.html %}

Yksittäisen kaavan tietokohteen koko ko. tietojärjestelmään tallennettu kehityshistoria saadaan noutamalla kaikki ko. tyyppisen tietokohteen objektit, joilla on sama ```identiteettiTunnus```-attribuutin arvo.

Yhteinen kaavatietovarasto on vastuussa uusien identiteettitunnusten luomisesta tarvittaessa tallennustapahtumien yhteydessä, ja niiden välittämisestä tiedoksi tallentavalle tietojärjestelmälle. Tallentavan tietojärjestelmän tulee tallentaa itselleen kopiot tietovaraston tallennustapahtuman yhteydessä palautamistä kaavan ja sen tietokohteiden identiteettitunnuksista, sillä ne tulee sisällyttää ko. tietokohteiden seuraavien versioden tallennettavaksi lähetettäviin objekteihin.

{% include common/clause_start.html type="req" id="elinkaari/vaat-identiteettitunnus-gen" %}
* Mikäli tallennettavalle tietokohteelle ei ole annettu ```identiteettitunnus```-attribuuttia, tai tietovarasto ei sisällä sellaista saman luokan tietokohdetta, jolla sama ```identiteettiTunnus```-attribuutin arvo, kaavatietovarasto luo ko. objektille uuden identiteettitunnuksen, joka korvaa tuottavan tietojärjestelmän objektille mahdollisesti antaman ```identiteettiTunnus```-attribuutin arvon. Tällöin objektia pidetään uuden tietokohteen ensimmäisenä versiona.
* Mikäli tietovarasto sisältää saman luokan tietokohteen, jolla on sama ```identiteettiTunnus```-attribuutin arvo kuin tallennetavalla objektilla, objekti tallennetaan kaavatietovarastoon ko. tietokohteen uutena versiona. Tällöin tallennettavan objektin ```identiteettiTunnus```-attribuutin arvo ei muutu.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-kaavan-identiteettitunnus" %}
[Kaava](../../looginenmalli/dokumentaatio/#kaava)-luokan tietokohteen tallennuksen yhteydessä kaavatietovarasto tarkistaa, että sen attribuutti [kaavaTunnus](#kaavatunnus) on annettu ja validi.
* Mikäli kohde katsotaan sen ```identiteettiTunnus```-attribuutin arvon perusteella uudeksi tietokohteeksi, sama ```kaavaTunnnus```-attribuutti ei saa olla käytössä kaavatietovaraston muilla [Kaava](dokumentaatio/#kaava)-luokan objekteilla.
* Mikäli kohde katsotaan sen ```identiteettiTunnus```-attribuutin arvon perusteella aiemmin tallennetun tietokohteen uudeksi versioksi, aiemmin tallennetun version ```kaavaTunnnus```-attribuutin tulee olla sama kuin tallennettavassa objektissa.
{% include common/clause_end.html %}

{% include common/clause_start.html type="rec" id="elinkaari/suos-identiteettitunnus-form" %}
Identiteettitunnuksen suositeltu muoto on UUID.
{% include common/clause_end.html %}

Esimerkki: ```640bff6b-c16a-4947-af8d-d86f89106be1```

### Paikallinen tunnus
Paikallinen tunnus yksilöi tietokohteen yhden version kaavatietovaraston sisällä. 

{% include common/clause_start.html type="req" id="elinkaari/vaat-paikallinentunnus-maar" %}
Kaavatietomallin tietokohteissa paikallinen tunnus kuvataan attribuutilla ```paikallinenTunnus```. Kaikilla saman kaavatietovaraston objekteilla (ml. saman tietokohteen eri versiot) tulee olla eri ```paikallinenTunnus```-attribuutin arvo.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-paikallinentunnus-gen" %}
Tietokohteiden paikallinen tunnus muuttuu sen jokaisen version tallennuksen yhteydessä. Kaavatietovarasto vastaa paikallisten tunnusten luomisesta tallennustapahtuman yhteydessä. Tuottavan tietojärjestelmän mahdollisesti asettamat arvot korvataan.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-paikallinentunnus-form" %}
Paikallinen tunnus koostuu identiteettitunnuksesta ja siihen erotinmerkillä liitetystä versiokohtaisesta, esimerkiksi tarkkaan tallennusajanhetkeen perustuvasta merkkijonosta.
{% include common/clause_end.html %}

{% include common/clause_start.html type="rec" id="elinkaari/suos-paikallinentunnus-merk" %}
Paikallisen tunnuksen muodostamisessa tulee välttää merkkejä, jotka joudutaan URL-koodaamaan rajapintapalvelujen kutsuissa. Paikkatietokohteen paikallista tunnusta käytetään fyysisten tietomallien pääavaimena, esim. GeoJSON Feature ```id```-omaisuuden ja GML:n ```gml:id```-attribuutin arvona, ja siten esimerkiksi OGC Web Feature Service (WFS) - ja OGC API - Features -rajapintapalvelujen paikkatietokohteen yksilöivissä kyselyissä.
{% include common/clause_end.html %}

Tallennusajanhetkeen päättyvää paikallista tunnusta voidaan käyttää ilman sekaannusmahdollisuuksia samalla logiikalla myös paikallisissa versionneissa, eli sellaisissa kaavan versioiden tallennuksissa, joita ei viedä lainkaan kaavatietovarastoon.

Esimerkki: ```640bff6b-c16a-4947-af8d-d86f89106be1.b05cf48d46d8c905c54522f44b0a12daff11604e```

{% include common/note.html content="Käyttämällä paikallisena tunnuksena pelkkää identiteettitunnuksesta riippumatonta UUID-tunnusta päästäisiin lyhyempiin tunnuksiin, mutta menetetään yhteys identiteettitunnusten ja paikallisten tunnusten välillä, mikä saattaa hankaloittaa erilaisten vikatilanteiden selvitystä ja toimintavarmuuden testaamista, kun pelkkien tunnusten perusteella ei voida päätellä ovatko kaksi objektia saman tietokohteen eri versioita." %}

### Nimiavaruus
{% include common/clause_start.html type="req" id="elinkaari/vaat-nimiavaruus-maar" %}
Nimiavaruus määrää kaavatietomallin kaikkien tietokohteiden viittaustunnusten alkuosan yhden kaavatietovaraston sisällä. Kaavatietomallin tietokohteissa paikallinen tunnus kuvataan attribuutilla ```nimiavaruus```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-nimiavaruus-form" %}
Nimiavaruus on HTTP URI -muotoinen.
{% include common/clause_end.html %}

Nimiavaruus on syytä valita huolella siten, että se olisi mahdollisimman pysyvä, eikä sitä tarvitsisi tulevaisuudessa muuttaa esimerkiksi valtionhallinnon virastojen tai ministeriröiden mahdollisten uudelleenorganisointien ja -nimeämisten johdosta. Valittu URL-osoite tulee myös voida aina tarvittaessa ohjata kulloinkin käytössä olevaan rajapintapalveluun (HTTP redirect). 

{% include common/clause_start.html type="req" id="elinkaari/vaat-nimiavaruus-gen" %}
Kaavatietovarasto vastaa ```nimiavaruus```-attribuuttien asetamisesta tallennustapahtuman yhteydessä. Tuottavan tietojärjestelmän mahdollisesti antamat arvot korvataan.
{% include common/clause_end.html %}

Esimerkki: ```http://uri.suomi.fi/object/rytj/kaava```

### Viittaustunnus
{% include common/clause_start.html type="req" id="elinkaari/vaat-viittaustunnus-maar" %}
Viittaustunnus yksilöi kaavan tietokohteen yhden, keskitettyyn kaavatietovaraston tallentun kehitysversion globaalisti. Kaavatietomallin tietokohteissa viittaustunnus kuvataan attribuutilla ```viittausTunnus```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-viittaustunnus-form" %}
Viittaustunnus on HTTP URI -muotoinen ja se muodostuu nimiavaruudesta, tietokohteen luokan nimestä ja paikallisesta tunnuksesta yhdessä kauttaviivoilla (```/```) erotettuina.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-viittaustunnus-gen" %}
Kaavatietovarasto vastaa ```viittausTunnus```-attribuuttien asetamisesta tallennustapahtuman yhteydessä. Tuottavan tietojärjestelmän mahdollisesti antamat arvot korvataan.
{% include common/clause_end.html %}

Tallentavan tietojärjestelmän ei siis tarvitse tallentaa luotuja viittaustunnuksia itselleen seuraavia tallennuksia varten.

{% include common/clause_start.html type="rec" id="elinkaari/suos-viittaustunnus-ohj" %}
Viittaustunnuksen on suositeltavaa ohjautua aina ko. tietokohteen version tietosisältöön kulloinkin toiminnassa olevassa kaavatietovaraston latauspalvelussa.
{% include common/clause_end.html %}

Esimerkki: ```http://uri.suomi.fi/object/rytj/kaava/SpatialPlan/640bff6b-c16a-4947-af8d-d86f89106be1.b05cf48d46d8c905c54522f44b0a12daff11604e```

### Tuottajakohtainen tunnus

{% include common/clause_start.html type="req" id="elinkaari/vaat-tuottajakohtainen-tunnus-maar" %}
Kaavatietoa tuottavat järjestelmät voivat niin halutessaan käyttää tuottajakohtaista tunnusta niiden omien tietojärjestelmäspesifisten tunnusten antamiseen kaavatietomallin tietokohteille. Kaavatietomallin tietokohteissa tuottajakohtainen tunnus kuvataan attribuutilla ```tuottajakohtainenTunnus```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-tuottajakohtainen-tunnus-gen" %}
Kaavatietovarasto ei koskaan muuta tuottavan tietojärjestelmän mahdollisesti asettamia tuottajakohtaisia tunnuksia, ja ne palautetaan sellaisenaan latattaessa tietokohteita tietovarastosta.
{% include common/clause_end.html %}

Tietojärjestelmät voivat käyttää tuottajakohtaisia tunnuksia kohdistamaan kaavatietovarastoon ja paikallisiin tietojärjestelmiin tallennettuja tietokohteita toisiinsa esimerkiksi päivitettäessä niiden tallennuksen yhteydessä syntyneitä tunnuksia, vertailtaessa kaavatietovarastoon tallennettuja kohteita ja paikallisia kohteita toisiinsa, sekä esitettäessä validointipalvelun tuloksia suunnitteluohjelmiston käyttäjälle.

Tuottajakohtaisilta tunnuksilta ei vaadita yksilöivyyttä tai mitään tiettyä yhtenäistä muotoa, mutta UUID-muodon käyttäminen tarjoaa hyvin määritellyn ja standardoidun tavan luoda tuottajakohtaisista tunnuksista yksilöiviä eri tietojärjestelmien kesken. Tästä saattaa olla etua haluttaessa tehdä tuotettavista kaavatiedoista mahdollisimman järjestelmäriippumattomia ja esimerkiksi taata tuottajakohtaisten tunnusten yksilöivyys yli mahdollisten kaavatietoa tuottavien tietojärjestelmien vaihdosten ja päivitysten. 

{% include common/clause_start.html type="rec" id="elinkaari/suos-tuottajakohtainen-tunnus-form" %}
Tuottajakohtaisen tunnuksen suositeltu muoto on UUID.
{% include common/clause_end.html %}

Esimerkki: ```k-123445```

### Kaavatunnus
{% include common/clause_start.html type="req" id="elinkaari/vaat-kaavatunnus-maar" %}
Kaavatunnus on kaavalle ennakolta haettava, kaavan kansallisesti yksilöivä tunnus. Kaatatietomallissa kaavatunnus kuvataan [Kaava](dokumentaatio/#kaava)-luokan attribuutilla ```kaavaTunnus```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-kaavatunnus-gen" %}
Tuottava tietojärjestelmän vastaa kaavatunnuksen asettamisesta [Kaava](dokumentaatio/#kaava)-luokan attribuutiksi. Se tulee olla asetettuna myös kaavan ensimmäisen kaavatietovarastoon tallennuksen yhteydessä.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-kaavatunnus-yks" %}
Kaavatunnus on Kaava-luokan objekteille globaalisti yksilöivä, eikä muutu saman kaavan eri elinkaaren aikaisten versioiden tallennuksen yhteydessä.
{% include common/clause_end.html %}

 Käytännössä myönnetyt kaavatunnukset kannattaa tallentaa valmiiksi kaavatietovarastoon, jotta voidaan tarkistaa onko tallennettavaksi tarkoitettu kaavatunnus myönnetty organisaatiolle, jonka kaavaa ollaan tallentamassa. Kuntakoodin tai muun hallinnollisen alueen tunnuksen käyttö osana kaavatunnusta ei ole suositeltavaa, sillä hallinnolliset alueet muuttuvat ajan kuluessa. Kun sidos tunnuksen ja hallinnollisen alueen välillä ei näy tunnuksessa, voidaan kaavan hallinnollista aluetta muuttaa joustavammin kaavan elinkaaren aikana.

{% include common/clause_start.html type="rec" id="elinkaari/suos-kaavatunnus-form" %}
Kaavatunnuksen suositeltu muoto on UUID.
{% include common/clause_end.html %}

Esimerkki: ```df5b2d6f-d6d6-4695-938c-dd7c4c784c28```

### Pysyvien tunnusten palauttaminen tuottavalle järjestelmälle

Versionhallinnan näkökulmasta on tärkeää, että kaavan tuottava tietojärjestelmä käyttää saman kaavan seuraavan version tallentamisessa kaavan ensimmäisen version tallennuksen yhteydessä luotua identiteettitunnusta. Vastaavasti kaikkien kaavan tietokohteiden osalta käytetään niiden ensimmäisen tallennuksen yhteydessä luotuja identiteettitunnuksia, mikäli objektin katsotaan kuvaavan ko. tietokohteen uutta versiota.

{% include common/clause_start.html type="req" id="elinkaari/vaat-tunnusten-palautus" %}
Tietovaraston tallennusrajapinta palauttaa tallennetun kaavan tiedot tuottavalle tietojärjestelmälle tallennusoperaation yhteydessä siten, että ne sisältävät yllä mainittujen tunnustenhallintasääntöjen mukaisesti mahdollisesti generoidut tai muokatut identiteettitunnukset, paikalliset tunnukset, nimiavaruudet ja viittaustunnukset kaikille tallennetuille tietokohteille.
{% include common/clause_end.html %}

### Kaavan tietokohteisiin viittaaminen ja viitteiden ylläpito

{% include common/clause_start.html type="req" id="elinkaari/vaat-kaavan-sisaiset-viittaukset" %}
Saman kaavan tietokohteiden keskinäiset assosiaatiot toteutetaan viitattavan tietokohteen [paikallinenTunnus](#paikallinen-tunnus)-attribuuttia käyttäen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-tietovaraston-sisaiset-viittaukset" %}
Kaavatietokohteen luokkien assosiaatiot eri kaavojen välillä tai kaavojen ja muiden maankäyttöpäätösten tietokohteiden välillä toteutetaan viitattavan tietokohteen [viittaustunnus](#viittaustunnus)-attribuuttia käyttäen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-viittaukset-ulkoa" %}
Pysyvät viittaukset Kaavatietomallin ulkopuolelta tietomallin tietokohteisiin toteutetaan viitattavan tietokohteen [viittaustunnus](#viittaustunnus)-attribuuttia käyttäen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-viittaukset-tallennettaessa" %}
Tallennettaessa Kaavatietomallin tietokohteita kaavatietovarastoon tietokohteiden tunnukset muuttuvat niiden pysyvään muotoon, kuten kuvattu luvussa [Tunnukset ja niiden hallinta](#tunnukset-ja-niiden-hallinta). Kaavatietovaraston vastuulla on päivittää kunkin paikallisen tunnuksen muuttamisen yhteydessä myös kaikkien ko. tietokohteen versioon sen paikallisen tunnuksen avulla viittaavien muiden ko. kaavan tietokohteiden viittaukset käyttämään tietokohteen muutettua paikallista tunnusta.   
{% include common/clause_end.html %}

### Koodistojen koodien tunnuksiin liittyvät vaatimukset

{% include common/clause_start.html type="req" id="elinkaari/vaat-koodien-yksiloivat-tunnukset" %}
Kullakin koodiston koodilla on oltava pysyvä tunnus, joka sellaisenaan yksilöi kyseisen koodin globaalisti ilman erilistä tietoa koodistosta, johon koodi kuuluu. Koodin tunnus on HTTP URI -muotoinen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-alakoodi-maar" %}
Olkoon koodi ```A``` mikä tahansa hierarkkisen koodiston sisältämä koodi. Koodin ```A``` alakoodilla tarkoitetaan koodia, joka on hierakkiassa sijoitettu koodin ```A``` alle. Koodi voi olla useamman ylemmän tason koodin alakoodi vain mikäli ko. ylemmän tason koodit ovat alakoodisuhteessa keskenään.
{% include common/clause_end.html %}

Käytännössä tietyn koodin alakoodit voidaan tunnistaa vertaamalla niiden tunnuksia:

{% include common/clause_start.html type="req" id="elinkaari/vaat-alakoodi-tunnus" %}
Koodin ```A``` alakoodin ```B``` tunnus alkaa koodin ```A``` tunnuksella ja sisältää sen jälkeen yhden tai useamman merkin.
{% include common/clause_end.html %}

## Muutokset ja tietojen versionti
{% include common/clause_start.html type="req" id="elinkaari/vaat-pysyva-sisalto" %}
Kukin kaavan tai sen osien tallennusoperaatio yhteiseen tietovarastoon muodostaa uuden version tallennettavista tietokohteista, mikäli yksittäinen tietokohde on miltään osin muuttunut verrattuna sen edelliseen versioon. Myös muutokset muissa Kaavatietomallin tietokohteissa, joihin tietokohteesta on viittaus, lasketaan tietokohteen muutoksiksi. Tallennetun tietokohteen version sisältö ei voi muuttua tallennuksen jälkeen, poislukien sen voimassaolon päättymiseen, seuraavaan versioon linkittämiseen ja elinkaaritilaan liittyvät attribuutit, joita kaavatietovarasto itse päivittää tietyissä tilanteissa.
{% include common/clause_end.html %}

Näin taataan ulkoisten viittausten eheys, sillä kaavan kaikkien kohteiden paikalliset ja viittaustunnukset viittaavat aina vain tiettyn, sisällöllisesti muuttumattomaan versioon viittatusta kohteesta. Suositeltavaa on, että kaikki tallennusversiot myös pidetään pysyvästi tallessa, jotta mahdolliset keskenäiset ja ulkopuolelta tulevat linkit eivät mene rikki muutosten yhteydessä.

### Muutosten leviäminen viittausten kautta
Kaavatietomallin tietokohteiden keskinäiset viittaukset kohdistuvat aina viitattavien tietokohteiden tiettyyn versioon, ja toisaalta kaikki kohteiden sisällölliset muutokset johtavat uusien versioiden tallentamiseen. Siten kohteiden välisten linkkien kohdetietoa täytyy muuttaa mikäli halutaan viitata jollain tapaa muuttuneeseen kohteeseen. Tämä päivitystarve johtaa edelleen myös viittaavan tietokohteen uuden version luomiseen, vaikka ainoa muuttunut tieto olisi linkki uuteen versioon viitatusta tietokohteesta. Molempiin suuntiin tietokohteiden välillä tehty linkitys saattaa siten johtaa hyvin laajalle leviävään muutosketjuun. Muutosten leviämistä voidaan rajoittaa  kaikkiin kaavan tietokohteisiin voidaan välttää tekemällä linkitys tietokohteiden välillä vain yhteen suuntaan, esimerkiksi vain joko kaavasta kaavakohteisiin ja kaavakohteista kaavamääräyksiin (ylhäältä alas), tai toisinpäin (alhaalta ylös). 

Kaavatietomallissa kukin [Kaavakohde](dokumentaatio/#kaavakohde) on linkitetty kahdensuuntaisesti kaavaan ja kukin [Kaavamääräys](dokumentaatio/#kaavamaarays) ja [Kaavasuositus](dokumentaatio/#kaavasuositus) kahdensuuntaisesti joko pelkästään suoraan kaavaan (yleismääräys/yleissuositus) tai myös kaavakohteisiin, joiden alueita ne koskevat. Tällöin yhden kaavamääräyksen muuttaminen johtaa uuden version luomiseen muutettavan kaavamääräyksen lisäksi myös siihen linkitetyistä kaavakohteista, ja edelleen niihin linkitetystä kaava-objektista, mikä puolestaan johtaa lopulta uusien versioiden luomiseen kaikista ko. kaavan muistakin kaavakohteista, kaavamääräyksistä ja -suosituksista, koska kaava-objektiin päin osoittavat linkit pitää muuttaa osoittamaan sen uuteen versioon.

Minkä tahansa kaavanmääräyksen tai -suosituksen muuttaminen johtaa siis kaikkien muidenkin ko. kaavan kaavakohteiden, kaavamääräysten ja kaavasuositusten uusiin versiohin, mikä on hieman ongelmallista todellisten kaavan muutosten seurannan kannalta. Kahdensuuntainen linkitys on kuitenkin tässä perusteltavissa. Suorat linkit kaavakohteista, kaavamääräyksistä ja kaavasuosituksista ylöspäin Kaava-luokan objektiin mahdollistavat tehokkaat ja yksikertaiset hakuoperaatiot tiettyyn kaavan versioon liittyvien kaavamääräysten ja -suositusten noutamiseksi. Toisaalta Kaava-luokan viittaukset alaspäin sen sisältämiin kaavakohteisiin, yleismääräyksen luonteisiin kaavamääräyksiin ja yleissuosituksen luonteisiin kaavasuosituksiin helpottavat kaikkien kaavaan liittyvien kaavamääräysten ja -suositusten poimintaa, kun ne voidaan löytää iteratiivisesti puumaista rakennetta seuraamalla.

Linkit kaava-objektista alaspäin mahdollistavat myös kaavaan liittyvien kaavakohteiden, kaavamääräysten ja kaavasuositusten poistamisen kaavaluonnoksesta tai ehdotuksesta vain jättämällä ne yksinkertaisesti pois seuraavasta kaavan tallennusversiosta: Mikäli kaava-objektissa ei olisi suoria linkkejä sen sisältämiin kaavakohteisiin, voisi se säilyä tallennuksessa muuttumattomana, vaikka tallennuksesta puuttuusikin yksi tai useampi aiempaa kaava-versioon sisältynyt kaavakohde. Muuttumattomasta kaava-objektista ei tällöin luotaisi uutta versiota, ja siten uudesta versiosta pois jätetytkin kaavakohteet viittaisivat edelleen uusimpaan (muuttumattomaan) kaavan versioon yhdessä muutettujen ja uusien kaavakohteiden kanssa. Vastaavasti kaavamääräysten poistaminen tietystä kaavakohteesta voidaan tehdä yksinkertaisesti jättämällä ne pois kaavan seuraavasta tallennusversiosta.

[Kaava](dokumentaatio/#kaava)-luokan assosiaatiot [Kaavaselostus](dokumentaatio/#kaavaselostus)- ja [OsallistumisJaArviointisuunnitelma](dokumentaatio/#osallistumisjaarviointisuunnitelma)-luokkiin ovat yksisuuntaisia. Tallennettu versio kaavaselostuksesta tai osallistumis- ja arviointisuunnitelmasta voi pysyä samana kaavan uuden version tallennuksen yhteydessä, jolloin niistä ei ole tarpeen luoda uusia versiota. Sama kaavaselostuksen tai osallistumis- ja arviointisuunnitelman versio voi siis liittyä useampaan saman kaavan tallennusversioon.

**Esimerkki**:

Tallennuspalveluun viedään kaavaehdotus, jonka yhteen kaavakohteeseen liittyvää kaavamääräystä [Lisärakennusoikeus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0309) on muutettu siten, että sen numeerinen arvo muuttuu arvosta ```1000 k-m2``` arvoon ```1500 k-m2```. Kaikki kaavan muut tietokohteet ovat identtisiä kaavan edellisen tallennusversion kanssa.

* Muuttuvasta kaavamääräys-tietokohteesta luodaan uusi versio.
* Kaavakohteesta, johon muuttunut kaavamääräys kohdistuu, luodaan uusi versio, jossa muuttuu vain linkki, viitaten nyt kaavamääräyksen uuteen versioon.
* Kaikista muista kaavan tietokohteista, joista on viittaus kyseiseen kaavakohteeseen, luodaan uudet versiot, joissa muuttuvat vain linkit, viitaten nyt kaavakohteen uuteen versioon, mukaan lukien kaava-objekti ja ko. kaavakohteen kaikki muut kaavamääräykset.
* Kaikista ko. kaavan muistakin kaavakohteista, kaavamääräyksistä ja kaavasuosituksista luodaan uudet versiot, koska niiden viittaukset muuttuneeseen kaava-tietokohteeseen pitää muuttaa.
* Kaavan mahdollisesti liittyvistä kaavaselostus- ja osallistumis- ja arviointisuunnitelma -tietokohteista ei luoda uusia versiota, vaan sekä uusi että vanha kaavan versio viittaavat samoihin selostus- ja OAS-tietokohteiden versioihin.


### Yksittäisen kaavan elinkaaren vaiheisiin liittyvät muutokset
Kaavatietomalli mahdollistaa tunnistettavien kaavan tietokohteiden eri kehitysversioiden erottamisen toisistaan. Kullakin tietomallin kohteella on sekä sen tosimaailman identiteettiin liittyvä ns. identiteettitunnus että yksittäisen tallennusversion tunnus (paikallinen tunnus). Tallennettaessa uutta versiota samasta kaavasta tai sen sisältämästä tietokohteesta, sen identiteettitunnus pysyy ennallaan, mutta sen paikallinen tunnus muuttuu. Tallennettaessa Kaava-luokan objektia se katsotaan saman tietokohteen uudeksi versioksi, mikäli sen kaavatunnus on sama. Muiden kaavatietomallin versioitavien objektien suhteen samuuden määritteleminen on tietoja tuottavien järjestelmien vastuulla: mikäli objektilla on tallennettavaksi lähetettäessä saman ```identititeettiTunnus```-attribuutin arvo kuin aiemmin tallennetulla, samantyyppisellä tietokohteella, katsotaan uusi objekti on saman tietokohteen uudeksi versioksi.

{% include common/clause_start.html type="req" id="elinkaari/vaat-version-korvaus" %}
Kun kaavan tietokohteesta tallennetaan uusi muuttunut versio, tulee tietokohteen edellisen version ```korvattuObjektilla```-assosiaatio asettaa viittaamaan tietokohteen uuteen versioon. Uuden tietokohteen version ```korvaaObjektin```-assosiaatio puolestaan asetetaan viittaamaan tietokohteen edelliseen, korvattavaan versioon. Molempien kohteiden ```tallennusAika```-attribuutin arvoksi asetetaan ajanhetki, jolloin tallennus ja muutos kaavatietovarastoon on tehty.
{% include common/clause_end.html %}

Yksittäisen tietokohteen yksityiskohtainen muutoshistoria kaavatietovarastossa saadaan seuraavalla sen ```korvattuObjektilla```- ja ```korvaaObjektin```-assosiaatioita. Ainoa muutos, joka ei näy tietokohteen omana versionaan, on kohteen kumoaminen, jolloin sen viimeisimmän version tietoja päivitetään sen elinkaaritilan, voimassaolon ja tallennusajan osalta. Aiempien versioiden tallennusajat eivät häviä tietokannasta eli esimerkiksi version ensimmäinen tallennusaika jää tietoon.

Attribuutin ```viimeisinMuutos``` arvo kuvaa ajanhetkeä, jolloin ko. tietokohteeseen on tehty sisällöllinen muutos tiedontuottajan tietojärjestelmässä. Tiedontuottajan järjestelmän osalta ei vaadita tiukkaa versiontipolitiikkaa, eli ```paikallinenTunnus```-attribuutin päivittämistä jokaisen tietokohteen muutoksen johdosta. ```viimeisinMuutos```-attribuutin päivittämien riittää kuvaamaan tiedon todellisen muuttumisajankohdan.

### Kaavan käsittely- ja vuorovaikutustapahtumien elinkaari
Kaavaprosessin historian yhdessä kuvaavat [AbstraktiTapahtuma](dokumentaatio/#abstraktitapahtuma)-luokasta perityt [Kasittelytapahtuma](dokumentaatio/#kasittelytapahtuma)- ja [Vuorovaikutustapahtuma](dokumentaatio/#vuorovaikutustapahtuma)-luokan tietokohteet linkitetään yksisuuntaisesti [AbstraktiMaankayttoasia](dokumentaatio/#abstraktimaankayttoasia)-luokkaan (Kaava-luokan yläluokka) päin. Tapahtumatietokohteiden uusina versiona tallennettavat muutokset eivät koskaan johda uuden version luomiseen Kaava-luokan tietokohteesta, sen kaavakohteista, kaavamääräyksistä tai -suosituksista. Syy tähän on se, että käsittely- ja vuorovaikutustapahtumien on tärkeää kohdistua nimenomaan tiettyyn, pysyvään versioon kaavasta.

Kulloinkin nähtävillä olevien kaavojen poimiminen on eräs kaavatietovaraston keskeisistä käyttötapauksista. Tiettyllä ajanhetkellä nähtävillä olevat tai nähtävillä olleet kaavojen versiot voidaan poimia valitsemalla ne kaavat, joihin kohdistuu [Vuorovaikutustapahtuma](dokumentaatio/#vuorovaikutustapahtuma), jonka ```laji```-attribuutin arvo on [Nähtävilläolo](http://uri.suomi.fi/codelist/rytj/RY_KaavanVuorovaikutustapahtumanLaji/code/01), ```tapahtumaAika```-attribuuttin aikaväli kattaa halutun ajankohdan ja ```peruttu```-attribuutin arvo on ```false```. Näiden vuorovaikutustapahtumien ```liittyvaAsia```-assosiaatio viittaa siihen [AbstraktiMaankayttoasia](dokumentaatio/#abstraktimaankayttoasia)-luokan instanssiin, joka ko. aikaan on nähtävillä. Katso kaavaehdotuksen ja tarkistetun kaavaehdotuksen nähtävilläolon ilmoittamiseen liittyvät vaatimukset kohdasta [Kaavan elinkaaritilan muutoksiin liittyvät käsittely- ja vuorovaikutustapahtumat](#kaavan-elinkaaritilan-muutoksiin-liittyvät-käsittely--ja-vuorovaikutustapahtumat).

{% include common/clause_start.html type="req" id="elinkaari/vaat-tapahtumien-poistaminen" %}
Kerran tallennettuja [AbstraktiTapahtuma](dokumentaatio/#abstraktitapahtuma)-luokan tietokohteita ei voi poistaa kaavatietovarastosta. Mikäli suunniteltu vuorovaikutustapahtuma ei syystä tai toisesta toteudu tai käsittelytapahtumaan liittyvä päätös kumotaan, tulee sen attribuutti ```peruttu``` asettaa arvoon ```true```.
{% include common/clause_end.html %}

### Kaavan ja sen tietokohteiden voimaantulo
Kaavan ```voimassaoloAika``` -attribuutin alkuaika on ajanhetki, jolloin kaava sen valitusajan umpeuduttua ja mahdollisten valitusten ja oikaisukehotusten käsittelyn jälkeen kuulutetaan voimaantulleeksi.

{% include common/clause_start.html type="req" id="elinkaari/vaat-kaavan-voimaantulo" %}
Voimaantulemisen kuuluttamisen yhteydessä kaavasta tallennetaan kaavatietovarastoon uusi versio, jossa sen 
* [Kaava](dokumentaatio/#kaava)-luokan objektin ```elinkaaritila```-attribuutin arvoksi on asetettu [Voimassa](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/10),
* [Kaava](dokumentaatio/#kaava)-luokan objektin ```voimassaoloAika```-attribuutin alkuajaksi on asetettu kuulutuksen ajanhetki ja loppuaikaa ei ole annettu, ja
* Kunkin kaavan [Kaavamaarays](dokumentaatio/#kaavamaarays)- ja [Kaavasuositus](dokumentaatio/#kaavasuositus)-luokan objektin ```elinkaaritila```-attribuuttien arvoksi [Voimassa](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/01) ja ```voimassaoloAika```-attribuutin alkuajaksi kuulutuksen ajanhetki ilman loppuaikaa.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-voimassaoloaika" %}
Kaava ja sen kaavamääräykset ja -suositukset ovat voimassa niiden ```voimassaoloAika```-attribuuttien määräämillä aikaväleillä. Mikäli ```voimassaoloAika```-attribuutin loppuaika puuttuu, on tietokohde voimassa toistaiseksi.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-elinkaaritila-voimassaoloaika" %}
 Kaava ja sen kaavamääräykset ja -suositukset voivat olla elinkaaritilassa [Voimassa](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/10) ainoastaan, mikäli niiden ```voimassaoloAika``` on annettu ja sisältää vain alkuajan ilman loppuaikaa. Kaavan ja sen kaavamääräysten ja -suositusten ```voimassaoloAika``` voi olla annettu vain mikäli ne ovat joko elinkaaritilassa [Voimassa](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/10) tai [Kumottu](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/11). Kaavan ja sen kaavamääräysten ja -suositusten ```voimassaoloAika``` sisältää sekä alku- että loppuajan vain, kun ne ovat elinkaaritilassa [Kumottu](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/11).
 {% include common/clause_end.html %}


### Kaavan määrääminen voimaan osittain
[Maankäyttö- ja rakennuslain pykälässä 201](https://www.finlex.fi/fi/laki/ajantasa/1999/19990132#L26P201) (säädös 132/1999) säädetään mahdollisuudesta määrätä kaava osittain voimaan:
> Kunnanhallitus voi valitusajan kuluttua määrätä yleis- ja asemakaavan tulemaan voimaan ennen kuin se on saanut lainvoiman kaava-alueen siltä osalta, johon valitusten tai oikaisukehotuksen ei voida katsoa kohdistuvan.

{% include common/clause_start.html type="req" id="elinkaari/vaat-osittainen-voimaantulo" %}
Tallennettaessa osittain voimaan määrättävä kaava, tulee tuottavassa tietojärjestelmässä asettaa [Kaava](dokumentaatio/#kaava)-luokan objektin ja sen sisältämien tietokohteiden attribuuttien arvot seuraavasti:
* [Kaava](dokumentaatio/#kaava)-luokan objektin ```elinkaaritila```-attribuutin arvoksi asetetaan [Osittain voimassa](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/09).
* [Kaava](dokumentaatio/#kaava)-luokan objektin ```voimassaoloAika```-attribuutin alkuajaksi asetaan voimaantulevaksi määräämisen ajanhetki, ja loppuaikaa ei anneta.
* Kunkin kaavan [Kaavamaarays](dokumentaatio/#kaavamaarays)- ja [Kaavasuositus](dokumentaatio/#kaavasuositus)-luokan objektin ```elinkaaritila```-attribuuttien arvoksi asetaan joko [Voimassa](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/10) tai [Kumottu](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/11) riippuen siitä katsotaanko valitusten tai oikaisukehotusten kohdistuvan ko. kaavamääräykseen tai kaavasuositukseen vai ei.
* ```elinkaaritila```-attribuutin arvon [Kumottu](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/11) saavien [Kaavamaarays](dokumentaatio/#kaavamaarays)- ja [Kaavasuositus](dokumentaatio/#kaavasuositus)-luokan objektien ```voimassaoloAika```-attribuuteille ei anneta lainkaan arvoa.
* ```elinkaaritila```-attribuutin arvon [Voimassa](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/10) saavien [Kaavamaarays](dokumentaatio/#kaavamaarays)- ja [Kaavasuositus](dokumentaatio/#kaavasuositus)-luokan objektien ```voimassaoloAika```-attribuuteille annetaan alkuajaksi asetaan voimaantulevaksi määräämisen ajanhetki, ja loppuaikaa ei anneta.
{% include common/clause_end.html %}

Kaavamääräysten ja -suositusten kumoaminen kaavan osittaisen voimaan määräyksen yhteydessä saattaa johtaa tilanteeseen, jossa tietyn [Kaavakohde](dokumentaatio/#kaavakohde)-luokan objektin alueelle ei enää kohdistu lainkaan kumoamattomia määräyksiä tai suosituksia. Tästä ei kuitenkaan automaattisesti aiheudu "reikää" kaava-alueeseen, sillä kaavan yleismääräykset voidaan edelleen haluta saattaa voimaan myös ko. kaavakohteen alueella.

{% include common/clause_start.html type="req" id="elinkaari/vaat-osittainen-voimaantulo-aluerajaus" %}
[Kaava](dokumentaatio/#kaava)-luokan tietokohteen uuden version ```aluerajaus```-attribuuttin arvo päivitetään poistamalla siitä ainoastaan kumottavia kaavamääräyksiä sisältävien kaavakohteiden geometriat vain siinä tapauksessa, että kyseinen osa kaavan alkuperäisestä alueesta halutaan jättää kokonaan kaavan suunnittelualueen ulkopuolelle. Suunnitelualueen ulkopuolelle jätettävälle alueelle ei saa olla kohdistua kumoamattomia kaavamääräyksiä tai -suosituksia.
{% include common/clause_end.html %}

### Kaavamuutokset ja vaihekaavat
Hyväksyttyjen kaavojen sisältämiä kaavamääräyksiä voidaan kumota tai korvata laatimalla kaavamuutos tai vaihekaava. Kaavatietomallissa sekä kaavamuutos että vaihekaava toteutetaan [Kaava](dokumentaatio/#kaava)-luokan avulla samoin kuin ensimmäinenkin tietylle alueelle laadittava kaava. Vaihekaavat erotetaan ensimmäisistä kaavoista ja kaavamuutoksista Kaava-luokan attribuutin ```laji``` (arvona koodisto [Kaavalaji](http://uri.suomi.fi/codelist/rytj/RY_Kaavalaji)) avulla. Vaihekaavat sisältävät tyypillisesti vain vähäisiä ja rajattuja muutoksia kaavoihin, joita niillä muutetaan. Muutettavien kaavojen kaavamääräykset säilyvät vaihekaavan alueella tyypillisesti pääosin ennallaan, ja niitä kumotaan ja korvataan vaihekaavassa vain tarpeellilta osin. Kaavamuutos puolestaan kumoaa voimaan tullessaan tyypillisesti yhden tai useamman aiemmin hyväksytyn kaavan kaikki kaavamääräykset ```aluerajaus```-attribuuttinsa määrittämällä alueella. 

{% include common/clause_start.html type="req" id="elinkaari/vaat-kumoamistieto-per-kaava" %}
Sekä kaavamuutosten että vaihekaavojen tapauksessa kaavalla kaikki kumottavat, aiemmin hyväksyttyjen kaavojen kaavamääräykset tulee yksilöidä kumoavassa kaavassa. Kutakin kaavaa kohti tulee antaa yksi [Kaava](dokumentaatio/#kaava)-luokan attribuutin ```kumoamistieto``` arvo tyyppiä [KaavanKumoamistieto](dokumentaatio/#kaavankumoamistieto), jonka ```kumottavanKaavanTunnus```-attribuutin arvo on kumottavan kaavan [viittaustunnus](#viittaustunnus)).
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-kumottava-maarayksen-tunnus" %}
Kumottavat kaavamääräykset kuvataan ensisijaisesti ```kumoattavanMaarayksenTunnus```-attribuutin arvojen avulla. Attribuutin arvo on kumottavan [Kaavamaarays](dokumentaatio/#kaavamaarays)-luokan tietokohteen [viittaustunnus](#viittaustunnus).
{% include common/clause_end.html %}

 Mikäli kumottavalle kaavamääräykselle ei kumottavassa kaavavassa ole määritelty yksilöivää ja yksiselitteistä tunnusta, ei kumoamista voi kohdistaa siihen ```kumoattavanMaarayksenTunnus```-attribuutin avulla. Näin voi olla esimerkiksi kun kumottava kaava tai sen yksittäiset kaavamääräykset eivät ole saatavissa Kaavatietomallin mukaisessa muodossa. Tässä tapauksessa kaavan kumottavat alueet kuvataan ```kumottavaKaavanAlue```-attribuutin määrittämän aluerajauksen avulla.
 
{% include common/clause_start.html type="req" id="elinkaari/vaat-kumottava-kaavan-alue" %}
Kumottavasta kaavasta kumotaan kaikki kaavamäärykset, jotka on kohdistettu kokonaan ```kumottavaKaavanAlue```-attribuutin määrittämän alueen sisälle. ```kumottavaKaavanAlue```-attribuutin avulla ei voi kumota kaavan yleismääräyksiä. Muutoskohteeksi tulee ottaa koko aiempi kaava, jos aiemman kaavan koko kaavaa koskevia yleismääräyksiä halutaan muuttaa.
 {% include common/clause_end.html %}
 
{% include common/clause_start.html type="req" id="elinkaari/vaat-kumoaa-kaavan-kokonaan" %}
 Mikäli kaavamuutoksella tai vaihekaavalla halutaan kumota kokonainen hyväksytty kaava kaikkine kaavamääräyksineen, käytetään ```kumoaaKaavanKokonaan```-attribuutin arvoa ```true```. Tällöin attribuutteja ```kumoattavanMaarayksenTunnus``` ja ```kumottavaKaavanAlue``` ei käytetä.
 {% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-kaavamuutoksen-voimaantulo" %}
 Kun kaavamuutoksesta tai vaihekaavasta tallennetaan versio, jonka ```elinkaaritila```-attribuutin arvo on [Voimassa](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/10), kaavatietovarasto päivittää niiden siinä kumottaviksi asetettujan kaavamääräysten, joiden ```elinkaaritila```-attribuutin arvo on [Voimassa](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/10), attribuutteja seuraavasti *luomatta niistä uusia versioita*:
 * ```voimassaoloAika```-attribuutin päättymisaika asetetaan samaksi kuin kaavamuutoksen tai vaihekaavan ```voimassaoloAika```-attribuutin alkamisaika.
 * ```elinkaaritila```-attribuutin arvoksi asetetaan [Kumottu](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/11).
 * ```tallennusAika```-attribuutin arvoksi asetetaan ajanhetki, jolloin kaavamuutos tai vaihekaava tallennettiin kaavatietovarastoon elinkaaritilassa [Voimassa](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/10).
 {% include common/clause_end.html %}

 Kaavatietomalli ei sisällä omaa tietorakennettaan ajantasaiselle kaava-aineistolle, joka sisältää annetun alueella tietyllä ajanhetkellä voimassaolevat kaavamääräykset (ns. ajantasakaava), huomioiden kaavamuutosten ja vaihekaavojen vaikutukset niiltä osin kun ne ovat ko. ajanhetkellä voimassa. Tällainen toiminnallisuus on kuitenkin aivan ilmeisesti yhteisen kaavatietovaraston palveluna erittäin hyödyllinen. Kaavamääräysten ```voimassaoloAika```-attribuutin arvojen avulla tällainen ajantasainen "kaavamatto" voidaan laskea mille tahansa ajanhetkelle, olettaen, että kaikki kyseisen alueen kaavat on viety tietovarastoon kaavatietomallin mukaisessa muodossa. Tietojärjestelmään on tarkoitus tuoda kaikki voimassa olevat kaavat ja kun kaikki kaavatiedot ovat tietomallimuotoisia kaavakohteen aiemmat tapahtumat ovat haettavissa.
 
 On huomattava, että pelkän ```elinkaaritila```-attribuutin avulla ei voida tietää, onko kaavamääräys tietyllä tarkasteluajanhetkellä lainvoimainen vai ei: Mikäli ajanhetkellä ```x``` voimaan tullut kaavamääräys on kumottu kaavamuutoksella, joka on tullut lainvoimaiseksi ajanhetkellä ```y```, on kaavamääräyksen ```elinkaaritila```-attribuutin arvo muutettu arvoon [Kumottu](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/11). Kyseinen kaavamääräys on tällöin kuitenkin edelleen lainvoimainen millä tahansa ajanhetkellä ```t, x <= t < y```.

Kunkin voimassaolevan kaavamääräyksen osalta voidaan tarkastella onko se asetettu kumottavaksi vireillä olevassa, vielä ei-lainvoimaisessa kaavamuutoksessa ja vaihekaavassa hakemalla siihen sen sisältävään kaavan kohdistuvat kaavamuutokset ja vaihekaavat, ja vertaamalla niiden ```kumoamistieto```-attribuuttien arvoja kaavamäääräyksen tietoihin.

## Kaavan elinkaaren vaiheet ja elinkaaritila-attribuutin käyttö
Kaavan ja sen sisältämien kaavamääräysten elinkaareen liittyvää tilaa hallitaan ko. tietokohteiden ```elinkaaritila```-attribuutin ja sen mahdolliset arvot kuvaavan [Elinkaaren tila](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila)-koodiston avulla. [Kaava](dokumentaatio/#kaava)-, [Kaavamaarays](dokumentaatio/#kaavamaarays)-, ja [Kaavasuositus](dokumentaatio/#kaavasuositus)-luokkien ```elinkaaritila```-attribuutit ovat pakollisia. 

[Elinkaaren tila](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaaritila)-koodisto kuvaa 14 mahdollista tilaa, joissa kaava voi olla sen elinkaaren eri vaiheissa:
* [Kaavoitusaloite](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/01)
* [Vireilletullut](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/02)
* [Valmistelu](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/03)
* [Kaavaehdotus](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/04)
* [Tarkistettu kaavaehdotus](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/05)
* [Hyväksytty kaava](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/06)
* [Oikaisukehotuksen alainen](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/07)
* [Valituksen alainen](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/08)
* [Osittain voimassa](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/09)
* [Voimassa](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/10)
* [Kumottu](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/11)
* [Kumoutunut](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/12)
* [Rauennut](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/13)
* [Hylätty](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/14)

Kaavojen, joiden elinkaaritila on Kaavoitusaloite,  Vireilletullut, Valmistelu, Kaavaehdotus, Tarkistettu kaavaehdotus, Hyväksytty kaava, Oikaisukehotuksen alainen tai Valituksen alainen, laadinta- ja päätösprosessi on kesken, eli niiden kaavamääräykset eivät (vielä) ole lainvoimaisia. Kaavat, jotka ovat elinkaaritilassa Osittain voimassa tai Voimassa sisältävät nykyajanhetkellä rajaamallaan alueella voimassa olevia kaavamääräyksiä. Koodit Kumottu, Kumoutunut, Rauennut ja Hylätty kuvaavat kaavan tiloja, joissa olevan kaavan elinkaari on päättynyt.

### Sallitut kaavan elinkaaren tilan muutokset
Kaavan elinkaaritila voi sen laadinta-, päätös-, valitus-, voimassaolo- ja kumoutumisvaiheidensa esiintyä ja muuttua vain tässä luvussa kuvatuilla tavoilla.

{% include common/clause_start.html type="req" id="elinkaari/vaat-ensimmainen-elinkaaritila" %}
Kaavan elinkaaritila tallennettaessa kaava ensimmäistä kertaa kaavatietovarastoon voi olla jokin seuraavista riippuen Kaavan ```digitaalinenAlkupera```-attribuutin arvosta:
   * [Tietomallin mukaan laadittu](http://uri.suomi.fi/codelist/rytj/RY_DigitaalinenAlkupera/code/01): tilat Kaavoitusaloite, Vireilletullut, Valmistelu, Kaavaehdotus, Tarkistettu kaavaehdotus tai Hyväksytty kaava.
   * [Kokonaan digitoitu](http://uri.suomi.fi/codelist/rytj/RY_DigitaalinenAlkupera/code/02), [Osittain digitoitu](http://uri.suomi.fi/codelist/rytj/RY_DigitaalinenAlkupera/code/03) tai [Kaavan rajaus digitoitu](http://uri.suomi.fi/codelist/rytj/RY_DigitaalinenAlkupera/code/04): tilat Osittain voimassa, Voimassa, Kumottu, Kumoutunut tai Rauennut.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-elinkaaritila-siirtymat" %}
Kaavan ```elinkaaritila```-attribuutin arvo voi kahden sen peräkkäisen tallennusversion välillä vain seuraavilla tavoilla:
* Tilasta ```Kaavoitusaloite``` tilaan ```Vireilletullut```, ```Valmistelu```, ```Kaavaehdotus```, ```Tarkistettu kaavaehdotus```, ```Hyväksytty kaava``` tai ```Hylätty```.
* Tilasta ```Vireilletullut``` tilaan ```Valmistelu```, ```Kaavaehdotus```, ```Tarkistettu kaavaehdotus```, ```Hyväksytty kaava``` tai ```Rauennut```.
* Tilasta ```Valmistelu``` tilaan ```Valmistelu```, ```Tarkistettu kaavaehdotus```, ```Hyväksytty kaava``` tai ```Rauennut```.
* Tilasta ```Kaavaehdotus``` tilaan ```Tarkistettu kaavaehdotus```, ```Hyväksytty kaava``` tai ```Rauennut```.
* Tilasta ```Tarkistettu kaavaehdotus``` tilaan ```Hyväksytty kaava``` tai ```Rauennut```.
* Tilasta ```Hyväksytty kaava``` tilaan ```Oikaisukehotuksen alainen```, ```Valituksen alainen```, ```Osittain voimassa```, ```Voimassa``` tai ```Kumoutunut```.
* Tilasta ```Oikaisukehotuksen alainen``` tilaan ```Valituksen alainen```, ```Osittain voimassa```, ```Voimassa``` tai ```Kumoutunut```.
* Tilasta ```Valituksen alainen``` tilaan ```Oikaisukehotuksen alainen```, ```Osittain voimassa```, ```Voimassa``` tai ```Kumoutunut```.
* Tilasta ```Osittain voimassa``` tilaan ```Kumottu```.
* Tilasta ```Voimassa``` tilaan ```Kumottu```.
* Tilasta ```Kumottu``` ei sallittuja siirtymiä.
* Tilasta ```Kumoutunut``` ei sallittuja siirtymiä.
* Tilasta ```Rauennut``` ei sallittuja siirtymiä.
* Tilasta ```Hylätty``` ei sallittuja siirtymiä.
{% include common/clause_end.html %}

Kaava ei ole lainvoimainen kun siitä on valitettu. Valitustilanteessa MRL 201 §:n mukaan kunnanhallitus voi valitusajan kuluttua määrätä yleis- ja asemakaavan tulemaan voimaan ennen kuin se on saanut lainvoiman kaava-alueen siltä osalta, johon valitusten tai oikaisukehotuksen ei voida katsoa kohdistuvan.  Kaava ei siis ole lainvoimainen kun kunta on määrännyt kaavan osittain voimaan. Kaava on lainvoimainen vasta kun oikeus on käsitellyt tulleet valitukset ja antanut päätöksensä ja tämä päätös on lainvoimainen.

Elinkaarisääntöjä päivitetään vuoden 2022 aikana.

### Kaavamääräysten ja -suositusten elinkaaren tila
Tavallisesti kaavan sisältämien kaavamääräysten ja -suositusten elinkaaritilan arvo on sama kuin koko kaavalla, mutta ne voivat erota toisistaan kahdessa tapauksessa:
* Kaavan osittaisen voimaan määräämisen tapauksessa osa kaavamääräyksistä ja -suosituksista voidaan kumota (ks. [Kaavan osittainen määrääminen voimaan](#elinkaari-vaat-osittainen-voimaantulo))
* Kaavamuutoksen tai vaihekaavan voimaantulo aiheuttaa siinä kumottaviksi yksilöityjen kaavamääräysten ja -suositusten kumoamisen (ks. [Kaavamuutokset ja vaihekaavat](#elinkaari-vaat-kaavamuutoksen-voimaantulo))

### Kaavan elinkaaritilan muutoksiin liittyvät käsittely- ja vuorovaikutustapahtumat
Kun kaavasta viedään kaavatietovarastoon uusi versio, jossa sen elinkaaritila on muuttunut, liittyy kyseisen kaavan version syntymiseen tyypillisesti jokin käsittelytapahtuma.

{% include common/clause_start.html type="req" id="elinkaari/vaat-elinkaaritilan-muutostapahtumat" %}
[Kaavan](dokumentaatio/#kaava) ```elinkaaritila```-attribuutin arvon seuraaviin muutoksiin tulee aina liittyä [Kasittelytapahtuma](dokumentaatio/#kasittelytapahtuma), jonka ```laji```-attribuutin arvo tulee olla elinkaarimuutosta vastaava:
* Muutos tilaan [Virelletullut](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/02): Liityttävä käsittelytapahtuman laji [Kaava virelletulo](http://uri.suomi.fi/codelist/rytj/RY_KaavanKasittelytapahtumanLaji/code/04)
* Muutos tilaan [Hyväksytty kaava](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/06): Liityttävä joko käsittelytapahtuman laji [Kaavan hyväksyminen](http://uri.suomi.fi/codelist/rytj/RY_KaavanKasittelytapahtumanLaji/code/09) tai [Kaavan hyväksyminen oikaisukehotuksen johdosta](http://uri.suomi.fi/codelist/rytj/RY_KaavanKasittelytapahtumanLaji/code/10).
* Muutos tilaan [Voimassa](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/10): Liityttävä käsittelytapahtuman laji [Kaavan voimaantulo](http://uri.suomi.fi/codelist/rytj/RY_KaavanKasittelytapahtumanLaji/code/13).

Yllä luetellut käsittelytapahtumat tulee tallentaa samaan aikaan elinkaaritilaltaan muuttuneen kaavan kanssa.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-ehdotuksen-nahtavilleasettaminen" %}
[Kaavan](dokumentaatio/#kaava) ```elinkaaritila```-attribuutin arvon muuttuminen arvosta [Kaavaehdotus](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/04) arvoon [Tarkistettu kaavaehdotus](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/05) tai [Hyväksytty kaava](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/06) vaatii, että kaavatietovarastossa on sekä [Kasittelytapahtuma](dokumentaatio/#kasittelytapahtuma) lajia [Kaavaehdotuksen nähtäville asettaminen](http://uri.suomi.fi/codelist/rytj/RY_KaavanKasittelytapahtumanLaji/code/06) että [Vuorovaikutustapahtuma](dokumentaatio/#vuorovaikutustapahtuma) lajia [Nähtävilläolo](http://uri.suomi.fi/codelist/rytj/RY_KaavanVuorovaikutustapahtumanLaji/code/01), joista molemmat viittavat johonkin ko. kaavan aiemmista [Kaavaehdotus](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/04)-tilassa olevista versioista assosiaatiolla ```liittyvaAsia```. Vuorovaikutustapahtuman attribuutin ```tapahtumaAika``` tulee kuvata aikaväli, jonka aikana kaavaehdotus on ollut nähtävillä.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-tarkistetun-ehdotuksen-nahtavilleasettaminen" %}
[Kaavan](dokumentaatio/#kaava) ```elinkaaritila```-attribuutin arvon muuttuminen arvosta [Tarkistettu kaavaehdotus](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/05) arvoon [Hyväksytty kaava](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/06) vaatii, että kaavatietovarastossa on sekä [Kasittelytapahtuma](dokumentaatio/#kasittelytapahtuma) lajia [Tarkistetun kaavaehdotuksen nähtäville asettaminen](http://uri.suomi.fi/codelist/rytj/RY_KaavanKasittelytapahtumanLaji/code/07) että [Vuorovaikutustapahtuma](dokumentaatio/#vuorovaikutustapahtuma) lajia [Nähtävilläolo](http://uri.suomi.fi/codelist/rytj/RY_KaavanVuorovaikutustapahtumanLaji/code/01), joista molemmat viittavat johonkin ko. kaavan aiemmista [Tarkistettu kaavaehdotus](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/05)-tilassa olevista versioista assosiaatiolla ```liittyvaAsia```. Vuorovaikutustapahtuman attribuutin ```tapahtumaAika``` tulee kuvata aikaväli, jonka aikana tarkistettu kaavaehdotus on ollut nähtävillä.
{% include common/clause_end.html %}

{% include common/clause_start.html type="rec" id="elinkaari/suos-nahtavillaolopaikka" %}
Mikäli kaavaehdotus tai tai tarkistettu kaavaehdotus on nähtävillä tietyssä fyysisessä paikassa, on suositeltavaa ilmaista kyseisen paikan sijainti [Vuorovaikutustapahtuma](dokumentaatio/#vuorovaikutustapahtuma)-luokan attribuutin ```sijainti```-attribuutin avulla.
{% include common/clause_end.html %}

Huomaa, että muutos tilaan [Kumottu](http://uri.suomi.fi/codelist/rytj/RY_KaavanElinkaariTila/code/11) voi liittyvä joko käsittelytapahtuman lajiin [Kaavan kumoaminen](http://uri.suomi.fi/codelist/rytj/RY_KaavanKasittelytapahtumanLaji/code/11) tai kaavan kumoamiseen [kaavamuutokseen tai vaihekaavan](#kaavamuutokset-ja-vaihekaavat) lainvoimaiseksi tulon yhteydessä.



<!--
## Esimerkkejä elinkaaritapahtumista

### Kaavan luominen ja muokkaus ennen ensimmäistä tallennusta kaavatietovarastoon

### Kaavan ensimmäinen tallennus kaavatietovarastoon

### Kaavan muokatun version tallennus kaavatietovarastoon

### Käsittely- tai vuorovaikutustapahtuman lisääminen

### Kaavan hyväksyminen

### Kaavan määrääminen voimaan osittain

### Kaavan voimaantulosta kuuluttaminen

### Kaavan, sen yksittäisten kaavamääräysten tai -suositusten kumoaminen
-->


