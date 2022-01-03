---
layout: "default"
description: "Tietomallin muutokset versiosta toiseen"
id: "muutosloki"
---
# Muutosloki
{:.no_toc}

1. 
{:toc}

## Muutokset versiosta 1.0 -> 2.0.0

### UML-mallin luokat

Siirrytty käyttämään {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/" title="Rakennetun ympäristön yhteiset tietokomponentit" %}-tietomallia, joka on tuotettu harmonisointityössä Kaavatietomallin, Tonttijakosuunnitelman sekä Rakentamiseen liittyvien lupapäätösten tietomallin välillä syksyllä 2021. Tässä yhteydessä aiemmin MKP-ydin -niminen paketti on siirretty omaan tietomalliinsa, ja laajennettu tarpeellisilta osin. Aiemmin ilman ä- ja ö-kirjaimia kirjoitetut luokkien, attirbuuttien ja assosiaatioiden nimet on nyt kirjoitettu suomenkielen mukaisesti ääkkösin (fyysisissä tietomalleissa ääkköset voidaan niin haluttaessa korvata edelleen a- ja o-kirjaimilla).

#### MKP-ydin -paketti

Paketin luokat yleistetty ja siirretty {% include common/moduleLink.html moduleId="yhteisetkomponentit" path="looginenmalli/dokumentaatio/" title="Yhteiset komponentit" %}-malliin. Yksityiskohteiset muutokset alla.

**AbstraktiVersioituObjekti**

* Uudelleennimetty -> VersioituObjekti.

**Asiakirja**

* Muutettu stereotyyppi FeatureType -> DataType.
* Lisätty attribuutti ```rooli: LanguageString[0..*]```.
* Poistettu assosiaatio ```liittyväAsiakirja:Asiakirja[0..*]```.

 **Lahtotietoaineisto**

 * Muutettu nimi -> ```Lähtötietoaineisto```.

 **AbstraktiMaankayttoasia**

 * Muutettu nimi -> ```Alueidenkäyttöasia```.
 * Lisätty uusi attrbuutti ```asianhallintaTunnus:Tunnusarvo[0..*]```.
 * Poistettu attribuutti ```oikeusvaikutteisuus:OikeusvaikutteisuudenLaji[0..1]```.
 * Muutettu assosiaatio ```asianLiite:Asiakirja[0..*]``` attribuutiksi ```asianLiite:Asiakirja[0..*]``` (```Yhteiset::Asiakirja``` on nyt stereotyypillä DataType, ei enää FeatureType).
 * Poistettu attribuutti ```voimassaoloAika:TM_Period[0..1]```.
 * Uudelleennimetty assosiaatio ```koskeeHallinnollistaAluetta``` -> ```hallinnollinenAlue```. 
 * Uudelleennimetty assosiaatio ```hyodynnettyAineisto``` -> ```liittyväAineisto```.
 * Muutettu assosiaatio ```vastuullinenOrganisaatio:Organisaatio[0..1]``` -> ```vastuutaho:Toimija[0..1]```.

**AbstraktiTapahtuma**

* Muutettu nimi -> ```Tapahtuma```.
* Muutettu assosiaatio ```liittyvaAsiakirja:Asiakirja[0..*]``` attribuutiksi ```liittyväAsiakirja:Asiakirja[0..*]``` (```Yhteiset::Asiakirja``` on nyt stereotyypillä DataType, ei enää FeatureType).

**Kasittelytapahtuma**

* Muutettu nimi -> ```Käsittelytapahtuma```.
* Muutettu assosiaatio ```kasittelija:Organisaatio[0..1]``` -> ```käsittelijä:Toimija[0..*]```.

#### Kaavatiedot-paketti

**Kaava**

* Yläluokka on muutettu ```MKP-ydin::AbstraktiMaankayttoasia``` -> ```Yhteiset::AlueidenKäyttöasia```
* Lisätty attribuutti ```oikeusvaikutteisuus```, joka oli ennen yläluokassa ```AbstraktiMaankayttoasia```.
* Attribuutti ```virelletuloAika``` on siirretty yläluokkaan ```Yhteiset::AlueidenKäyttöasia```.
* Attribuutti ```hyväksymisAika``` ilmaistaan nyt ```KaavanHyväksymispäätös```-luokan attribuutilla ```päätöspäivämäärä```, jonka tyyppi on ```Date```. Yhteys ```KaavanHyväksymispäätös```-luokkaan menee yläluokan ```Yhteiset::AlueidenKäyttöasia``` assosiaation ```päätös``` kautta.
* Assosiaatio ```laatija``` viittaa nyt luokkaan ```Yhteiset::SuunnitelmanLaatija``` aiemman ```KaavanLaatija```-luokan sijasta.
* Assosiaatiot ```osallistumisJaArviointisuunnitelma``` ja ```selostus``` ovat nyt kaksisuuntaisia, ja ```Kaava```-luokan päässä kompositio-tyyppisiä. Tämä [vaikuttaa elinkaarisääntöihin](looginenmalli/elinkaarisaannot.html#muutosten-levi%C3%A4minen-viittausten-kautta) siten, että kunkin uuden Kaava-luokan version tallennuksen yhteydessä tulee muodostaa uudet versiot myös assosioiduista Kaavaselostus- ja OsallistumisJaArviointisuunnitelma-luokkien instansseista. Uudet instanssit voivat kuitenkin niin haluttaessa viitata samaan, aiemmin tallennettuun dokumenttiin.
* Assosiaatiot ```kaavakohde```, ```kaavamääräys```, ja ```kaavasuositus``` ovat nyt kaksisuuntaisia. Tähän liittyen yläluokkien ```AbstraktiTietoyksikko```- ja ```AbstraktiKaavakohde```-luokista ```Kaavamääräys```-,```Kaavasuositus```- ja ```Kaavakohde```-luokkiin periytyneet erilliset ```kaava``` assosiaatiot on poistettu.

**AbstraktiKaavakohde**

* Yleistetty ja siirretty Yhteiset komponentit -mallin luokkaksi ```RakennetynYmpäristönKohde```
* Lisätty uusi attribuutti ```kuvaus:LanguageString[0..*]```.

**AbstraktiTietoyksikko**

* Yleistetty ja siirretty Yhteiset komponentit -mallin luokkaksi ```Tietoyksikkö```.
* Lisätty uusi attribuutti ```liittyväAsiakirja:Asiakirja[0..*]```.
* Lisätty uusi kaksisuuntainen assosiaatio ```ryhmä:Tietoryhmä[0..1]```.
* Muutettu assosiaatio ```kohdistus``` viittaamaan ```Yhteiset::RakennetunYmpäristönKohde```-luokkaan ```AbstraktiKaavakohde``` luokan asemesta.

**KaavanaLaatija**

* Yleistetty ja siirretty Yhteiset komponentit -mallin luokkaksi ```SuunnitelmanLaatija```.

**Kaavaselostus**

* Muutettu assosiaatio ```asiakirja:Asiakirja[0..*]``` attribuutiksi ```tiedosto:Asiakirja[0..*]``` (```Yhteiset::Asiakirja``` on nyt stereotyypillä DataType, ei enää FeatureType).

**OsallistumisJaArviointisuunnitelma**

* Muutettu assosiaatio ```asiakirja:Asiakirja[0..*]``` attribuutiksi ```tiedosto:Asiakirja[0..*]``` (```Yhteiset::Asiakirja``` on nyt stereotyypillä DataType, ei enää FeatureType).

**Kaavakohde**

* Uusi pakollinen attribuutti ```kohdenumero:int```.
* Poistettu attribuutti ```laji:AbstraktiKaavakohdLaji[0..1]```, jonka käyttö oli kielletty jo versiossa 1.0.
* Lisätty rajoite, joka tekee perityn ```geometria```-attribuutin pakolliseksi, koska sen pakollisuutta on höllennetty yläluokassa.

**Kaavamääräys**

* Periytyy nyt uudesta luokasta ```Yhteiset::Määräys```.
* Attribuutti ```Lisätieto``` peritytyy nyt yläluokasta ```Yhteiset::Määräys```.
* Uusi pakollinen attribuutti ```määräysumero:int```.
* Lisätty rajoite, joka vaatii ```kohdistus```-assosiaation tyypin olevan ```Kaavakohde```.
* Assosiaatio ```liittyväAsiakirja``` on korvattu yliluokan ```Yhteiset::Tietoyksikkö``` attribuutilla ```liittyväAsiakirja```.

**Kaavasuositus**

* Uusi pakollinen attribuutti ```suositusnumero:int```.
* Lisätty rajoite, joka vaatii ```kohdistus```-assosiaation tyypin olevan ```Kaavakohde```.
* Assosiaatio ```liittyväAsiakirja``` on korvattu yliluokan ```Yhteiset::Tietoyksikkö``` attribuutilla ```liittyväAsiakirja```.

**Lisätieto**

* Yleistetty ja siirretty Yhteiset komponentit -mallin luokkaksi ```Lisätieto```.
* Muutettu attribuutin ```arvo``` tyyppiä ```AbstaktiArvo``` -> ```OminaisuudenArvo```.

**AbstraktiArvo ja sen aliluokat Ajanhetkiarvo, Aikaväliarvo, GeometriaArvo, Koodiarvo, NumeerinenArvo, NumeerinenArvoväli, Korkauspiste, Korkeusväli ja TekstiArvo**

* Uudelleennimetty ```AbstraktiArvo```-luokka ```OminaisuudenArvo```-nimiseksi. Siirretty aliluokkieen Yhteiset komponentit -malliin muutoin sellaisenaan.

**Tunnusarvo**

* Uudelleennimetty attribuutti ```rekisterinTunnus:URI[0..1]``` -> ```järjestelmänTunnus:URI[0..1]```.
* Uudelleennimetty attribuutti ```rekisterinNimi:LanguageString[0..*]``` -> ```järjestelmänNimi:LanguageString[0..*]```.

**Suunnittelukohde**
Poistettu, oli jäänyt UML-mallin 1.0-versioon epähuomiossa.


### Dokumentaatio

Kesken

### Laatu- ja elinkaarisäännöt

Kesken

