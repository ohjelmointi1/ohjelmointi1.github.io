---
title: Merkkijonot
layout: default
nav_order: 4
---

# Merkkijonot

Merkkijonot ovat meille jo aikaisemmilta oppitunneita tuttua tekstidataa. Merkkijonot ovat "alkeistietotyypeistä" poiketen olioita, eli niillä on metodeja, joiden avulla merkkijonojen sisältöä voidaan käsitellä hyvin monipuolisesti.

Tällä oppitunnilla tutustumme merkkijonojen metodeihin ja merkkijonojen vertailuun.

* Sisällysluettelo
{:toc}



# String-luokka

Kuten olemme aiemmin todenneet, merkkijonot ovat tyyppiä `String`. String on **luokka** ja yksittäiset merkkijonot ovat **olioita**. Merkkijonoja voidaan luoda kirjoittamalla sisältö suoraan lainausmerkkeihin `"esimerkki"` tai lukemalla niitä esimerkiksi Scannerin avulla: `lukija.nextLine()`.

Koska merkkijonot ovat olioita, niitä ei voida vertailla vertailuoperaattorilla `==`. Vertailu `merkkijono1 == merkkijono2` ei vertaile merkkijonojen sisältämiä merkkejä, vaan sitä, ovatko molemmat merkkijonot **sama** merkkijono muistissa. Kaksi sisällöltään samanlaista merkkijonoa tuottavat siis pääsääntöisesti vertailussa epätosia arvoja.

Vertailuoperaattorin sijaan merkkijonojen vertailu voidaan tehdä `String`-luokan metodeilla, joita käsittelemme seuraavaksi.

## [Oppitunnin videotallenne: Merkkijonojen vertailu, metodit ja Eclipsen debuggeri](https://web.microsoftstream.com/video/8d6bbb56-51f0-48f5-8110-ccde31d19342) *23:51*

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/8d6bbb56-51f0-48f5-8110-ccde31d19342?autoplay=false&amp;showinfo=true" allowfullscreen style="border:none;"></iframe>

Tällä videolla käsitellään merkkijonojen vertailua sekä vertailuoperaattorilla (`==`) että `equals`-metodilla. Opettelemme myös tutustumaan ohjelman vaiheittaisiin suoritukseen Eclipsen debug-työkalun avulla. Videolla editoitava tiedosto löytyy GitHubista: [Puujalkavitsi.java](https://github.com/ohjelmointi1/ohjelmointi1-3015/blob/main/src/viikko02/merkkijonot/Puujalkavitsi.java)


## Olioiden vertailu: equals ja equalsIgnoreCase

Olioita vertailtaessa yhtäsuuruusoperaatio `==` vertailee, onko kyseessä __sama olio__. Se ei siis vertaile olioiden sisältöä, eli tässä tapauksessa merkkijonon merkkejä. **Samansisältöiset merkkijonot ovat siis samoja ainoastaan silloin, kun vertaillaan tiettyä merkkijono-oliota itseensä.**

Merkkijonoja vertaillaan siksi aina `equals`- ja `equalsIgnoreCase` –metodeilla, jotka vertailevat merkkijonojen sisältöjä. Molemmat vertailumetodit palauttavat aina totuusarvon `true` tai `false`.

```java
String vastaus = lukija.nextLine(); // "Kyllä"

// equals-metodi vertailee, ovatko merkkijonot sisällöltään samat:
if (vastaus.equals("kyllä")) {
     // tätä lohkoa ei suoriteta, koska kirjainkoko ei täsmää
}

// equalsIgnoreCase-metodi ei huomioi kirjainkokoa:
if (vastaus.equalsIgnoreCase("kyllä")) {
     // tämä lohko suoritetaan!
}
```



## Merkkijonojen metodien käyttäminen

Merkkijonojen metodit on määritetty Javan [String-luokassa](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html).

Merkkijonojen metodeja voidaan kutsua suoraan merkkijonolle tai muuttujien avulla:

```java
int pituus = "mikä on tämän merkkijonon pituus?".length();  // 33
String isolla = "muuta tämä isoksi".toUpperCase();          // "MUUTA TÄMÄ ISOKSI"
String pienella = "Muuta Tämä Pieneksi".toLowerCase();      // "muuta tämä pieneksi"
String trimmattu = "  poista tyhjät alusta ja lopusta  ".trim(); // "poista tyhjät alusta ja lopusta"

String tilinumero = "    fi3315723000500504  ".trim().toUpperCase(); // "FI3315723000500504"
```

Huomaa, että mikään yllä olevista metodeista ei muuta alkuperäistä merkkijonoa, vaan ne palauttavat uuden merkkijonon.


## [Videotallenne: String-luokan metodit: length, substring...](https://web.microsoftstream.com/video/c1991f30-5797-45e7-8030-a24ecb751064) *20:11*

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/c1991f30-5797-45e7-8030-a24ecb751064?autoplay=false&amp;showinfo=true" allowfullscreen style="border:none;"></iframe>

Tällä videolla käsittelemme merkkijonojen indeksejä, pilkkomista, yhdistelyä sekä pituuksia. Videolla käsiteltävä tiedosto löytyy GitHubista: [Numeronyymit.java](https://github.com/ohjelmointi1/ohjelmointi1-3015/blob/main/src/viikko02/merkkijonot/Numeronyymit.java)

## Muuttumattomuus (immutability)

Merkkijonot ovat muuttumattomia, eli kerran luotua **merkkijonoa ei voi muuttaa**. `String`-luokan metodit eivät koskaan muuta alkuperäistä merkkijonoa, vaan luovat niistä kopioita. Uusi merkkijono voidaan tosin asettaa samaan muuttujaan, jolloin se korvaa vanhan arvon:

```java
String text = "hello";
text.toUpperCase();

System.out.println(text);  // tulostaa "hello" (alkuperäinen merkkijono ei muuttunut)

text = text.toUpperCase(); // otetaan uusi merkkijono talteen samaan muuttujaan
System.out.println(text);  // tulostaa "HELLO"
```

## Merkkijonon osajonot

Merkkijonosta halutaan usein lukea jokin tietty osa. Tämä onnistuu metodilla `substring`. `substring`-metodia voidaan käyttää kahdella tavalla:

1. yksiparametrisena palauttamaan merkkijonon loppuosa: `"abcd".substring(2)`
1. kaksiparametrisena palauttamaan parametrien määrittelemä osajono merkkijonosta: `"abcd".substring(1, 3)`

**Merkkijonojen indeksit alkavat aina nollasta!** Substring-metodin ensimmäinen parametri tarkoittaa ensimmäistä indeksiä, joka otetaan mukaan osamerkkijonoon, kun taas toinen parametri on ensimmäinen uuden merkkijonon ulkopuolelle jäävä indeksi.

Parametriarvoilla `(5, 10)` saadaan siis merkit indekseistä **5, 6, 7, 8 ja 9**.

Koska substring-metodin paluuarvo on tyyppiä `String`, voidaan metodin paluuarvo ottaa talteen `String`-tyyppiseen muuttujaan:

```java
String rekisterinumero = "AKU-313";
// indeksit:              0123456

System.out.println(rekisterinumero.substring(0, 3)); // merkit indekseistä 0, 1, ja 2: "AKU"
System.out.println(rekisterinumero.substring(4));    // merkkijonon loppu alkaen indeksistä 4: "313"
```

Yllä indeksi `3` on kovakoodattu, mikä aiheuttaa bugeja, kun rekisterinumerossa on alle kolme kirjainta. Viivan paikka kannattaakin selvittää ohjelmallisesti hyödyntämällä merkkijonojen `indexOf`-metodia:

```java
String rekisterinumero = "LOL-2";

int viiva = rekisterinumero.indexOf("-");               // 3

String alkuosa = rekisterinumero.substring(0, viiva);   // "LOL"
String loppuosa = rekisterinumero.substring(viiva + 1); // "2"
```

## [Videotallenne: Merkkijonojen muuttaminen, muuttumattomuus ja satunnaisen salasanan generointi](https://web.microsoftstream.com/video/78f6744a-2dc0-4708-9aac-fcf0cdd49c12) *20:28*

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/78f6744a-2dc0-4708-9aac-fcf0cdd49c12?autoplay=false&amp;showinfo=true" allowfullscreen style="border:none;"></iframe>

Tällä videolla sovellamme merkkijonojen käsittelyä yhdessä toistorakenteen kanssa, ja luomme satunnaisia salasanoja generoivan [Salasana.java](https://github.com/ohjelmointi1/ohjelmointi1-3015/blob/main/src/viikko02/merkkijonot/Salasana.java)-luokan.


## Moniriviset merkkijonot (text blocks)

Javan uusimmissa versioissa on mahdollista määritellä kätevästi monirivisiä merkkijonoja kolmen lainausmerkin `"""` avulla:

```java
String ostoslista = """
    Ostoslista:
    - maitoa
    - leipää
    - juustoa
    - kahvia""";

System.out.println(ostoslista);
```

Java osaa jättää huomiotta monirivisten merkkijonojen sisennykset, joten yllä oleva esimerkkikoodi tulostaa ostoslistan seuraavasti:

```
Ostoslista:
- maitoa
- leipää
- juustoa
- kahvia
```

Javan vanhemmilla versioilla voit kirjoittaa vain yksirivisiä merkkijonoja, joissa rivinvaihdot on merkitty `\n`-rivinvaihtomerkeillä (esitellään tällä sivulla alempana).


# String-luokan metodeja

Tutustu metodeihin tarkemmin täällä: [https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html)

Tyyppi, nimi ja parametrit        | Kuvaus
----------------------------------| ------------
`char charAt(int index)`          | Yksittäinen kirjain tietystä indeksistä
`public boolean startsWith(String prefix)`  | Tarkistaa alkaako merkkijono täsmälleen annetuilla merkeillä
`public boolean endsWith(String suffix)`    | Tarkistaa päättyykö merkkijono täsmälleen annettuihin merkkeihin
`boolean contains(String s)`      | Tarkistaa onko annettu merkkijono osa tätä merkkijonoa
`int indexOf(String str)`         | Antaa indeksin, josta osamerkkijono löytyy, **tai -1 jos ei löydy**
`int length()`                    | Merkkijonon pituus
`boolean matches(String regex)`   | Tarkistaa vastaako merkkijono annettua säännöllistä lauseketta
`String replace(CharSequence target, CharSequence replacement)` | Korvaa kaikki ensimmäistä annettua osaa vastaavat kohdat jälkimmäisellä
`String[] split(String regex)`    | Pilkkoo merkkijonon taulukoksi annetun säännöllisen lausekkeen kohdilta
`String substring(int beginIndex)`| Palauttaa merkkijonon annetusta indeksistä loppuun
`String substring(int beginIndex, int endIndex)` | Palauttaa merkkijonon annetusta alkuindeksistä (loppuindeksi - 1):een
`String toLowerCase()`            | Muuttaa merkkijonon kaikki kirjaimet pieniksi
`String toUpperCase()`            | Muuttaa merkkijonon kaikki kirjaimet ISOIKSI
`String trim()`                   | Poistaa sekä alusta että lopusta kaikki tyhjät merkit

Muista, että merkkijonojen metodit eivät koskaan muuta kyseistä merkkijonoa, vaan ne palauttavat uusia merkkijonoja.

## Esimerkkejä merkkijonojen metodeista

```java
public class MerkkijonojenMetodit {

    public static void main(String[] args) {
        String osoite = "https://ohjelmointi1.github.io/";
        String kurssikoodi = "swd4tn032-3099";


        boolean onSuojattu = osoite.startsWith("https://");
        System.out.println("Suojattu: " + onSuojattu);


        int valiviiva = kurssikoodi.indexOf("-");
        String opintojakso = kurssikoodi.substring(0, valiviiva);
        System.out.println("Opintojakso: " + opintojakso.toUpperCase());


        String toteutusnumero = kurssikoodi.substring(valiviiva + 1);
        System.out.println("Toteutusnumero: " + toteutusnumero);


        boolean ohjelmistotuotanto = kurssikoodi.toLowerCase().contains("swd");
        System.out.println("Ohjelmistotuotanto: " + ohjelmistotuotanto);
    }
}
```

Yllä oleva koodi tulostaa seuraavaa:

```
Suojattu: true
Opintojakso: SWD4TN032
Toteutusnumero: 3099
Ohjelmistotuotanto: true
```

## Esimerkki metodikutsujen ketjuttamisesta

Monet metodit, kuten `replace`, palauttavat uusia merkkijonoja. Metodin palauttamille merkkijonoille voidaan kutsua uusia metodeja suoraan ns. "ketjuttamalla":

```java
public class HymioidenMuuttaminenEmojiksi {

    public static void main(String[] args) {

        // Seuraava `replace` kutsutaan aina edellisen operaation palauttamalle
        // merkkijonolle. Tätä kutsutaan "ketjuttamiseksi":
        String teksti = "Hei :) Mitä kuuluu? :-P".replace(":)", "😄")
                .replace(":-P", "😜")
                .replace("xD", "😁")
                .replace(":(", "😒");

        System.out.println(teksti);
    }
}
```

Yllä olevassa esimerkissä `replace`-metodi korvaa yksitellen eri hymiöitä ja palauttaa aina uuden merkkijonon. Lopuksi viimeisen `replace`-kutsun tulos sijoitetaan `teksti`-muuttujaan.


# Yleiset erikoismerkit merkkijonoissa

Kaikkia erikoismerkkejä ei voida esittää sellaisenaan merkkijonoissa. Esimerkiksi lainausmerkki merkkijonon sisällä sekoittuisi merkkijonon päättävään lainausmerkkiin. Erikoismerkit täytyykin esittää erityisten kontrollimerkkien avulla.

[https://docs.oracle.com/javase/tutorial/java/data/characters.html](https://docs.oracle.com/javase/tutorial/java/data/characters.html)

Syntaksi       | Kuvaus
---------------| ------
\\t            | Insert a tab in the text at this point.
\\n            | Insert a newline in the text at this point.
\\"            | Insert a double quote character in the text at this point.
\\\\           | Insert a backslash character in the text at this point.

Rivinvaihtomerkin käyttäminen merkkijonossa:

```java
System.out.println("Ensimmäinen rivi\nToinen rivi");
```

```
Ensimmäinen rivi
Toinen rivi
```

Kenoviiva kirjoitetaan aina tuplana:

```java
String polku = "C:\\Users\\Minä\\Documents\\"; // C:\Users\Minä\Documents\
```


Lainausmerkkejä joudutaan käsittelemään usein merkkijonoissa, jotka sisältävät esimerkiksi HTML-elementtejä tai säännöllisiä lausekkeita:

```java
int hinta = 500;
System.out.println("<span class=\"hinta\">" + hinta + " €</span>");
```

```
<span class="hinta">500 €</span>
```

Tapauksesta riippuen kenoviivoja joudutaan joskus laittamaan hyvin monia peräkkäin:

[![Backslashes](https://imgs.xkcd.com/comics/backslashes.png)](https://xkcd.com/1638/)

Kuva: [XKCD, Backslashes](https://xkcd.com/1638/). Creative Commons Attribution-NonCommercial 2.5


# Lukujen poimiminen merkkijonoista

Scannerin avulla on kätevää lukea tekstistä erilaisia lukuja. Todellisuudessa kuitenkin suurin osa sovellusten käyttämästä datasta tulee jostain muualta kuin Scannerilta, joten tarvitaan myös muita tapoja lukea numeroita merkkijonoista.

Luettavan luvun tyypistä riippuen käytä joko `Integer.parseInt`- tai `Double.parseDouble`-metodia seuraavasti:

```java
int kokonaisluku = Integer.parseInt("123456");
double liukuluku = Double.parseDouble("12.3456");

String teksti = "123456";
int tekstiNumeroksi = Integer.parseInt(teksti);
```

# Yksittäiset kirjaimet: char

Javassa on erillinen `char`-tietotyyppi yksittäisiä merkkejä varten. Yksittäinen merkki aloitetaan ja lopetetaan heittomerkillä, esim. `'a'`. Yksittäiset merkit eivät ole olioita, eli niillä ei ole metodeja. Niiden pituus on aina 1, eli kahta tai useampaa merkkiä ei voida esittää char-tyypillä.

Merkkijonolta voidaan pyytää yksittäisiä merkkejä niiden indeksin perusteella. Tämä onnistuu metodilla `charAt(int indeksi)`, joka saa parametrina halutun merkin indeksin merkkijonossa.

Char-tietotyypin avulla voidaan tehdä alkeisoperaatioita, eli ikään kuin käsitellä niitä numeroina:

```java
for (char kirjain = 'a'; kirjain <= 'z'; kirjain++) {
    System.out.println(kirjain);
}
```

Käytännössä `char`-tyyppiä tarvitaan melko harvoin, ja usein onkin käytännöllisempää käsitellä yhden merkin pituisia merkkijonoja.

# Edistynyttä sisältöä: säännölliset lausekkeet, regular expressions / regex

> "Säännöllinen lauseke määrittelee joukon merkkijonoja tiiviissä muodossa. Säännöllisiä lausekkeita käytetään muunmuassa merkkijonojen oikeellisuuden tarkistamiseen. Merkkijonojen oikeellisuuden tarkastaminen tapahtuu luomalla säännöllinen lauseke, joka määrittelee merkkijonot, jotka ovat oikein."
>
> "Oikeellisuuden tarkistus säännöllisten lausekkeiden avulla tapahtuu ensin sopivan säännöllisen lausekkeen määrittelyn. Tämän jälkeen käytetään `String`-luokan metodia `matches`, joka tarkistaa vastaako merkkijono parametrina annettua säännöllistä lauseketta. Opiskelijanumeron tapauksessa sopiva säännöllinen lauseke on `01[0-9]{7}`"

*Lähde: Helsingin yliopiston Agile Education Research -tutkimusryhmän ohjelmointikurssi (Creative Commons BY-NC-SA)  [https://materiaalit.github.io/ohjelmointi-s17/part10/#section-19-saannolliset-lausekkeet](https://materiaalit.github.io/ohjelmointi-s17/part10/#section-19-saannolliset-lausekkeet)*


## "teksti".matches(String regex); // edistynyttä sisältöä

`matches`-metodi vertaa merkkijonoa annettuun säännölliseen lausekkeeseen ja palauttaa `true` tai `false` riippuen siitä, vastaako merkkijono lauseketta. Säännölliset lausekkeet (regular expression) ovat merkkijonoja, jotka muodostavat "kuvion" (pattern), jota vasten merkkijonoja verrataan.

Muutamia esimerkkejä selityksineen:

Regex                   | Esimerkki   | Selitys
------------------------| ------------| --------
[0-9]+                  | `12345678`  | 1-n kpl numeroita
[0-9]{7}                | `1234567`   | tasan 7 kpl numeroita
[a-zåäö]{4,10}          | `abcdåäö`   | Pieniä kirjaimia a-z, å, ä. Yhteensä 4-10 kpl.
[A-Z]{1,3}-[0-9]{1,3}   | `ABC-123`   | 1-3 isoa kirjainta, viiva ja 1-3 numeroa
[+-]?\d+,?\d*           | `1,2` `34` `+5,6` `-7,89` | luku, jonka alussa saattaa olla etumerkki, ja jossa voi olla myös välissä pilkku <sup><a href="https://stackoverflow.com/q/12117024">lähde</a></sup>
.                       | `x` `y` `9` | mikä tahansa merkki (paitsi rivinvaihto)

Säännöllinen lauseke kannattaa suunnitella ja testata jo ennen sen käyttämistä Java-ohjelmassa. Säännöllisten lausekkeiden kokeilemiseksi ja testaamiseksi on erilaisia verkkopalveluita, kuten [regex101.com](https://regex101.com/), joka näyttää myös sivun oikeassa laidassa selostuksen kirjoittamasi lausekkeen sisällöstä.

## Opiskelijanumeron tarkastaminen

Haaga-Helian opiskelijanumeron tapauksessa sopiva säännöllinen lauseke on `"a[0-9]{7}"` (a-kirjain ja 7 numeroa). Käyttäjän syöttämän opiskelijanumeron tarkistaminen käy seuraavasti:

```java
/* Tämä esimerkki on sovellettu Helsingin yliopiston Agile Education Research -tutkimusryhmän
 * ohjelmointikurssilta ja se on lisensoitu Creative Commons BY-NC-SA-lisenssillä.
 * https://materiaalit.github.io/ohjelmointi-s17/part10/#section-19-saannolliset-lausekkeet */

Scanner lukija = new Scanner(System.in);

System.out.print("Anna opiskelijanumero: ");
String numero = lukija.nextLine();

if (numero.matches("a[0-9]{7}")) {
    System.out.println("Muoto on oikea.");
} else {
    System.out.println("Muoto on väärä.");
}
```

## Regex-sääntöjä

Tutustu regex-sääntöihin osoitteessa: [https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html)

Huom! Kuten ylempänä on esitetty, merkkijonoissa kenoviiva `\` on erikoismerkki, jota ei voida käyttää sellaisenaan. Kenoviiva tulee esittää Javan merkkijonoissa aina kahtena kenoviivana `\\`. Regex-säännön `\d` eteen tulee siis Javassa laittaa "ylimääräinen" kenoviiva:

```java
boolean match = "1234".matches("\\d+");
```

Säännölliset lausekkeet ovat erittäin ilmaisuvoimainen tapa käsitellä merkkijonoja, mutta ne ovat usein vaikeasti luettavia ja testattavia. Onkin hyvin mahdollista, että käyttäessäsi säännöllisiä lausekkeita ratkaistaksesi ongelman kohtaat tukun uusia ongelmia.

[![Perl Problems](https://imgs.xkcd.com/comics/perl_problems.png)](https://xkcd.com/1171/)

Kuva: [XKCD, Perl Problems](https://xkcd.com/1171/). Creative Commons Attribution-NonCommercial 2.5


# Edistynyttä sisältöä: Merkkijonojen muotoilu

Muodostettaessa merkkijonoja, joihin halutaan sijoittaa esimerkiksi muuttujissa olevia arvoja, lopputulos voi joskus olla varsin vaikeasti luettavaa:

```java
int hinta = 3500;
String muotoiltu = "3 500 €";

String html = "<option value=\"" + hinta + "\">" + muotoiltu + "</option>";
```

Arvojen sijoittamiseksi osaksi merkkijonoa onkin olemassa toinen lähestymistapa, jossa `String`-luokan `format`-metodille määritellään haluttu muoto ja tähän muotoon sijoitettavat arvot:

```java
int hinta = 3500;
String muotoiltu = "3 500 €";

String html = String.format("<option value=\"%d\">%s €</option>", hinta, muotoiltu);
```

Lisätietoja format-metodista sekä siinä käytettävistä muotoilumääreistä (`%s`, `%d`) löydät esim. osoitteesta [https://www.educative.io/edpresso/what-is-the-stringformat-method-in-java](https://www.educative.io/edpresso/what-is-the-stringformat-method-in-java).


# Tunnille soveltuvia tehtäväideoita

## Satunnaisen salasanan generointi

Toteuta ohjelma, joka generoi satunnaisia vahvoja salasanoja hyödyntäen Javan [Random](https://docs.oracle.com/javase/8/docs/api/java/util/Random.html)-luokkaa sekä merkkijonoja. Satunnaislukuja voit luoda Random-satunnaislukugeneraattorilla esim. seuraavasti:

```java
Random satunnaisGeneraattori = new Random();
int satunnainen = satunnaisGeneraattori.nextInt(maksimi); // 0 <= satunnainen && satunnainen < maksimi
```

Pidemmän salasanan arpomiseksi toista satunnaislogiikkaa toistorakenteessa. Lisäksi tarvitset luokkasi alussa seuraavan `import`-komennon:

```java
import java.util.Random;
```

Vähemmän vakuuttava tapa satunnaisluvun generoimiseksi olisi esim. arpakuutio:

[![Random Number](https://imgs.xkcd.com/comics/random_number.png)](https://xkcd.com/221/)

Kuva: [XKCD, Random number](https://xkcd.com/221/). Creative Commons Attribution-NonCommercial 2.5

## Numeronyymit

> *"Numeronyms are used to abbreviate long words that would be too cumbersome to accurately type all the time. We can call an abbreviation a numeronym if it contains both letters and numbers."*
>
> Anna Monus, 2018. 10 Numeronyms Web Developers Should Know. [https://www.hongkiat.com/blog/tech-numeronyms/](https://www.hongkiat.com/blog/tech-numeronyms/)

Kirjoitetaan ohjelma, joka lyhentää merkkijonot seuraavalla ohjelmistoalalla tutulla logiikalla. Sanasta säilytetään ensimmäinen ja viimeinen kirjain, ja niiden väli korvataan numerolla, joka kertoo välissä olleiden merkkien määrän:

Esimerkki               | Lyhenne
------------------------|---------
internationalization    | i18n
localization            | l10n
kubernetes              | k8s




