---
layout: "default"
title: "Kaavatietomalli - soveltamisprofiili - asemakaava"
description: ""
id: "profiili-ak"
model: "kaavatiedot"
modelversion: "1.1-dev"
status: "Ehdotus"
---
# Kaavatietomallin soveltamisprofiili asemakaava-aineistoille
{:.no_toc}

1. 
{:toc}

## Johdanto

Tämän dokumentin vaatimukset ja suositukset muodostavat Kaavatietomallin loogisen tietomallin soveltamisprofiilin asemakaava-aineistoille. Soveltamisprofiili kuvaa ne rajoitukset ja lisävaatimukset, joita tulee noudattaa Kaavatietomallin [UML-kielisen kuvauksen](../../looginenmalli/uml/) ja sen [sanallisen dokumentaation](../../looginenmalli/dokumentaatio/) soveltamisessa asemakaavojen tietoaineistojen kuvaamiseen.

Tämän muodollisen dokumentin tietoja täydentää [Kaavatietomallin keittokirja - asemakaava](./keittokirja.html), joka sisältää käytännön esimerkkejä Kaavatietomallin soveltamisesta asemakaavoituksen kaavoitusratkaisuihin.

{% include clause_start.html type="req" id="prof-ak/vaat-asemakaava-aineisto-maar" %}
Kaavatietomallin mukainen asemakaava-aineisto koostuu [Kaava](../../looginenmalli/dokumentaatio/#kaava)-luokan instansseista, joiden ```laji```-attribuutin arvo on jokin [Kaavalajit]()-koodiston koodin [Asemakaava](http://uri.suomi.fi/codelist/rytj/RY_Kaavalaji/code/3) [alakoodeista](../../looginenmalli/elinkaarisaannot.html#elinkaari-vaat-alakoodi-maar), sekä näihin instansseihin Kaavatietomallin mukaisesti liittyvistä muiden luokkien instansseista.
{% include clause_end.html %}

## Koodistot

### Vuorovaikutustapahtuman laji
{% include clause_start.html type="req" id="prof-ak/vaat-vuorovaikutustapahtuman-laji" %}
Luokan [AbstraktiVuorovaikutustapahtumanLaji](../../looginenmalli/dokumentaatio/#abstraktivuorovaikutustapahtumanlaji) sijaan tulee käyttää tarkentavaa luokkaa [KaavanVuorovaikutustapahtumanLaji](../../looginenmalli/dokumentaatio/#kaavanvuorovaikutustapahtumanlaji).
{% include clause_end.html %}

### Käsittelytapahtuman laji
{% include clause_start.html type="req" id="prof-ak/vaat-kasittelytapahtuman-laji" %}
Luokan [AbstraktiKasittelytapahtumanLaji](../../looginenmalli/dokumentaatio/#abstraktikasittelytapahtumanlaji) sijaan tulee käyttää tarkentavaa luokkaa [KaavanKasittelytapahtumanLaji](../../looginenmalli/dokumentaatio/#kaavankasittelytapahtumanlaji).
{% include clause_end.html %}

### Kaavakohdelaji
[AbstraktiKaavakohdelaji](../../looginenmalli/dokumentaatio/#abstraktikaavakohdelaji)-koodisto on varattu tulevaisuuden käyttöön. Tässä tietomalliin versiossa ei määritellä asemakaavakohtaista koodistoa kaavakohdelajeille.

{% include clause_start.html type="req" id="prof-ak/vaat-kaavakohdelaji" %}
[Kaavakohde](../../looginenmalli/dokumentaatio/#kaavakohde)-luokan ```laji```-attribuuttia ei saa käyttää informaation välittämiseen. Mikäli sille on annettu ei-tyhjä arvo, se tulee jättää huomiotta.  
{% include clause_end.html %}

### Kaavoitusteema
{% include clause_start.html type="req" id="prof-ak/vaat-kaavoitusteema" %}
Luokan [AbstraktiKaavoitusteema](../../looginenmalli/dokumentaatio/#abstraktikaavoitusteema) sijaan tulee käyttää tarkentavaa luokkaa [KaavoitusteemaAsemakaava](../../looginenmalli/dokumentaatio/#kaavoitusteemaasemakaava).
{% include clause_end.html %}

### Kaavamääräyslaji
{% include clause_start.html type="req" id="prof-ak/vaat-kaavamaarayslaji" %}
Luokan [AbstraktiKaavamaaraysLaji](../../looginenmalli/dokumentaatio/#abstraktikaavamaarayslaji) sijaan tulee käyttää tarkentavaa luokkaa [KaavamaaraysLajiAsemakaava](../../looginenmalli/dokumentaatio/#kaavamaarayslajiasemakaava).
{% include clause_end.html %}

### Kaavamääräyksen lisätiedon laji
{% include clause_start.html type="req" id="prof-ak/vaat-kaavamaarayksen-lisatieton-laji" %}
Luokan [AbstraktiLisatiedonLaji](../../looginenmalli/dokumentaatio/#abstraktilisatiedonlaji) sijaan tulee käyttää tarkentavaa luokkaa [LisatiedonLajiAsemakaava](../../looginenmalli/dokumentaatio/#lisatiedonlajiasemakaava).
{% include clause_end.html %}

## Kaavamääräyslajien arvot ja lisätiedot

### Alueen käyttötarkoitus
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01>

Ryhmittelyotsikko, vain koodin [alakoodeja](../../looginenmalli/elinkaarisaannot.html#elinkaari-vaat-alakoodi-maar) käytetään.

{% include clause_start.html type="req" id="prof-ak/vaat-alueen-kayttotarkoitus" %}
Kaikkien asemakaavojen tietoaineistojen sisältämien [Kaavamaarays](../../looginenmalli/dokumentaatio/#kaavamaarays)-luokan instanssien, joiden ```laji```-attribuutin arvo on jokin [Alueen käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01)-koodin alakoodi, osalta tulee noudattaa seuraavia rajoituksia:
* ```arvo```-attribuutin arvoina saa esiintyä nolla tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa. Muun tyyppiset arvot eivät ole sallittuja.
* ```lisatieto```-attribuutin arvoina saa esiintyä nolla tai useampi [Lisatieto](../../looginenmalli/dokumentaatio/#lisatieto), jonka laji on [Poisluettava käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_LisatiedonLaji_AK/code/04), ja jonka ```arvo```-attribuutin arvoina on yksi tai useampi [KoodiArvo](../../looginenmalli/dokumentaatio/#koodiarvo), jotka viittaavat koodiston [KaavamääraysLaji](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01) koodien [Alueen käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01) tai [Alueen osan käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/02) alakoodeihin. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

Poisluettavat käyttötarkoituslajit tulee valita siten, että ne kohdistuvat ```arvo```-attribuuttien avulla valittuun yleispiirteisempään joukkoon käyttötarkoituksia poislukien niistä osan. Esim. [Työ ja tuotanto](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0106) poislukien [Alue, jolle saa sijoittaa merkittävän, vaarallisia kemikaaleja valmistavan tai varastoivan laitoksen](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/010604).

{% include question.html content="Tulisiko olla oma lisätiedon laji 'Käyttötarkoituksen osuus maapinta-alasta', jonka avulla voitaisiin määrätä käyttötarkoituksen jakautuminen tapauksissa, josssa kyse ei ole rakentamisesta tai kun sallittua kerrosalaa tai -tilavuutta ei määrätä kaavassa?" %}


### Alueen osan käyttötarkoitus
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/02>

Ryhmittelyotsikko, vain [alakoodeja](../../looginenmalli/elinkaarisaannot.html#elinkaari-vaat-alakoodi-maar) käytetään.

{% include clause_start.html type="req" id="prof-ak/vaat-alueen-osan-kayttotarkoitus" %}
Kaikkien asemakaavojen tietoaineistojen sisältämien [Kaavamaarays](../../looginenmalli/dokumentaatio/#kaavamaarays)-luokan instanssien, joiden ```laji```-attribuutin arvo on jokin [Alueen osan käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/02)-koodin alakoodi, osalta tulee noudattaa seuraavia rajoituksia:
* ```arvo```-attribuutin arvoina saa esiintyä nolla tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa. Muun tyyppiset arvot eivät ole sallittuja.
* ```lisatieto```-attribuutin arvoina saa esiintyä nolla tai useampi [Lisatieto](../../looginenmalli/dokumentaatio/#lisatieto), jonka laji on [Poisluettava käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_LisatiedonLaji_AK/code/04), ja jonka ```arvo```-attribuutin arvoina on yksi tai useampi [KoodiArvo](../../looginenmalli/dokumentaatio/#koodiarvo), jotka viittaavat koodiston [KaavamääraysLaji](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01) koodin [Alueen osan käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/02) alakoodeihin. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

Poisluettavat käyttötarkoituslajit tulee valita siten, että ne kohdistuvat ```arvo```-attribuuttien avulla valittuun yleispiirteisempään joukkoon käyttötarkoituksia poislukien niistä osan.

{% include question.html content="Tulisiko olla oma lisätiedon laji 'Käyttötarkoituksen osuus maapinta-alasta', jonka avulla voitaisiin määrätä käyttötarkoituksen jakautuminen tapauksissa, josssa kyse ei ole rakentamisesta tai kun sallittua kerrosalaa tai -tilavuutta ei määrätä kaavassa?" %}

### Rakentamisen määrä
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji/code/03>

Ryhmittelyotsikko, vain [alakoodeja](../../looginenmalli/elinkaarisaannot.html#elinkaari-vaat-alakoodi-maar) käytetään.

#### Sallittu kerrosala
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0301>

{% include clause_start.html type="req" id="prof-ak/vaat-sallittu-kerrosala-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) tai yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), joka kertoo sallitun rakentamiseen kokonaismäärän kerrosneliömetreinä (```k-m2```) sen kaavakohteen aluella, johon kaavamääräys on liitetty. Numeerisen arvon tai arvovälin minimi- ja maksimiarvojen on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-sallittu-kerrosala-lisatiedot" %}
```lisatieto```-attribuutin arvoina saa esiintyä nolla tai useampi [Lisatieto](../../looginenmalli/dokumentaatio/#lisatieto), jonka laji on [Käyttötarkoituksen osuus kerrosalasta](http://uri.suomi.fi/codelist/rytj/RY_Lisatiedonlaji_AK/code/01), jolla on täsmälleen kaksi arvoa:
*  Yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) tai yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), jotka kertovat sallitun tiettyyn käyttötarkoitukseen kohdistettavan kerroalan määrän koko sallitusta kerrosalasta joko kerrosneliömetreinä (```k-m2```) tai prosentteina (```%```). Numeerisen arvon tai arvovälin minimi- ja maksimiarvojen on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta.
* Yksi [KoodiArvo](../../looginenmalli/dokumentaatio/#koodiarvo), joka viittaa KaavamääraysLaji-koodiston koodien [Alueen käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01) tai [Alueen osan käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/02) johonkin alakoodiin.
{% include clause_end.html %}

Mikäli sallittua rakentamisen määrää ei ole jaoteltu käyttötarkoituksittain, ei lisätietoja käytetä.

#### Sallittu rakennustilavuus
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0302>

{% include clause_start.html type="req" id="prof-ak/vaat-sallittu-rakennustilavuus-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) tai yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), jotka kertovat sallitun rakentamisen kokonaismäärän kuutiometreinä (```m3```) sen kaavakohteen aluella, johon kaavamääräys on liitetty. Numeerisen arvon tai arvovälin minimi- ja maksimiarvojen on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-sallittu-rakennustilavuus-lisatiedot" %}
```lisatieto```-attribuutin arvoina saa esiintyä nolla tai useampi [Lisatieto](../../looginenmalli/dokumentaatio/#lisatieto), jonka laji on [Käyttötarkoituksen osuus kerrosalasta](http://uri.suomi.fi/codelist/rytj/RY_Lisatiedonlaji_AK/code/01), jolla on täsmälleen kaksi arvoa:
*  Yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) tai yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), jotka kertovat sallitun tiettyyn käyttötarkoitukseen kohdistettavan rakennustilavuuden määrän koko sallitusta rakennustilavuudesta joko kuutiometreinä (```k-m3```) tai prosentteina (```%```). Numeerisen arvon tai arvovälin minimi- ja maksimiarvojen on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta.
* Yksi [KoodiArvo](../../looginenmalli/dokumentaatio/#koodiarvo), joka viittaa [KaavamääraysLaji](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01) koodien [Alueen käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01) tai [Alueen osan käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/02) johonkin alakoodiin.
{% include clause_end.html %}

Mikäli sallittua rakentamisen määrää ei ole jaoteltu käyttötarkoituksittain, ei lisätietoja käytetä.

{% include question.html content="Tuleeko käyttää termiä 'kerroskuutiometri' vai riittääkö 'kuutiometri'? Miten rakennustilavuus lasketaan (vrt.kerrosneliömetrit)?" %}

{% include question.html content="Onko järkevää ilmaista sallittu rakennustilavuus eri kaavamääräyslajina kuin sallittu kerrosala. Nykyisellään rakenne on identtinen, vain yksiköt eroavat" %}

#### Tehokkuusluku
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0303>

{% include clause_start.html type="req" id="prof-ak/vaat-tehokkuusluku-arvot" %}
```arvo```-attribuutin arvona saa esiintyä joko yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) tai yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), jotka kertovat rakennustehokkuden, eli alueen rakennusten yhteenlasketun kerrosalan suhteessa alueen pinta-alaan, sen kaavakohteen aluella, johon kaavamääräys on liitetty. Ilmaistaan tehokkuuslukuna ```e```, yksikkönä ```k-m2/m2```. Muun tyyppiset arvot eivät ole sallittuja. Numeerisen arvon tai arvovälin minimi- ja maksimiarvojen on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-vaat-tehokkuusluku-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include question.html content="Pitäisikö määräyksen nimi olla Rakennustehokkuus, tehokkuusluku on tapa ilmaista käsite numerona?" %}

#### Maanpäällinen kerrosluku
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0304>

{% include clause_start.html type="req" id="prof-ak/vaat-maanpaallinen-kerrosluku-arvot" %}
```arvo```-attribuutin arvona saa esiintyä joko yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) tai yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), jotka kertovat rakennusten maanpäällisten kerrosten sallitun lukumäärän sen kaavakohteen aluella, johon kaavamääräys on liitetty. Numeerisen arvon tai arvovälin minimi- ja maksimiarvojen on toteutettava [Integer](../../looginenmalli/dokumentaatio/#integer)-rajapinta. Yksikköjä ei käytetä. Muun tyyppiset arvot eivät ole sallittuja. 
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-maanpaallinen-kerrosluku-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Maanalainen kerrosluku
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0305>

{% include clause_start.html type="req" id="prof-ak/vaat-maanalainen-kerrosluku-arvot" %}
```arvo```-attribuutin arvona saa esiintyä joko yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) tai yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), jotka kertovat rakennusten maanalaisten kerrosten sallitun lukumäärän sen kaavakohteen aluella, johon kaavamääräys on liitetty. Numeerisen arvon tai arvovälin minimi- ja maksimiarvojen on toteutettava [Integer](../../looginenmalli/dokumentaatio/#integer)-rajapinta. Yksikköjä ei käytetä. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-maanalainen-kerrosluku-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}


#### Kellarin sallittu kerrosalaosuus
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0306>

{% include clause_start.html type="req" id="prof-ak/vaat-kellarin-sallittu-kerrosalaosuus-arvot" %}
```arvo```-attribuutin arvona saa esiintyä joko yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) tai yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), jotka kertovat kuinka suuren osan kunkin rakennuksen suurimman kerroksen alasta saa kellarikerroksessa käyttää kerrosalaan luettavaksi tilaksi sen kaavakohteen aluella, johon kaavamääräys on liitetty. Numeerisen arvon tai arvovälin minimi- ja maksimiarvojen on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta. Ilmaistaan prosentteina (```%```). Muun tyyppiset arvot eivät ole sallittuja. 
{% include clause_end.html %}

{% include tip.html content="Murtolukuna ilmaistun osuuden voi ilmaista likimääräisesti myös arvovälinä, esim. ```1/3``` olisi ```33-34%```" %}

{% include clause_start.html type="req" id="prof-ak/vaat-kellarin-sallittu-kerrosalaosuus-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Ullakon sallittu kerrosalaosuus
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0307>

{% include clause_start.html type="req" id="prof-ak/vaat-ullakon-sallittu-kerrosalaosuus-arvot" %}
```arvo```-attribuutin arvona saa esiintyä joko yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) tai yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), jotka kertovat kuinka suuren osan kunkin rakennuksen suurimman kerroksen alasta saa ullakkokerroksessa käyttää kerrosalaan luettavaksi tilaksi sen kaavakohteen aluella, johon kaavamääräys on liitetty. Numeerisen arvon tai arvovälin minimi- ja maksimiarvojen on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta. Ilmaistaan prosentteina (```%```). Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include tip.html content="Murtolukuna ilmaistun osuuden voi ilmaista likimääräisesti myös arvovälinä, esim. ```1/3``` olisi ```33-34%```" %}

{% include clause_start.html type="req" id="prof-ak/vaat-ullakon-sallittu-kerrosalaosuus-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Rakennuspaikkojen määrä
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0308>

{% include clause_start.html type="req" id="prof-ak/vaat-rakennuspaikkojen-maara-arvot" %}
```arvo```-attribuutin arvona saa esiintyä yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) joka kertoo sallitun rakennuspaikkojen enimmäismäärän sen kaavakohteen aluella, johon kaavamääräys on liitetty. Numeerisen arvon tai arvovälin minimi- ja maksimiarvojen on toteutettava [Integer](../../looginenmalli/dokumentaatio/#integer)-rajapinta. Yksikköä ei käytetä. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-rakennuspaikkojen-maara-lisatiedot" %}
```lisatieto```-attribuutin arvoina saa esiintyä nolla tai useampi [Lisatieto](../../looginenmalli/dokumentaatio/#lisatieto), jonka laji on [Käyttötarkoituskohdistus](http://uri.suomi.fi/codelist/rytj/RY_Lisatiedonlaji_AK/code/02), jolla on täsmälleen yksi ```arvo``` lajia [KoodiArvo](../../looginenmalli/dokumentaatio/#koodiarvo), joka viittaa johonkin [Rakennusluokitus 2018](http://uri.suomi.fi/codelist/jhs/rakennus_1_20180712)-koodiston koodiin. Muun tyyppiset arvot eivät ole sallittuja.

Mikäli vähintään yksi lisätieto on annettu, koskee rakennuspaikkojen lukumäärä vain lisätietojen avulla rajattuja rakennustyyppejä.
{% include clause_end.html %}

{% include note.html content="Käytetään tavallisesti vain ranta-asemakaavoissa" %}

#### Lisärakennusoikeus
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0309>

{% include clause_start.html type="req" id="prof-ak/vaat-lisarakennusoikeus-arvot" %}
```arvo```-attribuutin mahdolliset arvot ovat seuraavat:
* Yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) tai yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), joka kertoo sallitun lisärakentamisen kokonaismäärän joko kerrosneliömetreinä (```k-m2```) tai kuutiometreinä (```m3```) sen kaavakohteen aluella, johon kaavamääräys on liitetty. Numeerisen arvon tai arvovälin minimi- ja maksimiarvojen on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta.
* Nolla tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa.
{% include clause_end.html %}


{% include clause_start.html type="req" id="prof-ak/vaat-lisarakennusoikeus-lisatiedot" %}
```lisatieto```-attribuutin arvoina saa esiintyä yksi tai useampi [Lisatieto](../../looginenmalli/dokumentaatio/#lisatieto), jonka laji on [Käyttötarkoituksen osuus kerrosalasta](http://uri.suomi.fi/codelist/rytj/RY_Lisatiedonlaji_AK/code/01), jolla on täsmälleen kaksi arvoa:
*  Yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) tai yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), jotka kertovat sallitun tiettyyn käyttötarkoitukseen kohdistettavan kerroalan määrän koko sallitusta kerrosalasta joko kerrosneliömetreinä (```k-m2```), kuutioina (```m3```) tai prosentteina (```%```). Numeerisen arvon tai arvovälin minimi- ja maksimiarvojen on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta.
* Yksi [KoodiArvo](../../looginenmalli/dokumentaatio/#koodiarvo), joka viittaa [KaavamääraysLaji](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01) koodien [Alueen käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01) tai [Alueen osan käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/02) johonkin alakoodiin.
{% include clause_end.html %}

{% include question.html content="Miten lisärakennusoikeus eroaa käyttötarkoituskohtaisesti sallitusta kerrosalasta tai rakennustilavuudesta? Missä tapauksissa lisärakennusoikeutta käytettäisiin? Nykyisellään rakenne on lähes identtinen" %}

### Rakennusten sijoitus
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/04>

Ryhmittelyotsikko, vain [alakoodeja](../../looginenmalli/elinkaarisaannot.html#elinkaari-vaat-alakoodi-maar) käytetään.

#### Rakentamisen suhde alueen pinta-alaan
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0401>

{% include clause_start.html type="req" id="prof-ak/vaat-rak-suhde-alueen-pinta-alaan-arvot" %}
```arvo```-attribuutin arvona saa esiintyä joko yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) tai yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), joka kertoo kuinka suuren osan sen kaavakohteen pinta-alasta, johon kaavamääräys on liitetty, saa käyttää rakentamiseen. Numeerisen arvon tai arvovälin minimi- ja maksimiarvojen on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta. Ilmaistaan prosenttilukuna (```%```). Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-rak-suhde-alueen-pinta-alaan-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Etäisyys naapuritontin rajasta
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0402>

{% include clause_start.html type="req" id="prof-ak/vaat-etaisyys-naapuritontin-rajasta-arvot" %}
```arvo```-attribuutin mahdolliset arvot ovat seuraavat:
* Yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo), joka kertoo rakennusten vähimmäisetäisyyden naapuritontin rajasta sen kaavakohteen alueella, johon kaavamääräys on liitetty. Numeerisen arvon on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta. Yksikkönä metri (```m```).
* Nolla tai useampi [GeometriaArvo](../../looginenmalli/dokumentaatio/#geometriaarvo), joka on päällekkäin sen kaavakohteen geometrian osan kanssa, jonka puoleista osaa etäisyysvaatimus koskee.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-etaisyys-naapuritontin-rajasta-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Rakennusala
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0403>

{% include clause_start.html type="req" id="prof-ak/vaat-rakennusala-maar" %}
Ilmaisee, että kaavakohteen alue on rakennusala. Mikäli rakennusaloja on määritelty jonkin suuremman kaavakohteen alueen sisälle, tulee rakennukset suuremman kaavakohteen alueella rakentaa siten, että ne sijoittuvat kokonaan jokin rakennusalan sisälle.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-rakennusala-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä nolla tai useampi [KoodiArvo](../../looginenmalli/dokumentaatio/#koodiarvo), jotka kuvaa rakennusalalle rakennettavaksi tarkoitetun rakennuksen lajin viittaamalla koodistoon [Rakennusluokitus 2018](http://uri.suomi.fi/codelist/jhs/rakennus_1_20180712).
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-rakennusala-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Rakennettava kiinni rajaan
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0404>

{% include clause_start.html type="req" id="prof-ak/vaat-rakennettava-kiinni-rajaan-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [GeometriaArvo](../../looginenmalli/dokumentaatio/#geometriaarvo), joka on päällekkäin sen kaavakohteen geometrian osan kanssa, johon alueen rakennukset tulee rakentaa kiinni. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-rakennettava-kiinni-rajaan-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Rakennuspaikka
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0405>

{% include clause_start.html type="req" id="prof-ak/vaat-rakennuspaikka-maar" %}
Ilmaisee, että kaavakohteen geometria kuvaa paikkaa, jolla on rakennus tai johon voidaan rakentaa yksi tai useampi rakennus.
{% include clause_end.html %}

{% include question.html content="Voiko yhteen rakennuspaikkaan rakentaa useamman rakennuksen?" %}

{% include clause_start.html type="req" id="prof-ak/vaat-rakennuspaikka-arvot" %}
```arvo```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-rakennuspaikka-lisatiedot" %}
```lisatieto```-attribuutin arvoina saa esiintyä nolla tai useampi [Lisatieto](../../looginenmalli/dokumentaatio/#lisatieto), jonka laji on [Käyttötarkoituskohdistus](http://uri.suomi.fi/codelist/rytj/RY_Lisatiedonlaji_AK/code/02), jolla on täsmälleen yksi ```arvo``` lajia [KoodiArvo](../../looginenmalli/dokumentaatio/#koodiarvo), joka viittaa johonkin [Rakennusluokitus 2018](http://uri.suomi.fi/codelist/jhs/rakennus_1_20180712)-koodiston koodiin. Muun tyyppiset arvot eivät ole sallittuja.

Mikäli vähintään yksi lisätieto on annettu, saa rakennuspaikkaan rakentaa vain lisätietojen avulla rajattuja rakennustyyppejä.
{% include clause_end.html %}

{% include note.html content="Käytetään tavallisesti vain ranta-asemakaavoissa" %}

#### Muu rakennusten sijoitukseen liittyvä määräys
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0406>

{% include clause_start.html type="req" id="prof-ak/vaat-muu-rakennusten-sijoitus-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-muu-rakennusten-sijoitus-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

### Rakentamistapa
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/05>

Ryhmittelyotsikko, vain [alakoodeja](../../looginenmalli/elinkaarisaannot.html#elinkaari-vaat-alakoodi-maar) käytetään.

#### Kattokaltevuus
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0501>

{% include clause_start.html type="req" id="prof-ak/vaat-kattokaltevuus-arvot" %}
```arvo```-attribuutin arvoja saa esiintyä yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) tai yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), joka kertoo rakennusten katon sallitun kaltevuuden asteina (```deg```) sen kaavakohteen alueella, johon kaavamääräys on liitetty. Numeerisen arvon tai arvovälin minimi- ja maksimiarvojen on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-kattokaltevuus-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Uloke
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0502>

{% include clause_start.html type="req" id="prof-ak/vaat-uloke-maar" %}
Ilmaisee, että kaavakohteen geometria kuvaa liikenne- rautatie- tai katualueen osaa, johon saa sijoittaa yläpuolisen rakentamisen vaatimia kantavia rakenteita, jotka eivät haittaa liikennealueen käyttöä.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-uloke-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä nolla tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-uloke-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Rakennuksen harjasuunta
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0503>

{% include clause_start.html type="req" id="prof-ak/vaat-harjasuunta-arvot" %}
```arvo```-attribuutin arvona saa esiintyä yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo) tai yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), jotka kertovat rakennusten katon harjan sallitun kompassisuunnan asteina (```deg```) sen kaavakohteen alueella, johon kaavamääräys on liitetty. Numeerisen arvon tai arvovälin minimi- ja maksimiarvojen on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-harjasuunta-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Kulkuaukko
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0504>

{% include clause_start.html type="req" id="prof-ak/vaat-kulkuaukko-maar" %}
Ilmaisee, että kaavakohteen geometria kuvaa rakennukseen liittyvää paikkaa, johon tulee jättää kulkuaukko.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-kulkuaukko-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä nolla tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-kulkuaukko-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Valokatteinen tila
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0505>

{% include clause_start.html type="req" id="prof-ak/vaat-valokatteinen-tila-maar" %}
Ilmaisee, että kaavakohteen geometria kuvaa alueen osaa, johon tulee rakentaa valokatteinen tila.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-valokatteinen-tila-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä nolla tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-valokatteinen-tila-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Suora uloskäynti porrashuoneista
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0506>

{% include clause_start.html type="req" id="prof-ak/vaat-suora-uloskaynti-porrashuoneista-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [GeometriaArvo](../../looginenmalli/dokumentaatio/#geometriaarvo), joka on päällekkäin sen kaavakohteen geometrian osan kanssa, jonka kohdalla tulee olla suora uloskäunti porrashuoneista. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-suora-uloskaynti-porrashuoneista-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Ikkunaton seinä
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0507>

{% include clause_start.html type="req" id="prof-ak/vaat-ei-ikkunoita-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [GeometriaArvo](../../looginenmalli/dokumentaatio/#geometriaarvo), joka on päällekkäin sen kaavakohteen geometrian osan kanssa, jonka puoleisten rakennusten seiniin ei saa sijoittaa ikkunoita. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-ei-ikkunoita-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include note.html content="Koodistossa otsikolla 'Ei saa rakentaa ikkunoita', tulisiko muuttaa?" %}


#### Ääneneristävyys
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0508>

{% include clause_start.html type="req" id="prof-ak/vaat-aaneneristavyys-arvot" %}
```arvo```-attribuutin mahdolliset arvot ovat seuraavat:
* Yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo), joka kuvaa rakennuksen ulkoseinien sekä ikkunoiden ja muiden rakenteiden vähimmäisääneneristävyyden liikennemelua vastaan desibeleinä (```db```). Numeerisen arvon on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta.
* Nolla tai useampi [GeometriaArvo](../../looginenmalli/dokumentaatio/#geometriaarvo), joka on päällekkäin sen kaavakohteen geometrian osan kanssa, jonka puoleisia sivuja kaavamääräys koskee.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-aaneneristavyys-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Parvekkeet sijoitettava rungon sisään
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0509>

{% include clause_start.html type="req" id="prof-ak/vaat-parvekkeet-rungon-sisaan-maar" %}
Ilmaisee, että kaavakohteen aluella rakennusten parvekkeet tulee rakentaa talon rungon sisään.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-parvekkeet-rungon-sisaan-arvot" %}
```arvo```-attribuutin arvona saa esiintyä nolla tai useampi [GeometriaArvo](../../looginenmalli/dokumentaatio/#geometriaarvo), joka on päällekkäin sen kaavakohteen geometrian osan kanssa, jonka puoleisia sivuja kaavamääräys koskee. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-parvekkeet-rungon-sisaan-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Hissi
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0510>

{% include clause_start.html type="req" id="prof-ak/vaat-hissi-maar" %}
Ilmaisee, että kaavakohteen aluella rakennuksiin tai niiden tietyille sivuille on rakennettava hissit.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-hissi-arvot" %}
```arvo```-attribuutin arvona saa esiintyä nolla tai useampi [GeometriaArvo](../../looginenmalli/dokumentaatio/#geometriaarvo), joka on päällekkäin sen kaavakohteen geometrian osan kanssa, joka puoleisia sivuja kaavamääräys koskee. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-hissi-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Viherkatto
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0511>

{% include clause_start.html type="req" id="prof-ak/vaat-viherkatto-maar" %}
Ilmaisee, että kaavakohteen aluelle sijoitettavaan rakennukseen tai sen osaan on rakennettava viherkatto.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-viherkatto-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä nolla tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-viherkatto-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Kelluvat asuinrakennukset
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0512>

{% include clause_start.html type="req" id="prof-ak/vaat-kelluvat-rakennukset-maar" %}
Ilmaisee, että kaavakohteen aluelle sijoitettavat rakennukset voidaan toteuttaa veden päällä kelluvina.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-kelluvat-rakennukset-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä nolla tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-kelluvat-rakennukset-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include question.html content="Pitäisikö määräyslajia laventaa koskemaan mitä tahansa rakennuksia, ei vain asuinrakennuksia?" %}

#### Muu rakentamistapaan liittyvä määräys
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0513>

{% include clause_start.html type="req" id="prof-ak/vaat-muu-rakentamistapa-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka kuvaa kaavamääräyksen. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-muu-rakentamistapa-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

### Korkeusasema
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/06>

Ryhmittelyotsikko, vain [alakoodeja](../../looginenmalli/elinkaarisaannot.html#elinkaari-vaat-alakoodi-maar) käytetään.

#### Maanpinnan korkeusasema
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0601>

Kaava-aineistossa voidaan ilmaista maanpinnan nimelliskorkeus merenpinnasta tietyissä pisteissä kaavamääräyksenä, vaikka sen arvon tuleekin perustua kaavan lähtötietoaineiston topografiseen tietoon.

{% include clause_start.html type="req" id="prof-ak/vaat-maanpinnan-korkeusasema-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi [Korkeuspiste](../../looginenmalli/dokumentaatio/#korkeuspiste) tai yksi [Korkeusvali](../../looginenmalli/dokumentaatio/#korkeusvali), jotka kertovat maanpinnan korkeuden merenpinnasta sovitun pystysuuntaisen koordinaatiston arvona kaavakohteen sijainnissa. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-maanpinnan-korkeusasema-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include question.html content="Miksi maanpinnan korkeusasema on kaavamääräys? Ei voi olla ristiriidassa topografisen pohjakartta-aineiston korkeuskäyrien kanssa?" %}

#### Rakennuksen vesikaton ylimmän kohdan korkeusasema
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0602>

{% include clause_start.html type="req" id="prof-ak/vaat-vesikaton-korkeusasema-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi [Korkeuspiste](../../looginenmalli/dokumentaatio/#korkeuspiste) tai yksi [Korkeusvali](../../looginenmalli/dokumentaatio/#korkeusvali), jotka kertovat kaavakohteen alueelle sijoitettavien rakennusten vesikaton ylimmän kohdan korkeuden merenpinnasta sovitun pystysuuntaisen koordinaatiston arvona. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-vesikaton-korkeusasema-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}


#### Rakennuksen julkisivupinnan ja vesikaton leikkauskohdan korkeusasema
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0603>

{% include clause_start.html type="req" id="prof-ak/vaat-julkisivupinnan-ja-vesikaton-leikkauksen-korkeusasema-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi [Korkeuspiste](../../looginenmalli/dokumentaatio/#korkeuspiste) tai yksi [Korkeusvali](../../looginenmalli/dokumentaatio/#korkeusvali), jotka kertovat kaavakohteen alueelle sijoitettavien rakennusten julkisivupinnan ja vesikaton leikkauskohdan korkeuden merenpinnasta sovitun pystysuuntaisen koordinaatiston arvona. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-julkisivupinnan-ja-vesikaton-leikkauksen-korkeusasema-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Rakennuksen julkisivun korkeus
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0604>

{% include clause_start.html type="req" id="prof-ak/vaat-julkisivun-enimmaiskorkeus-arvot" %}
```arvo```-attribuutin arvona saa esiintyä yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), joka kertoo kaavakohteen alueelle sijoitettavien rakennusten julkisivujen minimikorkeuden, maksimikorkeuden tai molemmat. Numeerisen arvon on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta. Yksikkönä metri (```m```). Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-julkisivun-enimmaiskorkeus-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include note.html content="Koodin otsikko on 'Rakennuksen julkisivun enimmäiskorkeus metreinä' Tässä määräys on yleisempi" %}

#### Rakennusten, rakenteiden ja laitteiden ylin korkeusasema
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0605>

{% include clause_start.html type="req" id="prof-ak/vaat-rakennusten-rakent-lait-korkeusasema-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi [Korkeuspiste](../../looginenmalli/dokumentaatio/#korkeuspiste) tai yksi [Korkeusvali](../../looginenmalli/dokumentaatio/#korkeusvali), jotka kertovat kaavakohteen alueelle sijoitettavien rakennusten, rakenteiden ja laitteiden ylimmän korkeuden merenpinnasta sovitun pystysuuntaisen koordinaatiston arvona. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-rakennusten-rakent-lait-korkeusasema-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include note.html content="Koodin otsikossa 'Rakennuksen, rakenteiden ja laitteiden...', pitäisi olla kaikki monikossa?" %}

#### Maanalaisen kohteen korkeusasema
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0606>

{% include clause_start.html type="req" id="prof-ak/vaat-maanalaisen-kohteen-korkeusasema-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi [Korkeuspiste](../../looginenmalli/dokumentaatio/#korkeuspiste) tai yksi [Korkeusvali](../../looginenmalli/dokumentaatio/#korkeusvali), jotka kertovat maanalaisen kaavakohteen perustason korkeuden merenpinnasta sovitun pystysuuntaisen koordinaatiston arvona. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include question.html content="Mitä korkeutta tämä tarkalleen ottaen tarkoittaa? Mikä on oikea termi tälle 'perustasolle'?" %}

{% include clause_start.html type="req" id="prof-ak/vaat-maanalaisen-kohteen-korkeusasema-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Muu korkeusasemaan liittyvä määräys
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0607>

{% include clause_start.html type="req" id="prof-ak/vaat-muu-korkeusasema-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka kuvaa kaavamääräyksen. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-muu-korkeusasema-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

### Ulkoalueet
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/07>

Ryhmittelyotsikko, vain [alakoodeja](../../looginenmalli/elinkaarisaannot.html#elinkaari-vaat-alakoodi-maar) käytetään.

#### Vihertehokkuus
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0701>

{% include clause_start.html type="req" id="prof-ak/vaat-vihertehokuus-maar" %}
Ilmisee, että kaavakohteen suunnittelussa ja toteuttamisessa tulee käyttää [viherkerroinmenetelmää](https://ilmastotyokalut.fi/vihrea-infrastruktuuri/viherkerroinmenetelma/).
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-vihertehokuus-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä nolla tai yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo), joka kertoo kaavakohteen alueen tonttien viherkertoimen vähimmäisarvon. Numeerisen arvon on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta. Muun tyyppiset arvot eivät ole sallittuja.

Mikäli arvoa ei anneta, tulee noudattaa viherkerroinmenetelmässä määriteltyjä viherkertoimien ehdottomia minitasoja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-vihertehokuus-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include tip.html content="Viherkerroinmenetelmän viherkerroinluokien minimitasot on kuvattu dokumentin [Viherkerroinmenetelmän kehittäminen Helsingin kaupungille](https://www.ymk-projektit.fi/suunnitteluopas/files/2014/07/Viherkerroin_julkaisu_ymk_08141.pdf) luvussa 3.4.2 Luokkien tavoite- ja minitasot (Julkaisija: Helsingin kaupungin ympäristökeskus, Helsinki 2014)" %}

#### Puusto tai kasvillisuus säilytettävä tai korvattava
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0702>

{% include clause_start.html type="req" id="prof-ak/vaat-puusto-kasvillisuus-sail-tai-korv-maar" %}
Ilmaisee, että kaavakohteen aluella oleva puusto tai muu kasvillisuus on säilytettävä tai korvattava.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-puusto-kasvillisuus-sail-tai-korv-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä nolla tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-puusto-kasvillisuus-sail-tai-korv-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}


#### Olemassa oleva puusto säilytettävä
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0703>

{% include clause_start.html type="req" id="prof-ak/vaat-puusto-sailytettava-maar" %}
Ilmaisee, että kaavakohteen aluella oleva puusto on säilytettävä.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-puusto-sailytettava-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä nolla tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-puusto-sailytettava-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Maisema säilytettävä avoimena
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0704>

{% include clause_start.html type="req" id="prof-ak/vaat-maisema-sailytettava-avoimena-maar" %}
Ilmaisee, että kaavakohteen alueen maisema on säilytettävä avoimena.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-maisema-sailytettava-avoimena-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä nolla tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-maisema-sailytettava-avoimena-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Muu ulkoalueiden toteuttamiseen liittyvä määräys
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0705>

{% include clause_start.html type="req" id="prof-ak/vaat-muu-ulkoalue-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka kuvaa kaavamääräyksen. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-muu-ulkoalue-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

### Liikenne
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/08>

Ryhmittelyotsikko, vain [alakoodeja](../../looginenmalli/elinkaarisaannot.html#elinkaari-vaat-alakoodi-maar) käytetään.

{% include question.html content="Kevyen liikenteen/pyöräily/jalankulku väyliä ei ole kuvattu asemakaavan kaavamääräyksinä. Alueen käyttötarkoituksessa on kyllä jalankululle ja pyöräilylle varattu alue. Miten ilmaistaan yhdistetty jalankulku ja pyöräilyväylä?" %}


{% include question.html content="AK-kaavamääräyksissä ei ole raitiotie/pikaraitiotie/metroväyliä erikseen, vain yleinen rautatieliikenteen alue. Pitäiskö olla? Entä julkisen liikenteen pysäkit ja metron sisäänkäynti?" %}

#### Ajoneuvoliittymä
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0801>

{% include clause_start.html type="req" id="prof-ak/vaat-ajoneuvoliittyma-arvot" %}
```arvo```-attribuutin arvona saa esiintyä yksi tai useampi [GeometriaArvo](../../looginenmalli/dokumentaatio/#geometriaarvo), joka on päällekkäin sen kaavakohteen geometrian osan kanssa, joka kuvaa ajoneuvoliittymän sijaintia alueen rajalla. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-ajoneuvoliittyma-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Ajoneuvoliittymän kielto
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0802>

{% include clause_start.html type="req" id="prof-ak/vaat-ajoneuvoliittyma-kielto-arvot" %}
```arvo```-attribuutin arvona saa esiintyä yksi tai useampi [GeometriaArvo](../../looginenmalli/dokumentaatio/#geometriaarvo), joka on päällekkäin sen kaavakohteen geometrian osan kanssa, jonka kohdalle ei saa rakentaa ajoneuvoliittymää. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-ajoneuvoliittyma-kielto-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Autopaikkojen määrä
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0803>

Moottoajoneuvoille varattujen pysäköintipaikkojen lukumäärä voidaan ilmaista joko kaavakohteen alueelle toteutettavien paikkojen kokonaismääränä, lukumääränä per asunto tai lukumääränä per rakennusten kerrosneliömetri. Viimeksi mainitussa tapauksessa voidaan lukumäärä tarkentaa lisäksi koskemaan ainoastaan annettuun käyttötarkoitukseen toteutettavia kerrosneliömetrejä.

{% include clause_start.html type="req" id="prof-ak/vaat-autopaikkojen-maara-arvot" %}
```arvo```-attribuutin arvona saa esiintyä nolla yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali) joka kertoo vaaditun pysäköintipaikkojen minimimäärän, maksimimäärän tai molemmat sen kaavakohteen aluella, johon kaavamääräys on liitetty. Numeerisen arvovälin minimi- ja maksimiarvojen on toteutettava [Integer](../../looginenmalli/dokumentaatio/#integer)-rajapinta. Yksikköä ei käytetä. Muun tyyppiset arvot eivät ole sallittuja.

Mikäli arvoa ei anneta, tulee lukumäärä ilmaista ```lisätieto```-attribuutin avulla.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-autopaikkojen-maara-lisatiedot" %}
```lisatieto```-attribuutin arvoina saa esiintyä nolla tai useampi [Lisatieto](../../looginenmalli/dokumentaatio/#lisatieto), jonka laji on joko [Lukumäärä per kerrosneliömetri](http://uri.suomi.fi/codelist/rytj/RY_Lisatiedonlaji_AK/code/12), tai [Lukumäärä per asunto](http://uri.suomi.fi/codelist/rytj/RY_Lisatiedonlaji_AK/code/13).

Mikäli lisätiedon laji on [Lukumäärä per kerrosneliömetri](http://uri.suomi.fi/codelist/rytj/RY_Lisatiedonlaji_AK/code/12), tulee sillä olla vähintään yksi ja enintään kaksi arvoa:
*  Yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), joka kertoo pysäköintipaikkojen minimimäärän, maksimimäärän tai molemmat jokaista kaavakohteen alueella sijaitsevan rakennuksen kerrosneliömetriä kohden. Numeerisen arvovälin minimi- ja maksimiarvojen on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta. Yksikköä ei käytetä.
* Nolla tai yksi [KoodiArvo](../../looginenmalli/dokumentaatio/#koodiarvo), joka viittaa [KaavamääraysLaji](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01) koodien [Alueen käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01) tai [Alueen osan käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/02) johonkin alakoodiin.

Mikäli lisätiedon laji on [Lukumäärä per asunto](http://uri.suomi.fi/codelist/rytj/RY_Lisatiedonlaji_AK/code/13), tulee sillä olla täsmälleen yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), joka kertoo pysäköintipaikkojen minimimäärän, maksimimäärän tai molemmat jokaista kaavakohteen alueella sijaitsevan rakennuksen asuntoa kohden. Yksikköä ei käytetä.
{% include clause_end.html %}

{% include tip.html content="Mikäli halutaan antaa pysyköintipaikojen lukumäärät erikseen eri käyttötarkoituksiin, voidaan käyttää useampaa [Lukumäärä per kerrosneliömetri](http://uri.suomi.fi/codelist/rytj/RY_Lisatiedonlaji_AK/code/12)-lajin lisätietoa, joissa kussakin annetaan lukumäärä tiettyjä käyttötarkoituksia kohden." %}

#### Polkupyöräpysäköinnin määrä
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0804>

Polkupyöräpysäköintipaikkojen lukumäärä voidaan ilmaista joko kaavakohteen alueelle toteutettavien paikkojen kokonaismääränä, lukumääränä per asunto tai lukumääränä per rakennusten kerrosneliömetri. Viimeksi mainitussa tapauksessa voidaan lukumäärä tarkentaa lisäksi koskemaan ainoastaan annettuun käyttötarkoitukseen toteutettavia kerrosneliömetrejä.

{% include clause_start.html type="req" id="prof-ak/vaat-polkupyorapaikkojen-maara-arvot" %}
```arvo```-attribuutin arvona saa esiintyä nolla yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), joka kertoo vaaditun pysäköintipaikkojen  minimimäärän, maksimimäärän tai molemmat sen kaavakohteen aluella, johon kaavamääräys on liitetty. Numeerisen arvovälin minimi- ja maksimiarvojen on toteutettava [Integer](../../looginenmalli/dokumentaatio/#integer)-rajapinta. Yksikköä ei käytetä. Muun tyyppiset arvot eivät ole sallittuja.

Mikäli arvoa ei anneta, tulee lukumäärä ilmaista ```lisätieto```-attribuutin avulla.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-polkupyorapaikkojen-maara-lisatiedot" %}
```lisatieto```-attribuutin arvoina saa esiintyä nolla tai useampi [Lisatieto](../../looginenmalli/dokumentaatio/#lisatieto), jonka laji on joko [Lukumäärä per kerrosneliömetri](http://uri.suomi.fi/codelist/rytj/RY_Lisatiedonlaji_AK/code/12), tai [Lukumäärä per asunto](http://uri.suomi.fi/codelist/rytj/RY_Lisatiedonlaji_AK/code/13).

Mikäli lisätiedon laji on [Lukumäärä per kerrosneliömetri](http://uri.suomi.fi/codelist/rytj/RY_Lisatiedonlaji_AK/code/12), tulee sillä olla vähintään yksi ja enintään kaksi arvoa:
*  Yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), joka kertoo pysäköintipaikkojen minimimäärän, maksimimäärän tai molemmat jokaista kaavakohteen alueella sijaitsevan rakennuksen kerrosneliömetriä kohden. Numeerisen arvovälin minimi- ja maksimiarvojen on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta. Yksikköä ei käytetä.
* Nolla tai Yksi [KoodiArvo](../../looginenmalli/dokumentaatio/#koodiarvo), joka viittaa [KaavamääraysLaji](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01) koodien [Alueen käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01) tai [Alueen osan käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/02) johonkin alakoodiin.

Mikäli lisätiedon laji on [Lukumäärä per asunto](http://uri.suomi.fi/codelist/rytj/RY_Lisatiedonlaji_AK/code/13), tulee sillä olla täsmälleen yksi [NumeerinenArvovali](../../looginenmalli/dokumentaatio/#numeerinenarvovali), joka kertoo pysäköintipaikkojen minimimäärän, maksimimäärän tai molemmat jokaista kaavakohteen alueella sijaitsevan rakennuksen asuntoa kohden. Numeerisen arvovälin minimi- ja maksimiarvojen on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta. Yksikköä ei käytetä.

Muun tyyppiset lisätietojen arvot eivät ole sallittuja.

{% include clause_end.html %}

{% include tip.html content="Mikäli halutaan antaa pysyköintipaikojen lukumäärät erikseen eri käyttötarkoituksiin, voidaan käyttää useampaa [Lukumäärä per kerrosneliömetri](http://uri.suomi.fi/codelist/rytj/RY_Lisatiedonlaji_AK/code/12)-lajin lisätietoa, joissa kussakin annetaan lukumäärä tiettyjä käyttötarkoituksia kohden." %}

#### Muu liikenteeseen liityvä määräys
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0805>

{% include clause_start.html type="req" id="prof-ak/vaat-muu-liikenne-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka kuvaa kaavamääräyksen. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-muu-liikenne-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

### Ympäristöarvojen vaaliminen
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/09>

Ryhmittelyotsikko, vain [alakoodeja](../../looginenmalli/elinkaarisaannot.html#elinkaari-vaat-alakoodi-maar) käytetään.

#### Kulttuurihistoriallisesti arvokas alue tai kohde
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0901>

{% include clause_start.html type="req" id="prof-ak/vaat-kulttuurihist-merkittava-alue" %}
Kaikkien asemakaavojen tietoaineistojen sisältämien [Kaavamaarays](../../looginenmalli/dokumentaatio/#kaavamaarays)-luokan instanssien, joiden ```laji```-attribuutin arvo on jokin [Kultturihistoriallisesti arvokas alue tai kohde](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0901)-koodin alakoodi, osalta tulee noudattaa seuraavia rajoituksia:
* ```arvo```-attribuutin arvona saa esiintyä nolla tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa. Muun tyyppiset arvot eivät ole sallittuja.
* ```lisatieto```-attribuutin arvoina saa esiintyä nolla tai useampi [Lisatieto](../../looginenmalli/dokumentaatio/#lisatieto), joka ```laji``` on yksi seuraavista:   
   * [Kulttuurihistoriallinen merkittävyys](http://uri.suomi.fi/codelist/rytj/RY_LisatiedonLaji_AK/code/05), jonka arvoina on yksi tai useampi [KoodiArvo](../../looginenmalli/dokumentaatio/#koodiarvo), jotka viittaavat johonkin [Kulttuurihistoriallinen merkittävyys](http://uri.suomi.fi/codelist/rakrek/kulthistmer) koodiston koodeista,
   * [Kulttuurihistoriallinen arvotyyppi](http://uri.suomi.fi/codelist/rytj/RY_LisatiedonLaji_AK/code/06), jonka arvoina on yksi tai useampi [KoodiArvo](../../looginenmalli/dokumentaatio/#koodiarvo), jotka viittaavat johonkin [Kulttuurihistoriallinen arvotyyppi](http://uri.suomi.fi/codelist/rakrek/Kulthistatyyp) koodiston koodeista,
   * [Kulttuurihistoriallinen tyyppi](http://uri.suomi.fi/codelist/rytj/RY_LisatiedonLaji_AK/code/07), jonka arvoina on yksi tai useampi [KoodiArvo](../../looginenmalli/dokumentaatio/#koodiarvo), jotka viittaavat johonkin [Kulttuurihistoriallinen tyyppi](http://uri.suomi.fi/codelist/rakrek/kulthistyyp) koodiston koodeista, tai
   * [Kulttuurihistoriallisen merkittävyyden kriteerit](http://uri.suomi.fi/codelist/rytj/RY_LisatiedonLaji_AK/code/08), jonka arvoina on yksi tai useampi[KoodiArvo](../../looginenmalli/dokumentaatio/#koodiarvo), joka viittaa johonkin [Kulttuurihistoriallisen merkittävyyden kriteerit](http://uri.suomi.fi/codelist/rakrek/KultKritee) koodiston koodeista.
Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include question.html content="Kulttuurihistoriallisen merkittävyyden kriteerit on monikossa, kun muut koodien otsikot ovat yksikössä, pitäisikö myös se vaihtaa yksikköön? Samat nimet ovat käytössä viitatuissa rakrek-koodistoissa." %}

{% include question.html content="Tämä pääluokka toimii nyt kaatoluokkana, koska sitä ei ole rajattu vain ryhmittelyotsikoksi. Onko tämä tarkoitus?" %}

##### Suojeltava alue tai alueen osa
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/090101>

{% include clause_start.html type="req" id="prof-ak/vaat-suojeltava-alue" %}
Ilmaisee, että kaavakohde kuvaa suojeltavan alueen tai alueen osan.
{% include clause_end.html %}

##### Suojeltava rakennus
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/090102>

{% include clause_start.html type="req" id="prof-ak/vaat-suojeltava-rakennus-maar" %}
Ilmaisee, että kaavakohde kuvaa suojeltavan [rakennuksen](http://uri.suomi.fi/terminology/rakymp/c6).
{% include clause_end.html %}

##### Suojeltava rakennelma
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/090103>

{% include clause_start.html type="req" id="prof-ak/vaat-suojeltava-rakennelma-maar" %}
Ilmaisee, että kaavakohde kuvaa suojeltavan [rakennelman](http://uri.suomi.fi/terminology/mrl/concept-125).
{% include clause_end.html %}

##### Kiinteä suojeltava kohde
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/090104>

{% include clause_start.html type="req" id="prof-ak/vaat-kiintea-suojeltava-kohde-maar" %}
Ilmaisee, että kaavakohde kuvaa kiinteän suojeltavan kohteen.
{% include clause_end.html %}

##### Kiinteä muinaisjäännös
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/090105>

{% include clause_start.html type="req" id="prof-ak/vaat-kiintea-muinaisjaannos-maar" %}
Ilmaisee, että kaavakohde kuvaa kiinteän muinaisjäännöksen.
{% include clause_end.html %}

#### Luontoarvoiltaan arvokas alue tai kohde
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0902>

{% include clause_start.html type="req" id="prof-ak/vaat-kulttuurihist-merkittava-alue" %}
Kaikkien asemakaavojen tietoaineistojen sisältämien [Kaavamaarays](../../looginenmalli/dokumentaatio/#kaavamaarays)-luokan instanssien, joiden ```laji```-attribuutin arvo on jokin [Luontoarvoiltaan arvokas alue tai kohde](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0902)-koodin alakoodi, osalta tulee noudattaa seuraavia rajoituksia:
* ```arvo```-attribuutin arvona saa esiintyä nolla tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa. Muun tyyppiset arvot eivät ole sallittuja.
* ```lisatieto```-attribuutin arvoina saa esiintyä nolla tai useampi [Lisatieto](../../looginenmalli/dokumentaatio/#lisatieto), joka ```laji``` on yksi seuraavista:   
   * [Ympäristöarvon peruste](http://uri.suomi.fi/codelist/rytj/RY_LisatiedonLaji_AK/code/09), jolla on yksi arvona yksi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo), joka kuvaa ympäristöarvon perusteen sanallisesti, tai
   * [Ympäristö- tai luontoarvon merkittävyys](http://uri.suomi.fi/codelist/rytj/RY_LisatiedonLaji_AK/code/10), on yksi arvona yksi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo), joka kuvaa ympäristö- tai luontoarvon merkittävyyden sanallisesti.

Muun tyyppiset lisätietojen arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include note.html content="Mikäli ympäristöarvojen perusteet ja merkittävyydet kuvataan tulevaisuudessa omina koodistoinaan, tulee lisätietojen sallittuja arvoja muuttaa viittaamaan niihin" %}

{% include question.html content="Tämä pääluokka toimii nyt kaatoluokkana, koska sitä ei ole rajattu vain ryhmittelyotsikoksi. Onko tämä tarkoitus?" %}

##### Suojeltu puu
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/090201>

{% include clause_start.html type="req" id="prof-ak/vaat-suojeltu-puu-maar" %}
Ilmaisee, että kaavakohde kuvaa suojellun puun.
{% include clause_end.html %}

{% include question.html content="Onko koodi tarkoituksella nimenomaan suojeltu, eikä suojeltava?" %}

##### Säilytettävä puu
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/090202>

{% include clause_start.html type="req" id="prof-ak/vaat-sailytettava-puu-maar" %}
Ilmaisee, että kaavakohde kuvaa säilytettävän puun.
{% include clause_end.html %}

##### Suojeltava vesistö tai vesialue
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/090203>

{% include clause_start.html type="req" id="prof-ak/vaat-suojeltava-vesisto-maar" %}
Ilmaisee, että kaavakohde kuvaa suojeltavan vesistön tai vesialueen.
{% include clause_end.html %}

##### Luonnon monimuotoisuuden kannalta tärkeä alue
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/090204>

{% include clause_start.html type="req" id="prof-ak/vaat-luonnon-monimuotoisuus-maar" %}
Ilmaisee, että kaavakohde kuvaa luonnon monimuotoisuuden kannalta tärkeän alueen.
{% include clause_end.html %}

##### Ekologinen yhteys
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/090205>

{% include clause_start.html type="req" id="prof-ak/vaat-ekologinen-yhteys-maar" %}
Ilmaisee, että kaavakohde kuvaa ekologisen yhteyden.
{% include clause_end.html %}

#### Alue, jolla ympäristö säilytetään
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0903>

{% include clause_start.html type="req" id="prof-ak/vaat-sailytettava-ymparisto-maar" %}
Ilmaisee, että kaavakohde kuvaa alueen, jolla ympäristö säilytetään.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-sailytettava-ymparisto-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-sailytettava-ymparisto-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Alue, jolla on erityistä ulkoilun ohjaamistarvetta
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/0904>

{% include clause_start.html type="req" id="prof-ak/vaat-ulkoilun-ohjaamistarve-maar" %}
Ilmaisee, että kaavakohde kuvaa alueen, jolla on sen luontoarvojen vuoksi erityistä ulkoilun ohjaamistarvetta.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-ulkoilun-ohjaamistarve-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-ulkoilun-ohjaamistarve-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

### Tonttijako
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/10>

Ryhmittelyotsikko, vain [alakoodeja](../../looginenmalli/elinkaarisaannot.html#elinkaari-vaat-alakoodi-maar) käytetään.

#### Sivova tonttijako laadittava
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1001>

{% include clause_start.html type="req" id="prof-ak/vaat-sitova-tonttijako-maar" %}
Ilmaisee, että kaavakohde kuvaa alueen, jolle on laadittava erillinen sitova tonttijako.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-sitova-tonttijako-arvot" %}
```arvo```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-sitova-tonttijako-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Esitontti
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1001>

{% include clause_start.html type="req" id="prof-ak/vaat-esitontti-maar" %}
Ilmaisee, että kaavakohde kuvaa alueen, josta on tarkoitus muodostaa tontti.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-esitontti-arvot" %}
```arvo```-attribuutin arvona saa esiintyä nolla tai useampi [TunnusArvo](../../looginenmalli/dokumentaatio/#tunnusarvo), jotka kuvaavat tulevan tontin pysyviä tunnuksia tietojärjestelmissä tai rekistereissä.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-esitontti-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

### Yleismääräykset
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/11>

Ryhmittelyotsikko, vain [alakoodeja](../../looginenmalli/elinkaarisaannot.html#elinkaari-vaat-alakoodi-maar) käytetään.

#### Yleismääräys
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1101>

{% include clause_start.html type="req" id="prof-ak/vaat-yleismaarays-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka kuvaa kaavamääräyksen. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-yleismaarays-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}


#### Ajanmukaisuuden arvioinnin aikaraja
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1102>

{% include clause_start.html type="req" id="prof-ak/vaat-ajanmukaiden-arviointi-aikaraja-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä joko
* yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo), joka kuvaa sen kaavan hyväksymisestä alkavan ajanjakson pituuden, jonka kuluttua kaavan ajanmukaisuus on arvioitava. Numeerisen arvon  on toteutettava [Integer](../../looginenmalli/dokumentaatio/#integer)-rajapinta. Yksikkönä vuosi (```v```), tai kuukausi (```kk```) tai
* yksi [Ajanhetkiarvo](../../looginenmalli/dokumentaatio/#ajanhetkiarvo), joka kuvaa päivämäärän, johon mennessä kaavan ajanmukaisuus on arvioitava.
Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-ajanmukaiden-arviointi-aikaraja-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Aluetta koskevat sitovat rakentamistapaohjeet
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1103>

{% include clause_start.html type="req" id="prof-ak/vaat-sitovat-rakentamistapaohjeet-maar" %}
Ilmaisee, että kaavakohde kuvaa alueen, jota koskevat sitovat rakentamistapaohjeet.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-sitovat-rakentamistapaohjeet-arvot" %}
```arvo```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-sitovat-rakentamistapaohjeet-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include clause_start.html type="rec" id="prof-ak/suos-sitovat-rakentamistapaohjeet-liittyva-asiakirja" %}
Rakentamistapaohje on suositeltavaa linkittää kaavamääräykseen ```liittyvaAsiakirja```-assosiaation avulla.
{% include clause_end.html %}

#### Aluetta koskevat rakentamistapaohjeet
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1104>

{% include clause_start.html type="req" id="prof-ak/vaat-ei-sitovat-rakentamistapaohjeet-maar" %}
Ilmaisee, että kaavakohde kuvaa alueen, jota koskevat ei-sitovat rakentamistapaohjeet.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-ei-sitovat-rakentamistapaohjeet-arvot" %}
```arvo```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-ei-sitovat-rakentamistapaohjeet-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include clause_start.html type="rec" id="prof-ak/suos-ei-sitovat-rakentamistapaohjeet-liittyva-asiakirja" %}
Rakentamistapaohje on suositeltavaa linkittää kaavamääräykseen ```liittyvaAsiakirja```-assosiaation avulla.
{% include clause_end.html %}

### Yhdyskuntatekninen huolto
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/12>

Ryhmittelyotsikko, vain [alakoodeja](../../looginenmalli/elinkaarisaannot.html#elinkaari-vaat-alakoodi-maar) käytetään.

#### Alin painovoimainen viemäröintitaso
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1201>

{% include clause_start.html type="req" id="prof-ak/vaat-alin-painovoimainen-viemarointitaso-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi [Korkeuspiste](../../looginenmalli/dokumentaatio/#korkeuspiste), joka kertoo alimman painovoimaisen viemäröintitason korkeuden sovitun pystysuuntaisen koordinaatiston arvona. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-alin-painovoimainen-viemarointitaso-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Aurinkokennojen alin sijoittumistaso
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1202>

{% include clause_start.html type="req" id="prof-ak/vaat-alin-aurinkokennojen-sijoittumistaso-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi [Korkeuspiste](../../looginenmalli/dokumentaatio/#korkeuspiste), joka kertoo alimman aurinkokennojen sijoittumistason korkeuden sovitun pystysuuntaisen koordinaatiston arvona. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-alin-alin-aurinkokennojen-sijoittumistaso-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Vaatimus hulevesisuunnitelman laatimisesta
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1203>

{% include clause_start.html type="req" id="prof-ak/vaat-hulevesisuunnitelma-laadittava-maar" %}
Ilmaisee, että kaavakohde kuvaa alueen, jolle on laadittava hulevesisuunnitelma.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-hulevesisuunnitelma-laadittava-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä nolla tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-hulevesisuunnitelma-laadittava-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Liitettävä kaukolämpöverkkoon
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1204>

{% include clause_start.html type="req" id="prof-ak/vaat-liitettava-kaukolampoverkkoon-maar" %}
Ilmaisee, että kaavakohde kuvaa alueen, joka on liitettävä kaukolämpöverkkoon.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-liitettava-kaukolampoverkkoon-arvot" %}
```arvo```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-liitettava-kaukolampoverkkoon-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Hulevesien imeyttämisen periaate tai vaatimus
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1205>

{% include clause_start.html type="req" id="prof-ak/vaat-hulevesien-imeyttaminen-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka kuvaa hulevesien imeyttämisen periaatteen tai vaatimuksen. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-hulevesien-imeyttaminen-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Muu yhdyskuntatekniseen huoltoon liittyvä määräys
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1206>

{% include clause_start.html type="req" id="prof-ak/vaat-muu-yhdyskuntatekninen-huolto-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka kuvaa kaavamääräyksen. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-muu-yhdyskuntatekninen-huolto-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

### Ympäristön ja terveyden suojelu
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/13>

Ryhmittelyotsikko, vain [alakoodeja](../../looginenmalli/elinkaarisaannot.html#elinkaari-vaat-alakoodi-maar) käytetään.

#### Pilaantunut maa-alue
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1301>

{% include clause_start.html type="req" id="prof-ak/vaat-pilaantunut-maa-alue-maar" %}
Ilmaisee, että kaavakohde kuvaa alueen, jolla on ihmisen toiminnan seurauksena haitallisia aineita siinä määrin, että niistä aiheutuu haittaa tai merkittävä riski ympäristölle tai terveydelle, viihtyisyyden vähentymistä tai muuta niihin verrattavissa olevaa haittaa.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-pilaantunut-maa-alue-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä nolla tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka täydentää kaavamääräystietoa, esimerkiksi lisätietoa pilaantumisen laadusta. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-pilaantunut-maa-alue-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include clause_start.html type="rec" id="prof-ak/suos-pilaantunut-maa-alue-liittyva-asiakirja" %}
Mikäli pilaantumiseen liittyen on laadittu selvitys on suositeltavaa linkittää se kaavamääräykseen ```liittyvaAsiakirja```-assosiaation avulla.
{% include clause_end.html %}

{% include question.html content="Miksi pilaantunut maa-alue on kaavamääräys? Pitäisikö pilaantuneiden maa-alueiden olla osa lähtötietoaineistoja? SYKEn MATTI-järjestelmä?" %}

#### Meluaita
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1302>

{% include clause_start.html type="req" id="prof-ak/vaat-meluaita-maar" %}
Ilmaisee, että kaavakohde kuvaa alueen, jolle tulee rakentaa meluaita.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-meluaita-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä nolla tai yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo), joka kuvaa aidan vähimmäisääneneristävyyden liikennemelua vastaan desibeleinä (```db```). Numeerisen arvon on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-meluaita-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Meluvalli
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1303>

{% include clause_start.html type="req" id="prof-ak/vaat-meluvalli-maar" %}
Ilmaisee, että kaavakohde kuvaa alueen, jolle tulee rakentaa meluvalli.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-meluvalli-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä nolla tai yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo), joka kuvaa vallin vähimmäisääneneristävyyden liikennemelua vastaan desibeleinä (```db```). Numeerisen arvon on toteutettava [Real](../../looginenmalli/dokumentaatio/#real)-rajapinta. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-meluvalli-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Melualue
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1304>

{% include clause_start.html type="req" id="prof-ak/vaat-melualue-maar" %}
Ilmaisee, että kaavakohde kuvaa alueen, jolla esiintyy siinä määrin melua, että siitä voi aiheutua merkittävää haittaa.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-melualue-arvot" %}
```arvo```-attribuutin arvona saa esiintyä nolla tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), jolla kuvataan melun tyyppiä ja haitallisuutta. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-melualue-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include question.html content="Miksi melualue on kaavamääräys? Pitäisikö melualueiden olla osa lähtötietoaineistoja?" %}

#### Radonhaitta huomioitava
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1305>

{% include clause_start.html type="req" id="prof-ak/vaat-radonhaitta-maar" %}
Ilmaisee, että kaavakohde kuvaa alueen, jolla maaperästä saattaa erittyä radonkaasua siinä määrin, että siitä voi aiheutua terveyshaittaa. Radonhaitta on huomioitava rakennettaessa.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-radonhaitta-arvot" %}
```arvo```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-radonhaitta-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Muu ympäristönsuojeluun liittyvä määräys
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1306>

{% include clause_start.html type="req" id="prof-ak/vaat-muu-ymparistonsuojelu-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), joka kuvaa kaavamääräyksen. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-muu-ymparistonsuojelu-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

### Nimistö
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/14>

Ryhmittelyotsikko, vain [alakoodeja](../../looginenmalli/elinkaarisaannot.html#elinkaari-vaat-alakoodi-maar) käytetään.

#### Kadun tai tien nimi
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1401>

{% include clause_start.html type="req" id="prof-ak/vaat-kadun-tien-nimi-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), jolla annetaan kaavakohteen kuvaaman kadun tai tien nimi. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-kadun-tien-nimi-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Torin tai aukion nimi
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1402>

{% include clause_start.html type="req" id="prof-ak/vaat-torin-aukion-nimi-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), jolla annetaan kaavakohteen kuvaaman torin tai aukion nimi. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-torin-aukion-nimi-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Puiston tai muun yleisen alueen nimi
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1403>

{% include clause_start.html type="req" id="prof-ak/vaat-yleisen-alueen-nimi-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), jolla annetaan kaavakohteen kuvaaman torin tai aukion nimi. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-yleisen-alueen-nimi-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}


#### Kaupungin- tai kunnanosan nimi
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1404>

{% include clause_start.html type="req" id="prof-ak/vaat-kaupungin-kunnan-osan-nimi-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), jolla annetaan kaavakohteen kuvaaman kaupungin- tai kunnanosan nimi. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-kaupungin-kunnan-osan-nimi-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Korttelinumero
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1405>

{% include clause_start.html type="req" id="prof-ak/vaat-korttelinumero-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi [NumeerinenArvo](../../looginenmalli/dokumentaatio/#numeerinenarvo), jolla annetaan kaavakohteen kuvaaman korttelin korttelinumero. Numeerisen arvon on toteutettava [Integer](../../looginenmalli/dokumentaatio/#integer)-rajapinta. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-korttelinumero-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

#### Muu nimistö
**Koodi**: <http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/1406>

{% include clause_start.html type="req" id="prof-ak/vaat-muu-nimi-arvot" %}
```arvo```-attribuutin arvoina saa esiintyä yksi tai useampi [TekstiArvo](../../looginenmalli/dokumentaatio/#tekstiarvo) (yksi kullakin kielellä), jolla annetaan kaavakohteen kuvaaman kohteen nimi. Muun tyyppiset arvot eivät ole sallittuja.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-muu-nimi-lisatiedot" %}
```lisatieto```-attribuutilla ei saa olla arvoja.
{% include clause_end.html %}

## Laatusäännöt
Nämä laatusäännöt laajentavat Kaavatietomallin [yleisiä laatusääntöjä](../../looginenmalli/laatusaannot.html).

### Käyttötarkoitusalueet

{% include clause_start.html type="req" id="prof-ak/vaat-kayttotarkoitusalue-maar" %}
Asemakaavan käyttötarkoitusalue on [Kaavakohde](dokumentaatio/#kaavakohde)-luokan objekti, joka liittyy assosiaatiolla ```maarays``` yhteen tai useampaan sellaiseen [Kaavamaarays](dokumentaatio/#kaavamaarays)-luokan objektiin, jonka ```laji```-attribuutin arvo on jokin [Alueen käyttötarkoitus](http://uri.suomi.fi/codelist/rytj/RY_KaavamaaraysLaji_AK/code/01)-koodin alakoodeista.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-aluemainen-kayttotarkoitusalue" %}
Asemakaavan käyttötarkoitusalueiden ```geometria```-attribuutin kuvaamaan geometrian tulee olla aluemainen.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-ei-leikkaavat-kayttotarkoitusalueet" %}
Asemakaavan käyttötarkoitusalueet eivät saa leikata toisiaan.
{% include clause_end.html %}

{% include clause_start.html type="req" id="prof-ak/vaat-asemakaavan-kayttotarkoituspeite" %}
Asemakaavan, jonka ```elinkaaritila```-attribuutin arvo on kaavaehdotus tai myöhempi (Kaavaehdotus, Tarkistettu kaavaehdotus, Hyväksytty kaava, Oikaisukehotuksen alainen, Valituksen alainen, Osittain voimassa, Voimassa, Kumottu tai Kumoutunut), sisältämien käyttötarkoitusalueiden tulee peittää sen ```aluerajaus```-attribuutin ilmaisema kaavan alue siten, että kukin alueen sisäpiste sisältyy täsmälleen yhteen käyttötarkoitusalueeseen.
{% include clause_end.html %}

{% include question.html content="Alueen käyttötarkoituksen antaminen yhtenä kaavamääräyslajina tekee laatusäännöistä monimutkaisia, kun käyttötarkoitusalueita ei voida erotella tietyn yhden kaavamääräyslajin, vaan sen alakoodien avulla. Pitäisikö sittenkin antaa alueen käyttötarkoitus omana kaavamääräyslajinaan tai jopa palata ajatukseen kaavakohdelajin käyttämisestä käyttötarkoitusalueiden ilmoittamiseen?" %}

### Korkeusasemat

{% include clause_start.html type="req" id="prof-ak/vaat-maanpinnan-korkeusasema-konsistenssi" %}
[Maanpinnan korkeusasema](#maanpinnan-korkeusasema) -kaavamääräyksen arvon on vastattava kaavan [Pohjakartta](http://uri.suomi.fi/codelist/rytj/RY_LahtotietoaineistonLaji/code/11)-lajin [Lahtotietoaineiston](../../looginenmallin/dokumentaatio/#lahtotietoaineisto) topografisen aineiston maanpinnan korkeutta kaavakohteen sijannissa kuvaavaa arvoa.
{% include clause_end.html %}

