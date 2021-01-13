# Ohjelmoinnin aloitus

Tällä oppitunnilla tutustumme Java-lähdekooditiedostojen rakenteeseen sekä koodin kirjoittamiseen ja suorittamiseen Eclipse-sovelluskehittimessä. Käsittelemme numeerisia sekä tekstimuotoisia tietotyyppejä ja teemme yksinkertaista vuorovaikutusta käyttäjän kanssa tulosteiden ja syötteiden avulla. Lopuksi tunnilla opittuja asioita harjoitellaan Viope-järjestelmässä olevien tehtävien avulla.

<div class="js-toc"></div>

# Java-luokan rakenne

Java-ohjelmat koostuvat aina luokista (class). Tyypillisesti kukin luokka tallennetaan samannimiseen .java-päätteiseen tiedostoon. Tiedoston sisällä ohjelmakoodi alkaa ja päättyy luokan määrittelyyn:

```java
// Tiedosto HelloWorld.java
public class HelloWorld {

}
```

Ohjelman varsinaiset käskyt kirjoitetaan niin sanottuihin metodeihin, jotka ovat hyvin samankaltaisia kuin monissa kielissä käytettävät funktiot. Metodit koostuvat käskyistä, jotka kirjoitetaan omille riveilleen ja rivit päätetään puolipisteellä.
  

```java
// Tiedosto HelloWorld.java
public class HelloWorld {

    // Kaikki metodit kirjoitetaan luokkien sisään
    public static void main(String[] args) {

        // Tekstiä voidaan tulostaa System.out.println-komennolla:
        System.out.println("Hello world!");

    }
}
```


Javassa `main`-metodilla on erityinen rooli: ohjelman suoritus alkaa main-metodista. Tätä koodia suoritettaessa ohjelma käynnistyy siis main-metodista ja ruudulle tulostuu teksti `Hello world!`.

Tulostettava teksti on kirjoitettu koodissa lainausmerkkeihin, koska se ei ole suoritettavaa koodia, vaan tekstidataa. Tekstimuotoista dataa kutsutaan ohjelmoinnin yhteydessä merkkijonoiksi (string).


# Java-kielisen ohjelman suorittaminen

Java on käännettävä ohjelmointikieli. Kytännössä se tarkoittaa sitä, että ohjelmoija kirjoittaa lähdekoodin "ihmisen ymmärrettävään muotoon", eli Java-kielisinä komentoina ja rakenteina. 

Tämän jälkeen Java-koodi käännetään tavukoodiksi, joka on eräänlainen välimuoto ihmisen ja tietokoneen ymmärtämien kielten välillä. Lopulta käännetty tavukoodi voidaan suorittaa Javan virtuaalikoneella, joka tulkkaa käskyt kunkin käyttöjärjestelmän mukaisiksi konekielisiksi komennoiksi. 

## Kääntämisen edut

Koska koodi käännetään ennen suoritusta, tarkistaa kääntäjä koodin syntaksisen oikeellisuuden jo ennen koodin suorittamista. Näin esimerkiksi huolimattomuusvirheet, kuten puuttuvat merkit ja kirjoitusvirheet, havaitaan hyvin nopeasti.

Koska Java-koodi käännetään tavukoodiksi eikä suoraan tietyn järjestelmän mukaisiksi käskyiksi, voidaan samaa käännettyä Java-ohjelmaa suorittaa hyvin erilaisilla järjestelmillä. Kunkin järjestelmän Java-virtuaalikone pystyy tulkitsemaan saman käännetyn ohjelman käskyt omiksi komennoikseen.

# Eclipse-sovelluskehitin

Eclipse automatisoi lähdekoodin kääntämisen ja tekee ohjelman suorituksesta helppoa. Et tule edes huomaamaan että ohjelmointiin liittyy kyseinen välivaihe. Eclipse kuitenkin kääntää Java-koodisi automaattisesti aina kun tallennat tiedoston. Eclipsen käyttöliittymään ilmestyvät punaiset ja keltaiset virheet ja varoitukset ovat Java-kääntäjän havaitsemia ongelmia.

## Tehtävä: Eclipsen käyttö

1. Avatkaa koneiltanne Eclipse-sovelluskehitin
2. Eclipse pyytää aluksi valitsemaan työtilan (workspace), eli hakemiston tiedostojen tallennusta varten
3. Luokaa työtila haluamaanne hakemistoon (kampuksen koneilla esim. M-asemalle)
4. Luokaa itsellenne uusi Java-projekti: `File 🡪 New 🡪 Java project`
5. Lisätkää projektiin uusi Java-luokka nimeltä TerveMaailma (`TerveMaailma.java`)
6. Lisätkää luokkaan main-metodi, jonka sisällä tulostakaa teksti "Terve maailma!"
7. Suorittakaa kirjoittamanne koodi (Eclipsen run-painike)
8. Eclipsen konsoliin pitäisi nyt tulostua toivottu teksti

## Viopen tyypillisiä virhetilanteita

* package-lause luokan alussa

    Vaikka ohjelmoisit omat ratkaisusi Eclipsessä hyvien käytäntöjen mukaisesti erillisiin paketteihin, tulee `package`-rivit poistaa aina palautettavien tiedostojen alusta. Viope ei tue paketteja tehtävien ratkaisuissa.

* Käännösvirhe

    Jos luokassa on syntaksivirhe, ei kääntäjä pysty kääntämään ratkaisuasi eikä ohjelman suoritus ala lainkaan. Tällaisten tapausten välttämiseksi on tärkeää toteuttaa ja testata ratkaisusi aina ensin Eclipsessä, ja vasta sen jälkeen kopioida ainakin syntaksiltaan toimivaksi varmistettu ratkaisu Viopeen.

* Virheellinen luokan nimi

    Vaikka ohjelma toimisi täysin oikein omalla Eclipselläsi, saattaa se aiheuttaa käännösvirheen, mikäli luokkasi nimi on eri kuin mitä Viope odottaa. Tarkista siis, että luokan nimi `class Nimi { ... }` on kirjoitettu oikein kirjainkoko huomioiden.

[Tyypillisiä virhetilanteita ja niiden ratkaisuja on dokumentoitu Wikiin.](Viope)


# Tekstin ja lukujen tulostaminen

Javassa on erilaisia metodeita ja tietovirtoja, joilla voidaan tulostaa esim. tekstiä ja lukuja ruudulle.

`System.out` on oletustietovirta, johon voidaan tulostaa seuraavasti:

```java
System.out.println(tuloste);
```

`println` tulostaa annetun arvon ja lopuksi aina rivinvaihdon, eli seuraava tuloste tulostuu eri riville. `print` tekee saman, mutta ilman rivinvaihtoa tulosteen loppuun:

```java
System.out.print(tuloste);
```

`print`-metodia käytettäessä seuraava tuloste jatkuu samalle riville.


## Tulostusesimerkki

```java
// tiedosto Tulostaja.java
public class Tulostaja {
    public static void main(String[] args) {
        // laskuoperaatiot suoritetaan aina ensin ja vasta sitten tulostetaan:
        System.out.println(1 + 2);
        System.out.println(4 - 1);
        System.out.println(2 * 4);
        System.out.println(9 / 2); // huomaa tämän operaation tulos!! (4)
    }
}
```

Kuten yllä huomaat, luvuille voidaan Javassa suorittaa tavanomaiset laskuoperaatiot: yhteen-, vähennys-, kerto- ja jakolaskut. Kokonaislukujen jakolaskuun liittyy kuitenkin erikoinen piirre, jota käsittelemme alempana.


# Muuttujat

Ohjelmissa käytettäviä arvoja, esimerkiksi numeroita (int) tai merkkijonoja (String), voidaan pitää tallessa muuttujissa. 

Javassa muuttujilla on aina ennalta määritettävä tyyppi, joka määrää sen, minkä tyyppisiä arvoja kyseiseen muuttujaan voidaan asettaa, esim:

```java
int leveys; // luo uuden muuttujan
```

Muuttujiin asetetaan arvoja sijoitusoperaattorilla `=`:

```java
int leveys = 3; // luo uuden muuttujan ja asettaa siihen alkuarvon
```

Muuttujia voidaan käyttää myöhemmin esimerkiksi laskutoimituksissa kirjoittamalla luvun tilalle muuttujan nimi:

```java
int leveys = 2;
int korkeus = 3;
int ala = leveys * korkeus;

System.out.println(ala);

// asetetaan uusia arvoja:
leveys = 4;
korkeus = 6;

// mikä luku tulostuu viimeisenä?
System.out.println(ala);
```

## String-muuttuja

Vastaavasti merkkijonoja voidaan asettaa muuttujiin, kun muuttujan tyypiksi määritellään `String`, eli merkkijono:

```java
String etunimi = "Matti";
```

Merkkijonoja voidaan yhdistää toisiinsa, eli konkatenoida, plus-merkillä `+`:

```java
String etunimi = "Matti";
String sukunimi = "Meikäläinen";

String kokonimi = etunimi + " " + sukunimi;

// Tulostaa tekstin: Matti Meikäläinen
System.out.println(kokonimi);
```

Yllä käytettyjen muuttujien tyyppi on `String`, eli niihin voidaan asettaa ainoastaan merkkijonoja.

## Vakiot

Muuttuja voidaan myös määritellä ”vakioksi”, jolloin siihen asetettavaa arvoa ei voida enää korvata toisella arvolla. Tämä tehdään lisäämällä sana `final` muuttujan määrittelyn alkuun:

```java
final double PI = 3.141592;
```

Yllä olevan muuttujan tyypiksi on määritetty `double`, joka on yleisin Javassa käytettävä tietotyyppi desimaalilukujen käsittelemiseksi.


## Muuttujien nimeäminen

Hyvä lähde koodin tyylikäytäntöjen opetteluun on esimerkiksi Google Java Style Guide, https://google.github.io/styleguide/javaguide.html#s5-naming.

* Muuttujien nimissä voi olla kirjaimia, numeroita sekä joitakin erikoismerkkejä
* useimpien erikoismerkkien ja ääkkösten käyttöä ei kuitenkaan suositella
* Muuttujan nimi ei saa alkaa numerolla
* Usean sanan pituiset muuttujan nimet kirjoitetaan yhteen, jälkimmäiset sanat isoilla alkukirjaimilla (camelCase):

```diff
+ String nykyinenKuukausi = "tammikuu";  // näin!
- String nykyinen kuukausi = "tammikuu"; // ei näin!

+ int paivia = 31; // näin!
- int päiviä = 31; // ei näin!
```

Kun muuttuja on määritetty vakioksi, se kirjoitetaan usein isoilla kirjaimilla:

```java
final double PI = 3.141592;

// Javassa on myös valmis arvo piille:
// https://docs.oracle.com/javase/8/docs/api/java/lang/Math.html#PI
```


# Javan tyypit (staattinen tyypitys)

Java-kääntäjä varmistaa, että muuttujiin ei aseteta väärän tyyppisiä arvoja. Esim. `int`-tyyppisessä muuttujassa voidaan varastoida ainoastaan kokonaislukuja:

```java
int numero = 1;

// Aiheutuu käännösvirhe "Type mismatch: cannot convert from String to int"
numero = "kaksi";
```

Huomaa, että virhe tapahtuu jo ennen kuin ohjelmaa voidaan suorittaa. Tämä johtuu siitä, että Java on käännettävä ohjelmointikieli.


## Javan tietotyyppejä: kokonaisluvut (int ja long)

Javassa kokonaisluvut ovat oletuksena tyyppiä `int` (integer). `int` on 32-bittinen kokonaisluku väliltä  -2 147 483 648 – 2 147 483 647.

Kun tarvitaan suurempia lukuja, voidaan käyttää `long`-tyyppisiä lukuja.

long on 64-bittinen kokonaisluku väliltä -9 223 372 036 854 775 808 – 9 223 372 036 854 775 807

Luku määritellään long-tyyppisenä kirjoittamalla sen perään L-kirjain: 

```
987654321098765432L
```

Suurten lukujen hahmottaminen yhteenkirjoitettuna voi olla hankalaa. Java mahdollistaa myös [alaviivan käyttämisen erottimena pitkien lukujen esityksissä](https://docs.oracle.com/javase/7/docs/technotes/guides/language/underscores-literals.html):

```
987_654_321_098_765_432L
```

Muuttujien tyypeiksi int ja long määritellään seuraavasti:

```java
// Normaali kokonaisluku (int)
int ika = 20;

// Hyvin iso kokonaisluku (long)
long ihmisia = 7_644_362_948L;
```

Lisäksi on olemassa pienemmät lukutyypit `byte` ja `short`, joita tarvitaan harvemmin.

## Kokonaislukujen "ylivuoto"

Jos laskutoimituksen tulos on suurempi, kuin mitä kyseinen lukutyyppi pystyy esittämään, tapahtuu ns. ylivuoto, eli numero "pyörähtää ympäri"

Kokeile suorittaa seuraavat rivit. Mitä tuloksia saat ja miksi?

```java
// int-luvun ylivuoto:
System.out.println(2_147_483_647);
System.out.println(2_147_483_647 + 1);

// Sama long-tyyppisellä luvulla
System.out.println(2_147_483_647L + 1);
```

**Huom!** Kokonaislukujen ylivuoto ei niinkään liity Javaan, vaan yleisesti siihen, miten luvut esitetään tietokoneen muistissa ykkösten ja nollien avulla.


## Javan tietotyyppejä: liukuluvut (double)

Tietojenkäsittelyssä desimaalilukuja käsitellään tyypillisesti liukulukuina. Liukuluku-termi tulee siitä, että luvussa kokonais- ja desimaaliosille ei ole varattu kiinteää määrää bittejä, vaan pisteen paikka "liukuu" sen mukaan, kuinka suuresta tai pienestä luvusta on kyse.

Liukulukujen toteutuksesta johtuen niillä laskettaessa esiintyy usein pieniä laskuvirheitä, minkä vuoksi niitä ei tule käyttää täydellistä tarkkuutta vaativissa tarkoituksissa.

Javan oletustietotyyppi liukuluvuille on nimeltään `double`. Doublen tarkkuus desimaalilukuna on noin 15 numeroa, esimerkiksi `1234567.89012345`.

Esim. piin likiarvo on double-tyyppisenä voisi olla `3.141592653589793`.

Lisäksi on olemassa myös epätarkempi float, jota käytetään lähinnä silloin, kun lukuja on valtavia määriä ja niiden tarkkuudesta voidaan tinkiä.

## Laskuvirheet liukuluvuilla

Laskutoimitukset liukuluvuilla ovat erittäin nopeita. Tietokoneet käsittelevät mm. pelien grafiikkaa ja muuta matematiikkaa liukuluvuilla.

Liukulukujen toteutuksesta johtuen niillä laskettaessa esiintyy kuitenkin usein pieniä tarkkuusvirheitä, minkä vuoksi niitä ei tule käyttää täydellistä tarkkuutta vaativissa tarkoituksissa.

Kokeile suorittaa seuraava yhteenlasku. Minkä tuloksen saat?

```java
System.out.println(0.1 + 0.2); 
```

Liukulukujen laskuvirhe ei niinkään liity Javaan, vaan yleisesti siihen, miten liukuluvut esitetään tietokoneen muistissa.


## Aritmeettiset operaatiot

Operaattori | Käyttötarkoitus
------------|----------------
\+          | Yhteenlasku (myös merkkijonojen yhdistäminen)
\-          | Vähennyslasku
\*          | Kertolasku
/           | Jakolasku
%           | Jakojäännös


Lähde: https://docs.oracle.com/javase/tutorial/java/nutsandbolts/op1.html

#### Laskuoperaatiot Javassa

```java
1 + 2 == 3
4 - 1 == 3
2 * 4 == 8
8 / 2 == 4

// % -operaattorilla saadaan laskettua jakolaskun jakojäännös:
9 % 2 == 1

9.0 / 2 == 4.5

// Huom! Kokonaislukujen jakolasku on katkaiseva, eli 
// tulosta ei pyöristetä ja desimaaliosa "katkeaa" pois:
9 / 2 == 4
```

Jos jakolasku tehdään kahdelle kokonaisluvulle, tulokseksi saadaan myös kokonaisluku, ja mahdollinen desimaaliosa "katkeaa pois". Jos vähintään toinen luvuista on liukuluku, tulee tuloksesta liukuluku, jolloin katkaisua ei tapahdu.

Kokonaisluvusta saadaan tarvittaessa liukuluku helposti esim. kertomalla se luvulla `1.0`:

```java
// a saadaan "muutettua" liukuluvuksi kertomalla se 1.0:lla.
// Tällöin myös tulos c on liukuluku, eikä desimaaliosan katkaisua tapahdu:
(1.0 * a) / b == c
```

## Lukujen pyöristäminen `round` sekä `ceil` ja `floor`

Javan `Math`-luokasta löytyy lukuisia erilaisia metodeja, joiden avulla voidaan pyöristää ylös, alas tai lähimpään kokonaislukuun:

```java
// Pyöristys aina alaspäin: 6.0
double a = Math.floor(6.8);

// Pyöristys aina ylöspäin: 7.0
double b = Math.ceil(6.1); 

// Pyöristys aina lähimpään tasalukuun: 6.0
double c = Math.round(5.6); 
```

Math.ceil:

> Returns the smallest (closest to negative infinity) double value that is greater than or equal to the argument and is equal to a mathematical integer. 
>
> https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Math.html#ceil(double)

Math.floor:

> Returns the largest (closest to positive infinity) double value that is less than or equal to the argument and is equal to a mathematical integer.
>
> https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Math.html#floor(double)

Math.round:

> Returns the closest int to the argument, with ties rounding to positive infinity.
>
> https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Math.html#round(double)


## Liukuluvun muuttaminen kokonaisluvuksi

Liukuluvulle voidaan tehdä **tyyppimuunos** kokonaisluvuksi kirjoittamalla sen eteen suluissa `(int)`:

```java
int a = (int) Math.round(5.6); // pyöristää ensin, ja sitten katkaisee
```

### Yksittäisten arvojen operaatiot

Operaattori | Kuvaus
------------|---------
++          | Kasvattaa arvoa yhdellä
--          | Vähentää arvoa yhdellä
!           | Kääntää totuusarvon päinvastaiseksi

https://docs.oracle.com/javase/tutorial/java/nutsandbolts/op1.html

```java
int luku = 10;
luku++;

System.out.println(luku); // 11
luku--;

System.out.println(luku); // 10

boolean ok = true;

// ! kääntää totuusarvon vastakkaiseksi:
System.out.println(!ok); // false
```

### Luvun kasvattaminen, vähentäminen tai kertominen

```java
int numero = 6;

numero += 5; 		// numero = numero + 5
numero *= 3; 		// numero = numero * 3
numero /= 7; 		// numero = numero / 7

// Mikä luku tulostuu lopulta? Miksi?
System.out.println(numero);

// Tulos on 4, koska: (6 + 5) * 3 / 7 = 4.714,
// josta desimaaliosa leikkautuu pois!
```

## Koodausharjoitus

Alla esitetyssä luokassa on kolme muuttujaa, joiden arvot tulostetaan ruudulle. Muokkaa ohjelmaa siten, että ohjelma laskee ja tulostaa myös muuttujien keskiarvon `7.333333333333333`. 

Keskiarvoa ei saa pyöristää tai muulla tavoin muotoilla. 

**Huom!** Jos muuttujien arvoja muutetaan, tulee myös tulostuksen muuttua. Älä siis "kovakoodaa" lukuja.


```java
public class LukujenKeskiarvo {

    public static void main(String[] args) {
        int eka = 9;
        int toka = 7;
        int kolmas = 6;

        System.out.println("eka: " + eka);
        System.out.println("toka: " + toka);
        System.out.println("kolmas: " + kolmas);

        // täydennä tänne keskiarvon laskeminen
        System.out.println("keskiarvo: ");
    }
}
```

Tämä tehtävä on lainattu [Helsingin yliopiston Agile Education Research -tutkimusryhmän ohjelmointikurssilta](https://2017-ohjelmointi.github.io/part1/#exercise-8-kolmen-luvun-keskiarvo) ja se on lisensoitu Creative Commons BY-NC-SA-lisenssillä.


# Syötteen lukeminen näppäimistöltä

Javassa on erilaisia tietovirtoja, kuten:

Tietovirta  | Tarkoitus
------------|------------------
`System.in` | syötteiden lukeminen käyttäjältä (konsolista)
`System.out`| tulostaminen konsoliin
`System.err`| virheilmoitusten tulostaminen (punainen teksti)

Tiedon lukemiseksi `System.in`-tietovirrasta kannattaa käyttää `Scanner`-luokkaa, joka tarjoaa käteviä metodeja eri tyyppisten syötteiden lukemiseksi.


## Scanner-luokka

Kun Java-ohjelmia suoritetaan komentoriviltä, voidaan ohjelmalle antaa näppäimistöä käyttäen mm. tekstiä ja lukuja.

Kun käyttäjä kirjoittaa tekstiä ja painaa enter-painiketta, kirjoitetut merkit päätyvät Javan `System.in` -tietovirtaan.

Kirjoitettu teksti ja numerot voidaan lukea tietovirrasta merkkijonoiksi ja numeroiksi `Scanner`-luokan avulla. `Scanner`-luokka sijaitse `java.util`-nimisessä "paketissa", josta se täytyy ottaa käyttöön omaan Java-luokkaan import-komennolla:

```java
import java.util.Scanner;
```

### Käyttäjän syötteen lukeminen

Kun Scanner on otettu käyttöön import-käskyllä, voidaan ohjelmaan luoda uusi syötteitä lukeva Scanner-olio. Oliot luodaan aina `new`-avainsanalla. `Scanner`-luokan tapauksessa oliota luotaessa pitää lisäksi määritellä, mistä tietovirrasta syötteet luetaan:

```java
// luodaan olio, joka lukee System.in-tietovirtaa:
Scanner lukija = new Scanner(System.in);
```

Jotta scanneria voidaan käyttää tietojen lukemiseen, täytyy se ottaa luonnin jälkeen talteen `Scanner`-tyyppisen muuttujan. Kun Scanner-olio on luotu ja se on tallessa muuttujassa, voidaan sen avulla lukea mm. tekstiä ja numeroita.  

Kokonainen rivi tekstiä voidaan lukea nextLine-nimisellä metodilla:

```java
Scanner lukija = new Scanner(System.in);
System.out.println("Kirjoita tekstiä: ");

String teksti = lukija.nextLine();
```

Jos tietovirrassa ei ole valmiiksi dataa, jää ohjelma odottamaan, että käyttäjä kirjoittaa syötteen ja painaa enter-painiketta. Jos käyttäjä on jo kirjoittanut dataa tietovirtaan, lukee Scanner valmiiksi syötettyä dataa.

Annettu teksti otetaan tässä esimerkissä talteen sijoittamalla se `String`-tyyppiseen muuttujaan:

```java
String teksti = lukija.nextLine();
```

Tämän jälkeen `teksti`-muuttujaa voidaan käyttää kuten mitä tahansa merkkijonomuuttujaa. Samalla `Scanner`-oliolla voidaan myös lukea lukuisia eri syötteitä peräjälkeen.

### Eri tyyppisten syötteiden lukeminen

`nextLine()`–metodi lukee tietovirrasta tekstiä seuraavaan rivinvaihtoon asti. Vastaavasti tietovirrasta voidaan lukea yksittäisiä sanoja tai eri tyyppisiä lukuja:

* `nextInt()` lukee tietovirrasta seuraavan kokonaisluvun
* `nextDouble()` lukee tietovirrasta seuraavan liukuluvun
* `next()` lukee tietovirrasta merkit seuraavaan tyhjään merkkiin asti

```java
Scanner lukija = new Scanner(System.in);

System.out.println("Kirjoita sana:");
String sana = lukija.next();

System.out.println("Kirjoita kokonaisluku:");
int luku = lukija.nextInt();

System.out.println("Kirjoita liukuluku:");
double liukuluku = lukija.nextDouble();
```

**Huom!** Jos tietovirrassa on odottamassa esim. kirjaimia, ja sieltä yritetään lukea numeroa, ohjelma kaatuu ajonaikaiseen poikkeukseen.

## Koodausharjoitus

Kirjoita luokka `HeiEtunimi`. Toteuta luokkaan `main`-metodi, jossa kysytään ensin käyttäjän etunimi ja sen jälkeen tervehditään käyttäjää nimeltä. 

Esimerkki ohjelman suorituksesta:

```
Syötä etunimi: Teppo
Hei Teppo!
```

# Liukulukujen tulostaminen

Liukulukuja tulostettaessa tulostettavien desimaalien määrä vaihtelee ja desimaalierottimena käytetään oletuksena pistettä. Tulostettavien desimaalien määrään ja käytettävään desimaalierottimeen voidaan vaikuttaa muotoilemalla desimaaliluvut Javan `DecimalFormat`-luokan avulla.

**Tulet tarvitsemaan DecimalFormat-luokkaa Viope-tehtävien ratkaisemisessa.**

## `DecimalFormat`-luokka

`DecimalFormat`-luokka otetaan käyttöön kirjoittamalla luokan alkuun `import`-komento:

```java
import java.text.DecimalFormat;
```

Sen jälkeen luodaan uusi `DecimalFormat`-olio, jolle kerrotaan, missä muodossa luvut halutaan tulostaa. `"0.00"` muotoilee luvun kahden desimaalin tarkkuudella käyttäen käyttöjärjestelmän desimaalierotinta (pilkku tai piste).

DecimalFormat-oliolla on `format`-metodi, joka muotoilee liukuluvun merkkijonoksi. Esimerkiksi:

```java
// koodiin kirjoitetaan liukuluvut pisteellä eroteltuna:
double liukuluku = 123.456789;

// liukuluvut tulostetaan normaalisti pisteellä eroteltuna ilman pyöristyksiä:
System.out.println(liukuluku); // tulostaa 123.456789

// luodaan olio, joka muotoilee lukuja kahden desimaalin tarkkuudella:
DecimalFormat kaksiDesimaalia = new DecimalFormat("0.00");

// annetaan muotoiltava luku format-metodille, saadaan takaisin muotoiltu merkkijono:
String muotoiltu = kaksiDesimaalia.format(liukuluku);

// tulostetaan lopulta muotoiltu merkkijono:
System.out.println(muotoiltu); // 123,46 <-- pyöristetty kahteen desimaaliin, erottimena pilkku
```

# Kommentit

Javassa on kolme eri kommenttityyliä:

```java
/**
 * Luokan ja julkisten metodien "viralliset" dokumentaatiokommentit 
 * kirjoitetaan näin.
 *
 * @see https://google.github.io/styleguide/javaguide.html#s7-javadoc
 */
public class Kommentit {

    public static void main(String[] args) {
        /*
         * Koodinpätkille voidaan kirjoittaa monirivisiä kommentteja näin.
         */
        int luku = 1;

        // Yksirivisille kommenteille laitetaan vain kaksi kauttaviivaa
        System.out.println(luku);
    }
}
```


## Kertausta

Mistä johtuu, että alla oleva luku näyttää olevan esitetty tarpeettoman suurella tarkkuudella?

![Pyöristysvirhe](https://github.com/haagahelia/swd4tn032-TH_JJ/raw/master/muistiinpanot/assets/pyoristysvirhe.png)

Laskutoimitukset liukuluvuilla ovat erittäin nopeita. Tietokoneet käsittelevät mm. pelien grafiikkaa ja muuta matematiikkaa liukuluvuilla. Esim. Javascript ei muuta käytäkään. Liukulukujen toteutuksesta johtuen niillä laskettaessa esiintyy kuitenkin usein pieniä tarkkuusvirheitä, minkä vuoksi niitä ei tule käyttää täydellistä tarkkuutta vaativissa tarkoituksissa.

Kokeile suorittaa seuraava yhteenlasku. Minkä tuloksen saat?

```java
System.out.println(0.1 + 0.2); // tulostaa 0.30000000000000004
```

Liukulukujen laskuvirhe ei niinkään liity Javaan, vaan yleisesti siihen, miten liukuluvut esitetään tietokoneen muistissa. Kaikkia lukuja ei vain ole mahdollista esittää rajatulla määrällä desimaaleja. Vastaavasti kymmenjärjestelmässä ei voida tarkasti esittää lukua `1/3`.

# Viope-harjoitukset

Rekisteröitykää viimeistään nyt Viopeen ja liittykää kurssille. Harjoitukset lähtevät käyntiin heti, ensimmäisiä tehtäviä tehtiin jo tällä tunnilla.

Kun kohtaatte ongelmia tehtävissä, pyytäkää apua ja vinkkejä kurssin Teams-työtilan keskustelualueella!

**Muistathan, että teknisistä syistä johtuen Viopeen palautettavista ratkaistuista täytyy poistaa mahdolliset `package`-rivit luokan yläpuolelta.**


---

Tämän oppimateriaalin on kehittänyt Teemu Havulinna ja se on lisensoitu [Creative Commons BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/) -lisenssillä.


<script src="/tocbot/tocbot.min.js"></script>

<link rel="stylesheet" href="/tocbot/tocbot.css">

<script>
tocbot.init({ tocSelector: '.js-toc', contentSelector: '.main-content' });
</script>