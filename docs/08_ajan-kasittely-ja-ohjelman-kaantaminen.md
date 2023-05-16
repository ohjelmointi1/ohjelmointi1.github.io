---
title: Ajan käsittely ja ohjelman kääntäminen
layout: default
nav_order: 8
---

# Ajan käsittely ja ohjelman kääntäminen
{: .no_toc }

Tällä oppitunnilla perehdymme Javan tapohin käsitellä aikaa. Aikaa käsitellään **olioiden** ja **luokkien** avulla, mikä toimii erinomaisena pohjustuksena seuraavalla viikolla käsiteltävään **olio-ohjelmointiaiheeseen**, jossa luomme itse vastaavia luokkia ja niiden olioita.
{: .fs-5 }

Ajan käsittelyn lisäksi tutustumme siihen, miten Java-ohjelmia voidaan suorittaa Eclipsen ulkopuolella. Tähänastinen IDE-ympäristöön sidoksissa oleva suorittaminen soveltuu ainoastaan ohjelmistokehityksen yhteyteen, mutta ohjelmat on myös pakattavissa siten, että ne voidaan suorittaa miltä vain komentoriviltä.
{: .fs-5 }

---

## Sisällysluettelo
{: .no_toc .text-delta }

* Sisällysluettelo
{:toc}


# [Video: Javan aikaluokat ja niiden käyttäminen](https://web.microsoftstream.com/video/848a270b-1d74-4493-8d13-17db6b3a656a) *15:05*

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/848a270b-1d74-4493-8d13-17db6b3a656a?autoplay=false&amp;showinfo=true" allowfullscreen style="border:none;"></iframe>



# java.time.*

Nykyaikainen Javan standardikirjasto (Java 8+) käsittelee aikaa johdonmukaisesti ja selkeästi. Aikaisemmissa versioissa ajan käsittely on ollut ajoittain sekavaa ja virhealtista.


{: .warning }
> Javan vanhentuneilla luokilla kuukausien indeksit alkavat toisinaan nollasta. Seuraavassa esimerkissä vanha `Date`-luokka käsittelee kuukaudet numeroilla 0-11, joten kuukausi 12 vuotaa seuraavan vuoden puolelle:
>
> ```java
> // 💥 2022, 12, 24 tarkoittaa 24. TAMMIKUUTA 2023 💥
> Date eiOikeastiJoulu = new Date(2022, 12, 24);
> ```

Nykyisillä `java.time`-paketin aikaluokilla kuukausien indeksit alkavat yhdestä ja luokkien käyttäminen on monin tavoin johdonmukaisempaa:

```java
// nykyinen tapa (oikein):
LocalDate joulu = LocalDate.of(2022, 12, 24);
```

Merkittävä osa nettilähteistä esittelee vanhentuneita tai "epävirallisia" tapoja ajan käsittelyyn, joten suosittelen käyttämään lähteitä, joissa hyödynnetään `java.time`-paketista löytyviä aikaluokkia.


# java.time-paketin aikaluokkia

`java.time.LocalDate`

"A date without a time-zone in the ISO-8601 calendar system, such as 2007-12-03."

`java.time.LocalTime`

"A time without a time-zone in the ISO-8601 calendar system, such as 10:15:30."

`java.time.LocalDateTime`

"A date-time without a time-zone in the ISO-8601 calendar system, such as 2007-12-03T10:15:30."

`java.time.ZonedDateTime`

"A date-time with a time-zone in the ISO-8601 calendar system, such as 2007-12-03T10:15:30+01:00 Europe/Paris."

Lähde: [https://docs.oracle.com/javase/8/docs/api/java/time/](https://docs.oracle.com/javase/8/docs/api/java/time/)

Aikaluokkia käytettäessä niiden import-komennot lisätään luokan alkuun:

```java
import java.time.LocalDate;
import java.time.LocalDateTime;
```

## Nykyinen päivä ja kellonaika

```java
LocalDate nykyinenPaivamaara = LocalDate.now();

LocalDateTime nykyinenPaivaJaKellonaika = LocalDateTime.now();
```

## Arvojen hakeminen aikaolioilta

`LocalDate` ja `LocalDateTime` ovat **olioita**, jotka pitävät sisällään runsaasti dataa ja logiikkaa. Näiltä olioilta voidaan pyytää erillisiä arvoja **metodikutsujen avulla**:

```java
// 'nyt' on LocalDateTime-tyyppinen olio:
LocalDateTime nyt = LocalDateTime.now();

// päivämäärään liittyvien osien pyytäminen
System.out.println(nyt.getYear());
System.out.println(nyt.getMonthValue());
System.out.println(nyt.getDayOfMonth());

// kellonaikaan liittyvien osien pyytäminen
System.out.println(nyt.getHour());
System.out.println(nyt.getMinute());
System.out.println(nyt.getSecond());
```

Yllä hyödynnetyt metodit palauttavat aivan tavallisia kokonaislukuja, jotka voidaan myös sijoittaa muuttujiin esim. seuraavasti:

```java
// 'nyt' on LocalDateTime-tyyppinen olio:
LocalDateTime nyt = LocalDateTime.now();

int vuosi = nyt.getYear();

int kuukausi = nyt.getMonthValue();

int paiva = nyt.getDayOfMonth();
```

## Tietyn päivämäärän luominen

`LocalDateTime.now()` loi meille yllä nykyhetkeä vastaavan aikaolion. Metodeilla `of` voimme luoda tietyn ajanhetken käyttäen kokonaislukuja, tai `parse`-metodilla voimme lukea merkkijonomuotoisen päivämäärän päivämääräolioksi:

```java
LocalDate paivaKokonaisluvuista = LocalDate.of(2022, 12, 24);

LocalDate paivaMerkkijonosta = LocalDate.parse("2022-12-24");
```

Vastaavat `of`- ja `parse`-metodit löytyvät lukuisille muillekin aikaluokalle.



## Kokonaisluvut vs. oliot

Aikaa voidaan käsitellä sekä kokonaislukuina että olioina. Olioita käytettäessä saamme käyttöömme myös niihin liittyviä operaatioita, kuten vaikka tiedon siitä, onko kyseinen vuosi karkausvuosi:

```java
// Nykyinen vuosi Year-oliona:
Year thisYear = Year.now();

// Karkausvuoden selvittäminen olion metodia kutsumalla:
boolean isLeapYear = thisYear.isLeap();

// Nykyinen vuosi kokonaislukuna:
int yearNumber = thisYear.getValue();

// Vuosi 2030 oliona:
Year anotherYear = Year.of(2030);
```

# Ajan "laskeminen" ja vertailu

Aikaolioiden avulla voimme laskea uusia ajankohtia `minus` ja `plus` -metodeilla. `LocalDate`-olioilla on esimerkiksi metodit päivien, kuukausien ja vuosien lisäämiseksi ja vähentämiseksi, jotka palauttavat aina uusia aikaolioita:

```java
LocalDate nextWeek = LocalDate.now().plusDays(7);
LocalDate yesterday = LocalDate.now().minusDays(1);
```

Luokat sisältävät myös useita erilaisia metodeja eri ajankohtien vertailemiseksi:

```java
if (yesterday.isBefore(nextWeek)) {
    // suoritetaan jos tosi
}

if (yesterday.isAfter(nextWeek)) {
    // suoritetaan jos tosi
}

if (oneDay.equals(otherDay)) {
    // suoritetaan jos tosi
}
```

## Ajanjaksot, Period-luokka

Ajanjaksoja varten on olemassa esimerkiksi luokat `Period` ja `Duration`. Näiden avulla voidaan esimerkiksi selvittää, kuinka pitä jakso kahden eri ajanhetken välillä on:

```java
import java.time.Period; // luokan alkuun
```

```java
// ajankohta 1:
LocalDate independence = LocalDate.of(1917, 12, 6);

// ajankohta 2:
LocalDate today = LocalDate.now();

// ajankohtien välin laskeminen:
Period period = Period.between(independence, today);

int years = period.getYears();
int months = period.getMonths();
int days = period.getDays();

System.out.println(years + " v, " + months + " kk, " + days + " pv");
```

## ChronoUnit

`ChronoUnit` sisältää Javan aikayksiköt, joilla on myös hyödyllisiä metodeja. Esimerkiksi `ChronoUnit.DAYS` auttaa laskemaan montako päivää kahden ajanhetken välillä on, kun taas `ChronoUnit.MINUTES` auttaa laskemaan saman minuutteina:

```java
LocalDate joulu = LocalDate.of(2022, 24, 12);
LocalDate tanaan = LocalDate.now();

long paiviaJouluun = ChronoUnit.DAYS.between(joulu, tanaan);
```

# [Video: aikaan liittyvä ohjelmalogiikka, myöhästymismaksut ja juhlapyhät](https://web.microsoftstream.com/video/b6e65db2-c071-4db4-aee9-62d7f6e34066) *55:19*

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/b6e65db2-c071-4db4-aee9-62d7f6e34066?autoplay=false&amp;showinfo=true" allowfullscreen style="border:none;"></iframe>

Videolla esiintyvät lähdekoodit:

* [Myohastymismaksu.java](https://github.com/ohjelmointi1/ohjelmointi1-3015/blob/main/src/viikko04/aika/Myohastymismaksu.java)
* [Juhlapyhat.java](https://github.com/ohjelmointi1/ohjelmointi1-3015/blob/main/src/viikko04/aika/Juhlapyhat.java)
* [Tauko.java](https://github.com/ohjelmointi1/ohjelmointi1-3015/blob/main/src/viikko04/aika/Tauko.java)


# Ajan merkkijonoesitykset

Ajan merkkijonoesitykset noudattavat Javassa [ISO 8601 -standardia](https://en.wikipedia.org/wiki/ISO_8601). Eri aikaluokkien `parse`-metodit odottavat saavansa ajanhetken merkkijonona esim. seuraavissa muodoissa:

```
2022-01-20T18:01:08+00:00
2022-01-20T18:01:08Z
2022-01-20
```

Standardin päivämäärän ja kellonajan kirjoitusasun lisäksi on olemassa lukuisia paikallisia tapoja ilmoittaa päiviä ja aikoja, mikä tekee ajan käsittelystä toisinaan hankalaa:

[![ISO 8601](https://imgs.xkcd.com/comics/iso_8601.png)](https://xkcd.com/1179/)

[XKCD, ISO 8601](https://xkcd.com/1179/). Creative Commons Attribution-NonCommercial 2.5


## Ajan merkkijonomuunnokset

Aikaa on usein tarve esittää merkkijonoina käyttäjille. Oletuksena Javan aikaluokat hyödyntävät ISO-standardin mukaisia esityksiä, jotka ovat helposti koneluettavissa, mutta eivät aivan vastaa arjessa usein käytettyjä esitysmuotoja.

Ajankohtia voidaan muotoilla hieman kuten desimaalilukuja, `DateTimeFormatter`-luokan avulla (vrt. DecimalFormat-luokka):

```java
import java.time.format.DateTimeFormatter; // luokan alkuun
```

`DateTimeFormatter`-oliolle annetaan käytettävä muoto merkkijonona, jonka jälkeen se muotoilee aikaoliota annettuun muotoon `format`-metodilla:

```java
// "d.M.yyyy" on suomalaisille tuttu esitystapa:
DateTimeFormatter formaatti = DateTimeFormatter.ofPattern("d.M.yyyy");

LocalDate tanaan = LocalDate.now();

// Päivämäärän muuttaminen merkkijonoksi edellä määrätyssä muodossa:
String pvm = tanaan.format(formaatti);
```

`DateTimeFormatter`-luokkaa voidaan käyttää myös määrittelemään luettavan merkkijonon sisältämä muoto, jos parse-metodille joudutaan antamaan muussa kuin ISO-formaatissa olevia ajanhetkiä:

```java
DateTimeFormatter formaatti = DateTimeFormatter.ofPattern("d.M.yyyy");

// Kotimaisen päivämäärän parsiminen LocalDate-olioksi:
LocalDate pvm = LocalDate.parse("6.12.1917", formaatti);
```

## Ajan muotoilumääreitä

`DateTimeFormatter` tukee seuraavia merkkejä ajankohtien formaateissa:

Merkit      | Selitys   | Esimerkki
------------|-----------|------------
yyyy        | Vuosi     | 2000
M           | Kuukausi  | 9
MM          | Kuukausi* | 09
d           | Päivä     | 1
H           | Tunti     | 9
m           | Minuutti  | 5
s           | Sekunti   | 45

\* Samaa merkkiä voidaan toistaa, jolloin esim. päivä (dd), kuukausi (MM), tunti (HH) ja minuutti (mm) saadaan aina kahden numeron pituisena. Tarvittaessa luvun edessä esitetään tällöin nolla.



# Java-ohjelman kääntäminen ja suorittaminen komentoriviltä

Tämän viikon viimeisenä aiheena perehdymme siihen, miten Java-ohjelmia voidaan suorittaa Eclipsen ulkopuolella. Tähänastinen IDE-ympäristöön sidoksissa oleva suorittaminen soveltuu ainoastaan ohjelmistokehityksen yhteyteen, mutta ohjelmat on myös pakattavissa siten, että ne voidaan suorittaa miltä vain komentoriviltä.

Jos toteuttaisimme ohjelmallemme graafisen käyttöliittymän, sen suorittaminen olisi entistä suoraviivaisempaa. Toistaiseksi kuitenkin työskentelemme tekstikäyttöliittymän asettamissa rajoissa.

## [Video: ohjelman kääntäminen, paketointi ja suorittaminen](https://web.microsoftstream.com/video/8648dc7e-4195-4bea-b872-86dcd22c76af) *19:55*

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/8648dc7e-4195-4bea-b872-86dcd22c76af?autoplay=false&amp;showinfo=true" allowfullscreen style="border:none;"></iframe>

Videolla esiintyvät lähdekoodit:

* [Tauko.java](https://github.com/ohjelmointi1/ohjelmointi1-3015/blob/main/src/viikko04/aika/Tauko.java)



## Lähdekoodin kääntäminen tavukoodiksi

Ennen kun Java-koodia voidaan suorittaa, se täytyy kääntää. Kääntäminen tapahtuu Eclipsessä automaattisesti taustalla, mutta Eclipsen ulkopuolella kääntämisen voi tehdä itse `javac`-komennolla. Kääntämiseen liittyy monia hyviä puolia, joista yksi hyvin konkreettinen on ohjelman tarkistaminen virheiden varalta jo ennen sen suorittamista:

> *"Ohjelman suorittaminen on helppoa, mutta pinnan alla tapahtuu paljon. Kun ohjelma halutaan suorittaa, lähdekoodi käännetään ensin Java-ohjelmointikielen tavukoodiksi. Tämä kääntäminen tapahtuu Javan omalla kääntäjällä, joka on myös ohjelma. Tämän jälkeen ohjelma käynnistetään, eli siinä olevat käskyt suoritetaan yksi kerrallaan Java-kielistä tavukoodia ymmärtävän Java-tulkin toimesta."*
>
> *"Tämä käännösprosessi vaikuttaa siihen, miten ja milloin ohjelmien virheet ilmenevät. Kun ohjelma käännetään ennen suoritusta, kääntämiseen käytettävä ohjelma voi etsiä ohjelmasta virheitä. Tämä vaikuttaa myös ohjelmoinnissa käytetyn ohjelmointiympäristön tarjoamiin vinkkeihin, jolloin ohjelmoija voi saada palautetta ohjelmassa olevista virheistä heti."*
>
> *"Käytössämme oleva ohjelmointiympäristö kääntää ja suorittaa ohjelman yhdellä napinpainalluksella. Ohjelmointiympäristö kääntää ohjelmaa kuitenkin jatkuvasti, jolloin se pystyy ilmoittamaan virheistä."*
>
> [Agile Education Research, 2020](https://www.helsinki.fi/en/researchgroups/data-driven-education). [Tulostaminen](https://ohjelmointi-20.mooc.fi/osa-1/2-tulostaminen). [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.fi)

Käytännössä kääntäminen tapahtuu esimerkiksi PowerShell-komentorivillä `javac`-komennolla:

```
> javac viikko02\merkkijonot\Salasana.java
```

Komentoa suoritettaessa sinun tulee olla projektin lähdekoodien juurihakemistossa, eli esim. `workspace\ohjelmointi1\src\`. `javac`-komennolle annetaan parametrina käännettävän lähdekooditiedoston polku. Polun voi antaa Windows-ympäristössä joko kenoviivoilla `\` tai kauttaviivoilla `/` eroteltuna.

Kääntämisen jälkeen tiedostojärjestelmään ilmestyy `.java`-tiedoston rinnalle käännetty `.class`-tiedosto. Tätä tiedostoa voidaan käyttää `java`-komennon kanssa ohjelman suorittamiseksi.

## Käännetyn ohjelman suorittaminen

Käännetyn ohjelmaluokan suorittaminen tapahtuu `java`-komennolla:

```
> java viikko02.merkkijonot.Salasana

Satunnainen salasana: \)W.#OF#8EotJq3w[l5PjV%T4URs%;KS9a.fWJu#SeFe"gZ!EqAig(i
```

Vaikka komento näyttää hyvin samanlaiselta kuin aikaisempi `javac`-komento, sille ei anneta tiedoston polkua, vaan Java-luokan nimi paketteineen. Koska kyseessä on luokan nimi, sen perään ei kirjoiteta tiedostopäätettä.


## Ohjelman paketoiminen ja paketoidun ohjelman suorittaminen

Yksittäisten käännettyjen tiedostojen kääntäminen ja käsitteleminen erillisten hakemistojen avulla useista luokista koostuvien ohjelmien yhteydessä on epäkäytännöllistä. Tämän vuoksi [ohjelmia voidaan myös paketoida](https://happycoding.io/tutorials/java/exporting-jars#eclipse) **jar**-tiedostoiksi (Java Archive). Eclipsen export-toiminnon avulla voit pakata projektisi **jar**-paketiksi, joka sisältää kaikki ohjelmasi tarvitsemat luokat.

Kun ohjelma on paketoitu, se voidaan suorittaa `java`-komennolla ja `jar`-vivulla seuraavasti:

```
> java -jar salasanageneraattori.jar

Satunnainen salasana: \)W.#OF#8EotJq3w[l5PjV%T4URs%;KS9a.fWJu#SeFe"gZ!EqAig(i
```

## Windows-komentorivien merkistöongelmat

Mikäli käytät Windowsin komentoriviä tai PowerShell:iä, voit törmätä ongelmiin ääkkösten ja erikoismerkkien kanssa. Tämä johtuu siitä, että Windowsin komentorivi (cmd.exe) käyttää oletuksena paikallisia merkistöjä, eikä universaalia UTF-8:aa. Voit vaihtaa komentorivin tai PowerShellin käyttämän merkistön UTF-8:ksi seuraavalla komennolla:

```
> chcp 65001
```

Vaihdettuasi merkistön kokeile suorittaa komentoja uudelleen. Lue tarvittaessa lisävinkkejä [StackOverflow](https://superuser.com/questions/269818/change-default-code-page-of-windows-console-to-utf-8):sta.


# Tehtäväideoita oppitunnille

## Joululaskuri

Kirjoitetaan ohjelma, joka laskee kuinka monta yötä on jouluun. Ohjelma voi tarkistaa myös tapauksen, jossa joulu on jo mennyt, jolloin lasketaan päivät seuraavan vuoden jouluun.

## Pyhäpäivälaskuri

Kirjoitetaan ohjelma, joka selvittää juhannuksen sekä muut ajankohdaltaan vaihtelevat juhlapyhät tiettynä vuonna. Toteutetaan ohjelma siten, että muodostettu aineisto voidaan tuoda Google Calendar -sovellukseen import-toiminnolla.

* [Suomen juhlapäivät (Wikipedia)](https://fi.wikipedia.org/wiki/Suomen_juhlap%C3%A4iv%C3%A4t)
* [Pääsiäisen laskeminen (Wikipedia)](https://fi.wikipedia.org/wiki/P%C3%A4%C3%A4si%C3%A4isen_laskeminen)

## Ikälaskuri

Kirjoita ohjelma, joka pyytää käyttäjältä päivämäärän muodossa `pp.kk.vvvv`, ja kertoo kuinka pitkä aika kuluvan päivän ja annetun päivän välillä on.

Tarvitset todennäköisesti nämä luokat:

* Scanner
* LocalDate
* DateTimeFormatter (d.M.yyyy)
* Period tai ChronoUnit.DAYS

-


