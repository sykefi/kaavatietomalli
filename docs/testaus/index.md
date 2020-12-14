---
layout: "default"
title: "Kaavatietomalli - testaus"
description: ""
page: "testaus"
status: "Keskeneräinen"
---
# Kaavatietomallin testaus

Testauksessa koestettiin läpi prosessi kaavatiedon tuottamisesta, sen käsittelemisestä tiedonhallintajärjestelmässä sekä kaavatiedon esittäminen ja hyödyntäminnen loppukäyttäjän sovelluksessa. Tavoitteena oli tämän prosessin aikana tunnistaa tietomallin vahvuudet ja heikkoudet käytännön toteutuksissa. Työssä tunnistettiin parannuskohtia, joista suurin osa pystyttiin korjaamaan työn aikana tai kehittämään menetelmät, miten tietomallia voidaan jatkokehittää parempaan suuntaan.

## Mitä testattiin

* Tietomallin mukaisen yleis- ja asemakaavatiedon tuottaminen: kaavan ulkoraja, kaavakohteet ja kaavamääräykset
* Kaavatiedon vastaanottoa ja tallentamista tietojärjestelmään
* Yksilöivät tunnisteet ja niihin liittyvä elinkaarikäsittely
* Kaavatiedon julkaisemista rajapintapalvelelussa
* Kaavatiedon hyödyntämistä sovelluksessa: paikkatiedon ja kaavatiedon esittämistä sekä tiedon laskentaa (mm. Tyvi-lomakkeen tietojen laskeminen)

Testauksessa tuotettiin kaavatietoa, tiedonhallintajärjestelmä sen tallentamiseksi sekä rajapinnat tiedon vastaaanottoon ja jakeluun.

## Rajaukset

Testauksen ulkopuolelle jätettiin:
* Kaikkia tietomallin luokkia ei testattu (kts. ylle testatut luokat)
* Kaavan visualisointi
* Ajantasakaavan muodostaminen


# Testauksen toteutustapa ja -aika

Testaus toteutettiin 9.-25.11.2020. Testauksen suoritti Ilkka Rinne, Sanna Hautala, Mikko Solismaa ja Sampo Savolainen Spatineolta sekä Pilvi Nummi (Asiantuntijat N+1). Testauksessa tehtiin seuraavat asiat:

* Olemassaolevaa kaavoitustietoa digitoitiin tietomallin mukaiseen muotoon
* Tiedonhallintajärjestelmä (tietokanta, tallennuspalvelu ja rajapinnat)
* Testauksen käyttöliittymä

## Tuotetut kaavat

Sparrausryhmässä kerättiin potentiaalisia kaavoja testausta varten. Näistä valikoitiin sellaiset tapaukset, jotka kattavat keskeisimmät käyttötapaukset: 

1. Asemakaavan laadinta alueelle, jolle ei ole aiempaa asemakaavaa. Testauksessa käytiin läpi keskeiset vaiheet prosessista (vireilletulo, kaavaehdotus, kaavaehdotuksen tarkistaminen, hyväksytty kaava ja lainvoimainen kaava). Tähän valittiin ***Sipoon Nevas gård***
2. Vaiheasemakaava, jossa testataan yhden kaavakohteen muutosta. Tähän valittiin ***Espoon Servinniemi***
3. Strategisen tason yleiskaavan laadinta, joka ohjaa kaupungin rakennetun ympäristön kokonaisuuden suunnittelua. Tähän valittiin ***Tampere / Hervannan alue***
4. Rakentamista ohjaava yleiskaava. Tähän valittiin ***Lahden Enonsaari***

Lähtöaineisto oli useassa eri formaatissa. Käytössä oli kaavojen kuvat PDF-muodossa sekä vaihtelevan tasoista digitaalista aineistoa (DWG, MapInfo TAB, Shapefile).

Testauksessa tuotettiin kaavoista kaavan ulkoraja, kaavakohteet ja kaavamääräykset (sekä ulkorajaan että kaavakohteisiin liittyvät).

### Digitointiprosessi

Digitointi tehtiin kahdessa vaiheessa: geometrian muodostainen ja ominaisuustietojen tuottaminen.

Geometriat muodostettiin QGIS:in avulla digitaalisesta lähtöaineistosta. Lopputulos tallennettin GeoJSON-muodossa. QGIS ei kuitenkaan sovellu rakenteellisten kohteen ominaisuustietojen syöttämiseen. Sen sijaan ominaisuustiedot tuotettiin ohjelmistokehittimellä. Työssä käytettiin avoimen lähdekoodin versiota Visual Studio Codesta. Ohjelmistokehittimeen sai lisäosan, joka näytti muokattavan geometrian halutun taustakartan päällä. Tämä auttoi digitointiprosessissa merkittävästi, sillä kohdetta oli helppo verrata alkuperäiseen kaavaselostukseen.

Lopputuloksena jokaisesta kaavasta ja kaavan versiosta tuotettiin oma hakemisto. Hakemistoon tallennettiin kaavan ulkoraja ja siihen liittyvät kaavamääräykset omaan tiedostoonsa ja kukin kaavakohde ja tähän liittyvät määräykset omiin tiedostoihinsa. Tiedostot olivat GeoJSON-muodssa FeatureCollectioneita.

Tässä vaiheessa kohteilla ei ollut vielä omia tunnisteita ja linkitys kohteiden välillä perustui siihen miten geometriaan (ulkoraja tai kaavakohde) liittyvät määräykset olivat samassa tiedostossa keskenään. Lopullisen tallennuspalveluun lähetettävä tietomallin mukainen FeatureCollection-tiedosto tuotettiin python-skripti, joka loi kaikille kohteille localId:n ja tuotti linkitykset kohteiden välille. Lopputuloksena siis yksi GeoJSON-tiedosto kokonaiselle kaavalle.

TODO: linkkejä muodostettuihin tiedostoihin? todellisiin viimeisten muutosten mukaisiin

## Testaukseen tuotettu tietonhallintajärjestelmä

Testausta varten toteutettiin tiedonhallintajärjestelmä. Järjestelmä asennettiin Spatineon pilvipalveluympäristöön testausta varten. Järjestelmä koostui kolmesta pääosasta:

* Tietokanta
* Tallennuspalvelu
* OGC API - Features -rajapintapalvelu

Tietokantana oli PostGIS. Tallennuspalvelu ja rajapintapalvelu toteutettiin NodeJS:llä.


### Tietokanta

Tietokantana käytettiin Postgresql-tietokantaa PostGIS-laajennoksella. Tietojen tallennusta varten tehtiin kolme tietokantataulua: kaavan ulkorajat, kaavakohteet ja kaavamääräykset. Kaikissa kolmessa taulussa oli samat sarakkeet: id (pääavain), created_time (tallennusaika), geom (geometriatieto) ja properties. Properties-sarake sisälsi kohteen kaikki ominaisuustiedot rakenteellisessa muodossa (jsonb-sarake).

Tietokantaan tallennetuissa kohteissa linkitykset kohteiden välillä sisältävät ainoastaan viittauksen kohteen id:hen (`linkedFeatureId`). Lopulliset selaimessa käytettävät linkit luodaan vasta rajapinnan palauttamissa kohteissa.

Tietokantataulujen lisäksi testattiin luoda kustakin tietokantataulusta näkymä, jossa rakenteellisen tiedon yksittäiset kentät (=tiedot, joita on maksimissaan vain yksi kappale kohteella) on sarakkeina. Ne osat ominaisuustiedoista, joita voi olla useampia kuin yksi kappale on jsonb-sarakkeina taulussa. Nämä näkymät auttoivat tietokannan hahmottamisessa testausjärjestelmää rakennettaessa. Kuitenkin tallennuspalvelu ja rajapinta toteutettiin ilman näkymiä suoraan tietokantataulujen avulla.

### Tallennuspalvelu

Tallennuspalvelu vastaanottaa yhden kokonaisen kaavan kerrallaan. Kaava lähetetään GeoJSON FeatureCollection:ina HTTP POST-sanomana tallennuspalveluun. Palvelu suorittaa kaavalle erinäisiä tarkistuksia ennen kaavan kohteiden tallentamista. Muun muassa:

* Collectionissa tulee olla tasan yksi SpatialPlan
* Collectionissa tulee olla 1..n kpl PlanRegulationObject:eja
* Collectionissa tulee olla 1..n kpl PlanRegulation:eja
* SpatialPlanillä tulee olla PlanId ja jos sillä on asetettu identityId, nämä eivät saa olla ristiriidassa tietokantaan aiemmin tallennetun kaavan ulkorajan kanssa

Latauspalvelu luo identityId:n kakille kohteille, joilla sitä ei aiemmin ole ollut. Luotu id on uuid v4:n mukainen. Lisäksi latauspalvelu luo koko lataukselle versionId:n (perustuen tallennushetkeen) ja leimaa tämän saman versionId:n kaikkiin tallennettaviin kohteisiin. Lopuksi ennen tallentamista kaikkien kohteiden GeoJSON id:ksi asetetaan `[kohteen identityId].[kohteen versionId]` (huom. kaikilla on siis sama versionId) ja kohteiden väliset linkitykset päivitetään näiden lopullisten id:itten perusteella.

### OGC API - Features -rajapintapalvelu

Rajapinta toteutettiin avoimen lähdekoodin SOFP-palvelimella (sofp-core ja sofp-postgis-backend). Testauksen yhteydessä SOFP:ia laajennettiin siten, että sen PostGIS-laajennos osaa hyödyntää jsonb-sarakkeeseen tallennettuja kohteiden ominaisuustietoja.

Testauksessa toteutettiin kaksi rinnakkaista rajapintaa. Toinen näistä hyödyntää tietokantatauluja ja toinen näistä lataa kohteet ja niiden tiedot näkymistä. Näkymiin pohjautuva versio rajapinnasta oli koe, joka todettiin tarpeettoman monimutkaiseksi testauksen tarpeisiin nähden eikä sitä hyödynnetty käyttöliittymässä. Tässä dokumentissa käsitellään tietokantatauluhin perustuvaa rajapintaa ellei toisin mainita.

OGC API - Features -rajapinnassa tiedot julkaistaan Collectioneissa. Collectionin palauttamilla kohteilla tulee olla yhdenmukainen tietomalli. Tämän periaatteen johdosta testattu kaavatieto julkaistiin kolmessa collectionissa: SpatialPlan, PlanRegulationObject ja PlanRegulation. Näiden kolmen lisäksi koetettiin rakentaa neljäs, "FeatureCollection"-niminen, collection, josta palautuisi kokonainen kaava kaikkineen kohteineen. Jälkimmäisestä lisää kohdan "FeatureCollection-rajapinta" alla.

Rajapinnasta yhden kokonaisen kaavan tietojen haku toimii kolmivaiheisesti:
* Ensin noudetaan SpatialPlan-collectionista kaava, jonka tiedot haetaan
* PlanRegulationObject:it haetaan SpatialPlan-kohteen linkkien avulla
* PlanRegulation:it haetaan SpatialPlan-kohteen ja PlanRegulationObject-kohteiden linkkien avulla

Testauksessa käytetyn kaltaisen rajapinnan kohdalla kokonaisen kaavan haku vaatii siis useita, jopa satoja hakuja. Hakujen tekeminen on kuitenkin helppoa, koska rajapinnan palauttamissa kohteissa on valmiit linkit rajapintaan, joiden avulla viitatut kohteet on erittäin helppo hakea.

Rajapinta löytyy osoitteesta: https://ym-yk-ak.spatineo-devops.com/api

On huomattavaa, että OGC API - Features -palvelun OpenAPI-kuvaus on puutteellinen kohteiden tietomallin suhteen.


#### Kokeellinen FeatureCollection-rajapinta

Testauksen aikana todettiin, että olisi hyödyllistä olla rajapinta, mistä voi hakea kaavan kaikkineen kohteineen kerrallaan. Testauksessa kuitenkin huomattiin tiettyjä periaatteellisia ongelmia valitun OGC API - Features rajapintatekniikan kanssa.

Ensimmäinen kokeiltu menetelmä oli luoda collection, mikä palauttaisi kaiken tyyppisiä kohteita (SpatialPlan. PlanRegulationObject ja PlanRegulation). Ajatuksena oli, että collectionista voisi hakea kaikki yhden kaavan kohteet OGC API - Features -rajapinnan mukaisesti rajaamalla haku kaavan tunnisteen mukaan. OGC API - Features palvelun collectionin palauttamien kohteiden ominaisuustietojen rakenteen tulisi kuitenkin olla yhtenäinen. Teknisesti olisi mahdollista toteuttaa tällainen rajapinta, mutta periaatteen tasolla tässä on ristiriita.

Toinen menetelmä oli tehdä collection, joka palauttaisi kaavan yhtenä FeatureCollection-oliona. Tässä poistuisi ensimmäisen kokeilun periaatteellinen ongelma. Ongelmaksi kuitenkin muodostuu kaavatiedon potentiaalinen monimutkaisuus ja etenkin sen koko. API Featuresissa tiedon sivuttaminen on ratkaistu kohdetasolla; suuri määrä palautettavaa tietoa jaetaan kohteiden perusteella eri sivuille. Käyttäjä voi ladata koko tulosjoukon hakemalla kunkin sivun peräkkäin. Jos kaava palautettaisiin yhtenä FeatureCollection-kohteena, ei tulosjoukkoa voi sivuttaa. Lisäksi GeoJSON standardin mukaan FeatureCollectionin memberinä ei saa olla FeatureCollectioneitä, joten tällä tavalla toteutettuna rajapinta ei palauttaisi validia GeoJSON:ia.

Kompromissi OGC API - Featuresin peraatteen ja helpon kokonaisen kaavatideon noutamisen välillä olisi noutaa kaavan SpatialPlan ja sen jälkeen tämän objektin id:n perusteella kaikki siihen liittyvät PlanRegulationObject ja PlanRegulation:it omista collectioneistaan. Tällaista hakua ei kuitenkaan toteutettu testaukseen, vaan valittiin hakemaan kohteen yksittäin niihin viittaavien kohteiden linkkien perusteella.


## Testauksen käyttöliittymä

Kaavatiedon esittämiseksi rakennettiin selainsovellus. Sovellus rakennettiin Reactilla ja OpenLayersillä ja taustakarttana on OpenStreetMap. Sovellus on tarkoitettu tietokoneen näytöllä käytettäväksi, mutta toimii välttävästi myös mobiiliselaimella.

Sovellus löytyy osoitteesta: https://ym-yk-ak.spatineo-devops.com/

Sovelluksessa käyttäjä valitsee ensin yhden viidestä saatavilla olevasta kaavasta. Kaavan valinnan jälkeen käyttäjän tulee valita kaavan versio. Kun tämä on valittu, lataa sovellus kaavan tiedot rajapintapalvelusta ja esittää kaavan kartalla. On tärkeä huomata, että testauksessa keskityttiin koneluettavan kaavan tuottamiseen ja hyödyntämiseen, mutta ei visualisointiin.

Sovelluksessa voi filtteröidä kaavakohteita näihin kohdistuvien kaavamääräyslajien avulla. Näin kartalla visualisoidaan ainoastaan kaavan ulkoraja ja ne kaavakohteet, joihin kohdistuu kyseisen määräyslajin määräyksiä. Tällä voidaa visualisoida helposti kaavaa eri määräyslajin näkökulmasta.

Kaavakohteiden ja niiden määräykset saa näkyviin listaan klikkaamalla kartalta. Listalla näkyy kaikki ne kohteet, jotka ovat klikatun pisteen kohdalla. Kunkin kohteen ja määräyksen kohdalla on myös linkki, josta voi avata yksittäisen kaavakohteen tai määräyksen kohteen OGC API - Features rajapinnasta. Kaavan ulkorajan ja sen määräyksen saa näkyviin listalle klikkaamalla kartan päällä olevaa nappia.


# Testauksen tulokset

Testauksen aikana havaitut haasteet ja puutteet tietomallissa dokumentoitiin [githubiin](https://github.com/YM-rakennettu-ymparisto/AK-YK-tietomallit/issues?q=is%3Aissue+label%3AKehityssprintti). Tässä raportissa on nostettu esiin havainnoista muutama keskeinen:

## Linkkaukset kohteista toiseen

Testauksen aikana keskusteltiin linkityksestä oliosta toiseen. Tunnistettiin, että kaksisuuntaisella linkityksellä muutos mihin tahansa olioon (ulkoraja, kaavakohde, määräys) johtaa kaikkien kaavaan liitettyjen olioiden versiointiin. 

[Github issue](https://github.com/YM-rakennettu-ymparisto/AK-YK-tietomallit/issues/57)
[Analyysi elinkaarisäännöissä](https://ym-rakennettu-ymparisto.github.io/AK-YK-tietomallit/1.0/looginenmalli/elinkaarisaannot.html#muutosten-levi%C3%A4minen-viittausten-kautta)

## Puuttuvia koodilistojen arvoja

Testauksen aikana tunnistettiin 19 puuttunutt koodilistan arvoa. Havaitut puutteet korjattiin testauksen aikana ja sen jälkeen.

## Tunnusten muoto - URI vs UUID

Rajapintapalvelun kohdalla HTTP-muotoiset osoitteet aiheuttavat tarpeetonta hankaluutta käytössä. Tämä käytännössä siksi, että tällaiset tunnukset sisältävät merkkejä (mm. `:`, `/`, `?`, `&` ja `=`), joilla on  erityismerkitys HTTP-osoitteissa. Jos ja kun osoitteella linkataan tunnuksen avulla tiettyyn tunnukseen, tulee osoitteesta tarpeettoman vaikea ja hankala lukea. Tästä lisää [elinkaarisäännöissä](https://ym-rakennettu-ymparisto.github.io/AK-YK-tietomallit/1.0/looginenmalli/elinkaarisaannot.html).

## Liikenne-aihepiirin käyttötarkoitukset

Testauksessa kävi ilmi, että liikenne-aihepiirin kaavamääräyksien ja käyttötarkoitusten kohdalla on epäselviää, mikä tieto on kaavamääräyslaji ja mikä käyttötarkoituslaji [65](https://github.com/YM-rakennettu-ymparisto/AK-YK-tietomallit/issues/65).

# Yhteenveto

Tietomalli toimi hyvin testauksessa. Digitointi oli helppoa suhteuttaen siihen, että käytössä ei ollut tietomallin mukaisen tiedon tuottamiseen tarkoitettua erityistyökalua. Malli on yleinen ja siten hyvin joustava ja siten kykenee muotoutumaan niin käytäntöjen kuin ympäröivän lainsäädännön ja toimintatapojen kehittyessä. Kuitenkin yleisyyden takia on tärkeää huolehtia tiedon eheystarkistuksista, jotta tiedon laadusta voidaan huolehtia. Eheystarkistus- ja validointipalvelun olisi hyvä toimia lähes reaaliaikaisesti eikä ainoastaan tallennusvaiheessa tai erillisenä validointitoimenpiteenä.

Tietomallipohjaisen kaavoituksen hyötyjä tuli todistettua testauksessa Tyvi-lomakkeen tietojan laskemisessa. Käyttöliittymäsovellukseen toteutettiin nykymallin kaltainen lomake ja siihen tietojen laskeminen noin kahdessa tunnissa.

Kaavoituksen käytännöt, koodistot ja säännöstöt tulevat elämään RYTJ:n elinkaaren aikana. Näin ollen järjestelmässä on varauduttava tähän, jotta tieto voidaan muuntaa yhteismitalliseen muotoon mm. laskentaa ja ristiintarkistuksia varten. Ajan kuluessa ja historian säännöstökerrostumien kasautuessa tästä tulee elinehto järjestelmän kehittämisen ja ylläpidettävyyden takaamiseksi.


