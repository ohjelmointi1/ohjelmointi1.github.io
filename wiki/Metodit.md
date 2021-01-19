[&larr; Takaisin etusivulle](/)

<h1 class="js-toc-ignore">Metodit</h1>

Tämä dokumentti on tiivistelmä Helsingin yliopiston [Agile Education Research](https://www.helsinki.fi/en/researchgroups/data-driven-education) -tutkimusryhmän [MOOC-ohjelmointikurssin materiaalista](https://materiaalit.github.io/ohjelmointi-18/part2/). Tiivistelmä koostuu suorista lainauksista ja sitä on täydennetty Haaga-Helian ohjelmointikurssin sisällöllä. Lisenssi: [Creative Commons BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.fi).


**Sisällysluettelo**

<div class="js-toc"></div>



## Mikä on metodi?

Teknisesti ottaen metodi tarkoittaa nimettyä lauseista koostuvaa joukkoa, jota voi kutsua muualta ohjelmakoodista nimen perusteella. Yksi hyvin yleinen käyttämämme metodi on `println`:

```java
System.out.println("Hello world");
```

`println`-metodin toteutus pitää sisällään koodirivit, jotka tarvitaan sille annetun arvon tulostamiseksi. Metodin sisäinen toteutus -- eli joukko suoritettavia lauseita -- on tässä tapauksessa Java-ohjelmointikielen piilottama.


## Metodikutsun vaikutus ohjelman suoritukseen

Metodin suorituksen jälkeen palataan takaisin kohtaan, missä ennen metodikutsua oltiin menossa, ja ohjelman suoritus jatkuu tästä. 

Olemme tottuneet näkemään metodikutsun yhteydessä aina pisteen, esim. `lukija.nextLine()`. Tässä metodin nimi onkin pisteen oikeanpuoleinen osa, eli `nextLine()`. Pisteen vasemmanpuoleinen osa, eli tässä `lukija` kertoo kenen metodista on kyse.

Metodikutsun lopussa on aina sulut. Metodista riippuen sulkujen sisälle laitetaan arvoja tai sulut jätetään tyhjäksi.

## Metodin palauttama data, eli **paluuarvot**

Olemme nähneet kurssin aikana sekä metodeja, jotka eivät palauta lainkaan arvoja että metodeja, jotka tuottavat tuloksenaan jonkin arvon:

```java
// parseInt palauttaa int-tyyppisen arvon:
int luku = Integer.parseInt("1234");

// println ei palauta arvoa, joten se on void-tyyppinen:
System.out.println("Tämä metodi ei palauta arvoa");
```

Metodin koodista voidaan siis välittää arvoja takaisin metodia kutsuneelle koodille. Tämä tehdään `return`-avainsanalla, johon palaamme myöhemmin.


## Metodille annettava data, eli **parametriarvot**

Metodit tarvitsevat usein metodia kutsuvalta koodilta arvoja, joiden perusteella ne suorittavat toimintansa. Esimerkiksi `println` tarvitsee tulostettavan datan ja `parseInt` tarvitsee merkkijonon, jonka se tulkitsee numeroksi. Metodille välitettäviä arvoja kutsutaan **parametriarvoiksi**, ja ne kirjoitetaan metodikutsussa metodin nimen jälkeen tuleviin sulkuihin:

```java
// metodille välitetään merkkijono:
System.out.println("Tämä merkkijono välitetään parametrina");

// metodille välitetään kokonaislukuja:
int maksimi = Math.max(10, 20);

// metodille välitetään lista:
Collections.sort(omaLista);
```

Toiset metodit eivät tarvitse lainkaan parametriarvoja, jolloin metodikutsussa sulut jätetään tyhjiksi:

```java
Scanner lukija = new Scanner(System.in);

// monet metodit eivät tarvitse lainkaan parametriarvoja:
int i = lukija.nextInt();
String s = lukija.nextLine();
```

# Omien metodien määrittely

Javan valmiiden metodien käytön lisäksi ohjelmoija voi luonnollisesti myös itse kirjoittaa uusia metodeja. Metodit edesauttavat uudelleenkäytettävän ja ymmärrettävän koodin kirjoittamista ja mahdollistavat monipuolisempien sovellusten toteuttamisen. Ohjelman suorituksen ei enää tarvitse edetä yhdessä koodilohkossa ylhäältä alas, vaan suoritus voi edetä monipuolisemmin useita erilaisia reittejä.

Kuten käytännössä kaikki koodi, myös metodit kirjoitetaan luokan sisään eli luokan määrittelyssä esiteltyjen aaltosulkujen väliin. Metodeja ei voida määritellä sisäkkäin, eli kaikki metodit ovat luokan sisällä samalla tasolla peräkkäin. Metodien järjestyksellä ei ole Javan kannalta merkitystä.


## Main-metodi

Olemme kurssilla tähän asti määritellyt lukuisia kertoja main-metodin:

```java
public static void main(String[] args) {
    
}
```

Metodin otsikko koostuu tässä tapauksessa seuraavista avainsanoista:

* `public` – julkinen metodi, jota voidaan kutsua mistä vain
* `static` – staattinen eli luokkametodi, joka ei kuulu millekään yksittäiselle oliolle
* `void` – metodi ei palauta mitään arvoa
* `main` – metodin nimi, main-nimisellä metodilla on erityinen rooli ohjelman käynnistyksessä
* `String[] args` – yksi parametrimuuttuja: merkkijonotaulukko, jonka nimi on args

Metodin otsikon jälkeen kirjoitetaan aina aaltosulut `{   }`, joiden sisään kirjoitetaan metodin runko.

Muistiinpanojen seuraavat osat käsittelevät näiden merkitystä sekä sitä, mitä muita mahdollisia arvoja voimme käyttää näiden lisäksi.

Main-metodimme lisäksi voisimme hyvin määritellä luokkaamme kaksi muutakin metodia: `sayHello` ja `sayGoodbye`:

```java
public class Esimerkki {

    public static void main(String[] args) {
        sayHello();
        sayGoodbye();
    }

    public static void sayHello() {
        System.out.println("Hello!");
    }

    public static void sayGoodbye() {
        System.out.println("Goodbye!");
    }
}
```

Kumpikaan näistä metodeista ei saa parametriarvoja eikä palauta parametriarvoja, joten niiden vuorovaikutus main-metodin kanssa on vielä vähäistä.


## Metodien rakenne

Metodimäärittelyn ensimmäisellä rivillä on metodin nimi. Nimen vasemmalla puolella tässä vaiheessa määreet `public static void`:

```java
public static void tervehdi() {
    System.out.println("Terveiset metodista!");
}
```

Metodin nimen sisältävän rivin alla on aaltosulkeilla `{  }` erotettu koodilohko, jonka sisälle kirjoitetaan metodin koodi, eli ne komennot, jotka metodia kutsuttaessa suoritetaan. Metodin nimen voit itse valita, kunhan se noudattaa Javan nimeämissääntöjä.

## Metodien kutsuminen

Itsekirjoitetun metodin kutsu on helppoa, kirjoitetaan metodin nimi ja perään sulut ja puolipiste.

Seuraavassa main-metodi eli pääohjelma kutsuu tervehdi-metodia yhteensä neljä kertaa.

```java
public static void main(String[] args) {
    System.out.println("Kokeillaan metodia:");
    tervehdi();

    System.out.println("Toimii! Kokeillaan vielä:");
    tervehdi();
    tervehdi();
    tervehdi();
}

public static void tervehdi() {
    System.out.println("Terveiset metodista!");
}
```

```
Kokeillaan metodia:
Terveiset metodista!
Toimii! Kokeillaan vielä:
Terveiset metodista!
Terveiset metodista!
Terveiset metodista!
```

Katso tämä esimerkki Java Visualizerissa: [https://goo.gl/9E1E12](https://goo.gl/9E1E12)

<iframe style="width: 100%; height: 480px;" src="https://cscircles.cemc.uwaterloo.ca/java_visualize/iframe-embed.html?faking_cpp=false#data=%7B%22user_script%22%3A%22public%20class%20ToisenMetodinKutsuminen%20%7B%5Cn%20%20%20%5Cn%20%20%20public%20static%20void%20main(String%5B%5D%20args)%20%7B%5Cn%20%20%20%20%20%20System.out.println(%5C%22Kokeillaan%20metodia%3A%5C%22)%3B%5Cn%20%20%20%20%20%20tervehdi()%3B%5Cn%5Cn%20%20%20%20%20%20System.out.println(%5C%22Toimii!%20Kokeillaan%20viel%C3%A4%3A%5C%22)%3B%5Cn%20%20%20%20%20%20tervehdi()%3B%5Cn%20%20%20%20%20%20tervehdi()%3B%5Cn%20%20%20%20%20%20tervehdi()%3B%5Cn%20%20%20%7D%5Cn%5Cn%20%20%20public%20static%20void%20tervehdi()%20%7B%5Cn%20%20%20%20%20%20System.out.println(%5C%22Terveiset%20metodista!%5C%22)%3B%5Cn%20%20%20%7D%5Cn%5Cn%7D%22%2C%22options%22%3A%7B%22showStringsAsValues%22%3Atrue%2C%22showAllFields%22%3Afalse%7D%2C%22args%22%3A%5B%5D%2C%22stdin%22%3A%22%22%7D&cumulative=false&heapPrimitives=false&drawParentPointers=false&textReferences=false&showOnlyOutputs=false&py=3&curInstr=0&resizeContainer=true&highlightLines=true&rightStdout=true" frameborder="0" scrolling="no"></iframe>

## Metodien nimeäminen ja sisennykset

Metodit nimetään siten, että ensimmäinen sana kirjoitetaan pienellä ja loput alkavat isolla alkukirjaimella. Tällaisesta kirjoitustavasta käytetään nimitystä **camelCase**. Tämän lisäksi, metodin sisällä koodi on sisennetty taas neljä merkkiä.

Käytännöt metodien nimeämiselle ja sisentämiselle vaihtelevat eri ohjelmointikielten välillä.

```java
// OK:
public static void tamaMetodiSanooMur() { 
    System.out.println("mur"); 
}

// ei ok:
public static void Tama_metodi_sanoo_mur ( ) { 
System.out.println("mur"); 
}
```

## Parametriarvot ja paluuarvot

Metodille suluissa annettua syötettä kutsutaan metodin parametriksi -- metodin parametreilla annetaan metodeille tarkempaa tietoa odotetusta suorituksesta. Esimerkiksi tulostuslauseelle kerrotaan parametrin avulla mitä pitäisi tulostaa.

```java
// Ensin kutsutaan scannerin metodia lukija.nextLine.
// Metodi palauttaa paluuarvonaan käyttäjän syöttämän merkkijonon, joka asetetaan talteen muuttujaan. 
String syote = lukija.nextLine();

// Seuraavaksi kutsutaan metodia Integer.parseInt. Metodikutsun parametrina annetaan
// merkkijono, jonka edellisen metodin kutsu palautti. parseInt-metodin paluuarvo
// puolestaan on annettua merkkijonoa vastaava kokonaisluku. 
// Lopuksi parseInt-metodin palauttama arvo asetetaan talteen uuteen muuttujaan.
int luku = Integer.parseInt(syote);
```

Paluuarvoa voidaan heti käyttää myös parametrina:

```java
// Ensin kutsutaan sisempänä olevaa metodia lukija.nextLine.
// Metodi palauttaa paluuarvonaan käyttäjän syöttämän merkkijonon. 
// Seuraavaksi kutsutaan metodia Integer.parseInt. 
// Metodikutsun parametrina välitetään merkkijono, jonka nextLine-metodin kutsu palautti. 
Metodin paluuarvona on merkkijonoa vastaava kokonaisluku, joka asetetaan talteen uuteen muuttujaan.
int luku = Integer.parseInt(lukija.nextLine());
```

## Parametrimuuttujat ja parametriarvot omissa metodeissa

**Parametrit** ovat siis **metodille annettavia arvoja**, joita käytetään metodin suorituksessa. Metodin **parametrimuuttujat** määritellään metodin ylimmällä rivillä metodin nimen jälkeen olevien sulkujen sisällä.

Kun metodia kutsutaan, sen **parametrimuuttujiin** asetetaan annetut arvot. Metodin sisällä annettu **arvo on käytettävissä parametrimuuttujan kautta**.


### Esimerkki: AgenttiTervehdys

```java
public class AgenttiTervehdys {

    public static void main(String[] args) {
        // metodikutsussa on annettava arvot, jotka vastaavat metodiin määriteltyjä parametreja
        tervehdi("James", "Bond");
        tervehdi("Gracie", "Hart");
    }

    // 'etu' ja 'suku' ovat String-muuttujia, joita kutsutaan parametrimuuttujiksi
    public static void tervehdi(String etu, String suku) {
        System.out.println("Nimeni on " + suku +             ", " + etu + " " + suku);
    }
}
```
Katso tämä esimerkki Java Visualizerissa: https://goo.gl/cahGq1

### Esimerkki: tilaston tulostaminen

Seuraavassa esimerkissä haluamme tulostaa toistuvasti otsikoita "## Otsikko ##"-syntaksilla. Otsikkojen tulostaminen on siirretty omaan metodiinsa, jotta samaa koodia ei tarvitse toistaa moneen kertaan ja jotta mahdolliset muutokset otsikon tyyliin voidaan tehdä vain yhteen kohtaan ohjelmassa:

```java
public class KoodinPilkkominenOsiinVoidMetodeilla {

    public static void main(String[] args) {
        // Määritellään metodi, joka tulostaa tekstin ja laittaa ympärille "##"-merkit
        tulostaOtsikko("Tammikuun sademäärät");
        tulostaTilasto(10, 15, 6);

        System.out.println();

        // metodikutussa voi olla ihan eri nimiset muuttujat kuin metodin otsikossa:
        // vrt. "helmikuunOtsikko" ja "otsikko"
        String helmikuunOtsikko = "Helmikuun sademäärät";
        tulostaOtsikko(helmikuunOtsikko);
        tulostaTilasto(11, 18, 9);
    }

    private static void tulostaOtsikko(String otsikko) {
        // Tässä metodissa ei ole edes pääsyä main-metodin muuttujiin!
        System.out.println("## " + otsikko + " ##");
    }

    // Tälle metodille annetaan aina KOLME parametriarvoa
    private static void tulostaTilasto(int keskiarvo, int suurin, int pienin) {
        System.out.println("Keskiarvo: " + keskiarvo);
        System.out.println("Suurin: " + suurin);
        System.out.println("Pienin: " + pienin);
    }
}
```
[Tutustu koodin suoritukseen Visualizerissa](https://cscircles.cemc.uwaterloo.ca/java_visualize/#code=public+class+KoodinPilkkominenOsiinVoidMetodeilla+%7B%0A%0A++++public+static+void+main(String%5B%5D+args)+%7B%0A++++++++//+M%C3%A4%C3%A4ritell%C3%A4%C3%A4n+metodi,+joka+tulostaa+tekstin+ja+laittaa+ymp%C3%A4rille+%22%23%23%22-merkit%0A++++++++tulostaOtsikko(%22Tammikuun+sadem%C3%A4%C3%A4r%C3%A4t%22)%3B%0A++++++++tulostaTilasto(10,+15,+6)%3B%0A%0A++++++++System.out.println()%3B%0A%0A++++++++//+metodikutussa+voi+olla+ihan+eri+nimiset+muuttujat+kuin+metodin+otsikossa%0A++++++++String+helmikuunOtsikko+%3D+%22Helmikuun+sadem%C3%A4%C3%A4r%C3%A4t%22%3B%0A++++++++tulostaOtsikko(helmikuunOtsikko)%3B%0A++++++++tulostaTilasto(11,+18,+9)%3B%0A++++%7D%0A%0A++++private+static+void+tulostaOtsikko(String+otsikko)+%7B%0A++++++++//+T%C3%A4ss%C3%A4+metodissa+ei+ole+edes+p%C3%A4%C3%A4sy%C3%A4+main-metodin+muuttujiin!%0A++++++++System.out.println(%22%23%23+%22+%2B+otsikko+%2B+%22+%23%23%22)%3B%0A++++%7D%0A%0A++++//+T%C3%A4lle+metodille+annetaan+aina+KOLME+parametriarvoa%0A++++private+static+void+tulostaTilasto(int+keskiarvo,+int+suurin,+int+pienin)+%7B%0A++++++++System.out.println(%22Keskiarvo%3A+%22+%2B+keskiarvo)%3B%0A++++++++System.out.println(%22Suurin%3A+%22+%2B+suurin)%3B%0A++++++++System.out.println(%22Pienin%3A+%22+%2B+pienin)%3B%0A++++%7D%0A%7D&mode=display&curInstr=0)


## Metodin paluuarvot ja return-käsky

Jos metodi palauttaa arvon, tulee metodin määrittelyn yhteydessä kertoa palautettavan arvon tyyppi. Muulloin määrittelyssä käytetään avainsanaa `void`. `void` metodit eivät koskaan voi palauttaa arvoja.

Konkreettinen arvon palautus tapahtuu komennolla `return`, jota seuraa palautettava arvo (tai muuttujan tai lauseke, jonka arvo palautetaan).

Jos metodille määritellään paluuarvon tyyppi, on sen **pakko** palauttaa arvo.

```java
public static void main(String[] args) {
    // metodin suorituksen jälkeen sen palauttama arvo voidaan ottaa talteen:
    int luku = palautetaanAinaKymppi();

    System.out.println("metodi palautti: " + luku);
}

public static int palautetaanAinaKymppi() {
    // return-käsky palauttaa sen jälkeen olevan arvon:
    return 10;
}
```

## Monta parametriarvoa ja muuttujat metodin sisällä

Metodille voidaan määritellä useita parametreja. Tällöin metodin kutsussa parametrit annetaan samassa järjestyksessä. Muuttujien määrittely muissa metodeissa tapahtuu aivan kuten main-metodissa. 

Seuraava metodi laskee parametrina saamiensa lukujen keskiarvon. Keskiarvon laskemisessa käytetään apumuuttujia `summa` ja `ka`. Nämä **paikalliset muuttujat**, aivan kuten parametrimuuttujat `luku1`, `luku2` ja `luku3`, ovat voimassa ainoastaan metodin sisällä.

```java
public static double keskiarvo(int luku1, int luku2, int luku3) {

    int summa = luku1 + luku2 + luku3;
    double ka = summa / 3.0;

    return ka;
}
```

**Huomaa että metodin sisäiset muuttujat summa ja ka eivät näy metodin ulkopuolelle. Sama koskee myös parametrimuttujia luku1, luku2 ja luku3.**

Tulos voidaan palauttaa myös suoraan ilman sen tallentamista väliaikaiseen muuttujaan. Tämä onkin usein varsin tyypillistä:

```java
// sama kuin yllä, mutta ilman väliaikaisia  muuttujia "summa" ja "ka"
public static double keskiarvo(int luku1, int luku2, int luku3) {
    return (luku1 + luku2 + luku3) / 3.0;
}
```

## Muuttujien näkyvyys ja nimeäminen

Metodin parametrimuuttujien nimillä ei ole vaikutusta metodin ulkopuolelle. Metodikutsuissa voidaan käyttää aivan eri nimisiä muuttujia, esim:

```java
public static void main(String[] args) {
    int a = 10;
    int b = 14;
    int c = 42;

    // metodikutsussa on muuttujat a, b ja c, metodin parametrimuuttujat ovat luku1, luku2 ja luku3
    double kesk = keskiarvo(a, b, c);

    // ...
}

public static double keskiarvo(int luku1, int luku2, int luku3) {

    int summa = luku1 + luku2 + luku3;
    double ka = summa / 3.0;

    return ka;
}
```

## Muissa luokissa määriteltyjen metodien kutsuminen

Samassa luokassa olevan metodin kutsuminen oli helppoa: kirjoitetaan vain metodin nimi, sulut ja tarvittaessa parametriarvot.

Toisessa luokassa olevaa metodia kutsutaan **joko luokan tai olion kautta** riippuen siitä, onko kyseessä ns. staattinen luokkametodi vai oliometodi:

```java
String teksti = "Merkkijonot ovat olioita";

// toLowerCase on oliokohtainen, eli sitä kutsutaan esimerkiksi muuttujan kautta:
String pienella = teksti.toLowerCase();

// Math-luokan min-metodi ei kuulu oliolle, eli sitä kutsutaan suoraan luokan nimellä:
int pienin = Math.min(12, 15);
```

### Esimerkki luokkien välisistä metodikutsuista

Ohjelman suoritus käynnistyy `Nimirekisteri`-luokan `main`-metodissa, josta kutsutaan `NimenLyhentaja`-luokan `lyhenna`-metodia:

```java
/*
 * Harjoitellaan toisessa luokassa olevan metodin kutsumista!
 */
public class Nimirekisteri {

    public static void main(String[] args) {
        String keke = NimenLyhentaja.lyhenna("Keijo", "Rosberg");
        System.out.println(keke);

        String kimi = NimenLyhentaja.lyhenna("Kimi", "Räikkönen");
        System.out.println(kimi);

        // paluuarvoa voidaan käyttää myös suoraan seuraavan metodikutsun
        // parametriarvona:
        System.out.println(NimenLyhentaja.lyhenna("Mika", "Häkkinen"));
    }
}
```

```java
public class NimenLyhentaja {

    public static String lyhenna(String etunimi, String sukunimi) {

        // Muuntaa "Keijo" ja "Rosberg" -> "K. Rosberg"
        String lyhennetty = etunimi.substring(0, 1) + ". " + sukunimi;

        return lyhennetty;
    }

}
```

## Metodien näkyvyys, eli mistä metodia voidaan kutsua

Näkyvyys        | Selitys
----------------|-------------
public          | Metodi on käytettävissä kaikkialta
private         | Metodi on käytettävissä ainoastaan saman luokan sisältä
protected       | Metodi on käytettävissä saman luokan ja paketin sisältä, sekä aliluokista
(tyhjä)         | **Hyvin harvoin käytetty.** Käytettävissä saman luokan ja paketin sisältä. 

```java
public String julkinen() {
    return "käytettävissä missä tahansa";
}

private String yksityinen() {
    return "käytettävissä vain tästä luokasta";
}

protected String suojattu() {
    return "käytettävissä mm. aliluokista";
}

String oletusnakyvyys() {
    return "en suosittele tällaista näkyvyyttä";
}
```

## Vilkaisu olio-ohjelmointiin: luokkametodit ja oliometodit

Metodit määritellään aina joko luokkametodeiksi tai oliometodeiksi. **Staattiset eli luokkametodit** ovat käytettävissä sen luokan kautta, johon ne on määritetty.

**Oliometodit ovat käytettävissä olioiden kautta**, eikä niitä voida kutsua ilman olioita.

Toistaiseksi määrittelemme kaikki metodit staattisiksi, vaikka olemmekin hyödyntäneet useita oliometodeja mm. String ja Scanner –luokista.

**Esimerkki.java**

```java
public class Esimerkki {

    public static void staattinenMetodi() {
        System.out.println("staattinen eli luokkametodi");
    }

    // metodin otsikosta puuttuu 'static'
    public void olioMetodi() {
        System.out.println("oliokohtainen metodi");
    }
}
```

**Ohjelma.java**

```java
public class Ohjelma {
    public static void main(String[] args) {
        // Luokkametodia kutsutaan luokan kautta:
        Esimerkki.staattinenMetodi();

        // Oliometodin kutsua varten tarvitaan olio:
        Esimerkki olio = new Esimerkki();
        olio.olioMetodi();
    }
}
```

## Arvojen muuttaminen metodissa

Ns. perustietotyyppien arvot (int, double) kopioituvat metodikutsussa, eikä niiden käsittely metodissa vaikuta koskaan sinne, mistä metodikutsu tehtiin.

**Oliot puolestaan välittyvät viittauksina**, eli niiden muutokset näkyvät myös arvoa muuttavan metodin ulkopuolelle.

```java
public static void tulostaJarjestyksessa(List<Integer> numerot) {
    // Listan järjestäminen metodin sisällä muuttaa 
    // järjestyksen myös siellä, mistä tätä metodia 
    // kutsuttiin, koska listaa ei kopioida metodikutsussa
    Collections.sort(numerot);
    System.out.println(numerot);
}
```

Esimerkki: listan muuttuminen metodissa

```java
public static void main(String[] args) {
    List<Integer> lukuja = Arrays.asList(3, 1, 2);

    // minimi-metodi muuttaa tätä lukuja-listaa ja muutos näkyy myös tässä metodissa
    int minimi = pienin(lukuja);

    System.out.println(lukuja); // [1, 2, 3]
}

public static int pienin(List<Integer> arvot) {
    // collections.sort muuttaa sille annetun listan järjestystä:
    Collections.sort(arvot);

    // palauttaa ensimmäisen, eli pienimmän
    return arvot.get(0);
}
```

Tutustu interaktiiviseen esimerkkiin arvojen muuttumisesta ja muuttumattomuudesta [Java Visualizer-palvelussa](https://cscircles.cemc.uwaterloo.ca/java_visualize/#code=public+class+PassByValue+%7B%0A+++%0A+++static+void+reset(int+x)+%7B%0A++++++x+%3D+0%3B%0A+++%7D%0A+++%0A+++static+void+reset(int%5B%5D+x)+%7B%0A++++++for+(int+i+%3A+x)+%0A+++++++++i+%3D+0%3B%0A+++%7D%0A+++%0A+++static+void+reallyReset(int%5B%5D+x)+%7B%0A++++++for+(int+i%3D0%3B+i%3Cx.length%3B+i%2B%2B)%0A+++++++++x%5Bi%5D+%3D+0%3B%0A+++%7D%0A+++%0A+++public+static+void+main(String%5B%5D+args)+%7B%0A++++++int+a+%3D+3%3B%0A++++++int%5B%5D+arr+%3D+%7B5,+10,+15%7D%3B%0A++++++%0A++++++reset(a)%3B+//+this+won't+work%0A++++++System.out.println(a)%3B%0A++++++%0A++++++reset(arr)%3B+//+this+won't+work%0A++++++System.out.println(java.util.Arrays.toString(arr))%3B%0A++++++%0A++++++reallyReset(arr)%3B+//+this+works!%0A++++++System.out.println(java.util.Arrays.toString(arr))%3B%0A+++%7D%0A+++%0A%7D&mode=display&curInstr=0)!

---

Tämä dokumentti on tiivistelmä Helsingin yliopiston [Agile Education Research](https://www.helsinki.fi/en/researchgroups/data-driven-education) -tutkimusryhmän [MOOC-ohjelmointikurssin materiaalista](https://materiaalit.github.io/ohjelmointi-18/part2/). Tiivistelmä koostuu suorista lainauksista ja sitä on täydennetty Haaga-Helian ohjelmointikurssin sisällöllä. Lisenssi: [Creative Commons BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.fi).


<script src="/tocbot/tocbot.min.js"></script>
<script src="/scripts.js"></script>
<link rel="stylesheet" href="/tocbot/tocbot.css">