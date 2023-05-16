---
title: Olioiden vertaileminen
layout: default
nav_order: 11
---

# Olioiden vertaileminen
{: .no_toc }

Tällä oppitunnilla tutustumme tarkemmin olioiden yhtäsuuruuden ja suuruusjärjestyksen vertailemiseen. Kuten merkkijonoja käsitellessämme huomasimme, olioiden vertailu `==`-operaatiolla vertailee, ovatko kaksi oliota **samat** eikä olioiden sisältöä. Tämän oppitunnin aikana toteutamme omia vertailumetodeja, jotka toimivat myös Javan valmiiden metodien kanssa.
{: .fs-5 }

---

## Sisällysluettelo
{: .no_toc .text-delta }

* Sisällysluettelo
{:toc}

# Oppitunnin videot

Videoiden katsominen edellyttää kirjautumista MS Stream -palveluun Haaga-Helian käyttäjätunnuksellasi ja liittymistä kurssin Teams-ryhmään.

## [Olioiden vertailu: equals-metodi](https://web.microsoftstream.com/video/5900cbc8-bdf8-4398-9d36-5d54890eaad9) *38:34*

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/5900cbc8-bdf8-4398-9d36-5d54890eaad9?autoplay=false&showinfo=true" allowfullscreen style="border:none;"></iframe>

[Videolla esiintyvät lähdekoodit](https://github.com/ohjelmointi1/ohjelmointi1-3012/tree/main/src/viikko06/)


## [Olion tyypin selvittäminen ja tyyppimuunnokset](https://web.microsoftstream.com/video/e0f9ab75-4957-4286-9170-913cf835d1e8) *15:55*

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/e0f9ab75-4957-4286-9170-913cf835d1e8?autoplay=false&showinfo=true" allowfullscreen style="border:none;"></iframe>

[Videolla esiintyvät lähdekoodit](https://github.com/ohjelmointi1/ohjelmointi1-3012/tree/main/src/viikko06/)


## [Olioiden järjestäminen ja compareTo-metodi](https://web.microsoftstream.com/video/5ac62905-079c-4bcd-9fd5-470c1974518c) *37:11*

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/5ac62905-079c-4bcd-9fd5-470c1974518c?autoplay=false&showinfo=true" allowfullscreen style="border:none;"></iframe>

[Videolla esiintyvät lähdekoodit](https://github.com/ohjelmointi1/ohjelmointi1-3012/tree/main/src/viikko06/)


# Olioiden vertaileminen

Kuten merkkijonoja käsiteltäessä huomasimme, merkkijonojen vertailu `==`-operaattorilla vertailee olioviittauksia eikä merkkijonojen sisältöä:

```java
public class OlioidenVertailu {

    public static void main(String[] args) {
        String hauki1 = new String("Hauki");
        String hauki2 = new String("Hauki");

        // vertailee olioviittauksia eikä merkkijonojen sisältöä:
        System.out.println(hauki1 == hauki2); // tulostaa false

        // equals-metodi vertailee merkkijonojen sisältöä:
        System.out.println(hauki1.equals(hauki2)); // tulostaa true
    }
}
```

Merkkijonoja vertaillaankin aina joko `equals`- tai `equalsIgnoreCase`-metodilla. Entä jos haluaisimme vertailla itse kirjoittamamme `Tuote`-luokan olioita?

```java
public class Tuote {
    private String nimi;

    public Tuote(String nimi) {
        this.nimi = nimi;
    }
}
```

Törmäämme `Tuote`-oliolla samaan ongelmaan, että niiden vertailu yhtäsuuruusoperaattorilla tuottaa tuloksen `false`:

```java
Tuote maito1 = new Tuote("Maito");
Tuote maito2 = new Tuote("Maito");

// vertailee ovatko oliot samat:
System.out.println(maito1 == maito2); // false
```

`maito1 == maito2`-vertailu ei toimi, koska operaatio vertailee **ovatko oliot samat**, eikä huomioi olioiden sisältöä lainkaan.


# Equals-metodi

Merkkijonojen yhteydessä käyttämämme `equals`-metodi on määritetty Javassa automaattisesti kaikille luokille. Vaikka emme ole määritelleet `Tuote`-luokkaan `equals`-metodia, voimme silti kutsua sitä:

```java
// käyttää Javan valmista equals-metodia:
System.out.println(maito1.equals(maito2)); // false
```

Toisin kuin `String`-luokan kanssa, `equals`-metodi tuottaa nyt `false`, vaikka olioiden sisältö on täysin sama. Tämä johtuu siitä, että `equals`-metodi toimii oletuksena samalla logiikalla kuin `==`:

> *"The equals method for class Object implements the most discriminating possible equivalence relation on objects; that is, for any non-null reference values x and y, this method returns true if and only if x and y refer to the same object (x == y has the value true)."*
>
> Oracle. [Java API: Object](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Object.html#equals(java.lang.Object))

Jos haluamme että omien `Tuote`-olioiden vertailu `maito1.equals(maito2)` vertailee olioiden sisältöä, voimme toteuttaa oman `equals`-metodin!

{: .huom }
Omaa equals-metodia käsitellään tarkemmin [Helsingin yliopiston MOOC-kurssilla](https://ohjelmointi-20.mooc.fi/osa-8/3-olioiden-samankaltaisuus), jossa voit perehtyä olioiden samankaltaisuuden vertailuun tarkemmin.


## Oman equals-metodin toteuttaminen (edistynyttä sisältöä 🌶️)

Edellä esitetty `maito1.equals(maito2)`-vertailu ei toimi, koska `equals`-metodi vertailee oletuksena olioita samalla tavalla kuin `==`. Voimme kuitenkin määritellä aivan oman tapamme vertailla `Tuote`-olioita määrittelemällä oman `equals`-metodin, joka tarkastaa esimerkiksi tässä tapauksessa onko tuotteella sama nimi kuin toisella tuotteella.

```java
public class Tuote {
    private String nimi;

    public Tuote(String nimi) {
        this.nimi = nimi;
    }

    public String getNimi() {
        return this.nimi;
    }

    @Override
    public boolean equals(Object toinen) {
        // TODO: palaute true tai false riippuen Tuotteen nimestä
        return false;
    }

    @Override
    public String toString() {
        return "Tuote [nimi=" + nimi + "]";
    }
}
```

Huomaa, että `equals`-metodi ylikirjoittaa Javan standardikirjaston metodin, minkä vuoksi sen otsikon on oltava täsmälleen samanlainen kuin standardikirjastossa: `public boolean equals(Object toinen)`. Metodin on siis oltava julkinen oliometodi (ei static), joka palauttaa totuusarvon ja saa parametrinaan minkä tahansa toisen olion.

Metodeja korvattaessa on hyvä käytäntö lisätä metodin ylle `@Override`-**annotaatio**, joka toimii sekä dokumentaationa metodin korvaamisesta että Java-kääntäjän ohjeena varmistaa, että metodi korvattiin onnistuneesti. Tämä annotaatio on meille tuttu aikaisemmilta oppitunneilta myös `toString`-metodin yhteydestä.

{: .warning }
Huomaa, että metodille annettu `Object toinen` olio ei välttämättä ole toinen `Tuote`-olio, vaan se voi olla mikä tahansa olio:

```java
@Override
public boolean equals(Object toinen) {
    // TODO: palaute true tai false riippuen Tuotteen nimestä
    return false;
}
```

### Tyyppimuunnos ja instanceof

Mikäli olion tyypistä ei voida olla varmoja, niiden tyyppi voidaan tarkastaa Javassa `instanceof`-operaatiolla:

```java
if (toinen instanceof Tuote) {
    // TODO: palaute true tai false riippuen Tuotteen nimestä
    return false;
}
```

Mikäli yllä `toinen instanceof Tuote` tuottaa arvon `true`, tiedämme varmuudella, että annettu vertailtava olio on myös `Tuote`.

Emme voi kuitenkaan suoraan käsitellä saatua oliota tuotteena tai asettaa sitä muuttujaan, koska Java-kääntäjän näkökulmasta olio on yhä `Object`-tyyppiä eikä `Tuote`. Tiedämme kuitenkin varmuudella, että toinen olio on `Tuote`, joten voimme tehdä ns. tyyppimuunnoksen:

```java
Tuote toinenTuote = (Tuote) toinen;
```

{: .huom }
Tyyppimuunnos ei oikeasti muuta käsiteltävää oliota toisen tyyppiseksi. Se on vain keino kertoa Java-kääntäjälle, että kyseistä arvoa tulee käsitellä tietyn tyyppisenä.

Nyt kun sekä `this` että `toinenTuote` ovat `Tuote`-olioita, voimme vertailla niiden sisältöä toisiinsa:

```java
@Override
public boolean equals(Object toinen) {
    if (toinen instanceof Tuote) {
        Tuote toinenTuote = (Tuote) toinen;
        return this.nimi.equalsIgnoreCase(toinenTuote.nimi);

    } else {
        // ei ollut Tuote-olio, joten palautetaan false
        return false;

    }
}
```

```java
Tuote maito1 = new Tuote("Maito");
Tuote maito2 = new Tuote("Maito");
Tuote kauramaito = new Tuote("Kauramaito");

System.out.println(maito1.equals(maito2));      // true
System.out.println(maito1.equals(kauramaito));  // false
```

Oman luokkamme `equals` toimii nyt aivan kuten Javan valmiiden luokkien metodit, joten sitä voidaan kutsua itse kuten yllä. Se toimii myös automaattisesti Javan valmiiden metodien yhteydessä, kuten seuraavassa kappaleessa "Mihin tarvitsemme olioiden vertailua?" todetaan.


{: .huom }
[Javan uusimmissa versioissa](https://docs.oracle.com/en/java/javase/15/language/pattern-matching-instanceof-operator.html) `instanceof`-operaatiota on jatkokehitetty siten, että tarkastuksen jälkeen voidaan suoraan määritellä muuttuja, johon automaattisesti sijoitetaan tarkastettu olio, mikäli se läpäisi tarkastuksen. Näin edellä kirjoitettu koodi voidaan kirjoittaa ilman erillistä tyyppimuunnosta:

```java
if (toinen instanceof Tuote t) {
    return this.nimi.equalsIgnoreCase(t.nimi);
}
```

Yllä `t`-muuttuja viittaa samaan olioon kuin `toinen`, mutta muuttujan tyyppi on `Tuote` eikä `Object`. Näin `t.nimi` toimii suoraan if-lohkon sisällä ilman erillisiä tyyppimuunnoksia.

{: .warning}
Huom! Yllä esitetty uudempi syntaksi ei välttämättä toimi Viopen Java-versiossa.

# Mihin tarvitsemme olioiden vertailua?

Olioiden vertailulle ja `equals`-metodille on Javan standardikirjastossa paljon muutakin käyttöä kuin kahden muuttujan arvojen vertailu. `equals`-metodia hyödynnetään mm. etsiessä olioita listoilta:

```java
Tuote leipa = new Tuote("Leipä");
List<Tuote> tuotteet = List.of(new Tuote("Maito"), new Tuote("Piimä"), new Tuote("Leipä"));

boolean sisaltaaLeivan = tuotteet.contains(leipa);
System.out.println(sisaltaaLeivan); // true
```

`contains`-metodi kutsuu sisäisesti listan `indexOf`-metodia, joka selvittää etsittävän olion sijainnin listalla kutsumalla vuorollaan jokaisen listalla olevan olion `equals`-metodia:

```java
// Copyright (c) 2016, 2018, Oracle and/or its affiliates. All rights reserved.
for (int i = 0, s = size(); i < s; i++) {
    if (o.equals(get(i))) {
        return i;
    }
}
```

Lähde: [AdoptOpenJDK. GitHub.com](https://github.com/AdoptOpenJDK/openjdk-jdk12u/blob/master/src/java.base/share/classes/java/util/ImmutableCollections.java#L169)


Toteuttamamme `equals`-metodi toimii siis nyt yhdessä `contains`-metodin sekä `indexOf`-metodin kanssa ja leipä löytyy listalta. Jos emme olisi toteuttaneet omaa `equals`-metodia, edellä esitetty koodi ei toimisi, koska kyseessä on kaksi eri oliota.


```java
public class TuoteOhjelma {

    public static void main(String[] args) {
        Tuote maito1 = new Tuote("Maito");
        Tuote maito2 = new Tuote("Maito");

        System.out.println(maito1);
        System.out.println(maito2);

        System.out.println("Vertailuoperaattori: " + (maito1 == maito2)); // false, koska maito1 on eri olio kuin maito2
        System.out.println("equals: " + maito1.equals(maito2)); // palauttaa nyt true, koska toteutimme equals-metodin

        // MUITA HYÖTYJÄ EQUALS-METODISTA:

        List<Tuote> tuotteet = List.of(maito1, new Tuote("Leipä"), new Tuote("Piimä"));

        // Listoilta hakeminen käyttää taustalla equals-metodia:
        boolean onLeipa = tuotteet.contains(new Tuote("Leipä"));

        // Indeksin etsiminen käyttää taustalla equals-metodia:
        int piimaIndeksi = tuotteet.indexOf(new Tuote("Piimä"));

        System.out.println("contains: " + onLeipa); // Toimii! => true
        System.out.println("indexOf: " + piimaIndeksi); // Toimii => 2
    }
}
```

Tätä aihetta käsitellään tarkemmin [Helsingin yliopiston MOOC-kurssilla](https://ohjelmointi-20.mooc.fi/osa-8/3-olioiden-samankaltaisuus), jossa voit perehtyä olioiden samankaltaisuuden vertailuun tarkemmin.


# Olioiden järjestäminen listalla

Listoja ja taulukoita käsitellessämme olemme huomanneet, että `Collections.sort` sekä `Arrays.sort` osaavat automaattisesti järjestää Javan standardikirjaston olioita, kuten merkkijonoja, numeroita ja päivämääriä, sisältäviä listoja. Tällä kerralla perehdymme siihen, miksi omat oliomme eivät asetu automaattisesti järjestykseen, ja miten voimme määritellä oman luokkamme olioille luonnollisen järjestyksen.


## Järjestäminen ja Collections.sort

Oletetaan, että meillä on lista, jossa on neljä nimeä sekajärjestyksessä:

```java
List<String> nimet = Arrays.asList("Maija", "Matti", "Arja", "Aatami");
```

Tiedämme aikaisempien oppituntien perusteella, että Javassa on valmiina tapa vertailla ja järjestellä olioita:

```java
Collections.sort(nimet);

// Nimet ovat nyt aakkosjärjestyksessä:
System.out.println(nimet); // [Aatami, Arja, Maija, Matti]
```

Nimet oli helppoa laittaa järjestykseen `Collections.sort`-metodin avulla!


## Miten Java järjesti oliot?

`Collections.sort` osasi järjestää merkkijonot kasvavaan järjestykseen, koska `String`-luokka on yhteensopiva `Comparable`-tyypin kanssa. Kaikki `Comparable`-oliot osaavat vertailla omaa järjestystään suhteessa toiseen saman luokan olioon.

[Comparable-tyypin dokumentaatiosta](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Comparable.html) löydämme listan kaikista standardikirjaston luokista, jotka ovat järjestettävissä (kohta All Known Implementing Classes). `Collections.sort` osaa siis asetella merkkijonojen lisäksi liki 200 muutakin tyyppiä oikeaan järjestykseen automaattisesti.


## compareTo-metodi

Kaikkiin `Comparable`-luokkiin on tehty valmiiksi `compareTo`-niminen metodi, jonka avulla voidaan vertailla kahden olion keskenäistä järjestystä. `Collections.sort` kutsuu sisäisesti jokaisen merkkijonon  `compareTo`-metodia ja järjestää arvot vertailujen tulosten mukaan.

Voimme halutessamme myös itse kutsua `compareTo`-metodia ja tutkia sen tuloksia:

```java
String eka = "Maija";
String toka = "Aatami";

// Kutsutaan String-luokan compareTo-metodia:
int tulos = eka.compareTo(toka);

System.out.println(tulos); // tulostaa 12
```

`compareTo` palauttaa aina kokonaisluvun, josta päätellään, kumpi arvoista tulee järjestyksessä ensin:

> *"Compares this object with the specified object for order. Returns a negative integer, zero, or a positive integer as this object is less than, equal to, or greater than the specified object."*
>
> Oracle. [Java API: Comparable](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Comparable.html).

Vapaasti suomennettuna, vertailulogiikka toimii seuraavasti:

* Jos se olio, jonka metodia kutsuttiin on järjestyksessä ensin, `compareTo` palauttaa **negatiivisen luvun**.
* Jos parametrina annettu olio on järjestyksessä ensin, `compareTo` palauttaa **positiivisen luvun**.
* Muussa tapauksessa **palautetaan 0**.

Edellä oleva rivi `"Maija".compareTo("Aatami")` palauttaa arvon **12**, eli `"Maija"` on aakkosissa `"Aatami"`:n jälkeen. Seuraavat esimerkit näyttävät kaikki kolme erilaista tulosta:

```java
System.out.println("apple".compareTo("xerox")); // -23 on negatiivinen, eli a tulee ennen x:ää
System.out.println("windows".compareTo("bitcoin")); // 21 on positiivinen, eli w tulee b:n jälkeen
System.out.println("tesla".compareTo("tesla")); // tulos on nolla, eli merkkijonot ovat "yhtäsuuret"
```

Vertailun tulosta voidaan käyttää kuin mitä tahansa arvoa:

```java
String eka = "Kilo";
String toka = "Gramma";

int tulos = eka.compareTo(toka);

if (tulos < 0) {
    System.out.println(eka + " < " + toka);
} else if (0 < tulos) {
    System.out.println(eka + " > " + toka);
} else {
    System.out.println(eka + " == " + toka);
}
```

Edellä esitetyillä arvoilla yllä oleva koodi tulostaa `Kilo > Gramma`.


# Omien olioiden järjestäminen

Jos yritämme järjestää oman `Tuote`-luokan oliot `Collections.sort`-metodin avulla, saamme seuraavan virheilmoituksen:

> The method sort(List&lt;T&gt;) in the type Collections is not applicable for the arguments (List&lt;Tuote&gt;)

Tämä johtuu siitä, että **luokkamme ei ole yhteensopiva `Comparable`-tyypin kanssa**. `Collections.sort`-metodi ei siis pysty vertailemaan olioitamme keskenään.

Onneksi olioiden vertailemiseksi voimme määritellä myös vaihtoehtoisia vertailuoperaatioita.


## Vaihtoehtoiset vertailuoperaatiot Collections.sort-metodilla

Merkkijonojen vertailu `compareTo`-metodilla ei huomioi luonnostaan oikein eri kirjainkokoja tai eri kielissä olevia paikallisia merkkejä (ä, ö, å):

```java
List<String> nesteet = Arrays.asList("maito", "Vesi", "ketsuppi", "bensa", "Limu");
Collections.sort(nesteet);

System.out.println(nesteet); // Väärin: [Limu, Vesi, bensa, ketsuppi, maito]
```

Onneksi `String`-luokasta löytyy tähän tarkoitukseen sopiva valmis `compareToIgnoreCase`-metodi. Kun haluamme käyttää tätä metodia oletusmetodin sijasta, voimme määritellä vertailussa käytettävän metodin `Collections.sort`-kutsun toisena parametrina:

```java
// kerrotaan, että vertailussa halutaan käyttää String-luokan compareToIgnoreCase-metodia:
Collections.sort(nesteet, String::compareToIgnoreCase);

System.out.println(nesteet); // oikea aakkosjärjestys: [bensa, ketsuppi, Limu, maito, Vesi]
```

Yllä `Collections.sort`-metodille annetaan toisena parametrina `String::compareToIgnoreCase`, joka on ns. **metodiviittaus**. Metodiviittauksessa esiintyy ensin luokan nimi, sitten kaksi kaksoispistettä `::` ja lopuksi metodin nimi. Huomaa, että metodia **ei suoriteta** omassa koodissa, vaan se annetaan parametrina. **Siksi metodin nimen jälkeen ei kirjoiteta sulkuja** `()`.

Metodiviittauksen avulla `sort` käyttää vertailemiseen antamaamme metodia oletuksena olevaa `compareTo`-metodia. Lue lisää osoitteesta: [https://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html](https://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html)


## Listan järjesteleminen omilla luokilla (edistynyttä sisältöä 🌶️)

Vaikka oma `Tuote`-luokkamme ei ollut sellaisenaan yhteensopiva `Collections.sort`-metodin kanssa, voimme ohittaa tämän ongelman antamalla listan lisäksi vertailuoperaation.

Tutustu Javan `Comparator.comparing`-metodiin, jonka avulla voit määritellä vertailijan kutsumaan mitä tahansa oman luokkasi metodia olioiden järjestämiseksi: [https://www.baeldung.com/java-8-comparator-comparing](https://www.baeldung.com/java-8-comparator-comparing). Tällä kurssilla sinun kannattaa lukea artikkelista kohta [3.1. Key Selector Variant](https://www.baeldung.com/java-8-comparator-comparing#1-key-selector-variant) ja sitä aikaisemmat, mutta ei välttämättä tätä kohtaa pidemmälle.

`Comparator.comparing`-metodille voidaan antaa metodiviittaus mihin tahansa metodiin, jolloin `sort` käyttää vertailussa juuri tuon metodin palauttamia arvoja. Voisimme sen avulla esimerkiksi järjestää merkkijonot pituusjärjestykseen vertailemalla merkkijonojen pituuksia, jotka selviävät `length()`-metodin avulla: `Comparator.comparing(String::length)`:

```java
// tehdään järjestely merkkijonojen length-metodin mukaan:
Collections.sort(nesteet, Comparator.comparing(String::length));

System.out.println(nesteet); // kasvava pituusjärjestys: [Limu, Vesi, bensa, maito, ketsuppi]
```

Jos haluaisit järjestää `Tuote`-oliot vastaavasti niiden `nimi`-arvojen mukaiseen kasvavaan järjestykseen, se onnistuisi antamalla metodiviittaus `Tuote::getNimi`:

```java
Collections.sort(tuotteet, Comparator.comparing(Tuote::getNimi));
```

<!--### Contact-olioiden järjesteleminen nimen mukaan (edistynyttä sisältöä 🌶️)

Toteuta nyt kurssin esimerkkiprojektiin `Contact`-olioiden järjestäminen aakkosjärjestykseen nimen mukaan siten, että `Comparator.comparing`-metodi saa parametrinaan metodiviittauksen `Contact`-luokan `getName`-metodiin. Älä turhaan huolehdi nimien kirjainkoosta, niiden huomioiminen tekee tehtävästä astetta haastavamman.


## Esimerkki kokonaisuudessaan

```java
import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class OlioidenJarjestaminen {

    public static void main(String[] args) {
        // Nimet epäjärjestyksessä:
        List<String> nimet = Arrays.asList("Marja-Liisa Kirvesniemi", "Kaisa Mäkäräinen", "Krista Pärmäkoski");

        Collections.sort(nimet); // järjestää nimet compareTo-metodin avulla
        System.out.println(nimet); // tulostaa [Kaisa Mäkäräinen, Krista Pärmäkoski, Marja-Liisa Kirvesniemi]

        List<Tuote> tuotteet = Arrays.asList(new Tuote("Maito"), new Tuote("Leipä"), new Tuote("Piimä"));
        // Collections.sort ei toimi Tuote-olioiden kanssa, koska Tuote ei ole yhteensopiva Comparable-tyypin kanssa!
        // Collections.sort(tuotteet); // => KÄÄNNÖSVIRHE


        // Merkkijonot puolestaan ovat yhteensopivia "Comparable"-tyypin kanssa ja niillä on compareTo-metodi:
        int tulos = "Marja-Liisa".compareTo("Kaisa Mäkäräinen");

        System.out.println(tulos); // tulostaa 2. Positiivinen luku tarkoittaa, että 'this' tulee toisen jälkeen.
        System.out.println("a".compareTo("b")); // -1, eli 'this' on ennen toista merkkijonoa
        System.out.println("x".compareTo("x")); // 0, eli ovat samassa kohdassa

        // Kokeillaan järjestellä lista eri kokoisia kirjaimia:
        List<String> kirjaimet = Arrays.asList("b", "A", "X", "w");

        Collections.sort(kirjaimet); // Järjestää compareTo-metodilla
        System.out.println(kirjaimet); // Kirjainkoko aiheuttaa bugeja: [A, X, b, w] => VÄÄRÄ JÄRJESTYS

        // Miten vertailut toimivat yllä?
        System.out.println("X".compareTo("b")); // -10, negatiivinen eli iso X tulee ennen pientä b:tä (virhe)
        System.out.println("X".compareToIgnoreCase("b")); // 22, positiivinen eli compareToIgnoreCase toimii!

        // Kerrotaan Collections.sort-metodille, että käytä compareToIgnoreCase:a
        Collections.sort(kirjaimet, String::compareToIgnoreCase); // String::compareToIgnoreCase on metodiviittaus

        // Nyt vertailu tehtiin kirjainkosta riippumatta:
        System.out.println(kirjaimet); // [A, b, w, X], eli vertailu toimi!

        // Miten järjestellään nimen pituuden mukaan?
        // Kerrotaan Comparator-oliolle, että vertailee length-metodin tulosten mukaan!
        Collections.sort(nimet, Comparator.comparing(String::length)); // String::length on metodiviittaus

        // Nimet on nyt järjestetty merkkijonon pituuden mukaan:
        System.out.println(nimet); // Kaisa Mäkäräinen, Krista Pärmäkoski, Marja-Liisa Kirvesniemi
    }
}
```-->





