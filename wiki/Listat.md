[&larr; Takaisin etusivulle](/)


<h1 class="js-toc-ignore">Listat</h1>

Tällä viikolla tutustumme Javan kenties yleisimpään kokoelmaan: listoihin. Listat ovat tietorakenteita, joiden pituus kasvaa joustavasti, kun niihin lisätään uusia arvoja. Listoihin voidaan lisätä arvoja myös aiempien arvojen väliin ja listan väleistä voidaan poistaa arvoja. Listat ovat olioita ja niillä on metodeita, joiden avulla arvoja lisätään, poistetaan, etsitään jne.


**Sisällysluettelo**

<div class="js-toc"></div>


# Tehtäväpohjien kloonaaminen GitHubista

Tällä viikolla teemme Viopessa tehtäväkokonaisuuden, joka on lainattu [Helsingin yliopiston Ohjelmoinnin MOOC -kurssilta](https://ohjelmointi-20.mooc.fi/osa-3/2-listat). Tehtäväkokonaisuuden suoraviivaistamiseksi tehtäviin on saatavilla valmiit pohjat GitHubissa osoitteessa [https://github.com/swd1tn002/mooc.fi-2019-osa3/](https://github.com/swd1tn002/mooc.fi-2019-osa3/). Voit kopioida tehtäväpohjat itsellesi yksi kerrallaan Viope-tehtävän linkkien kautta, tai kopioida koko projektipohjan kerralla. Alla oleva video esittelee, miten projekti *kloonataan* GitHubista omaan Eclipseen:

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/05754f1f-06c2-4142-8423-7cbb22bff651?autoplay=false&amp;showinfo=true" allowfullscreen style="border:none;"></iframe>


# ArrayList:in perusteet

Seuraava [Helsingin yliopiston Ohjelmoinnin MOOC -kurssin](https://ohjelmointi-20.mooc.fi/osa-3/2-listat) video esittelee Javan ArrayList-tietorakenteen toimintaa ja käyttämistä:

<iframe width="560" height="315" src="https://www.youtube.com/embed/-y67VJ68Izs" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Hyödynnä myös Helsingin yliopiston MOOC-kurssin muita materiaaleja: [https://ohjelmointi-20.mooc.fi/osa-3/2-listat](https://ohjelmointi-20.mooc.fi/osa-3/2-listat). 


# Eri listatyypit: ArrayList vs. LinkedList

Javassa on useita eri listatyyppejä. Kaikki listat toimivat ulkoisesti samalla tavalla, vaikka niiden sisäiset toteutustavat vaihtelevat merkittävästi. `ArrayList` on sisäisesti toteutettu taulukon avulla, kun taas `LinkedList` on toteutettu linkittämällä listan alkiot toisiinsa "ketjuksi". Sopivin lista kuhunkin tarkoitukseen vaihtelee listan käyttötavasta riippuen, mutta pääsääntöisesti pärjäät hyvin käyttämällä aina `ArrayList`-listoja.

Listat sijaitsevat `java.util`-paketissa, joten ne otetaan käyttöön esim. seuraavilla `import`-käskyillä:

```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
```

Voit luoda itsellesi merkkijonolistoja seuraavasti:

```java
ArrayList<String> taulukkoLista = new ArrayList<String>();
LinkedList<String> linkitettyLista = new LinkedList<String>();
```


## Geneeriset tyypit

Listat ovat geneerisiä, eli niiden sisällön tyyppi voidaan määritellä itse. Edellä määritellyt listat säilyttävät merkkijonoja ja tämä `ArrayList` voi säilyttää kokonaislukuja:

```java
// kulmasuluissa oleva tyypin nimi kertoo, mitä arvoja listalla säilytetään:
ArrayList<Integer> numerot = new ArrayList<Integer>();
```

Java osaa päätellä luotavan listan tyypin muuttujan tyypistä, joten voimme määritellä listan luonnissa tyypin tyhjäksi `<>`. Java päättelee tyypiksi `<String>`:

```java
// jälkimmäiset kulmasulut voidaan jättää tyhjiksi:
ArrayList<String> merkkijonot = new ArrayList<>();
```

Yhdessä listassa voidaan varastoida ainoastaan yhdentyyppisiä arvoja, eikä varastoitavaa tyyppiä voida myöhemmin vaihtaa.


## Alkeistietotyypit ja kääreluokat

Listoilla käsiteltävien arvojen on oltava olioita, eli ei aikaisemmilta viikoilta tuttuja alkeistietotyyppejä, kuten `boolean`, `int` tai `double`. 

Alkeistietotyyppien varastoimiseksi Javassa on olemassa valmiita **kääreluokkia**, joiden oliot pitävät vain sisällään tallessa yksittäisiää alkeistyyppisiä arvoja. Kääreluokat on nimetty kuten alkeistyypit, mutta niiden nimet alkavat isolla alkukirjaimella, esim: `Boolean`, `Integer` ja `Double`. Kääreluokan avulla numerosi "kääritään" olion sisälle, jolloin myös numeroita voidaan käsitellä listoilla.

Java huolehtii onneksi kääreluokkien käyttämisestä automaattisesti lähes jokaisessa operaatiossa. Sinun tulee ainoastaan määritellä listan tyypiksi käytettävä kääreluokka:

```java
ArrayList<Integer> kokonaisluvut = new ArrayList<>();

ArrayList<Double> liukuluvut = new ArrayList<>();

ArrayList<Boolean> totuusarvot = new ArrayList<>();
```


# Listaoperaatiot

Listoja käytetään aina kutsumalla listan metodeja. Seuraava oppituntitallenne käy läpi keskeiset listaoperaatiot, jotka on esitetty myös tekstimuodossa alempana.

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/f6bc6f3b-374d-4776-bb7c-981707c5f648?autoplay=false&amp;showinfo=true" allowfullscreen style="border:none;"></iframe>


## Listalle lisääminen

`add`-metodi lisää listalle uusia arvoja listan loppuun:

```java
List<String> sanat = new ArrayList<>();

sanat.add("Hello");
sanat.add("World");

System.out.println(sanat); // [Hello, World]
```

## Lisääminen tiettyyn indeksiin

Listalle voidaan lisätä myös arvoja tiettyyn indeksiin. Tällöin `add`-metodille annetaan ensimmäiseksi parametriarvoksi haluttu indeksi. Seuraavien listalla olevien arvojen indeksit kasvavat yhdellä:

```java
List<String> sanat = new ArrayList<>();

// lisätään arvoja listan loppuun:
sanat.add("Hello");
sanat.add("World");

// lisätään arvoja tiettyyn indeksiin:
sanat.add(0, "Terve");
sanat.add(1, "Maailma");

System.out.println(sanat); // [Terve, Maailma, Hello, World]
```

## Listalta hakeminen

Listalta voidaan hakea yksittäisiä arvoja `get`-metodin avulla. Muista, että listojen indeksit alkavat aina nollasta!

```java
List<String> sanat = new ArrayList<>();

sanat.add("Hello");
sanat.add("World");

System.out.println(sanat.get(0)); // Hello
System.out.println(sanat.get(1)); // World
```

## Listalta poistaminen

Listalta voidaan poistaa joko tietyn indeksin perusteella tai tiettyjä arvoja `remove`-metodin avulla. Muista, että listojen indeksit alkavat aina nollasta!

```java
List<String> sanat = new ArrayList<>();

sanat.add("Hello");
sanat.add("World");
sanat.add("!");

// poistetaan indeksin perusteella:
sanat.remove(0);

// poistetaan tietty arvo:
sanat.remove("World");

System.out.println(sanat); // [!]
```

## Listan sisällön tutkiminen

Listoilta voidaan etsiä alkioita kahdella metodilla:

* `contains` palauttaa `true`, jos annettu arvo löytyy jostain kohtaa listalta
* `indexOf` palauttaa sen indeksin, josta annettu arvo löytyy
* Huom! Listojen indeksit alkavat aina nollasta
* Huom! Jos annettua arvoa ei löydy, `indexOf` palauttaa luvun `-1`

```java
ArrayList<String> nimet = new ArrayList<>();

nimet.add("Matti");
nimet.add("Maija");

System.out.println(nimet.contains("Matti")); // true
System.out.println(nimet.indexOf("Maija")); // 1
System.out.println(nimet.indexOf("Maikki")); // -1, eli ei löydy!
```

## Listalla olevien arvojen lukumäärä

Listan koko selviää `size`-metodilla:

```java
List<String> sanat = new ArrayList<>();

sanat.add("Hello");
sanat.add("World");

int pituus = sanat.size();
System.out.println(pituus); // 2
```

Listan pituutta tarvitaan usein, kun halutaan käsitellä listan kaikkia arvoja niiden indeksien avulla.

## Listan arvojen läpikäynti (indeksillä)

* Listan sisältö on usein tarpeellista käydä läpi alusta loppuun
* Tämä voidaan toteuttaa toistorakenteella, jossa lähdetään liikkeelle nollasta ja edetään viimeiseen indeksiin
* Koska indeksit alkavat nollasta, viimeinen indeksi on aina yhtä pienempi kuin listan pituus: `int vikaIdeksi = lista.size() – 1;`
* Toistorakenteen sisällä listan arvot voidaan pyytää yksi kerrallaan get-metodin avulla: `lista.get(i)`


```java
import java.util.ArrayList;
import java.util.List;

public class ListanLapikayntiFor {

    public static void main(String[] args) {
        List<Integer> numerot = new ArrayList<>();
        numerot.add(321);
        numerot.add(456);
        numerot.add(789);

        // käydään kaikki listan arvot läpi:
        for (int i = 0; i < numerot.size(); i++) {
            System.out.println(numerot.get(i));
        }
    }
}
```

### Listan arvojen läpikäynti (for-each)

For-each –silmukalla on mahdollista käydä kätevästi kaikki tietyn listan arvot läpi ilman, että pidämme itse kirjaa indeksistä ja haemme arvoja `get`-metodilla:

```java
import java.util.ArrayList;
import java.util.List;

public class ListanLapikayntiForEach {

    public static void main(String[] args) {
        List<Integer> numerot = new ArrayList<>();
        numerot.add(321);
        numerot.add(456);
        numerot.add(789);

        // käydään kaikki listan arvot läpi:
        for (Integer arvo : numerot) {
            System.out.println(arvo);
        }
    }
}
```

Katso esim: [https://stackoverflow.com/a/22114571](https://stackoverflow.com/a/22114571)


## Oppituntitallenne: listan sisällön tutkiminen ja arvojen läpikäynti

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/65e4f154-7369-4165-bf0c-3e5ddc9a6569?autoplay=false&amp;showinfo=true" allowfullscreen style="border:none;"></iframe>


# Listan luominen valmiilla arvoilla

Toisinaan ohjelmassa on tarpeen luoda lista joillain valmiilla ennalta tunnetuilla arvoilla. Tällaisen listan luominen `new ArrayList<>()`-operaatiolla ja täyttäminen `add`-metodilla olisi kovin työlästä. Voit sen sijaan käyttää `List.of`-metodia, jolle voit antaa listan sisällön valmiina:

```java
List<String> viikonpaivat = List.of("ma", "ti", "ke", "to", "pe", "la", "su"); 
```

Muista myös lisätä luokan alkuun `import java.util.List;`.

Huom! `List.of`-metodin palauttama lista ei ole tavallinen `ArrayList`, eli et voi muokata yllä esitettyä listaa enää sen luomisen jälkeen. Muut operaatiot, kuten arvojen haku, etsiminen ja läpikäynti, toimivat normaalisti.


# Listamuuttujien yhteensopivuus

Vaikka `ArrayList` ja `LinkedList` ovat toiminnallisesti täysin samanlaiset, et voi asettaa eri tyyppistä listaa toisen tyyppiseen muuttujaan. Poikkeuksen tähän sääntöön tekee kaikkien listojen yhteisen rajapinnan määrittelevä `List`-tyyppi, joka on yhteensopiva kaikkien listojen kanssa:

```java
List<String> nimet = new ArrayList<>();
List<String> osoitteet = new LinkedList<>();
List<String> kaupungit = List.of("Helsinki", "Porvoo");
```

Käyttämällä `List`-tyyppiä muuttujien tyyppinä ja myöhemmin metodien parametrien tyyppinä, vältät useita ongelmatilanteita mahdollisten epäyhteensopivien listojen kanssa.

Muista, että tarvitset `List`-tyypille oman `import`-komennot luokan alkuun:

```java
import java.util.List;
```

<!--Jos muuttujan tyypiksi määriteltäisiin tarkasti `ArrayList<String>`, voisimme asettaa muuttujaan **ainoastaan** `ArrayList`-tyyppisen listan. Tällöin emme voisi käyttää esim. `List.of`-luontitapaa valmiin listan luomiseksi:

```java
// VIRHE: Type mismatch: cannot convert from List<String> to ArrayList<String>
ArrayList<String> lista = List.of("sana", "toinen"); 
```
```java
// Toimii, koska List<String> on yhteensopiva kaikkien merkkijonolistojen kanssa:
List<String> lista = List.of("sana", "toinen"); 
```
-->

# Listan järjestäminen

Lista on mahdollista järjestää eli helposti alkioiden "luonnolliseen järjestykseen". `Collections`-apuluokalla on olemassa `sort`-niminen metodi, joka järjestää sille annetun listan:

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class KaupunkienSorttaus {

    public static void main(String[] args) {
        List<String> kaupungit = new ArrayList<>();
        kaupungit.add("Rauma");
        kaupungit.add("Helsinki");
        kaupungit.add("Espoo");
        kaupungit.add("Vantaa");
        kaupungit.add("Turku");

        // Tulostaa siinä järjestyksessä, kun lisäsimme arvot:
        System.out.println(kaupungit); // [Rauma, Helsinki, Espoo, Vantaa, Turku]

        Collections.sort(kaupungit); // järjestää "luonnolliseen" järjestykseen

        // Lista on nyt eri järjestyksessä:
        System.out.println(kaupungit); // [Espoo, Helsinki, Rauma, Turku, Vantaa]
    }
}
```

Huomaa, että merkkijonojen luonnollinen järjestys ei toimi odotetusti eri kokoisia kirjaimia vertaillessa, koska vertailussa käytetään merkkien Unicode-arvoja.


# Listan kopioiminen ja viittaustyyppiset muuttujat

Seuraavalla oppituntitallenteella käsitellään listojen käsittelyä eri muuttujien kautta sekä listojen kopioimista uusien listojen luomista varten:

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/98536d7e-5621-4927-bc63-45299746dfa4?autoplay=false&amp;showinfo=true" allowfullscreen style="border:none;"></iframe>


```java
List<String> naiset = new ArrayList<>();
naiset.add("Tuula");
naiset.add("Anne");

List<String> miehet = new ArrayList<>();
miehet.add("Juha");
miehet.add("Timo");

List<String> molemmat = new ArrayList<>(naiset);
molemmat.addAll(miehet);
```


# Tehtäväideoita tunnille

## Nimigeneraattori

Kirjoitetaan ohjelma, joka arpoo satunnaisia sanoja erilaisista ryhmistä ja muodostaa yritysten, bändien tai henkilöiden nimiä.

Opittavat aiheet: listan muodostaminen, listan pituuden selvittäminen ja listalta haku.


## HTML-valintarakenne

Kirjoitetaan ohjelma, johon määritellään lista asioista, jotka esitetään toistorakenteella HTML-muodossa.

Opittavat aiheet: listan muodostaminen, listan kaikkien arvojen läpikäynti.


---

Tämän oppimateriaalin on kehittänyt Teemu Havulinna ja se on lisensoitu [Creative Commons BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/) -lisenssillä.

<script src="/tocbot/tocbot.min.js"></script>
<script src="/scripts.js"></script>
<link rel="stylesheet" href="/tocbot/tocbot.css">