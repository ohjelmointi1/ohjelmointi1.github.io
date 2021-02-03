[&larr; Takaisin etusivulle](/)


<h1 class="js-toc-ignore">Taulukot (array)</h1>

Tällä kerralla tutustumme Javan taulukoihin. Taulukot ovat varsin alkeellisia tietorakenteita, joihin voidaan varastoida useita saman typpisiä arvoja. Materiaalissa ja oppitunnilla oletetaan perustason osaamista listojen käytöstä.

Toisin kuin listoilla, taulukon pituus on kiinteä, eli niitä ei voi lyhentää eikä kasvattaa. Taulukoilla ei myöskään ole metodeita eikä samanlaista luonnollista merkkijonoesitystä kuin listoilla. 

Listoilla ja taulukoilla on myös lukuisia yhtäläisyyksiä, ja `ArrayList`-listat jopa käyttävät sisäisesti taulukoita tietojensa tallentamiseen nimensä mukaisesti.


**Sisällysluettelo**

<div class="js-toc"></div>

# Oppituntitallenne: taulukon luominen, käsitteleminen ja läpikäynti

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/99c9ef6f-d2eb-4180-8c1b-0cfef766cb10?autoplay=false&amp;showinfo=true" allowfullscreen style="border:none;"></iframe>

# Taulukot ja taulukkomuuttujat

Taulukkoja sisältävien muuttujien tyypiksi kirjoitetaan tallennettavan tyypin nimi ja sen jälkeen hakasulut, esim:

```java
int[] numerot;
String[] sanat;
double[] liukuluvut;
boolean[] totuusarvot;

// myöhemmin kurssilla:
Yhteystieto[] yhteystiedot;
Auto[] autot;
```

Tässä vaiheessa kurssia pitäydymme Javan valmiissa tietotyypeissä kuten `String` emmekä vielä toteuta omia luokkia, kuten `Yhteystieto` tai `Auto`.

# Taulukon luominen

Taulukot luodaan new-avainsanalla ja taulukon pituus määritellään hakasuluissa. Hakasulkujen sisään määritellään tällä syntaksilla taulukon pituus. 

**Pituutta ei voi enää muuttaa taulukon luomisen jälkeen**.

```java
String[] viikonpaivat = new String[7];  // 7 merkkijonoa
int[] lottonumerot = new int[7];        // 7 numeroa
```


# Taulukon alkioihin viittaaminen

Taulukon alkioihin viitataan taulukon indeksien perusteella hakasulkujen avulla. Kuten listojen ja merkkijonojen tapauksessa, taulukoiden indeksit lasketaan seuraavasti:

* ensimmäinen indeksi on `0`
* viimeinen indeksi on `taulukon pituus - 1`

Arvoja voidaan asettaa taulukkoon sijoitusoperaattorilla `=`. Tällöin sijoitusoperaattorin vasemmalle puolelle kirjoitetaan taulukon muuttuja ja haluttu indeksi:

```java
viikonpaivat[0] = "maanantai";
viikonpaivat[1] = "tiistai";
// ...
viikonpaivat[6] = "sunnuntai";
```

Arvoja voidaan hakea taulukosta vastaavasti muuttujan ja indeksin avulla. Haettu arvo voidaan asettaa toiseen muuttujaan, tulostaa tai välittää eteenpäin, aivan kuten muutkin samantyyppiset arvot:

```java
// arvon hakeminen indeksistä 3:
String torstai = viikonpaivat[3];

// arvon hakeminen ja tulostaminen:
System.out.println(viikonpaivat[3]);

// arvon hakeminen, muuttaminen isoksi ja tulostaminen:
System.out.println(viikonpaivat[3].toUpperCase());
```

Toisin kuin listoja, taulukkoa ei täydy täyttää alusta loppuun, vaan voit täyttää sen missä järjestyksessä tahansa. Tässä esimerkissä luodaan kolmepaikkainen kokonaislukutaulukko, jonka jälkeen taulukon indekseihin 0 ja 2 asetetaan arvot:

```java
// Luodaan muuttuja ja taulukko:
int[] luvut = new int[3];

// Asetetaan taulukkoon arvoja:
luvut[0] = 2;
luvut[2] = 5;

// Arvojen lukeminen taulukosta:
System.out.println(luvut[0]);
int luku = luvut[2];
```

[Katso Java Visualizerissa!](https://goo.gl/Dmrxhz)

Tämä esimerkki on lainattu Helsingin yliopiston Agile Education Research –tutkimusryhmän oppimateriaalista, joka on lisensoitu Creative Commons BY-NC-SA-lisenssillä. [https://2017-ohjelmointi.github.io/part6/](https://2017-ohjelmointi.github.io/part6/)


# Taulukon tyhjät arvot

Koska taulukon *pituus ei voi muuttua*, on taulukossa heti luonnin jälkeen tarvittava määrä paikkoja. Oletusarvo numerotaulukoilla on nolla `0` ja boolean-taulukoilla `false`. Oliotaulukoilla (esim. merkkijonotaulukot), oletusarvo on tyhjä viittaus, eli `null`.

```java
// taulukko täytetään oletusarvoilla, eli nollilla:
int[] luvut = new int[3];       // [0, 0, 0]

// viittaustyyppisten taulukoiden oletusarvo on `null`:
String[] sanat = new String[4]; // [null, null, null, null]
```

# Taulukon luominen valmiilla arvoilla

Jos taulukkoon asetettavat alkuarvot ovat jo valmiiksi tiedossa, taulukko voidaan alustaa myös aaltosulkeiden avulla tietyille arvoille.

Tällöin taulukon pituutta ei ilmoiteta hakasuluissa, vaan pituus määräytyy alkuarvojen määrän mukaan, esim: 

```java
int[] lottorivi = new int[] { 3, 9, 15, 16, 26, 29, 33 };
```

Java osaa myös päätellä tässä tapauksessa taulukon tyypin, joten voimme kirjoittaa saman ilman `new int[]` -osaa:

```java
int[] lottorivi = { 3, 9, 15, 16, 26, 29, 33 };
```

Taulukoiden alustaminen valmiiksi tiedossa olevilla merkkijonoilla toimii samalla tavalla:

```java
String[] viikonpaivat = { "Ma", "Ti", "Ke", "To", "Pe", "La", "Su" };
```

## Taulukon koko ja sen arvojen läpikäynti

Taulukon koon saa selville taulukkoon liittyvän muuttujan `length` avulla. `length`-muuttujaan pääsee käsiksi kirjoittamalla taulukon muuttujan nimen, pisteen sekä length-muuttujan nimen, eli esimerkiksi:

```java
int[] luvut = new int[3];

int pituus = luvut.length;
``` 

**Huomaa**, että kyseessä ei ole metodikutsu kuten listoilla, eli `taulukko.length()` ei toimi.

Taulukon alkioiden läpikäynti voidaan toteuttaa esim. `while`- tai `for`-toistorakenteen avulla:

```java
int[] luvut = new int[4];
luvut[0] = 42;
luvut[1] = 13;
luvut[2] = 12;
luvut[3] = 7;

System.out.println("Taulukossa on " + luvut.length + " alkiota.");

int indeksi = 0;
while (indeksi < luvut.length) {
    System.out.println(luvut[indeksi]);
    indeksi++;
}
```
[Katso Java Visualizerissa!](https://goo.gl/XzEiAc)

Tämän esimerkki on lainattu Helsingin yliopiston Agile Education Research –tutkimusryhmän oppimateriaalista, joka on lisensoitu Creative Commons BY-NC-SA-lisenssillä. [https://2017-ohjelmointi.github.io/part6/](https://2017-ohjelmointi.github.io/part6/)

# Taulukon hyödyntämistä

Koska taulukot ovat jonkin verran listoja rajoittuneempi tietorakenne, voi olla, että päädyt itse luomaan taulukkoja harvemmin. Taulukot ovat kuitenkin hyödyllinen tietorakenne erityisesti silloin, kun tarvittava kokoelman koko on ennalta tiedossa. Myös Javan standardikirjastossa hyödynnetään taulukoita, eli vaikka et itse loisi omia taulukoita, tarvitset perustaidot taulukoiden hyödyntämisestä esimerkiksi pilkkoessasi merkkijonoja.

## Merkkijonon split-metodi

Merkkijonoilla (String-luokka) on `split`-niminen metodi, jolla merkkijono voidaan pilkkoa osiin tietyn merkin tai osamerkkijonon kohdalta. Split palauttaa **merkkijonotaulukon**, jossa on alkuperäisen merkkijonon osat ilman pilkkomisessa käytettyjä merkkejä.

```java
String teksti = "ma ti ke to pe la su";

// pilkotaan välilyöntien kohdalta
String[] paivat = teksti.split(" ");

int pituus = paivat.length;
System.out.println(pituus); // 7

System.out.println(paivat[0]); // ma
System.out.println(paivat[1]); // ti
System.out.println(paivat[2]); // ke

System.out.println(paivat[pituus - 1]); // su
```

Pilkkominen voi olla hyödyllistä esimerkiksi koneellisesti luettavaksi tarkoitettujen esitysmuotojen, kuten päivämäärien tai CSV-tiedostojen, lukemisessa:

```java
String ajanhetki = "2020-9-19T7:9:18";

String[] osat = ajanhetki.split("T");

System.out.println(osat[0]); // "2020-9-19"
System.out.println(osat[1]); // "7:9:18"

String paivamaara = osat[0];
String[] pvmOsat = paivamaara.split("-");
System.out.println(Arrays.toString(pvmOsat)); // ["2020", "9", "19"]

String kellonaika = osat[1];
String[] kelloOsat = kellonaika.split(":");
System.out.println(Arrays.toString(kelloOsat)); // ["7", "9", "18"]
```

## CSV-tiedostot (comma-separated values)

Taulukkomuotoisen tiedon tallentamiseen yksinkertaisina tekstitiedostoina käytetään usein CSV-tiedostoja:

> *"CSV on toteutukseltaan tekstitiedosto, jonka taulukkorakenteen eri kentät on eroteltu toisistaan pilkuilla ja rivinvaihdoilla. Jos jokin kenttä sisältää erikoismerkkejä, kyseinen kenttä ympäröidään pystysuorilla lainausmerkeillä ("). Ensimmäisellä rivillä voi olla kenttien selitykset samassa muodossa kuin mitä itse tiedot ovat."*
>
> Wikipedia. CSV. https://fi.wikipedia.org/wiki/CSV

[Wikipedian esimerkissä](https://fi.wikipedia.org/wiki/CSV) autojen tiedot on esitetty tallennettuna seuraavassa CSV-muodossa:

```
Vuosi,Merkki,Malli,Pituus
1997,Ford,E350,2.34
2000,Mercury,Cougar,2.38
```

[Sama data](https://fi.wikipedia.org/wiki/CSV) on esitettävissä myös taulukkomuodossa:

Vuosi	| Merkki	| Malli     | Pituus
--------|-----------|-----------|-------
1997	| Ford      | E350      | 2.34
2000	| Mercury   | Cougar    | 2.38

Koska CSV-tiedostot on helposti koneluettavia ja -kirjoitettavia, hyvin monet ohjelmat tukevat niitä tiedon tallennusmuotonaan. Myös CSV-tiedostojen käsittelyssä `split`-metodista on hyötyä, vaikkakin monimutkaisempia CSV-rakenteita kannattaa lukea erillisten kirjastojen avulla.


## Säätilasto-oppituntitallenne

Tunnilla kirjoitimme ohjelman, joka lukee Ilmatieteen laitoksen avointa csv-muotoista säädataa ja kertoo aineiston lämpimmän ja kylmimmän havainnon päivämäärineen.

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/fbbdf454-5222-43bb-840b-8579fdd47e13?autoplay=false&amp;showinfo=true" allowfullscreen style="border:none;"></iframe>

Voit tallentaa säädatan itsellesi csv-muodossa osoitteesta [https://www.ilmatieteenlaitos.fi/havaintojen-lataus](https://www.ilmatieteenlaitos.fi/havaintojen-lataus). Aineisto on lisensoitu lisenssillä [Creative Commons Nimeä 4.0](https://www.ilmatieteenlaitos.fi/avoin-data-lisenssi).



## For each –toistokäsky ja listojen sekä taulukoiden läpikäynti

Taulukon kaikki alkiot voidaan käydä läpi for each -toistokäskyllä, aivan kuten listojen alkiot. Kertaa tarvittaessa for each -rakenne (advanced for loop) lista-aiheen muistiinpanoista tai [Googlen avulla](https://www.google.com/search?q=for+each+loop+java+array).


```java
int[] luvut = {2, 4, 8, 16, 32, 64};

for (int luku : luvut) {
    System.out.println(luku);
}
```


## Vertailu: taulukoiden ja listojen eroja

Seuraavissa kahdessa esimerkkikoodissa luodaan merkkijonotaulukko sekä merkkijonolista, joihin molempiin asetetaan yksi arvo:

```java
// Luodaan 10 merkkijonon pituinen taulukko:
String[] taulukko = new String[10];

// Lisätään sana taulukkoon:
taulukko[0] = "taulukkoon";

System.out.println(taulukko[0]);

System.out.println(taulukko.length); // 10
```

```java
// Luodaan tyhjä merkkijonolista:
List<String> lista = new ArrayList<>();

// Lisätään sana listaan
lista.add("listalle");

System.out.println(lista.get(0));

System.out.println(lista.size()); // 1
```

Listojen ja taulukoiden toiminta on monilta osin samankaltaista. Taulukon pituus on kuitenkin muuttumaton, joten sen pituus on 10, vaikka sinne onkin lisätty vasta yksi merkkijono. Muut taulukon indeksit ovat vielä tyhjiä (`null`). Listan pituus kasvaa dynaamisesti, joten esimerkissä listan pituus on 1.

Taulukot                                            | Listat
----------------------------------------------------|--------------------------
Taulukon pituus määrätään sitä luotaessa            | Listan pituus kasvaa alkioita lisättäessä
Taulukon alkioita käsitellään hakasulkujen avulla   | Listan alkioita käsitellään metodien avulla
Taulukon pituus on aina kiinteä                     | Lista luodaan tyhjänä ja se kasvaa rajattomasti
Taulukko voidaan täyttää missä vain järjestyksessä  | Listan täyttäminen alkaa aina indeksistä 0
Taulukkoon ei voida lisätä arvoja väleihin          | Listalle voidaan lisätä arvoja väleihin

## Taulukon järjestäminen
Taulukon kaikki alkiot voidaan järjestää kasvavaan järjestykseen seuraavasti:

```java
Arrays.sort(numeroTaulukko);
```

Vertaa listojen järjestäminen:

```java
Collections.sort(numeroLista);
```

## Taulukon tulostaminen

Mitä tapahtuu kun taulukko tulostetaan?

```java
String[] kirjaimet = new String[] { "j", "a", "v", "a" };

Arrays.sort(kirjaimet);

// tulostaa hämmentävän merkkijonon: 
System.out.println(kirjaimet); // [Ljava.lang.String;@106d69c
```

**Taulukoilla ei ole oletuksena selkeää merkkijonoesitystä.**

`Arrays`-apuluokasta löytyy kuitenkin staattinen metodi `Arrays.toString(taulukko)` merkkijonoesityksen muodostamiseksi. `toString` muodostaa merkkijonon, jonka voimme ottaa talteen muuttujaan tai antaa suoraan esim. `println`-metodille:

```java
import java.util.Arrays; // alkuun tämä
```

```java
String[] nimet = { "Superman", "Batman", "Chuck Norris" };

Arrays.sort(nimet);

String merkkijonoksi = Arrays.toString(nimet);

System.out.println(merkkijonoksi); // [Batman, Chuck Norris, Superman]
```

## Viittaustyyppiset muuttujat käytännössä

Taulukoita käytetään Javassa viittaustyyppisillä muuttujilla, aivan kuten listoja, merkkijonoja ja muita olioita. Tämä tarkoittaa käytännössä sitä, että kun taulukko asetetaan muuttujaan tai välitetään parametrina toisaalle, taulukkoa *ei kopioida*, vaan *samaan taulukkoon viitataan useammasta paikasta*:

```java
String[] sanat = new String[10];
String[] verbit = sanat; // ei kopioi taulukkoa
```

Ilmiötä havainnollistetaan seuraavassa koodiesimerkissä, jossa `nimet` ja `lyhennetty` ovat täsmälleen sama taulukko:

```java
String[] nimet = { "Johan", "Ludvig", "Runeberg" };
String merkkijono = Arrays.toString(nimet);
System.out.println(merkkijono);

String etunimi = nimet[0]; // "Johan"
String toinenNimi = nimet[1]; // "Ludvig"
String sukunimi = nimet[2]; // "Runeberg"

// EI KOPIOI TAULUKKOA, VAAN VIITTAA SAMAAN TAULUKKOON:
String[] lyhennetty = nimet;

lyhennetty[0] = etunimi.substring(0, 1); // "J"
lyhennetty[1] = toinenNimi.substring(0, 1); // "L"

// Lyhennetty taulukko sisältää muuttuneet merkkijonot
System.out.println(Arrays.toString(lyhennetty));

// Myös alkuperäisen muuttujan kautta sisältö on muuttunut
System.out.println(Arrays.toString(nimet));
```

Voit tutustua koodin suoritukseen vaiheittain [Java Visualizer -työkalulla](https://cscircles.cemc.uwaterloo.ca/java_visualize/#code=import+java.util.Arrays%3B%0A%0Apublic+class+RuneberginLyhentaminen+%7B%0A+++public+static+void+main(String%5B%5D+args)+%7B%0A++++++String%5B%5D+nimet+%3D+%7B+%22Johan%22,+%22Ludvig%22,+%22Runeberg%22+%7D%3B%0A++++++String+merkkijono+%3D+Arrays.toString(nimet)%3B%0A++++++System.out.println(merkkijono)%3B%0A%0A++++++String+etunimi+%3D+nimet%5B0%5D%3B+//+%22Johan%22%0A++++++String+toinenNimi+%3D+nimet%5B1%5D%3B+//+%22Ludvig%22%0A++++++String+sukunimi+%3D+nimet%5B2%5D%3B+//+%22Runeberg%22%0A%0A++++++//+EI+KOPIOI+TAULUKKOA,+VAAN+VIITTAA+SAMAAN+TAULUKKOON%3A%0A++++++String%5B%5D+lyhennetty+%3D+nimet%3B%0A%0A++++++lyhennetty%5B0%5D+%3D+etunimi.substring(0,+1)%3B+//+%22J%22%0A++++++lyhennetty%5B1%5D+%3D+toinenNimi.substring(0,+1)%3B+//+%22L%22%0A%0A++++++//+Lyhennetty+taulukko+sis%C3%A4lt%C3%A4%C3%A4+muuttuneet+merkkijonot%0A++++++System.out.println(Arrays.toString(lyhennetty))%3B%0A%0A++++++//+My%C3%B6s+alkuper%C3%A4isen+muuttujan+kautta+sis%C3%A4lt%C3%B6+on+muuttunut%0A++++++System.out.println(Arrays.toString(nimet))%3B%0A+++%7D%0A%7D&mode=display&curInstr=0):

<iframe style="width: 100%; height: 480px;" src="https://cscircles.cemc.uwaterloo.ca/java_visualize/iframe-embed.html?faking_cpp=false#data=%7B%22user_script%22%3A%22import%20java.util.Arrays%3B%5Cn%5Cnpublic%20class%20RuneberginLyhentaminen%20%7B%5Cn%20%20%20public%20static%20void%20main(String%5B%5D%20args)%20%7B%5Cn%20%20%20%20%20%20String%5B%5D%20nimet%20%3D%20%7B%20%5C%22Johan%5C%22%2C%20%5C%22Ludvig%5C%22%2C%20%5C%22Runeberg%5C%22%20%7D%3B%5Cn%20%20%20%20%20%20String%20merkkijono%20%3D%20Arrays.toString(nimet)%3B%5Cn%20%20%20%20%20%20System.out.println(merkkijono)%3B%5Cn%5Cn%20%20%20%20%20%20String%20etunimi%20%3D%20nimet%5B0%5D%3B%20%2F%2F%20%5C%22Johan%5C%22%5Cn%20%20%20%20%20%20String%20toinenNimi%20%3D%20nimet%5B1%5D%3B%20%2F%2F%20%5C%22Ludvig%5C%22%5Cn%20%20%20%20%20%20String%20sukunimi%20%3D%20nimet%5B2%5D%3B%20%2F%2F%20%5C%22Runeberg%5C%22%5Cn%5Cn%20%20%20%20%20%20%2F%2F%20EI%20KOPIOI%20TAULUKKOA%2C%20VAAN%20VIITTAA%20SAMAAN%20TAULUKKOON%3A%5Cn%20%20%20%20%20%20String%5B%5D%20lyhennetty%20%3D%20nimet%3B%5Cn%5Cn%20%20%20%20%20%20lyhennetty%5B0%5D%20%3D%20etunimi.substring(0%2C%201)%3B%20%2F%2F%20%5C%22J%5C%22%5Cn%20%20%20%20%20%20lyhennetty%5B1%5D%20%3D%20toinenNimi.substring(0%2C%201)%3B%20%2F%2F%20%5C%22L%5C%22%5Cn%5Cn%20%20%20%20%20%20%2F%2F%20Lyhennetty%20taulukko%20sis%C3%A4lt%C3%A4%C3%A4%20muuttuneet%20merkkijonot%5Cn%20%20%20%20%20%20System.out.println(Arrays.toString(lyhennetty))%3B%5Cn%5Cn%20%20%20%20%20%20%2F%2F%20My%C3%B6s%20alkuper%C3%A4isen%20muuttujan%20kautta%20sis%C3%A4lt%C3%B6%20on%20muuttunut%5Cn%20%20%20%20%20%20System.out.println(Arrays.toString(nimet))%3B%5Cn%20%20%20%7D%5Cn%7D%22%2C%22options%22%3A%7B%22showStringsAsValues%22%3Atrue%2C%22showAllFields%22%3Afalse%7D%2C%22args%22%3A%5B%5D%2C%22stdin%22%3A%22%22%7D&cumulative=false&heapPrimitives=false&drawParentPointers=false&textReferences=false&showOnlyOutputs=false&py=3&curInstr=0&resizeContainer=true&highlightLines=true&rightStdout=true" frameborder="0" scrolling="no"></iframe>

## Syventävää tietoa: taulukon kopioiminen

Taulukkoa ei ole mahdollista lyhentää tai pidentää, mutta siitä voidaan luoda eri pituinen kopio:

* jos kopio on alkuperäistä taulukkoa lyhyempi, jää arvoja pois
* jos kopio on alkuperäistä pidempi, täytetään loppuosa oletusarvoilla (`null`, `0` jne).

Monet operaatiot, kuten taulukon järjestäminen, muuttavat alkuperäistä taulukkoa pysyvästi. Usein alkuperäinen data halutaan pitää muuttumattomana, jolloin operaatioita tehdään taulukon kopiolle.

```java
String[] kirjaimet = new String[] { "j", "a", "v", "a" };

String[] kopio = Arrays.copyOf(kirjaimet, kirjaimet.length);

String[] alkuosa = Arrays.copyOf(kirjaimet, 2); // [j, a]
```


## Syventävää tietoa: main-metodin args-taulukko

Main-metodin otsikossa esiintyvä `String[] args` on merkkijonotaulukko, joka sisältää ohjelmalle annetut komentoriviparametrit. Eclipsessä suoritettaessa ne ovat tyhjät, mutta komentorivisovelluksissa tarvitsemme tätä taulukkoa.

```java
import java.util.Arrays;

public class ArgsTaulukonTulostaminen {

    public static void main(String[] args) {
        // args on merkkijonotaulukko
        System.out.println(args.length);
        System.out.println(Arrays.toString(args));
    }
}
```


## Yhteenveto: Arrays-apuluokka


Ote hyödyllisistä apumetodeista taulukoiden käyttöön:

**Arrays.copyOf(original, int newLength)**

> Copies the specified array, truncating or padding (if necessary) so the copy has the specified length.

**Arrays.toString(array)**

> Returns a string representation of the contents of the specified array.

**Arrays.sort(array)**

> Sorts the specified array into ascending order.

Lähde: [https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html)


# Tehtäväideoita oppitunnille

## Lottotarkistin

Oppitunnilla kirjoitettiin ohjelma, joka käyttää useita taulukoita tarkistaakseen lottoriveillä olevat oikeat numerot.

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/613511d5-aa04-41ed-bc3b-d88c2fdd2f4e?autoplay=false&amp;showinfo=true" allowfullscreen style="border:none;"></iframe>

[Video: Lottotarkistin (sisäkkäiset toistorakenteet ja useita taulukoita)](https://web.microsoftstream.com/video/613511d5-aa04-41ed-bc3b-d88c2fdd2f4e)

---

Tämän oppimateriaalin on kehittänyt Teemu Havulinna ja se on lisensoitu [Creative Commons BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/) -lisenssillä.

<script src="/tocbot/tocbot.min.js"></script>
<script src="/scripts.js"></script>
<link rel="stylesheet" href="/tocbot/tocbot.css">