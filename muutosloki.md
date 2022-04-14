---
layout: "default"
description: "Kaavatietomallin muutokset versioista toiseen"
id: "muutosloki"
---
# Muutosloki

## Muutokset versiosta 1.1 versioon 1.1.1
Lisätty XML-skeeman generointiin liittyviä annotaatioita UML-malliin.

* Asetettu stereotyyppi GML Encoding::ApplicationSchema sekä paketille Kaavatiedot että MKP-ydin
* Asetettu seuraavat tagit Kaavatiedot-paketille:
   * targetNamespace: ```http://tietomallit.ymparisto.fi/kaavatiedot/v1.1```
   * xmlns: ```spatialplan```
   * xsdDocument: ```spatialplan.xsd```
   * xsdEncodingRule: ```gml33```
* Asetettu seuraavat tagit MKP-ydin -paketille:
   * targetNamespace: ```http://tietomallit.ymparisto.fi/mkp-ydin/v1.1```
   * xmlns: ```lud-core```
   * xsdDocument: ```land-use-decision-core.xsd```
   * xsdEncodingRule: ```gml33```
* Korjattu kaikkien CodeList-stereotyyppisten koodistoluokkien tagi asDictionary arvosta false arvoon true. Näin koodistoviittaukset generoituvat gml:ReferenceType-tyyppisiksi, ei enumeraatioksi.
* Korjattu Esimerkit/Rakentamisen määrä -paketin instanssikaaviossa Rakentamisen määrä - käyttötarkoituksittain jaettu kerrosala Lisätiedot-olioiden käyttötarkoitusmääräyksiin virheellisesti osoittaneet arvot osoittamaan Koodiarvo-oliohin, jotka puolestaan osoittavat määräyksiä vastaaviin koodeihin.
* Poistettu epähuomiossa jäänyt, käyttämätön Suunnittelukohde-luokka ja vaihdettu se Kaavakohde-luokkaan esimerkki-paketin Rakentamisen määrä - käyttötarkoituksittain -instanssikaaviossa.
* Lisätty puuttunut tyyppi (URI) attribuutille MKP-ydin::Asiakirja.lisatietolinkki


## Muutokset versiosta 1.0 versioon 1.1
Kaavatietomallin versio 1.1 lisää tietomalliin kaavayksikön ja kaavamääräysryhmän käsitteet ja niitä vastaavat luokat. Versio julkaistaan samaan aikaan kun kaavatietomallin versiosta 2.0 on jo laadittu luonnos, joka on syntynyt rakennetun ympäristön tietomallien harmonisointityön tuloksena 2022, ja jossa on kaavayksikön ja kaavamääräysryhmän lisäksi muitakin muutoksia. Tavoitteena tehdä versio, joka kaavayksikön ja kaavamääräysryhmän lisäystä lukuunottamatta muutoin pysyy identtisenä versioon 1.0 nähden ja on siten täysin taaksepäin yhteensopiva sen kanssa.

* Käsitemalli
   * Lisätty käsitteet Kaavayksikkö ja Kaavamääräysryhmä
* UML-malli
   * Lisätty luokat Kaavayksikko, Kaavamaaraysryhma ja Muodostajakiinteisto





