# Merkkijonot

Kuten olemme aiemmin todenneet, merkkijonot ovat tyyppiä `String`. String on **luokka** ja yksittäiset merkkijonot ovat **olioita**. Merkkijonot luodaan muista olioista poiketen ilman `new`-avainsanaa, kirjoittamalla merkkijonon sisältö suoraan lainausmerkkeihin: `"esimerkki"`.


<!--
Tehtäväidea: satunnaisen salasanan generointi
* for-looppi
* subString tai charAt?

Tehtäväidea: Numeronyymit
* https://www.hongkiat.com/blog/tech-numeronyms/
* L10N, I18N, K8S
-->

## String-luokka

Koska merkkijonot ovat olioita, niihin liittyy seuraavat seikat:
* **olioiden vertailu ei toimi odotetusti vertailuoperaattorilla** `==`
* merkkijonoilla on **paljon hyödyllisiä metodeja**, joilla niitä voidaan käsitellä

## Olioiden vertailu, `equals` ja `equalsIgnoreCase`

Olioita vertailtaessa yhtäsuuruusoperaatio `==` vertailee, onko kyseessä __sama olio__. Se ei siis vertaile olioiden sisältöä, eli tässä tapauksessa merkkijonon merkkejä. **Samansisältöiset merkkijonot ovat siis samoja ainoastaan silloin, kun vertaillaan tiettyä merkkijono-oliota itseensä.**

Merkkijonoja vertaillaan siksi aina `equals`- ja `equalsIgnoreCase` –metodeilla, jotka vertailevat merkkijonojen sisältöjä. Molemmat vertailumetodit palauttavat aina totuusarvon `true` tai `false`.

```java
String language = "JAVA";

if (language.equals("java")) {
     // tätä lohkoa ei suoriteta, koska kirjainkoko ei täsmää
}

if (language.equalsIgnoreCase("java")) {
     // tämä lohko suoritetaan, koska equalsIgnoreCase-metodi ei huomioi kirjainkokoa
}
```


### Merkkijonojen metodien käyttäminen

Merkkijonojen metodit on määritetty Javan [String-luokassa](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html). 

Merkkijonojen metodeja voidaan kutsua suoraan merkkijonolle:

```java
int pituus = "Hello world".length();            // --> 11
String iso = "Hello world".toUpperCase();       // --> "HELLO WORLD"
String pieni = "Hello world".toLowerCase();     // --> "hello world"
```

Vastaavasti metodeja voidaan kutsua muuttujien avulla:

```java
String text = "  Hello world  ";
text = text.trim();	// trim() poistaa tyhjät merkit alusta ja lopusta: "Hello world"
```

Huomaa, että `trim()` ei muuta alkuperäistä merkkijonoa, vaan palauttaa uuden merkkijonon, joka asetetaan yllä talteen samaan muuttujaan.


### Muuttumattomuus (immutability)

Merkkijonot ovat muuttumattomia, eli kerran luotua **merkkijonoa ei voi muuttaa**. `String`-luokan metodit eivät koskaan muuta alkuperäistä merkkijonoa, vaan luovat niistä kopioita. Samaan muuttujaan voidaan toki sijoittaa uusia merkkijonoja:

```java
String text = "hello";
text.toUpperCase();
System.out.println(text);  // tulostaa "hello" (alkuperäinen merkkijono ei muuttunut)

text = text.toUpperCase(); // otetaan uusi merkkijono talteen
System.out.println(text);  // tulostaa "HELLO"
```

### Merkkijonon osajono

Merkkijonosta halutaan usein lukea jokin tietty osa. Tämä onnistuu metodilla `substring`. `substring`-metodia voidaan käyttää kahdella tavalla: 

1. yksiparametrisena palauttamaan merkkijonon loppuosa: `"abcd".substring(2)`
1. kaksiparametrisena palauttamaan parametrien määrittelemä osajono merkkijonosta: `"abcd".substring(1, 3)`

**Merkkijonojen indeksit alkavat aina nollasta!** Substring-metodin ensimmäinen parametri tarkoittaa ensimmäistä indeksiä, joka otetaan mukaan osamerkkijonoon, kun taas toinen parametri on ensimmäinen uuden merkkijonon ulkopuolelle jäävä indeksi. 

Parametriarvoilla `(5, 10)` saadaan siis merkit indekseistä **5, 6, 7, 8 ja 9**.

Koska substring-metodin paluuarvo on tyyppiä `String`, voidaan metodin paluuarvo ottaa talteen `String`-tyyppiseen muuttujaan:

```java
String kirja = "Kalavale";

System.out.println(kirja.substring(4));     // merkkijonon loppu alkaen indeksistä 4
System.out.println(kirja.substring(2, 6));  // palauttaa merkit indekseistä 2, 3, 4 ja 5

String kirja2 = "8 veljestä";

String loppuosa = kirja2.substring(2);
System.out.println("7 " + loppuosa);        // 7 veljestä
```

Tämä esimerkki on lainattu Helsingin yliopiston Agile Education Research -tutkimusryhmän ohjelmointikurssilta ja se on lisensoitu Creative Commons BY-NC-SA-lisenssillä. https://2017-ohjelmointi.github.io/part5/#section-26-merkkijonon-osajono 

# String-luokan metodeja

Tutustu metodeihin tarkemmin täällä: https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html

Tyyppi, nimi ja parametrit        | Kuvaus
----------------------------------| ------------
`char charAt(int index)`          | Returns the char value at the specified index.
`public boolean startsWith(String prefix)`  | Tests if this string starts with the specified prefix.
`public boolean endsWith(String suffix)`    | Tests if this string ends with the specified suffix.
`boolean contains(String s)`      | Returns true if and only if this string contains the specified sequence of char values.
`int indexOf(String str)`         | Returns the index within this string of the first occurrence of the specified substring.
`int length()`                    | Returns the length of this string.
`boolean matches(String regex)`   | Tells whether or not this string matches the given regular expression.
`String replace(CharSequence target, CharSequence replacement)` | Replaces each substring of this string that matches the literal target sequence with the specified literal replacement sequence.
`String[] split(String regex)`    | Splits this string around matches of the given regular expression.
`String substring(int beginIndex)`| Returns a string that is a substring of this string.
`String substring(int beginIndex, int endIndex)` | Returns a string that is a substring of this string.
`String toLowerCase()`            | Converts all of the characters in this String to lower case
`String toUpperCase()`            | Converts all of the characters in this String to upper case
`String trim()`                   | Returns a string whose value is this string, with any leading and trailing whitespace removed.

## Esimerkkejä merkkijonojen metodeista

```java
public class MerkkijonojenMetodit {

    public static void main(String[] args) {
        String address = "https://www.example.com/";

        boolean isSecure = address.startsWith("https://");

        System.out.println(isSecure); // true

        String email = "john.smith@example.com";

        int dotIndex = email.indexOf(".");
        String firstName = email.substring(0, dotIndex);
        System.out.println(firstName); // john

        int atIndex = email.indexOf("@");
        String lastName = email.substring(dotIndex + 1, atIndex);
        System.out.println(lastName); // smith
    }
}
```

## Esimerkki metodikutsujen ketjuttamisesta

Monet metodit, kuten `replace`, palauttavat uusia merkkijonoja. Metodin palauttamille merkkijonoille voidaan kutsua uusia metodeja suoraan ns. "ketjuttamalla":

```java
public class StringReplaceJaKetjuttaminen {

    public static void main(String[] args) {
        // seuraava replace kutsutaan aina edellisen palauttamalle tulokselle
        // (ketjuttaminen):
        String numerot = "1 2 3 4".replace("1", "one").replace("2", "two").replace("3", "three").replace("4", "four");

        System.out.println(numerot);
    }
}
```

Yllä olevassa esimerkissä `numerot`-muuttujaan asetetaan lopulta ketjun päätteeksi palautettu viimeinen merkkijono. 

# Yleiset erikoismerkit merkkijonoissa

Kaikkia erikoismerkkejä ei voida esittää sellaisenaan merkkijonoissa. Esimerkiksi lainausmerkki merkkijonon sisällä sekoittuisi merkkijonon päättävään lainausmerkkiin. Erikoismerkit täytyykin esittää erityisten kontrollimerkkien avulla.

https://docs.oracle.com/javase/tutorial/java/data/characters.html

Syntaksi       | Kuvaus
---------------| ------
\\t            | Insert a tab in the text at this point.
\\n            | Insert a newline in the text at this point.
\\"            | Insert a double quote character in the text at this point.
\\\\           | Insert a backslash character in the text at this point.

```java
System.out.println("Ensimmäinen rivi\nToinen rivi");
System.out.println("Tekstiä \"lainausmerkeissä\".");
```

```
Ensimmäinen rivi
Toinen rivi
Tekstiä "lainausmerkeissä".
```

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

Javassa on erillinen `char`-tietotyyppi yksittäisiä merkkejä varten. Yksittäinen merkki aloitetaan ja lopetetaan heittomerkillä, esim. `'a'`. Yksittäiset merkit eivät ole olioita, eli niillä ei ole metodeja.

Merkkijonolta voidaan pyytää yksittäisiä merkkejä niiden indeksin perusteella. Tämä onnistuu metodilla `charAt(int indeksi)`, joka saa parametrina halutun merkin indeksin merkkijonossa. Muista, että merkkijonojen indeksien laskeminen alkaa aina nollasta, eli esimerkiksi neljäs merkki on indeksissä kolme.

```java
char kirjain = 'a';
System.out.println(kirjain); // a

String kirja = "Kalavale";

char merkki = kirja.charAt(3);
System.out.println("Neljäs merkki: " + merkki);  // Neljäs merkki: a
System.out.println("Eka merkki: " + kirja.charAt(0)); // Eka merkki: K
```

Tämä esimerkki on lainattu Helsingin yliopiston Agile Education Research -tutkimusryhmän ohjelmointikurssilta ja se on lisensoitu Creative Commons BY-NC-SA-lisenssillä. https://2017-ohjelmointi.github.io/part5/#section-25-yksittainen-merkki-merkkijonosta 


# Edistynyttä sisältöä: säännölliset lausekkeet, regular expressions / regex

> "Säännöllinen lauseke määrittelee joukon merkkijonoja tiiviissä muodossa. Säännöllisiä lausekkeita käytetään muunmuassa merkkijonojen oikeellisuuden tarkistamiseen. Merkkijonojen oikeellisuuden tarkastaminen tapahtuu luomalla säännöllinen lauseke, joka määrittelee merkkijonot, jotka ovat oikein."
>
> "Oikeellisuuden tarkistus säännöllisten lausekkeiden avulla tapahtuu ensin sopivan säännöllisen lausekkeen määrittelyn. Tämän jälkeen käytetään `String`-luokan metodia `matches`, joka tarkistaa vastaako merkkijono parametrina annettua säännöllistä lauseketta. Opiskelijanumeron tapauksessa sopiva säännöllinen lauseke on `01[0-9]{7}`"

*Lähde: Helsingin yliopiston Agile Education Research -tutkimusryhmän ohjelmointikurssi (Creative Commons BY-NC-SA)  https://materiaalit.github.io/ohjelmointi-s17/part10/#section-19-saannolliset-lausekkeet*

## `"teksti".matches(String regex); // edistynyttä sisältöä`

`matches`-metodi vertaa merkkijonoa annettuun säännölliseen lausekkeeseen ja palauttaa `true` tai `false` riippuen siitä, vastaako merkkijono lauseketta. Säännölliset lausekkeet (regular expression) ovat merkkijonoja, jotka muodostavat "kuvion" (pattern), jota vasten merkkijonoja verrataan.

Valikoituja esimerkkejä selityksineen:

Regex                   | Esimerkki   | Selitys
------------------------| ------------| --------
[0-9]+                  | 1234567890  | 1-n kpl numeroita
[0-9]{7}                | 1234567     | tasan 7 kpl numeroita
[a-zåäö -]{4,10}        | abc-d       | Pieniä kirjaimia a-z, å, ä, ö, väli tai viiva. Yhteensä 4-10 kpl.
[A-Z]{1,3}-[0-9]{1,3}   | ABC-123     | 1-3 isoa kirjainta, viiva ja 1-3 numeroa 

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

Tutustu regex-sääntöihin osoitteessa: https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html

Huom! Kuten ylempänä on esitetty, merkkijonoissa kenoviiva `\` on erikoismerkki, jota ei voida käyttää sellaisenaan. Kenoviiva tulee esittää Javan merkkijonoissa aina kahtena kenoviivana `\\`. Regex-säännön `\d` eteen tulee siis Javassa laittaa "ylimääräinen" kenoviiva: 

```java
boolean match = "1234".matches("\\d+");
```

Säännölliset lausekkeet ovat erittäin ilmaisuvoimainen tapa käsitellä merkkijonoja, mutta ne ovat usein vaikeasti luettavia ja testattavia. Onkin hyvin mahdollista, että käyttäessäsi säännöllisiä lausekkeita ratkaistaksesi ongelman kohtaat tukun uusia ongelmia.


[![Perl Problems](https://imgs.xkcd.com/comics/perl_problems.png)](https://xkcd.com/1171/)

https://xkcd.com/1171/ This work is licensed under a Creative Commons Attribution-NonCommercial 2.5 License

---

Tämän oppimateriaalin on kehittänyt Teemu Havulinna ja se on lisensoitu [Creative Commons BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/) -lisenssillä.