[&larr; Takaisin etusivulle](/)


<h1 class="js-toc-ignore">Olio-ohjelmointi (Object-oriented programming)</h1>

Olio-ohjelmointi on yleinen ohjelmointiparadigma, jota hyödynnetään lukuisissa ohjelmointikielissä. Myös Java on olio-ohjelmointikieli, vaikka emme toistaiseksi ole omissa ohjelmissamme soveltaneet juurikaan olio-ohjelmointia.

Olio-ohjelmoinnin avulla voimme jäsentää ohjelmamme toiminnallisuuden ja ohjelmassa esiintyvän datan loogisiksi itsenäisiksi kokonaisuuksiksi, joiden avulla pystymme ratkaisemaan ongelmia. **Olio-ohjelmoinnissa on siis samalla kyse tiedon mallintamisesta että ratkaisujen mallintamisesta.** 


**Sisällysluettelo**

<div class="js-toc"></div>

# Luokat ja oliot

Eri luokilla ja olioilla on erilaisia rooleja ratkaistavissa ongelmissa. Osa luokista ja olioista esimerkiksi mallintaa dataa, toiset suorittavat logiikkaa ja muut huolehtivat vuorovaikutuksesta käyttäjän tai toisten järjestelmien kanssa. Siksi ei ole yhtä ainoaa tapaa mallintaa luokkia ja olioita.

Olioiden ja luokkien käyttötapa riippuu monista seikoista. Jos pankkisovelluksessa käytetään olioita tilien mallintamiseen, tehdään tästä luokasta kenties miljoonia olioita. Samassa sovelluksessa voi olla myös luokkia, joista luodaan vain yksi olio, kuten tilinumeroiden oikeellisuuden tarkastaja. Vaikka molemmat käsitteet toteutetaan olio-ohjelmoinnilla, tilit mallintavat dataa ja tilinumeroiden tarkastaja logiikkaa.

Tällä opintojaksolla keskitymme aluksi luokkien ja olioiden hyödyntämiseen datan mallintamisessa, eli teemme luokkia, jotka vastaavat joitain reaalimaailman käsitteitä. Jatkokurssilla olio-ohjelmointia sovelletaan esimerkiksi olioina, joiden tarkoitus on toimia vuorovaikutuksessa tietokannan ja verkkoselainten kanssa.

## Suositeltavaa luettavaa

Johdatus olio-ohjelmointiin: [https://ohjelmointi-19.mooc.fi/osa-4/2-johdatus-olio-ohjelmointiin](https://ohjelmointi-19.mooc.fi/osa-4/2-johdatus-olio-ohjelmointiin)

Luokka ja olio: [https://ohjelmointi-19.mooc.fi/osa-4/3-luokka-ja-olio](https://ohjelmointi-19.mooc.fi/osa-4/3-luokka-ja-olio)

## Tiedon mallintaminen olioiden avulla

Olemme käyttäneet jo monenlaisia olioita omissa ohjelmissamme. Käsitellessämme esim. päivämääriä olemme käyttäneet `LocalDate`-luokkaa, emmekä toisistaan irrallisia muuttujia:

```java
// Päivämäärät olioina, kätevää:
LocalDate olio1 = LocalDate.of(2020, 1, 1);
LocalDate olio2 = LocalDate.of(2030, 12, 31);


// Päivämäärät primitiiveinä, epäkäytännöllistä:
int vuosi1 = 2020;
int kuukausi1 = 1;
int paiva1 = 1;

int vuosi2 = 2030;
int kuukausi2 = 12;
int paiva2 = 31;
```

Jokainen LocalDate-olio pitääkin sisällään juuri nämä kolme muuttujaa, mutta ne ovat kaikki tallessa yhdessä paikassa. JSON-tietomuodon avulla olio voitaisiin esittää tällaisessa muodossa:

```javascript
{
    "year": 2020,
    "month": 1,
    "day": 1
}
```

Kun tieto on mallinnettu olioina, voimme hyödyntää olioiden operaatioita, eli **metodeja**, erilaisten operaatioiden suorittamiseksi. `LocalDate`-luokan operaatioita ovat toistaiseksi olleet päivämäärien vertailu sekä päivämäärävälin pituuden laskeminen:

```java
LocalDate olio1 = LocalDate.of(2020, 1, 1);
LocalDate olio2 = LocalDate.of(2030, 12, 31);

// olioilla on metodeja, joiden avulla voimme suorittaa erilaisia operaatioita:
if (olio1.isBefore(olio2)) {
    System.out.println("Päivämäärä 1 on ennen päivämäärää 2!");
}
```

Päivämäärän vertailussa `LocalDate`-luokka piilottaa sisäänsä varsinaisen vertailussa suoritettavan logiikan, jota ei nyt tarvitse toistaa missään `LocalDate`-luokan ulkopuolella. Logiikka on kuitenkin käytettävissä kaikkialta luokan tarjoaman `isBefore`-oliometodin avulla, jolloin emme itse joudu toteuttamaan vastaavaa luokan sisään toteutettua vertailua: 

```java
/* Copyright (c) 2012, 2018, Oracle and/or its affiliates. All rights reserved. */
int compareTo0(LocalDate otherDate) {
    int cmp = (year - otherDate.year);
    if (cmp == 0) {
        cmp = (month - otherDate.month);
        if (cmp == 0) {
            cmp = (day - otherDate.day);
        }
    }
    return cmp;
}
```

**Luokan sisäistä toteutusta päivämäärien vertailemiseksi ei siis tarvitse tietää, jotta voimme hyödyntää sitä.**

Vastaavasti, jos haluamme laskea päivämäärän esimerkiksi 31 päivää minkä tahansa päivämäärän jälkeen, joudumme ratkaisussamme käsittelemään eri pituisia kuukausia, karkausvuosia ja vuodenvaihteen yli meneviä aikavälejä. On erittäin loogista, että tällaiset usein tarvittavat operaatiot paketoidaan omaksi kokonaisuudeksi, eli luokaksi, joka tarjoaa yksinkertaisen rajapinnan monimutkaisten operaatioiden suorittamiseksi:

```java
LocalDate uusiOlio = olio1.plusDays(31);
```

Teknisten yksityiskohtien piilottamista ja operaatioiden käsitteellistämistä kutsutaan **abstraktoinniksi**, ja se on yksi olio-ohjelmoinnin peruspilareista.


## Luokka ja olio

`LocalDate`-luokka määrittelee kaikille sen olioille yhteiset ominaisuudet ja yhteiset toiminnallisuudet. Voimme kutsua samoja metodeja mille tahansa päivämääräolioille. Jokainen erillinen päivämäärä on kuitenkin toisistaan riippumaton, mutta rakenteeltaan samanlainen. Yhdestä luokasta voidaan luoda rajoittamattoman määrän olioita.

Käyttäessämme olioita omassa koodissamme, **käytämme luokan nimeä muuttujan tyyppinä**. **Muuttujiin asetetaan arvoja, jotka ovat olioita**. Meille tuttu tietotyyppi `String` on luokka ja yksittäiset merkkijonot ovat sen olioita. Kaikilla merkkijonoilla on samat metodit, mutta eri sisältöiset merkkijono-oliot palauttavat metodeja kutsuttaessa eri arvoja. Ne ovat siis oliokohtaisia eli **oliometodeja**:

```java
String olio1 = "Eka merkkijono-olio";
String olio2 = "Toinen merkkijono-olio";

// samat metodit, mutta yksilölliset paluuarvot
int pituus1 = olio1.length();
int pituus2 = olio2.length();
```


## Datan mallintaminen luokalla

Aikaisemmin tällä kurssilla olemme käsitelleet mm. kaupunkien nimiä ja väkilukuja taulukkomuodossa (csv): 

Kaupunki	| Väkiluku 
------------|---------
Helsinki    | 653867
Espoo	    | 289413
Tampere	    | 238245
Vantaa	    | 233290
...         | ...

Kuten päivämäärien kanssa, kaupunkien ja niiden väkilukujen käsitteleminen yksittäisillä muuttujilla olisi hankalaa:

```java
// ei näin!
String nimi1 = "Helsinki";
int vakiluku1 = 653_867;

String nimi2 = "Espoo";
int vakiluku2 = 289_413;

//...
```

Kaupunkien ja väkilukujen esittäminen esimerkiksi listoina olisi myös epäluonnollista, koska nimet ja väkiluvut olisivat toisistaan irrallisia tietoja:

```java
// ei näin!
List<String> nimet = List.of("Helsinki", "Espoo");
List<Integer> vakiluvut = List.of(653_867, 289_413);
```

Kun ongelmasta tunnistetaan reaalimaailman käsitteitä, voidaan niitä vastaavia uusia rakenteita luoda myös ohjelmiin. Tässä esimerkissä on selvästi kyse kaupungeista, joten voimme luoda uuden käsitteen "Kaupunki". Tätä käsitettä kutsutaan luokaksi ja kaikkia yksittäisiä kaupunkeja olioiksi:

```java
// Kaupunki-käsite selkeyttää ohjelmaa ja kokoaa toisiinsa liittyvät tiedot yhteen 👍
Kaupunki hki = new Kaupunki("Helsinki", 653_867);
Kaupunki esp = new Kaupunki("Espoo", 289_413);
```

Voimme myös toteuttaa luokkiin operaatioita, jotka abstraktoivat suoritettavia operaatioita:

```java
Kaupunki hki = new Kaupunki("Helsinki", 653_867);
Kaupunki esp = new Kaupunki("Espoo", 289_413);

if (hki.onSuurempiKuin(esp)) {
    System.out.println("Vertailu tehtiin olion metodilla!");
}
```

## Oman luokan määrittely

Kukin luokka määritellään pääsääntöisesti omaan tiedostoonsa, jonka nimi on sama kuin luokan nimi ja pääte on ".java", aivan kuten tähänkin asti. Luokan nimi kirjoitetaan siten, että kaikki sanat ovat yhdessä ja sanoissa on isot alkukirjaimet (CamelCase). Luokan määrittely alkaa avainsanoilla `public` ja `class`. Kaupunki-luokan tiedosto näyttää aluksi seuraavalta:

```java
// Kaupunki.java
public class Kaupunki {

}
```

Huomaa, että tämän luokan on tarkoitus mallintaa käsitteitä eikä esim. toimia omana ohjelmanaan. **Luokkaan ei siis haluta tehdä esimerkiksi `main`-metodia, joka kuuluisi erilliseen ohjelmaluokkaan.** Ohjelman selkeän rakenteen vuoksi on erittäin tärkeää pilkkoa eri tarkoituksia palvelevat kokonaisuudet eri luokkiin. Main-metodiluokan tarkoitus on tarjota vuorovaikutus käyttäjän ja ohjelman välille, kun taas `Kaupunki`-luokan tarkoitus on esittää yksittäisiä tietoalkioita. Ohjelman pilkkomiseksi on olemassa erilaisia malleja, kuten ["separation of concerns"](https://www.google.com/search?q=separation+of+concerns) ja ["data, context and interaction"](https://www.google.com/search?q=data+context+and+interaction).


### Oliomuuttujat

Edellä olemme todenneet tarpeen tallentaa jokaiselle Kaupunki-oliolle oma nimi ja väkiluku. Näitä varten tarvitaan siis muuttujat. Tähän asti muuttujat on aina määritelty paikallisiksi muuttujiksi, jotka ovat voimassa vain tietyn metodin suorituksen ajan. Nyt haluamme kuitenkin tehdä **oliokohtaisia muuttujia**, eli **oliomuuttujia**, jotka ovat pysyviä, ja joiden **arvot säilyvät myös metodien suoritusten välissä**.

Olioiden pysyvät muuttujat määritellään luokan runkoon metodien ulkopuolelle:

```java
// Kaupunki.java
public class Kaupunki {

    String nimi = "";
    int vakiluku = 0;
    double pintaAla = 0;
}
```

Nyt näitä oliokohtaisia muuttujia voitaisiin käyttää koodissa esimerkiksi seuraavasti:

```java
Kaupunki hki = new Kaupunki();
hki.nimi = "Helsinki";
hki.vakiluku = 653_867;
hki.pintaAla = 214.25;

System.out.println(hki.nimi);
System.out.println(hki.vakiluku);

Kaupunki esp = new Kaupunki();
esp.nimi = "Espoo";
esp.vakiluku = 289_413;
esp.pintaAla = 312.32;

System.out.println(esp.nimi);
System.out.println(esp.vakiluku);
```

### Oliometodit

Luokalle voidaan nyt määritellä esimerkiksi oliokohtainen metodi, eli oliometodi, joka laskee väkiluvun ja pinta-alan perusteella kaupungin väestöntiheyden. Oliot voivat käyttää omia muuttujiaan erityisen `this`-viittauksen kautta:

```java
public class Kaupunki {

    String nimi;
    int vakiluku;
    double pintaAla;

    public double laskeVaestontiheys() {
        return this.vakiluku / this.pintaAla;
    }
}
```

Tätä metodia voidaan käyttää nyt kaikkien `Kaupunki`-olioden kautta:

```java
System.out.println(hki.laskeVaestontiheys());
System.out.println(esp.laskeVaestontiheys());
```

### Private-oliomuuttujat

Haluamme pääsääntöisesti sulkea muuttujat luokan sisään siten, että niitä voidaan käyttää ainoastaan luokan omilla metodeilla. Tätä varten oliomuuttujille määritellään käytännössä aina näkyvyys `private`:

```java
// Kaupunki.java
public class Kaupunki {

    // muuttujia käytetään jatkossa vain metodien kautta:
    private String nimi;
    private int vakiluku;
    private double pintaAla;


}
```

**Keskeisiä seikkoja oliomuuttujista:**

* Oliomuuttujat ovat **yksittäisille olioille kuuluvia muuttujia**.
* Oliomuuttujat **määritellään luokassa kaikkein ylimpänä**, ennen metodeja ja muita osia.
* Kaikilla saman luokan olioilla on **samat muuttujat, mutta omilla arvoillaan**.
* Oliomuuttujien arvot säilyvät olion koko olemassaolon ajan, toisin kuin metodien sisällä käytetyt paikalliset muuttujat.
* Oliomuuttujien näkyvyyttä voidaan rajoittaa aivan kuten metodien. Pääsääntöisesti ne ovat `private`.


### Olioiden luominen

Olioita luodaan `new`-avainsanalla. Joissain tapauksissa olemme luoneet olioita muillakin tavoilla, esim. `LocalDate.now()`, mutta myös näissä tapauksissa varsinainen olion luominen tapahtuu kulissien takana `new`-avainsanalla.

Avainsanan jälkeen kirjoitetaan olion luokan nimi ja sulut. Sulkujen sisään kirjoitamme parametriarvot kuten metodikutsujen kanssa:

```java
Kaupunki uusiOlio = new Kaupunki("Helsinki", 653_867);
```

Edellä oleva luontikäsky käsitellään Java-luokassa **konstruktorin** avulla. Konstruktori on ikään kuin metodi, jota kutsutaan automaattisesti olioita luotaessa. Konstruktorin nimi on sama kuin luokan nimi, eli tässä tapauksessa `Kaupunki`. Sen näkyvyys on tyypillisesti `public`. Luotu olio voidaan ottaa talteen muuttujaan esimerkin mukaisesti sijoitusoperaattorilla.

Konstruktorin parametrimuuttujat määritellään kuten metodeissa. Nimet voivat olla samat kuin oliomuuttujien nimet, mutta tällöin vaaditaan erityistä huolellisuutta sen suhteen, mitä arvoja kulloinkin käytetään. **Luokassa voi siis olla samannimisiä paikallisia- ja oliomuuttujia**.

```java
// Kaupunki.java

public class Kaupunki {

    private String nimi;
    private int vakiluku;

    // konstruktori
    public Kaupunki(String nimi, int vakiluku) {
        // TODO: tämä konstruktori ei vielä aseta arvoja talteen!
    }
}
```


### Arvojen asettaminen oliomuuttujiin

Oliot voivat käyttää omia muuttujiaan erityisen `this`-viittauksen kautta. Käytettäessä olion omaa `nimi`-muuttujaa, kirjoitamme `this.nimi`. Muuttujaan voitaisiin siis olion omassa konstruktorissa tai metodissa asettaa arvo seuraavasti:

```java
this.nimi = "Helsinki";
```

Annettu nimi ei kuitenkaan ole "kovakoodattu" luokan sisään, vaan haluamme luoda minkä tahansa nimisiä kaupunkeja. Tämän vuoksi nimi annetaan luontikäskyn mukana parametrina:

```java
public Kaupunki(String nimi, int vakiluku) {
    // annettu nimi ja vakiluku halutaan talteen olion omiin muuttujiin!
}
```

Parametrina annettu paikallinen ja väliaikainen arvo `nimi` voidaan asettaa pysyvään talteen olion oliomuuttujaan sijoittamalla se näin: 

```java
this.nimi = nimi; // vasemmalla oliomuuttuja, oikealla paikallinen muuttuja
```

Kokonaisuutena olion muuttujat ja niiden alustaminen voisivat tapahtua seuraavasti:

```java
// Kaupunki.java
public class Kaupunki {

    private String nimi;
    private int vakiluku;

    // konstruktori
    public Kaupunki(String nimi, int vakiluku) {
        // nimi on paikallinen muuttuja, this.nimi on oliomuuttuja
        this.nimi = nimi;
        this.vakiluku = vakiluku;
    }
}
```

**`this` viittaa konstruktorin ja metodien sisällä aina siihen olioon, jonka operaatiota ollaan suorittamassa.**

```java
System.out.println("Minun nimeni on " + this.nimi + "!");
```

Jos koodissa ei ole riskiä eri muuttujien sekoittumisesta, voidaan `this` jättää kirjoittamatta:

```java
System.out.println("Minun nimeni on " + nimi + "!");
```

On kuitenkin oikean lopputuloksen kannalta turvallisempaa käyttää `this`-viittausta aina kuin olla käyttämättä sitä. `this`-viittauksen käyttäminen ei siis ole aina välttämätöntä, mutta käytämme sitä tällä kurssilla systemaattisesti selkeyden vuoksi.


**Keskeisiä seikkoja olioiden alustamisesta:**

* Olioiden kaikki muuttujat ovat oletuksena aluksi tyhjiä.
* Niihin voidaan asettaa alkuarvot konstruktorin avulla.
* Konstruktori on ikään kuin metodi, jota kutsutaan automaattisesti olioita luotaessa.
* Konstruktorin nimi on sama kuin luokan nimi ja näkyvyys usein `public`.


### Oliometodit

Olemme kirjoittaneet kurssilla toistaiseksi staattisia metodeja. Staattisten metodien otsikossa esiintyy avainsana `static` ja metodeja kutsutaan luokan nimen avulla, esim: `double suurin = Math.max(1.0, 2.0);`.

**Staattiset metodit eivät ole oliokohtaisia, joten niissä ei voida hyödyntää oliomuuttujia**.

Kun haluamme määritellä oliometodeja, jätämme pois `static`-avainsanan. Tällöin metodia ei voida kutsua luokan nimen kautta, vaan sitä kutsutaan jollekin tietylle oliolle. Esimerkiksi `String`-luokan `length()` on oliokohtainen metodi. Merkkijonoluokalla ei ole yleistä pituutta joka voitaisiin laskea yleisellä tasolla `String.length();`, vaan pituus liittyy aina johonkin tiettyyn merkkijonoon: `etunimi.length();`.

Jos haluaisimme esimerkiksi toteuttaa yllä esitellyn `onSuurempiKuin`-metodin, joka palauttaa `true`, jos se kaupunki jonka metodia kutsutaan on suurempi kuin toinen, voidaan se toteuttaa seuraavasti:

```java
public boolean onSuurempiKuin(Kaupunki toinen) {
    return this.vakiluku > toinen.vakiluku;
}
```
Tätä metodia kutsuttaisiin olion kautta, eli esim. näin:

```java
Kaupunki hki = new Kaupunki("Helsinki", 653_867);
Kaupunki esp = new Kaupunki("Espoo", 289_413);

if (hki.onSuurempiKuin(esp)) {
    System.out.println("Eka kaupunki on suurempi");
}
```

Metodin otsikko on tuttu aikaisemmilta oppitunneilta. Metodi palauttaa totuusarvon (`boolean`) ja se saa parametrinaan `Kaupunki`-olion, jota käytetään `toinen`-muuttujan kautta. Metodin sisällä se olio, jonka kautta metodia kutsuttiin on käytettävissä erityisen `this`-muuttujan kautta: `this.vakiluku`.

Parametrina saadun olion väkiluku saadaan käyttöön `toinen`-muuttujan avulla, eli `toinen.vakiluku`. Itse vertailu on tavallinen "suurempi kuin" vertailuoperaatio, jonka paluuarvo palautetaan metodista.

```java
// Kaupunki.java

public class Kaupunki {

    private String nimi;
    private int vakiluku;

    public Kaupunki(String nimi, int vakiluku) {
        this.nimi = nimi;
        this.vakiluku = vakiluku;

    }

    public boolean onSuurempiKuin(Kaupunki toinen) {
        return this.vakiluku > toinen.vakiluku;
    }

}
```

### toString()-metodi ja sen korvaaminen: @Override

Jokaisella luokalla on olemassa `toString`-niminen metodi, jota kutsutaan **automaattisesti**, kun olioista muodostetaan merkkijonoja esimerkiksi tulostamista varten.

Jos et kirjoita omaan luokkaasi `toString`-metodia, muodostaa Java olioistasi melko vaikeaselkoisen merkkijonon, esim:
`Kaupunki@1db9742`.

Voit kirjoittaa luokallesi oman merkkijonoesityksen ohittamalla Javan valmiin `toString`-metodin (`@Override`). `toString` ei saa ottaa parametreja ja sen täytyy aina palauttaa merkkijono:

```java
@Override
public String toString() {
    return "Olion merkkijonoesitys";
}
```

Kaupunki-luokan `toString`-metodissa voidaan käyttää `this`-viittausta ja muodostaa merkkijono esimerkiksi seuraavasti:

```java
@Override
public String toString() {
    return this.nimi + " (" + this.vakiluku + ")";
}
```

Nyt esim. println-metodi tulostaa `Kaupunki`-olioista `toString`-metodimme mukaisia merkkijonoja:

```java
Kaupunki hki = new Kaupunki("Helsinki", 653_867);

// toString-metodia voidaan kutsua itse:
String merkkijono = hki.toString();
System.out.println(merkkijono); // Helsinki (653867)

// println osaa kutsua toString-metodia myös automaattisesti:
System.out.println(hki); // Helsinki (653867)
```


## Koodin jakaminen luokkiin: ohjelmaluokka

Eri luokilla on hyvin erilaiset roolit ohjelmassa. Joidenkin luokkien rooli on mallintaa dataa, kun taas joidenkin tarjota erilaisia operaatioita. Ohjelman eri osien roolien ymmärtämiseksi on tärkeää että emme sekoita yhteen luokkaan ristiriitaisia tai päällekkäisiä rooleja. `Kaupunki`-luokan tarkoitus on mallintaa lopullisessa ohjelmassa olevia satoja tietueita, eikä se liity ohjelman käyttöliittymään tai käynnistämiseen.

Olisikin luokan tarkoituksen näkökulmasta ristiriitaista, että `Kaupunki`-luokkaa käytettäisiin myös ns. pääohjelmana, joka käynnistää käyttöliittymän tai tekee muita suoritukseen liittyviä operaatioita. Tätä varten on hyvä tehdä oma luokkansa, jolla voidaan käyttää `Kaupunki`-olioita esim. seuraavasti:

```java
public class KaupunkiOhjelma {

    public static void main(String[] args) {
        Kaupunki hki = new Kaupunki("Helsinki", 653_867);
        Kaupunki esp = new Kaupunki("Espoo", 289_413);

        if (hki.onSuurempiKuin(esp)) {
            System.out.println("Eka kaupunki on suurempi");
        }
    }
}
```


## Getterit ja setterit

Koska oliomuuttujat on asetettu yksityisiksi, niitä ei voida suoraan käyttää luokan ulkopuolelta. Mikäli ohjelmassa on tarve käyttää nimeä tai väkilukua luokan ulkopuolelta, luokkaan määritellään näille muuttujille omat "getterit ja setterit", eli metodit, joilla voidaan kysyä nykyinen arvo tai asettaa uusi arvo:

```java
public String getNimi() {
    return this.nimi;
}

public void setNimi(String nimi) {
    this.nimi = nimi;
}

public int getVakiluku() {
    return this.vakiluku;
}

public void setVakiluku(int vakiluku) {
    this.vakiluku = vakiluku;
}
```

Lue lisää gettereistä ja settereistä: https://www.w3schools.com/java/java_encapsulation.asp


## Null-viittaukset

Javassa on erityinen arvo nimeltä `null`, joka on käytännössä tyhjä viittaus. Jos viittaustyyppistä muuttujaa ei ole asetettu viittaamaan mihinkään, siinä on tällöin arvo `null`. `null`-viittausten kanssa tulee olla tarkkana, koska ne saattavat aiheuttaa bugeja ja ohjelman kaatumista:

```java
public class Tili {

    private String tiliNumero; // tiliNumero-muuttujan arvo on alussa null, eli tyhjä viittaus

    public String getTiliNumero() {
        return tiliNumero;
    }

    public void setTiliNumero(String tiliNumero) {
        this.tiliNumero = tiliNumero;
    }
}
```

```java
Tili t = new Tili();
System.out.println(t.getTiliNumero()); // Tulostaa null, koska tilinumeroa ei ole asetettu!
```

### NullPointerException
`NullPointerException` on ajonaikainen poikkeus, joka on seurausta siitä, että tyhjää arvoa (`null`) käytetään kuin se olisi olio. **Aina kun on mahdollista, että jokin arvo on alustamatta, eli `null`, tulee se tarkastaa ennen arvon käyttämistä.**

```java
String numero = t.getTiliNumero();
System.out.println(numero.toUpperCase()); // kaatuu NullPointerException-poikkeukseen, jos tilinumeroa ei ole asetettu
```

**Tämän Tili-esimerkin tapauksessa olisi hyvä idea toteuttaa konstruktori, jonka avulla tilinumero olisi pakko antaa heti oliota luotaessa.**


### Null-arvon tarkastaminen

Yllä oleva ongelma `toUpperCase()`-metodikutsun kutsumisessa `null`-arvolle voidaan välttää esim. seuraavasti:

```java
String numero = t.getTiliNumero();

if (numero == null) {
    System.out.println("Ei tilinumeroa");
} else {
    System.out.println(numero.toUpperCase());
}
```

----

## Synonyymejä

* **Oliot, objektit, ilmentymät, instanssit**

    Luokan ilmentymille on olemassa useita nimiä, jotka kuitenkin tarkoittavat samaa asiaa. 
    
    Kontekstista ja lähteestä riippuen käytetään joskus eri termejä.

* **Oliomuuttujat, instanssimuuttujat, ilmentymämuuttujat, jäsenmuuttujat, kentät, attribuutit**

    Luokassa määritellyille olioiden muuttujille on myös lukuisia nimiä. 

    Kaikki niistä kuitenkin tarkoittavat muuttujaa, joka on yksilöllinen jokaiselle tietyn luokan oliolle.

---

## Esimerkki: yhteystiedot

Kuvitteellisessa sovelluksessa käsitellään yhteystietoja, joihin kuuluvat henkilön nimi, puhelinnumero ja sähköpostiosoite. Tietty nimi, numero ja e-mail liittyvät aina yhteen henkilöön, ja ohjelmassa käsitellään lukuisten henkilöiden yhteystietoja.

JSON-tiedostomuodossa ohjelmamme data voisi olla esimerkiksi tämän esimerkin kaltainen:

```json
[{
  "nimi": "Lindsey",
  "email": "ldrillingcourt0@so-net.ne.jp",
  "puhelin": "132-414-7730"
}, {
  "nimi": "Zilvia",
  "email": "zzamboniari1@dell.com",
  "puhelin": "445-276-2785"
}, {
  "nimi": "Moses",
  "email": null,
  "puhelin": "681-240-4656"
}, {
  "nimi": "Devondra",
  "email": "cyberchimps.com",
  "puhelin": "306-422-3408"
}]
```
JSON esimerkki: https://mockaroo.com/

Data koostuu selvästi keskenään rakenteellisesti samanlaisista tietoalkioista, joilla on yksilölliset arvot, kuten nimi ja email. Huomaa, että henkilölle "Moses" ei ole asetettu sähköpostiosoitetta, mutta sillä on silti olemassa "muuttuja" sähköpostin tallentamiseksi. **Puuttuvaa arvoa ei voida jättää tyhjäksi, vaan siihen on asetettu null-viittaus.**

Tietojen tallentaminen erillisissä muuttujissa olisi hankalaa ja virhealtista. Sen sijaan määritellään luokka `Yhteystieto` ja jokaista henkilöä varten luodaan olio eli ilmentymä tästä luokasta:

```java
String nimi1 = "Matti";
String email1 = "matti@example.com";
String puhelin1 = "04055512345";

String nimi2 = "Maija";
String email2 = "maija@example.com";
String puhelin2 = "05055598765";

Yhteystieto matti = new Yhteystieto("Matti", "matti@example.com", "04055512345");
Yhteystieto maija = new Yhteystieto("Maija", "maija@example.com", "05055598765");
```

### Yhteystieto-luokan toteutus

```java

public class Yhteystieto {
    private String nimi;
    private String email;
    private String puhelin;

    public Yhteystieto(String nimi, String email, String puhelin) {
        // annetut parametriarvot asetetaan konstruktorin sisällä talteen oliomuuttujiin
        this.nimi = nimi;
        this.email = email;
        this.puhelin = puhelin;
    }
}

```

Kun luokkaan on määritetty konstruktori, luokan olioita luotaessa annetaan parametreina samat arvot, kuin konstruktoriin on määritelty:

```java
Yhteystieto matti = new Yhteystieto("Matti Meikäläinen", "matti@example.com", "04055512345");

Yhteystieto maija = new Yhteystieto("Maija Meikäläinen", "maija@example.com", "05055598765");
```

### Oliomuuttujien käyttäminen

```java
public class Yhteystieto {
    private String nimi;
    private String email;
    private String puhelin;

    // ...konstruktori jätetty pois...

    public void tulostaNimi() {
        // lukee oliomuuttujan arvon ja tulostaa sen println-metodilla:
        System.out.println(this.nimi);
    }

    public String kerroEmail() {
        // lukee oliomuuttujan arvon ja palauttaa sen paluuarvona:
        return this.email;
    }

    public void asetaEmail(String uusiEmail) {
        // asettaa oliomuuttujaan uuden parametrina saadun arvon
        this.email = uusiEmail;
    }
}
```

### Oliometodin kutsuminen

Oliometodeita kutsutaan viittauksen, eli esim. muuttujan kautta. Metodi suoritetaan "sille oliolle", jonka kautta sitä kutsutaan. Parametriarvot annetaan kuten staattisia metodeita kutsuttaessa:

```java
Yhteystieto matti = new Yhteystieto(...);

// kysytään email ja laitetaan se talteen
String email = matti.kerroEmail();

// tulostetaan talteen laitettu email
System.out.println(email);

// laitetaan yhteystietoon uusi osoite
matti.asetaEmail("uusi@example.com");

// tulostetaan yhteystiedon nimi metodin sisällä
matti.tulostaNimi();
```

### toString()-metodi ja sen ohittaminen: @Override

Katso kuvaus toString-metodin toteuttamisesta ylempää tästä dokumentista.

```java
class Yhteystieto {

    // muuttujat, konstruktori ja muut metodit...

    @Override
    public String toString() {
        return this.nimi + " (" + this.email + ")";
    }
}
```

---

### Datan kapselointi (encapsulation)

Olioiden attribuuttien muuttamista halutaan hyvin usein rajoittaa:

* `Yhteystieto`-luokan sähköpostiosoitteeksi ei haluta hyväksyä muita kuin valideja sähköpostiosoitteita
* `Tili`-luokan saldon muuttaminen luokan ulkopuolelta halutaan estää

**Ratkaisu:** olion attribuutit merkitään yksityisiksi (private) ja arvoja käytetään vain metodien kautta!

Esim. sähköpostiosoitteen muoto voidaan tällöin tarkastaa metodissa ennen kuin se laitetaan talteen:

```java
class Yhteystieto {
    private String email;

    public boolean asetaEmail(String e) {
        if (e.matches(".+@.+\\..+")) {
            this.email = e;
            return true;
        } else {
            return false;
        }
    }
}
```

Esimerkin säännöllinen lauseke sähköpostin tarkastamiseksi ei ole täydellinen, mutta se on riittävän yksinkertainen tähän esimerkkiin.


## Viittauksen kopioiminen != olion kopioiminen

Olioita ei voi kopioida sijoittamalla niitä uusiin muuttujiin. Tällöin viitataan vain samaan olioon usealla eri muuttujalla:

```java
Yhteystieto y1 = new Yhteystieto("Adam", "050123", "adam@example.com");

// ei kopioi, vaan viittaa samaan olioon:
Yhteystieto y2 = y1;
```

Jos yllä olevassa esimerkissä kutsutaan `asetaEmail`-metodia muuttujan `y1` kautta, muuttuu sähköpostiosoite myös `y2`:ssa. Tämä johtuu siitä, että **olemme luoneet vain yhden olion, johon viitataan kahdella muuttujalla**.

---

Tämän oppimateriaalin on kehittänyt Teemu Havulinna ja se on lisensoitu [Creative Commons BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/) -lisenssillä.

<script src="/tocbot/tocbot.min.js"></script>
<script src="/scripts.js"></script>
<link rel="stylesheet" href="/tocbot/tocbot.css">