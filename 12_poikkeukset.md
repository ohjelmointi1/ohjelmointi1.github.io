---
title: Poikkeukset
layout: default
nav_order: 12
---

# Poikkeukset (exceptions)

Poikkeukset ovat ohjelman suorituksen aikana tapahtuvia tapahtumia, jotka aiheuttavat poikkeamia ohjelman normaaliin suoritusjärjestykseen. Vaikka ensikokemukset poikkeuksista ovat usein kielteisiä, ne ovat erittäin hyödyllinen työkalu erilaisten vikatilanteiden käsittelemiseksi ohjelmissa.

Ilman poikkeustenkäsittelyä ohjelma tyypillisesti "kaatuu", kun ohjelmassa tapahtuu jotain normaalista suorituksesta poikkeavaa, kuten yritetään käyttää listan olematonta indeksiä. Poikkeuksiin voidaan varautua, jolloin niiden sattuessa voidaan esimerkiksi yrittää uudelleen tai tulostaa virheilmoitus kaatamatta koko ohjelmaa.

Tällä opetuskerralla tutustumme tarkemmin poikkeuksiin, niiden hyödyntämiseen sekä niihin varautumiseen.

Huomaa, että Java-kääntäjän antamat virheet sekä varoitukset eivät liity poikkeuksiin, vaan ovat kokonaan eri asia. Poikkeukset tapahtuvat ohjelman suorituksen aikana, kun taas kääntäjä tekee työnsä ennen kuin ohjelma käynnistetään.


* Sisällysluettelo
{:toc}

# Oppitunnin videot

Videoiden katsominen edellyttää kirjautumista MS Stream -palveluun Haaga-Helian käyttäjätunnuksellasi ja liittymistä kurssin Teams-ryhmään.

## [Poikkeukset ja niihin varautuminen](https://web.microsoftstream.com/video/63ec3ae4-3b02-43b5-9903-45bf34c52c92) *47:05*

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/63ec3ae4-3b02-43b5-9903-45bf34c52c92?autoplay=false&showinfo=true" allowfullscreen style="border:none;"></iframe>

[Videolla esiintyvät lähdekoodit](https://github.com/ohjelmointi1/ohjelmointi1-3012/tree/main/src/viikko06/poikkeukset)


## [Virheiden paikantaminen, poikkeustyypit ja finally-lohko](https://web.microsoftstream.com/video/64f44c7d-b7ec-4d3c-9448-5aeb87cec819) *39:20*

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/64f44c7d-b7ec-4d3c-9448-5aeb87cec819?autoplay=false&showinfo=true" allowfullscreen style="border:none;"></iframe>

[Videolla esiintyvät lähdekoodit](https://github.com/ohjelmointi1/ohjelmointi1-3012/tree/main/src/viikko06/poikkeukset)


## [Poikkeusten heittäminen](https://web.microsoftstream.com/video/7ac99180-b044-4638-a360-12dded0e32d7) *25:20*

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/7ac99180-b044-4638-a360-12dded0e32d7?autoplay=false&showinfo=true" allowfullscreen style="border:none;"></iframe>

[Videolla esiintyvät lähdekoodit](https://github.com/ohjelmointi1/ohjelmointi1-3012/tree/main/src/viikko06/poikkeukset)


# Poikkeukset käytännössä

Poikkeukset ovat ohjelman suorituksen aikana tapahtuvia tapahtumia, jotka aiheuttavat poikkeamia ohjelman normaaliin suoritusjärjestykseen. *Java-kääntäjän havaitsemat virheet ja varoitukset ovat aivan toinen asia.*

Olette törmänneet tällä kurssilla poikkeuksiin mm. seuraavanlaisissa tilanteissa:

* käyttäjä syöttää väärin muotoillun luvun
* taulukosta, listasta tai merkkijonosta haetaan arvoa virheellisellä indeksillä
* metodia kutsutaan null-viittauksen kautta.

Muita tyypillisiä tilanteita poikkeuksille ovat mm:

* luettavaa tiedostoa ei löydy levyltä
* kirjoitettavaan tiedostoon ei ole kirjoitusoikeutta
* tietoliikenneyhteyden muodostaminen epäonnistuu.


Esimerkki poikkeuksen aiheuttamasta virheilmoituksesta:

```
Exception in thread "main" java.util.InputMismatchException
at java.util.Scanner.throwFor(Unknown Source)
at java.util.Scanner.next(Unknown Source)
at java.util.Scanner.nextInt(Unknown Source)
at java.util.Scanner.nextInt(Unknown Source)
at week1.ScannerExample.main(Example.java:11)
```

Voit tutustua poikkeuksiin tämän oppimateriaalin lisäksi esimerkiksi [Oraclen oppimateriaalin avulla](https://docs.oracle.com/javase/tutorial/essential/exceptions/index.html).


# Poikkeuksiin varautuminen

Poikkeuksiin voidaan varautua kirjoittamalla poikkeuksia aiheuttava koodi `try`-lohkon sisään. `try`-lohkon jälkeen kirjoitetaan `catch`-lohko, jonka sisällä oleva koodi suoritetaan, mikäli `try`-lohkon suorituksessa törmättiin `catch`-lohkoon märiteltyyn poikkeustyyppiin.

Try/catch-rakenteen perusmuoto on siis seuraava:

```java
try {
  // Koodi, jossa mahdollisesti tapahtuu virhe
} catch (Exception poikkeus) {
  // Koodi, joka suoritetaan, mikäli virhe tapahtui
}
```

Yllä esitetyssä esimerkissä on varauduttu `Exception`-tyyppiseen poikkeukseen. `Exception` on Javassa poikkeusten yhteinen yläluokka, joten käytännössä tämä koodi varautuu kaikkiin mahdollisiin poikkeuksiin. Samojen sulkujen sisällä esiintyy myös muuttujanimi `poikkeus`. Poikkeukset ovat sisimmältään olioita, ja `Exception poikkeus` on muuttujan määrittely. Palaamme tämän muuttujan hyödyntämiseen myöhemmin.

Mikäli haluamme koodissamme varautua nimenomaan tilanteeseen, jossa kokonaisluvun sijasta käyttäjä on syöttänyt muita merkkejä, voisimme varautua `try/catch`-rakenteella erityisesti `NumberFormatException`-poikkeukseen:

```java
try {
  int number = Integer.parseInt(syote);
  // ...
} catch (NumberFormatException poikkeus) {
  System.out.println("Syöte ei ole kokonaisluku!");
}
```

`catch`-lohkoja voi olla myös useita, jolloin ne käsittelevät eri tyyppisiä poikkeuksia.

## Eri tyyppisiin poikkeuksiin varautuminen

Virheen sattuessa `try`-lohkon sisällä lohkon suoritus keskeytyy välittömästi. Suoritus siirtyy sen `catch`-lohkon alkuun, joka on määritetty käsittelemään tämä poikkeustyyppi. Jos `try`-lohkossa sattuu poikkeus, jota vastaavaa `catch`-lohkoa ei ole, poikkeusta ei käsitellä lainkaan, joten ohjelma saattaa kaatua.

**Kysymys:** Millä syötteillä päädyt viereisessä esimerkkikoodissa oleviin catch-lohkoihin?

```java
String[] paivat = "ma ti ke to pe la su".split(" ");
Scanner lukija = new Scanner(System.in);

try {
    System.out.println("Valitse taulukon indeksi:");
    int valinta = lukija.nextInt();
    System.out.println(paivat[valinta]);

} catch (InputMismatchException e) {
    System.err.println("Epäkelpo kokonaisluku :(");

} catch (ArrayIndexOutOfBoundsException e) {
    System.err.println("Taulukossa ei ole vastaavaa arvoa :(");
}

lukija.close();
```

**Vastaukset:**

`InputMismatchException` syntyy silloin, kun `nextInt` lukee tietovirrasta jonkin muun arvon kuin kokonaisluvun.

`ArrayIndexOutOfBoundsException` syntyy silloin, kun annettu kokonaisluku on taulukon indeksien ulkopuolella.


# Try, throw ja catch

```java
try {
    numero = Integer.parseInt(text);
    // ...

} catch (NumberFormatException e) { // Nappaa vain NumberFormatException -poikkeukset!
    System.err.println("Epäkelpo kokonaisluku"); // Tulostaa tekstin virhe-streamiin: System.err

}
```

`Integer.parseInt` heittää `NumberFormatException`-poikkeuksen, mikäli se ei pysty lukemaan annetusta merkkijonosta numeroa. Kukin `catch`-lohko suoritetaan vain, jos `try`-lohkossa sattunut poikkeus on yhteensopiva kyseisessä `catch`-lohkossa olevan poikkeuksen kanssa.


## System.err

`System.err`:iä voidaan käyttää tulostamiseen kuten `System.out`:ia, mutta sitä käytetään ainoastaan virheiden tulostamiseen. Eclipsessä `System.err`-tietovirran tulosteet näytetään punaisella.

```java
// System.err
System.err.println("System.err tulostetaan punaisella");

// System.out
System.out.println("System.out tulostetaan mustalla");
```

Edistyneemmissä ohjelmissa eri tietovirrat voidaan myös ohjata eri sijainteihin, esimerkiksi `System.err` voidaan kirjoittaa tiedostoon myöhempää tutkimista varten ja `System.out` tulostaa ruudulle.


# Poikkeusolion käyttäminen

Poikkeukset ovat olioita, joilla on oliometodeja. Poikkeuksiin liittyy aina tiedot mm. siitä, minkälainen virhe on sattunut ja missä. Tapahtunut poikkeus on aina saatavilla `catch`-lohkon sisällä paikallisena muuttujana:

```java
try {
    int number = Integer.parseInt(syote);
    // ...

} catch (NumberFormatException poikkeus) { // Catch-lohkon 'poikkeus' on muuttuja!

    // poikkeus.getMessage() palauttaa selkokielisen virheilmoituksen.
    String virheviesti = poikkeus.getMessage();

    System.err.println(virheviesti);
}
```

Tässä esimerkissä muuttujan nimeksi on annettu `poikkeus`, mutta usein muuttujan nimenä nähdään esimerkiksi `e` (exception), `npe` (NullPointerException) tai vastaavia lyhenteitä.

# Finally-lohko

Try-catch –rakenteen lopuksi on mahdollista lisätä myös `finally`-lohko. `finally`-lohko suoritetaan aina lopuksi riippumatta siitä, tapahtuiko poikkeus vai ei. Koska `finally` lohko suoritetaan aina, se on hyvä paikka sijoittaa esimerkiksi resurssien sulkemisesta huolehtivat koodirivit:

```java
Scanner input = new Scanner(System.in);

try {
    System.out.println("Syötä kokonaisluku:");
    Integer.parseInt(input.nextLine());
    System.out.println("Kiitos");

} catch (NumberFormatException e) {
    System.err.println("Virheellinen luku");

} finally {
    // Tämä koodi suoritetaan aina, riippumatta siitä, tapahtuiko virheitä
    input.close();
}
```

# Koodaustehtävä

Kirjoita luokka `KysyUudestaan` ja lisää siihen main-metodi. Main-metodissa sinun tulee kysyä käyttäjältä kokonaislukutyyppistä syötettä. Jos käyttäjä antaa syötteen, joka ei ole kelvollinen kokonaisluku, ohjelmasi tulee kysyä syötettä uudelleen esimerkkisuorituksen mukaisesti. Kun käyttäjä syöttää kelvollisen kokonaisluvun, ohjelmasi tulee tulostaa annettu luku esimerkkisuorituksen mukaisesti.

```
Syötä kokonaisluku: sata
Virheellinen luku!

Syötä kokonaisluku: 100
Syötit luvun 100.
```

# Virheiden paikantaminen

Poikkeusoliot sisältävät paljon hyödyllistä tietoa siitä, minkälainen virhe tapahtui ja mitkä olivat virhettä edeltäneet vaiheet. Virheilmoituksen lukeminen onkin tärkeä taito ongelmien ratkaisemiseksi. Omissa ohjelmissamme virheet ovat vielä ohjelmien pienen koon vuoksi helposti löydettävissä, mutta isojen ohjelmistojen kohdalla virheiden paikantaminen voi olla hyvin vaikeaa. Virheiden paikantamista käsitellään tarkemmin esimerkiksi teknologiayritys Twilion blogikirjoituksessa [How to read and understand a Java Stacktrace](https://www.twilio.com/blog/how-to-read-and-understand-a-java-stacktrace).


## Suorituspino (stack)

Tietokoneen muistissa olevia aktiivisia metodikutsuja pidetään ns. pinossa. Ohjelmointiterminologiassa pino tarkoittaa tietorakennetta, johon uusin alkio lisätään aina ylimmäksi ja josta voidaan poistaa vain ylin alkio.

Kun metodista kutsutaan toista metodia, lisätään pinoon "kehys" kutsutun metodin suoritusta varten ja ohjelman suoritus siirtyy ylempään kehykseen. Kukin kehys pitää sisällään sitä vastaavan metodin paikalliset muuttujat ja tiedon siitä, millä rivillä kyseisen metodin suoritus on.

Kun metodi on suoritettu, poistetaan sitä varten luotu kehys ja suoritus palaa taas pinossa alaspäin siihen metodiin, josta suoritettua metodia kutsuttiin. Alempana pinossa olevat keskeneräiset metodien suoritukset odottavat, kunnes ylemmät pinokehykset on suoritettu.

## Pinon lukeminen (stack trace, pinovedos)

```
Exception in thread "main" java.util.InputMismatchException
at java.util.Scanner.throwFor(Unknown Source)
at java.util.Scanner.next(Unknown Source)
at java.util.Scanner.nextInt(Unknown Source)
at java.util.Scanner.nextInt(Unknown Source)
at week1.ScannerExample.main(Example.java:11)
```

Pinovedosta luetaan aina alhaalta ylöspäin. Yllä olevasta pinovedoksesta näet, että metodikutsut lähtivät liikkeelle alimmasta kehyksestä eli Example.java-tiedoston riviltä 11. Sieltä edettiin Javan Scanner-luokkaan, joka kutsui itse muutamaa omaa metodiaan. Lopulta aiheutui virhe `InputMismatchException`, joka näkyy pinovedoksessa ylimpänä.


## Pinon tulostaminen

Jos poikkeus päätyy pois omasta ohjelmastasi niin, ettei sitä napata missään ja ohjelma "kaatuu", tulostaa Java automaattisesti virheilmoituksen ja pinovedoksen (stack trace). Jos haluat oman ohjelmasi sisällä käsitellessäsi poikkeusta tulostaa suorituspinon, voit tehdä sen kutsumalla itse poikkeuksen `printStackTrace​()`-metodia:

```java
} catch (Exception poikkeus) {
    poikkeus.printStackTrace();
}
```

# Poikkeustyypit

Javassa on useita eri tyyppisiä poikkeuksia. Virheiden tyyppejä käsitellään tarkemmin artikkelissa [Types of Exceptions in Java
](https://stackify.com/types-of-exceptions-java/) (Sagar Arora, 2018. stackify.com). Tärkeimmät tyypit ovat seuraavaksi käsiteltävät virheet, ajonaikaiset poikkeukset sekä tarkastetut poikkeukset.


## Virheet / Errors

Ohjelman suoritusta estävät ulkoiset virhetilanteet, esim. muistin loppuminen. Error-tyyppiset virheet ovat varsin harvinaisia ja niihin varautuminen ajonaikaisesti on haastavaa.


## Ajonaikaiset poikkeukset / Runtime exceptions

Ajonaikaiset virheet ovat tyypillisesti ohjelmointivirheistä aiheutuvia virhetilanteita, jotka usein voitaisiin välttää ilman varsinaista poikkeustenhallintaa. Erilaisia ajonaikaisia poikkeustyyppejä on valtavasti, mutta yleisiä ovat esimerkiksi `NullPointerException`, `ArrayIndexOutOfBoundsException` ja `IllegalArgumentException` ([oracle.com](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/RuntimeException.html)).

Monet ajonaikaiset poikkeukset ovat vältettävissä tekemällä tarkastuksia ennen metodikutsuja. Virhe voidaan siis välttää tarkastamalla ensin, onko arvo `null` tai onko taulukon pituus riittävä.


## Tarkastetut poikkeukset / checked exceptions

Tarkastetut poikkeukset ovat poikkeuksia, joihin ohjelmassa on pakko varautua ja joista tulee selvitä. Java-kääntäjä varmistaa, että kaikkiin tarkistettuihin poikkeuksiin on varauduttu. Tarkastettuja poikkeuksia käytetään esimerkiksi tiedostojen käsittelyssä, jossa virheet ovat erittäin tyypillisiä. Toisin kuin ajonaikaisia poikkeuksia, tarkastettuja poikkeuksia ei usein voida välttää tarkistamalla esiehtoja.

Tyypillisiä tarkastettua poikkeuksia ovat mm. `IOException` ja `SQLException` ([oracle.com](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Exception.html)).

Jos metodi heittää tarkastetun poikkeuksen, täytyy sen otsikkoon lisätä `throws`-määre, esim:

```java
// https://docs.oracle.com/javase/10/docs/api/java/nio/file/Files.html
public static List<String> readAllLines​(Path path) throws IOException {
  // ...
}
```

Tällaista metodia kutsuvaan metodiin on aina pakko kirjoittaa joko try/catch –lohko tai kutsuvan metodin otsikkoon on myös lisättävä tieto samasta poikkeuksesta. Jos metodi ei käsittele poikkeusta, vaan päästää sen kutsuketjussa ylöspäin, kutsutaan sitä "kuplimiseksi". Poikkeus siis "kuplii" metodista toiseen.

Perehdymme tarkastettujen poikkeusten käsittelyyn tarkemmin seuraavalla oppitunnilla, jolla luemme ja kirjoitamme tiedostoja.


# Poikkeusten dokumentoiminen

Jos metodi heittää ajonaikaisen poikkeuksen, `throws`-määre voidaan lisätä, mutta se ei ole pakollinen. Vaikka `throws` ei ole pakollinen, se toimii hyvänä dokumentaationa metodin toiminnasta, esim. `Integer`-luokassa:

```java
public static int parseInt​(String s) throws NumberFormatException {
    // ...
}
```

`NumberFormatException` ei ole tarkastettu poikkeus, joten sitä varten ei ole pakko lisätä poikkeuksenkäsittelyä, vaikka poikkeus onkin määritetty metodin otsikkoon.


# Poikkeusten "heittäminen"

Poikkeukset ovat olioita, joten poikkeus voidaan luoda `new`-avainsanalla kuten muutkin oliot. Tässä esimerkissä valmistelemme poikkeuksen, joka kertoo että metodille annettu merkkijono ei saa olla tyhjä:

```java
IllegalArgumentException poikkeus = new IllegalArgumentException("Nimi ei saa olla tyhjä");
```

Poikkeuksia voidaan heittää `throw`-käskyllä. Throw-käskyn jälkeen kirjoitetaan heitettävä poikkeus:

```java
public void setNimi(String nimi) {

    // onko annettu nimi kelvollinen?
    if (nimi == null || nimi.isEmpty()) {
        // luodaan IllegalArgumentException-olio. Parametrina annetaan selkokielinen virheilmoitus:
        throw new IllegalArgumentException("Nimi ei saa olla tyhjä");
    }

    this.nimi = nimi; // tämä rivi suoritetaan vain, jos poikkeusta ei heitetty
}
```

Kun poikkeus heitetään, siirtyy ohjelman suoritus välittömästi joko saman rakenteen `catch`-lohkoon tai suorituspinossa edelliseen metodiin. Yllä olevassa koodissa esiintyvä sijoitusoperaatio `this.nimi = nimi` olisi voitu kirjoittaa `else`-lohkoon, mutta se olisi ollut turhaa, koska kyseiselle riville ei koskaan päädytä, mikäli nimi on tyhjä.


## Koodaustehtävä

Kirjoita ohjelma `ArvonTarkastus`, joka kysyy käyttäjältä yhden luvun. Ohjelmasi tulee luvun kysymisen jälkeen tarkastaa, että luku on vähintään 0 ja korkeintaan 23. Mikäli annettu luku X on sallittu, tulee ohjelmasi tulostaa teksti "Luku X on sallittu." ja ohjelman suorituksen pitää päättyä.

Mikäli luku ei ole sallittu, tulee ohjelmasi heittää Javan valmis `IllegalArgumentException`-poikkeus, minkä jälkeen ohjelmasi "kaatuu". Voit antaa poikkeukselle konstruktoriparametrina minkä tahansa virheilmoituksen tai jättää merkkijonon antamatta.

Huom: koska `IllegalArgumentException` sijaitsee `java.lang`-paketissa, sitä ei tarvitse erikseen ottaa käyttöön import-käskyllä.

```
Syötä luku väliltä 0-23: -1
Exception in thread "main" java.lang.IllegalArgumentException
```

# Omat poikkeusluokat (edistynyttä sisältöä)

Voit luoda omia poikkeusluokkia aivan kuten muitakin luokkia. Jotta luokkasi toimii poikkeusluokkana, sen täytyy "periä" jokin Javan poikkeusluokka:

* `java.lang.Exception` tarkastettu poikkeus
* `java.lang.RuntimeException` ajonaikainen poikkeus

```java
public class VirheellinenEmailPoikkeus extends RuntimeException {

    // Oman poikkeusluokan konstruktori:
    public VirheellinenEmailPoikkeus(String email) {

        // Kutsutaan perityn luokan konstruktoria:
        super(email + " is not a valid email address!");
    }
}
```

## Edistynyttä sisältöä: Oman poikkeuksen heittäminen

`VirheellinenEmailPoikkeus` heitetään, jos yhteystietoon ollaan asettamassa sähköpostiosoitteeksi tyhjää arvoa. Oikeassa sovelluksessa sähköpostiosoitteen muoto tarkastettaisiin esim. säännöllisellä lausekkeella.

```java
public class Yhteystieto {

    private String nimi;
    private String email;

    public void setEmail(String email) {
        if (email == null || "".equals(email)) {
            throw new VirheellinenEmailPoikkeus(email);
        }
        this.email = email;
    }
}
```




