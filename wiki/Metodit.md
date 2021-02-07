[&larr; Takaisin etusivulle](/)

<h1 class="js-toc-ignore">(Staattiset) metodit</h1>

Olemme käyttäneet ohjelmointikurssilla aikaisempien aiheiden yhteydessä lukuisia valmiita metodeja. Metodit ovat olleet luonteva osa ongelmanratkaisua, vaikka emme ole toistaiseksi kiinnittäneet niihin suurta huomiota tai toteuttaneet omia metodeja `main`-metodia lukuun ottamatta.

Tällä kertaa perehdymme tarkemmin omien **staattisten metodien** toteuttamiseen ja kutsumiseen sekä siihen, miten voimme välittää arvoja metodista toiseen ja takaisin. Emme vielä harjoittele olio-ohjelmoinnin käytäntöjä, joten palaamme asiaan oliometodien osalta myöhemmin olio-ohjelmoinnin yhteydessä.

Syitä oman ohjelman jakamiseksi useisiin metodeihin on lukuisia. Ensinnäkin metodien avulla voidaan vähentää toisteisuutta, jos samoja operaatioita tehdään useita kertoja tai useissa eri kohdissa koodia. Toiseksi metodien avulla voidaan vähentää kompleksisuutta, eli pilkkoa iso monimutkainen kokonaisuus pienemmiksi, helpommin ymmärrettäviksi paloiksi. Myöhemmin kurssilla olio-ohjelmoinnin yhteydessä metodien merkitys kasvaa entisestään, kun metodeista tulee oliokohtaisia.

Tämä oppimateriaali pohjautuu Helsingin yliopiston [Agile Education Research](https://www.helsinki.fi/en/researchgroups/data-driven-education) -tutkimusryhmän [MOOC-ohjelmointikurssin materiaaliin](https://materiaalit.github.io/ohjelmointi-18/part2/), jota suositellaan myös tälle ohjelmointikurssille. Lisenssi: [Creative Commons BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.fi).


**Sisällysluettelo**

<div class="js-toc"></div>


# Metodien käsitteet ja metodikutsut

Olemme tähän mennessä hyödyntäneet Javan standardikirjaston staattisia metodeja mm. `Integer`, `Double`, `Math`, `Arrays` ja `Collections` -luokista. Metodikutsuissa on esiintynyt tyypillisesti luokan nimi, metodin nimi ja sulut, joiden sisälle on määritelty metodille annettava data. Olemme puolestaan hyödyntäneet metodien palauttamia arvoja sijoittamalla niitä esimerkiksi uusiin muuttujiin. Käsittelemme seuraavissa kappaleissa näitä käsitteitä ja niihin liittyviä esimerkkejä.

## Parametriarvot

Metodin kutsumisessa olemme hyödyntäneet **parametriarvoja**, joiden avulla olemme välittäneet tietoa omasta koodistamme Javan standardikirjastossa toteutetuille koodiriveille:

```java
int pienempi = Math.min(42, 24);

int numero = Integer.parseInt("42");
```

Toiset metodit eivät tarvitse lainkaan ulkopuolisia arvoja toimiakseen. Näiden metodien kutsussa ei välitetä arvoja:

```java
LocalDate tanaan = LocalDate.now();
```

Vaikka metodille ei välitettäisi arvoja, kirjoitetaan silti metodikutsuun tyhjät sulut.


## Paluuarvot

Vastaavasti olemme vastaanottaneet **paluuarvoja**, eli dataa, jonka metodi palauttaa sen suorituksen päätyttyä:

```java
int paluuarvo = Integer.parseInt("42");
```

Yllä olevissa koodiesimerkeissä Javan `Math`-luokassa sijaitseva `min` on metodi, jolle välitetään kaksi parametriarvoa, ja joka palauttaa suorituksensa jälkeen takaisin paluuarvon.

Kaikki metodit eivät välttämättä tarvitse parametriarvoja tai palauta paluuarvoja. Esimerkiksi `System.out.println` **ei palauta** paluuarvoa, vaan se pelkästään tulostaa saamansa parametriarvon konsoliin:

```java
System.out.println("println-metodi ei palauta arvoa");
```

Metodit, jotka eivät palauta arvoja, merkitäänn myöhemmin **void**-avainsanalla.

# Ohjelman suorituksen eteneminen metodikutsuissa

Ohjelman suorituksen edetessä metodikutsuun, siirtyy suoritus suoritettavalta riviltä toisaalle. Kesken jäänyt metodi ja kaikki siinä paikallisesti olevat muuttujat jävät edelleen muistiin niin sanottuun kutsupinoon:

> *"Java-lähdekoodin suoritusympäristö pitää kirjaa suoritettavasta metodista kutsupinossa. Kutsupino sisältää kehyksiä, joista jokainen sisältää tiedon kyseisen metodin sisäisistä muuttujista sekä niiden arvoista. Kun metodia kutsutaan, kutsupinoon luodaan uusi kehys, joka sisältää metodin sisältämät muuttujat. Kun metodin suoritus loppuu, metodiin liittyvä kehys poistetaan kutsupinosta, jolloin suoritusta jatketaan kutsupinon edeltävästä metodista."*
>
> *"Kutsupino tarkoittaa metodien kutsumisen muodostamaa pinoa — juuri suoritettevana oleva metodi on aina pinon päällimmäisenä, ja metodin suorituksen päättyessä palataan pinossa seuraavana olevaan metodiin."*
>
> [Agile Education Research, 2019](https://www.helsinki.fi/en/researchgroups/data-driven-education). [Ohjelman pilkkominen osiin: metodit](https://ohjelmointi-19.mooc.fi/osa-2/3-metodit). [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.fi)

Metodit kutsuvat hyvin usein yhtä tai useampaa muuta metodia, joten kutsupino koostuu tyypillisesti lukuisista keskeneräisistä "kehyksistä".

<!--
# Metodille annettava data, eli **parametriarvot**

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
-->

# Metodin määrittely

Olemme kurssilla tähän asti määritelleet lukuisia kertoja main-metodin:

```java
public static void main(String[] args) {
    
}
```

Metodin otsikko koostuu tässä tapauksessa seuraavista avainsanoista:

* `public` – julkinen metodi, jota voidaan kutsua mistä vain
* `static` – staattinen eli luokkametodi, joka ei kuulu millekään yksittäiselle oliolle
* `void` – metodi ei palauta mitään arvoa
* `main` – metodin nimi, main-nimisellä metodilla on erityinen rooli ohjelman käynnistyksessä
* `String[] args` – yksi parametrimuuttuja: merkkijonotaulukko, jonka nimi on `args`

Metodin otsikon jälkeen kirjoitetaan aina aaltosulut `{   }`, joiden sisään kirjoitetaan metodin runko, kuten olemme aikaisemmissa harjoituksissa tehneet.

`static`-avainsana liittyy käyttämäämme staattiseen ohjelmointityyliin, jossa emme vielä mallinna ohjelmaa olioiden avulla. Toistaiseksi kaikki kirjoittamamme metodit kirjoitetaan staattisiksi, eli luokkametodeiksi, mutta käsittelemme tätä tarkemmin siirtyessämme myöhemmillä viikoilla olio-ohjelmointiin.

`void`-avainsana tarkoittaa, että metodi ei palauta mitään arvoa. Tällaista metodia kutsuttaessa sen tulosta ei voida esim. asettaa muuttujaan tai muilla tavoin hyödyntää.

Sulkujen sisällä esiintyvä `String[] args` on metodin parametrimuuttuja, johon palaamme alempana tässä materiaalissa.

## Muut omat metodit

Kuten `main`-metodi, myös muut metodit kirjoitetaan luokan sisään, eli lähdekooditiedoston uloimpien aaltosulkujen väliin. Metodeja ei voida määritellä sisäkkäin, eli kaikki metodit ovat luokan sisällä samalla tasolla peräkkäin. Metodien keskenäisellä järjestyksellä ei ole Javan kannalta merkitystä.

Yksinkertaisimmillaan metodi ei tarvitse lainkaan parametriarvoja eikä se palauta paluuarvoa. Tällöin siis sen otsikossa sulut ovat tyhjät `()` ja paluuarvon tyyppinä on `void` (tyhjä). Metodin nimen voit itse valita, kunhan se noudattaa Javan nimeämissääntöjä. Main-metodia mukaillen voisimme siis kirjoittaa seuraavan oman metodin:

```java
public static void tulostaKellonaika() {
    LocalTime kellonaika = LocalTime.now();
    System.out.println("Kello on " + kellonaika);
}
```

Yllä oleva metodi ei ota lainkaan parametriarvoja tai palauta uutta arvoa, mutta se voisi olla silti hyödyllinen ohjelmassa, jossa on tarpeen tulostaa kellonaikaa eri kohdissa.

Tätä metodia kutsuttaessa saman luokan sisällä kirjoitetaan yksinkertaisesti metodin nimi `tulostaKellonaika` ja tyhjät sulut:

```java
tulostaKellonaika();
```

Vastaavasti voisimme kirjoittaa esimerkiksi `tulostaPaivamaara`-metodin ja kutsua näitä molempia `main`-metodista:

```java
import java.time.LocalDate;
import java.time.LocalTime;

public class Metodit {

    public static void main(String[] args) {
        tulostaPaivamaara();
        tulostaKellonaika();
    }

    public static void tulostaPaivamaara() {
        LocalDate tanaan = LocalDate.now();
        System.out.println("Päivämäärä on " + tanaan);
    }

    public static void tulostaKellonaika() {
        LocalTime kellonaika = LocalTime.now();
        System.out.println("Kello on " + kellonaika);
    }
}
```

Kumpikaan edellä määritellyistä omista metodeista ei vastaanota parametriarvoja eikä palauta parametriarvoja, joten niiden vuorovaikutus main-metodin kanssa on vielä vähäistä.

Voit tutustua metodien suoritusjärjestykseen [Java Visualizer -visualisoinnin](https://cscircles.cemc.uwaterloo.ca/java_visualize/#code=import+java.time.LocalDate%3B%0Aimport+java.time.LocalTime%3B%0A%0Apublic+class+Metodit+%7B%0A%0A++++public+static+void+main(String%5B%5D+args)+%7B%0A++++++++tulostaPaivamaara()%3B%0A++++++++tulostaKellonaika()%3B%0A++++%7D%0A%0A++++public+static+void+tulostaPaivamaara()+%7B%0A++++++++LocalDate+tanaan+%3D+LocalDate.now()%3B%0A++++++++System.out.println(%22P%C3%A4iv%C3%A4m%C3%A4%C3%A4r%C3%A4+on+%22+%2B+tanaan)%3B%0A++++%7D%0A%0A++++public+static+void+tulostaKellonaika()+%7B%0A++++++++LocalTime+kellonaika+%3D+LocalTime.now()%3B%0A++++++++System.out.println(%22Kello+on+%22+%2B+kellonaika)%3B%0A++++%7D%0A%7D&mode=display&curInstr=0) avustuksella:

<iframe style="width: 100%; height: 480px;" src="https://cscircles.cemc.uwaterloo.ca/java_visualize/iframe-embed.html?faking_cpp=false#data=%7B%22user_script%22%3A%22import%20java.time.LocalDate%3B%5Cnimport%20java.time.LocalTime%3B%5Cn%5Cnpublic%20class%20Metodit%20%7B%5Cn%5Cn%20%20%20%20public%20static%20void%20main(String%5B%5D%20args)%20%7B%5Cn%20%20%20%20%20%20%20%20tulostaPaivamaara()%3B%5Cn%20%20%20%20%20%20%20%20tulostaKellonaika()%3B%5Cn%20%20%20%20%7D%5Cn%5Cn%20%20%20%20public%20static%20void%20tulostaPaivamaara()%20%7B%5Cn%20%20%20%20%20%20%20%20LocalDate%20tanaan%20%3D%20LocalDate.now()%3B%5Cn%20%20%20%20%20%20%20%20System.out.println(%5C%22P%C3%A4iv%C3%A4m%C3%A4%C3%A4r%C3%A4%20on%20%5C%22%20%2B%20tanaan)%3B%5Cn%20%20%20%20%7D%5Cn%5Cn%20%20%20%20public%20static%20void%20tulostaKellonaika()%20%7B%5Cn%20%20%20%20%20%20%20%20LocalTime%20kellonaika%20%3D%20LocalTime.now()%3B%5Cn%20%20%20%20%20%20%20%20System.out.println(%5C%22Kello%20on%20%5C%22%20%2B%20kellonaika)%3B%5Cn%20%20%20%20%7D%5Cn%7D%22%2C%22options%22%3A%7B%22showStringsAsValues%22%3Atrue%2C%22showAllFields%22%3Afalse%7D%2C%22args%22%3A%5B%5D%2C%22stdin%22%3A%22%22%7D&cumulative=false&heapPrimitives=false&drawParentPointers=false&textReferences=false&showOnlyOutputs=false&py=3&curInstr=0&resizeContainer=true&highlightLines=true&rightStdout=true" frameborder="0" scrolling="no"></iframe>

## Metodien nimeäminen ja sisennykset

> *"Metodit nimetään siten, että ensimmäinen sana kirjoitetaan pienellä ja loput alkavat isolla alkukirjaimella, tälläisestä kirjoitustavasta käytetään nimitystä camelCase. Tämän lisäksi, metodin sisällä koodi on sisennetty taas neljä merkkiä."*
>
> [Agile Education Research, 2019](https://www.helsinki.fi/en/researchgroups/data-driven-education). [Ohjelman pilkkominen osiin: metodit](https://ohjelmointi-19.mooc.fi/osa-2/3-metodit). [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.fi)

```java
// OK:
public static void tulostaPaivamaara() {
    LocalDate tanaan = LocalDate.now();
    System.out.println("Päivämäärä on " + tanaan);
}

// ei ok:
public static void Tulosta_paivamaara() {
LocalDate tanaan = LocalDate.now();
System.out.println("Päivämäärä on " + tanaan);
}
```

Yhtenäinen nimeämistyyli helpottaa sekä koodin ymmärtämistä että kirjoittamista. Käytännöt metodien nimeämiselle ja sisentämiselle vaihtelevat eri ohjelmointikielten välillä, mutta jokaisessa kielessä on omat parhaat käytäntönsä.

# Metodin parametrit

> *"Metodille suluissa annettua syötettä kutsutaan metodin parametriksi — metodin parametreilla annetaan metodeille tarkempaa tietoa odotetusta suorituksesta; esimerkiksi tulostuslauseelle kerrotaan parametrin avulla mitä pitäisi tulostaa."*
>
> [Agile Education Research, 2019](https://www.helsinki.fi/en/researchgroups/data-driven-education). [Ohjelman pilkkominen osiin: metodit](https://ohjelmointi-19.mooc.fi/osa-2/3-metodit). [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.fi)

Metodin sisällä sille annetut parametriarvot ovat käytettävissä otsikon sulkujen sisälle määriteltyjen **parametrimuuttujien** avulla. Parametrimuuttujat ovat käytännössä kuin mitkä tahansa metodin paikalliset muuttujat, mutta niihin asetetaan arvot automaattisesti metodikutsun yhteydessä:

```java
tulostaOtsikko("Ohjelmointi 1 - Metodit"); // teksti välitetään metodille parametrina
```

```java
public static void tulostaOtsikko(String otsikko) {
    System.out.println("<h1>" + otsikko + "</h1>");
}
```

Yllä olevan metodin kutsun on luonnollisesti oltava jonkun toisen metodin sisällä. Seuraavassa pienessä luokassa `main`-metodista kutsutaan `tulostaOtsikko`-metodia:

```java
public class Parametrimuuttuja {

    public static void main(String[] args) {
        String nimi = "Ohjelmointi 1 - Metodit";
        tulostaOtsikko(nimi);
    }

    public static void tulostaOtsikko(String otsikko) {
        System.out.println("<h1>" + otsikko + "</h1>");
    }
}
```

Huomaa, että sekä `main`-metodin sisällä määritelty `nimi` että `tulostaOtsikko`-metodissa määritelty `otsikko` ovat paikallisia muuttujia, eivätkä ne näy metodien ulkopuolelle. Metodikutsussa käytetään siis esimerkissä eri nimistä muuttujaa kuin metodin otsikossa. Muuttujien nimillä ei ole lainkaan merkitystä, koska metodikutsussa välitetään ainoastaan arvo, eli itse merkkijono.


# Metodin paluuarvot ja return-käsky

> *"Metodin määrittelyssä kerrotaan palauttaako metodi arvon. Jos metodi palauttaa arvon, tulee metodimäärittelyn yhteydessä kertoa palautettavan arvon tyyppi. Muulloin määrittelyssä käytetään avainsanaa void. Tähän mennessä tekemämme metodit ovat määritelty avainsanaa void käyttäen eli eivät ole palauttaneet arvoa."*
> 
> *"Konkreettinen arvon palautus tapahtuu komennolla `return`, jota seuraa palautettava arvo (tai muuttujan tai lauseke, jonka arvo palautetaan)."*
>
> [Agile Education Research, 2019](https://www.helsinki.fi/en/researchgroups/data-driven-education). [Ohjelman pilkkominen osiin: metodit](https://ohjelmointi-19.mooc.fi/osa-2/3-metodit). [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.fi)

Seuraava metodi palauttaa aina saman merkkijonon, joka sisältää aakkosten kirjaimet yhtenä merkkijonona:

```java
public static String annaPienetKirjaimet() {
    return "abcdefghijklmnopqrstuvwxyzåäö";
}
```

Pienet kirjaimet saadaan nyt pyydettyä tältä metodilta metodikutsun avulla. Metodin palauttama merkkijono voidaan ottaa talteen esimerkiksi uuteen muuttujaan:

```java
String pienet = annaPienetKirjaimet();
```

Metodit kutsuvat hyvin usein toisiaan. Jos haluaisimme toteuttaa lisäksi `annaIsotKirjaimet`-metodin, meidän kannattaisi hyvin todennäköisesti hyödyntää yllä esiteltyä metodia tämän uuden metodin sisällä:

```java
public static String annaIsotKirjaimet() {
    String pienet = annaPienetKirjaimet();
    return pienet.toUpperCase();
}
```

Muutaman merkkijonoja palauttavan apumetodin sekä niitä kutsuvan `annaSatunnainenMerkki`-metodin avulla voisimme toteuttaa esimerkiksi satunnaisen salasanan generoivan ohjelmaluokan:

```java
import java.util.Random;

// Huom! Tämä esimerkki on suorituskykynsä puolesta heikko
public class Salasanat {

    public static void main(String[] args) {
        String salasana = generoiSalasana();
        System.out.println("Satunnainen salasanasi on " + salasana);
    }

    public static String generoiSalasana() {
        String salasana = "";
        while (salasana.length() < 60) {
            salasana += annaSatunnainenMerkki();
        }
        return salasana;
    }

    public static String annaSatunnainenMerkki() {
        Random random = new Random();
        String merkit = annaPienetKirjaimet() + annaIsotKirjaimet() + annaNumerot() + annaErikoismerkit();

        int indeksi = random.nextInt(merkit.length());
        return merkit.substring(indeksi, indeksi + 1);
    }

    public static String annaErikoismerkit() {
        return "<>,;.:-!\"#¤$%&/\\()[]";
    }

    private static String annaNumerot() {
        return "0123456789";
    }

    public static String annaIsotKirjaimet() {
        String pienet = annaPienetKirjaimet();
        return pienet.toUpperCase();
    }

    public static String annaPienetKirjaimet() {
        return "abcdefghijklmnopqrstuvwxyzåäö";
    }
}
```

Yllä olevassa esimerkissä kaikki omat metodit palauttavat merkkijonoja, mutta millään niistä ei ole parametriarvoja. Metodit on toteutettu hyvin yksinkertaisiksi, mutta suorituskykynäkökulmasta tässä ratkaisussa olisi vielä kehitettävää.

Jos metodin paluuarvoksi on määritetty jotain muuta kuin `void`, sen on **aina pakko palauttaa arvo**.


## Parametrimuuttujat ja paikalliset muuttujat

> *"Metodille voidaan määritellä useita parametreja. Tällöin metodin kutsussa parametrit annetaan samassa järjestyksessä."*
>
> [Agile Education Research, 2019](https://www.helsinki.fi/en/researchgroups/data-driven-education). [Ohjelman pilkkominen osiin: metodit](https://ohjelmointi-19.mooc.fi/osa-2/3-metodit). [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.fi)

Alla olevassa esimerkkimetodissa on kaksi `double`-tyyppistä parametrimuuttujaa:

```java
/** Laskee alennuksen, kun halvempi tuote myydään puoleen hintaan. */
public static double laskeAlennus(double hinta1, double hinta2) {
    double halvempi = Math.min(hinta1, hinta2);

    return halvempi * 0.5;
}
```

Tämän metodin kutsussa tulee antaa metodin parametrimuuttujien mukaisesti aina kaksi liukulukua, esim. `laskeAlennus(a, b)`:

```java
public static void main(String[] args) {
    double a = 123.4;
    double b = 234.5;

    double alennus = laskeAlennus(a, b);

    double loppusumma = a + b - alennus;

    System.out.println("Hinta on yhteensä " + loppusumma);
}
```

Huomaa, että samoja liukulukuja käsitellään sekä `main`-metodissa että `laskeAlennus`-metodissa. Niillä kuitenkin eri metodeissa eri muuttujanimet (`a`, `b`, `hinta1` ja `hinta2`). Paikallisilla muuttujien nimillä ei ole mitään merkitystä metodin ulkopuolella.

# Metodien näkyvyys, eli mistä metodia voidaan kutsua

Tämän materiaalin esimerkeissä kaikki metodit on määritelty **julkisiksi**, eli näkyvyydellä `public`. Näkyvyys on tapana määritellä aina mahdollisimman yksityiseksi, eli oikeassa ohjelmassa olisimme määritelleet suurimman osan metodeista **yksityiseksi**(`private`). Julkisia metodeita voidaan kutsua mistä vain muista luokista, kun taas muiden näkyvyyksien kohdalla kutsuminen onnistuu vain rajoitetuista luokista:

Näkyvyys        | Selitys
----------------|-------------
`public`        | Metodi on käytettävissä kaikkialta
`private`       | Metodi on käytettävissä ainoastaan saman luokan sisältä
`protected`     | Metodi on käytettävissä saman luokan ja paketin sisältä, sekä aliluokista
*(tyhjä)*       | Käytettävissä saman luokan ja paketin sisältä. **Melko harvoin käytetty.**

Seuraavat neljä metodia on määritelty kukin eri näkyvyydellä:

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

# Toisessa luokassa määriteltyjen metodien kutsuminen

Samassa luokassa määritellyn metodin kutsuminen oli yllä helppoa: kirjoitetaan vain metodin nimi, sulut ja tarvittaessa parametriarvot. Toisessa luokassa olevaa staattista metodia kutsutaan **luokan nimen avulla**:

```java
Metodit.tulostaPaivamaara();
Metodit.tulostaKellonaika();
```

Sama paluuarvon kanssa:

```java
String satunnainenSalasana = Salasanat.generoiSalasana();
```

Omia metodejasi kutsutaan siis aivan samalla tavalla kuin Javan valmiita metodeja:

```java
int pienin = Math.min(12, 15);
```

**Huom!** Mikäli kutsuttavan metodin luokka sijaitsee eri **paketissa** kuin kutsuva luokka, joudut lisäämään tiedoston alkuun myös `import`-komennon. Ylempänä oppimateriaalissa käsitelty metodin näkyvyys vaikuttaa siihen, mistä muista luokista kyseistä metodia voidaan kutsua.

<!--
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
-->

---

Tämä oppimateriaali pohjautuu Helsingin yliopiston [Agile Education Research](https://www.helsinki.fi/en/researchgroups/data-driven-education) -tutkimusryhmän [MOOC-ohjelmointikurssin materiaaliin](https://materiaalit.github.io/ohjelmointi-18/part2/).

Materiaalin on muokannut Haaga-Helian ohjelmointikurssin mukaiseksi Teemu Havulinna.

Lisenssi: [Creative Commons BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.fi).

<script src="/tocbot/tocbot.min.js"></script>
<script src="/scripts.js"></script>
<link rel="stylesheet" href="/tocbot/tocbot.css">