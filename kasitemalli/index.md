---
layout: "default"
description: ""
id: "kasitemalli"
status: "Ehdotus"
---
# Käsitteet ja määritelmät
{:.no_toc}

1. 
{:toc}

## Käsitekaavio
![Kaavatietomallin keskeiset käsitteet](kaavan-kasitemalli.png "Kaavatietomallin keskeiset käsitteet")

(Lataa [käsitekaavio määritelmien kanssa](kaavan-kasitemalli-maaritelmat.png))

## Käsitteet
### Kaava
{% include common/definitionref.html dict="rytj-kaava" dictname="Kaavatietomalli" id="concept-1008" name="kaava" def="maankäyttö- ja rakennuslain mukaisen kaavoitusprosessin lopputuloksena syntyvä lainvoimainen maankäyttöä tai rakentamista ohjaava suunnitelma." %}

Viittaukset toisiin käsitteisiin:
* [Lähtötietoaineisto](#lähtötietoaineisto) [0..*]: kaavan laadinnassa hyödynnetty lähtötietoaineisto
* [Kaavaselostus](#kaavaselostus) [0..1]: kaavan kaavaselostus
* [Osallistumis- ja arviointisuunnitelma](#osallistumis--ja-arviointisuunnitelma) [0..1]: kaavan osallistumis- ja arviointisuunnitelma
* [Kaavan liite](#kaavan-liite) [0..*]: muu kaavan liite kuin selostus tai osallistumis- ja arviointisuunnitelma
* [Kaavan kumoamistieto](#kaavan-kumoamistieto) [0..1]: minkä kaavan tai sen osat kaava voimaantullessaan kumoaa
* [Kaavakohde](#kaavakohde) [0..*] (kompositio): kaavan liittyä kaavamääräyksiä tai -suosituksia kohdistava paikkatietokohde
* [Kaavamääräys](#kaavamääräys) [0..*] (kompositio): yleismääräys, joka koskee koko kaavan aluetta
* [Kaavasuositus](#kaavasuositus) [0..*] (kompositio): yleissuositus, joka koskee koko kaavan aluetta


### Lähtötietoaineisto
{% include common/definitionref.html dict="rytj-kaava" dictname="Kaavatietomalli" id="concept-13" name="kaavan lähtötietoaineisto" def="kaavan laadinnassa hyödynnetty tietoaineisto, joka sisältää sellaista kaavan tulkinnan yhteydessä hyödyllistä tietoa, jota ei luoda ja josta ei päätetä osana kaavoitusprosessia" note="Käytetyt lähtötietoaineistot yhdessä kuvaavat kaavan laadintavaiheessa käytettävissä ollutta taustatietoa, johon tehdyt suunnittelupäätökset ovat perustuneet.
Lähtötietoaineisto voidaan usein esittää graafisesti karttatasona, jossa aineiston sijainnilliset tietokomponentit ja niiden tietosisältö visualisoidaan käytetään standardisoituja merkintätapoja." %}


### Kaavaselostus
{% include common/definitionref.html dict="rakymp" dictname="Rakennetun ympäristön pääsanasto" id="c126" name="kaavaselostus" def="kaavaan liittyvä selostus, jossa esitetään kaavan tavoitteiden, mahdollisten vaihtoehtojen ja niiden vaikutusten sekä ratkaisujen perusteiden arvioimiseksi tarpeelliset tiedot" note="Kaavaselostus on laadittava kaikkien lakisääteisten kaavojen yhteydessä, mutta kaavaselostus ei ole juridisesti sitova." %}

### Osallistumis- ja arviointisuunnitelma
{% include common/definitionref.html dict="mrl" dictname="Maankäyttö- ja rakennuslain käsitteitä" id="concept-159" name="osallistumis- ja arviointisuunnitelma" def="kaavoituksen alkuvaiheessa laadittava suunnitelma, jossa kuvataan kaavoituksen lähtökohdat ja tavoitteet, suunniteltu aikataulu, osallistumis- ja vuorovaikutusmuodot sekä kaavan vaikutusten arviointitavat" %}

### Kaavan liite
{% include common/definitionref.html dict="rytj-kaava" dictname="Kaavatietomalli" id="concept-1007" name="kaavan liite" def="kaavaprosessiin tai kaavan tulkintaan liittyvä asiakirja, joka ei sisällä kaavan oikeusvaikutuksellista suunnitelma- tai säännöstietoa." note="esimerkiksi selvitys, suunnitelma, kartta, havainnekuva tai muistio." %}

### Käsittelytapahtuma
{% include common/definitionref.html dict="rytj-kaava" dictname="Kaavatietomalli" id="concept-1005" name="kaavan käsittelytapahtuma" def="kaavan käsittelyprosessiin kuuluva tapahtuma, jonka johdosta elinkaaren tila voi muuttua" note="Käsittelytapahtumaan voi dokumentteja, kuten päätöspöytäkirjoja. Esimerkiksi kaavan virelletulo, kaavaehdotuksen käsittely kunnanvaltuustossa tai kaavan voimaantulo." %}

Viittaukset toisiin käsitteisiin:
* [Kaava](#kaava) [1]: kaavan versio, johon tapahtuma liittyy

### Vuorovaikutustapahtuma
{% include common/definitionref.html dict="rytj-kaava" dictname="Kaavatietomalli" id="concept-1004" name="kaavan vuorovaikutustapahtuma" def="kaavanprosessiin kuuluva tapahtuma, jonka tarkoituksena on tarjota kaavan osallisille tai muille kiinnostuneille mahdollisuus lausua mielipiteensä ja antaa palautetta valmisteilla olevasta kaavasta tai sen osasta" note="Esimerkkejä vuorovaikutustapahtumista ovat kaavaehdotusen nähtävilläolo tai kuulemistilaisuus. Vuorovaikutustapahtumiin voi liittyä dokumentteja, kuten annettuja huomioita ja kysymyksiä, sekä niiden vastineita." %}

Viittaukset toisiin käsitteisiin:
* [Kaava](#kaava) [1]: kaavan versio, johon tapahtuma liittyy

### Kaavan kumoamistieto
{% include common/definitionref.html dict="rytj-kaava" dictname="Kaavatietomalli" id="concept-2000" name="kaavan kumoamistieto" def="tieto kaavan hyväksymisen johdosta kokonaisuudessaan kumoutuvasta kaavasta tai kaavan kumottavasta osa-alueesta, yksittäisistä kaavakohteista tai kaavamääräyksistä." note="kumoamistieto kuvaa miten kaavan voimaantulo vaikuttaa toisten kaavojen ja niiden sisältämien määräysten tai suositusten kumoutumiseen." %}

### Kaavakohde
{% include common/definitionref.html dict="rytj-kaava" dictname="Kaavatietomalli" id="concept-1009" name="kaavakohde" def="kaavaan sisältyvä aluerajaus tai kohde, jonka alueella maankäyttöä tai rakentamista halutaan ohjata" note="Kaavakohteella on maantieteellinen sijainti ja muoto. Velvoittava ohjausvaikutus kuvataan liittyvien kaavamääräysten ja ei-velvoittava liittyvien kaavasuositusten avulla." %}

Viittaukset toisiin käsitteisiin:
* [Kaava](#kaava) [1]: kaavan versio, johon kohde sisältyy

### Kaavamääräys
{% include common/definitionref.html dict="rytj-kaava" dictname="Kaavatietomalli" id="concept-1010" name="kaavamääräys" def="kaavaan sisältyvä velvoittava määräys, jolla ohjataan alueiden suunnittelua ja rakentamista." note="Kaavoissa käytettävät kaavamääräysten lajit on yhteisesti sovittu. Määräys voi kohdistua joko yksittäiseen kaavakohteeseen tai koko kaavaan. Kaavamääräykseen voi sisältyä sen lajiin perustuvaa ohjausvaikutusta tarkentavia arvoja ja lisätietoja." %}

Viittaukset toisiin käsitteisiin:
* [Kaava](#kaava) [1]: kaavan versio, johon määräys sisältyy
* [Arvo](#arvo) [0..*]: tarkentava arvo
* [Lisätieto](#lisätieto) [0..*]: tarkentava tai rajaava lisätieto
* [Kaavakohde](#kaavakohde) [0..*]: kaavakohteiden versio, johon määräyksen vaikutus kohdistuu. Jos ei ole, on kyseessä yleismääräys

### Kaavasuositus
{% include common/definitionref.html dict="rytj-kaava" dictname="Kaavatietomalli" id="concept-3002" name="kaavasuositus" def="kaavaan sisältyvä ei-velvoittava ohje, joka ilmentää esimerkiksi toteutuksen tapaa ja tavoitetta." note="Suositus voi kohdistua joko yksittäiseen kaavakohteeseen tai koko kaavaan. Kaavasuositukseen voi sisältyä sen ohjausvaikutusta tarkentavia arvoja." %}

Viittaukset toisiin käsitteisiin:
* [Kaava](#kaava) [1]: kaavan versio, johon suositus sisältyy
* [Arvo](#arvo) [0..*]: tarkentava arvo
* [Kaavakohde](#kaavakohde) [0..*]: kaavakohteiden versio, johon suosituksen vaikutus kohdistuu. Jos ei ole, on kyseessä yleissuositus


### Lisätieto
{% include common/definitionref.html dict="rytj-kaava" dictname="Kaavatietomalli" id="concept-2003" name="kaavamääräyksen lisätieto" def="kaavamääräyksen tietosisältöä tarkentava nimetty ominaisuus ja sen mahdollinen arvo." note="Kaavoissa käytettävät lisätiedon lajit on yhteisesti sovittu. Lisätiedolla voidaan esimerkiksi rajata tai kohdistaa määräyksen ohjausvaikutusta." %}

Viittaukset toisiin käsitteisiin:
* [Arvo](#arvo) [0..*]: tarkentava arvo

### Arvo
{% include common/definitionref.html dict="rytj-kaava" dictname="Kaavatietomalli" id="concept-1011" name="ominaisuuden arvo" def="kaavamääräystä, kaavasuositusta tai lisätietoa tarkentava arvo." note="Yhteinen yläluokka erityyppisille numeerisille, luetelluille ja sanallisille arvoille sekä arvoväleille" %}

### Kaavatietovarasto
{% include common/definitionref.html dict="rytj-kaava" dictname="Kaavatietomalli" id="concept-3004" name="kaavatietovarasto" def="tietojärjestelmä, jonka tehtävänä on vastaanottaa, säilyttää ja jaella tietomallimuotoista kaavatietoa laatu- ja elinkaarisääntöjen mukaisesti" note="kaavatietovarasto voi vastata kaavatiedon hallinnoinnista joko paikallisesti tai kansallisesti" %}

