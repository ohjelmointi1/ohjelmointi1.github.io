[&larr; Takaisin etusivulle](/)

<h1 class="js-toc-ignore">Olio-ohjelmointi: luokkien väliset yhteyssuhteet</h1>

Aiheen toisella oppitunnilla jatkamme olio-ohjelmoinnin käsittelyä ja toteutamme luokkia, jotka hyödyntävät muita toteuttamiamme luokkia. Käsittelemme lisäksi omien luokkiemme käyttämistä listoilla, sekä listojen määrittelemistä olioiden oliomuuttujiksi.


**Sisällysluettelo**

<div class="js-toc"></div>

# Oppiptuntitallenne: Luokan määrittely ja olioiden käsittely listoilla

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/d8040740-8c23-4948-a840-b40b6a32f8dc?autoplay=false&amp;showinfo=true" allowfullscreen style="border:none;"></iframe>

[MS Stream: Luokan määrittely ja olioiden käsittely listoilla](https://web.microsoftstream.com/video/d8040740-8c23-4948-a840-b40b6a32f8dc)


# Yhteystieto-esimerkki

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
JSON esimerkki: [https://mockaroo.com/](https://mockaroo.com/)

Data koostuu selvästi keskenään rakenteellisesti samanlaisista tietoalkioista, joilla on yksilölliset arvot, kuten nimi ja email. Huomaa, että henkilölle "Moses" ei ole asetettu sähköpostiosoitetta, mutta sillä on silti olemassa "muuttuja" sähköpostin tallentamiseksi. **Puuttuvaa arvoa ei voida jättää tyhjäksi, vaan siihen on asetettu null-viittaus.**

Tietojen tallentaminen erillisissä muuttujissa olisi hankalaa ja virhealtista. Sen sijaan määritellään luokka `Yhteystieto` ja jokaista henkilöä varten luodaan olio eli ilmentymä tästä luokasta:

```java
Yhteystieto lindsey = new Yhteystieto("Lindsey", "ldrillingcourt0@so-net.ne.jp", "132-414-7730");
Yhteystieto zilvia = new Yhteystieto("Zilvia", "zzamboniari1@dell.com", "445-276-2785");

List<Yhteystieto> yhteystiedot = new ArrayList<>();
yhteystiedot.add(lindsey);
yhteystiedot.add(zilvia);
```

## Yhteystieto-luokan toteutus

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
Yhteystieto lindsey = new Yhteystieto("Lindsey", "ldrillingcourt0@so-net.ne.jp", "132-414-7730");
Yhteystieto zilvia = new Yhteystieto("Zilvia", "zzamboniari1@dell.com", "445-276-2785");
```

## Oliomuuttujien käyttäminen

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

## Oliometodin kutsuminen

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

## toString()-metodi ja sen ohittaminen: @Override

Katso kuvaus `toString`-metodin toteuttamisesta ylempää tästä dokumentista. Yhteystieto-luokan merkkijonoesityksessä voisimme käyttää esimerkiksi nimeä ja sähköpostiosoitetta seuraavasti:

```java
class Yhteystieto {

    // ...muuttujat, konstruktori ja muut metodit...

    @Override
    public String toString() {
        return this.nimi + " (" + this.email + ")";
    }
}
```

Nyt oliota tulostettaessa saamme hieman loogisemman merkkijonoesityksen:

```java
Yhteystieto lindsey = new Yhteystieto("Lindsey", "ldrillingcourt0@so-net.ne.jp", "132-414-7730");

System.out.println(lindsey); // "Lindsey (ldrillingcourt0@so-net.ne.jp)"
```

# Datan kapselointi (encapsulation)

Olioiden attribuuttien muuttamista halutaan hyvin usein rajoittaa:

* `Yhteystieto`-luokan sähköpostiosoitteeksi ei haluta hyväksyä muita kuin valideja sähköpostiosoitteita
* `Tili`-luokan saldon muuttaminen luokan ulkopuolelta halutaan estää
* `Henkilotieto`-luokan syntymäpäiväksi halutaan sallia vain menneisyyteen sijoittuvia päivämääriä

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


# Luokkien väliset yhteyssuhteet

Olio-ohjelmointiparadigman mukaisissa ohjelmissa luokilla on erityyppisiä yhteyksiä toisiinsa. Sekä yhteyksien määrä, esimerkiksi yhdestä yhteen tai yhdestä moneen, että yhteyden luonne vaihtelevat tapauskohtaisesti.

> *"Association in Java is a connection or relation between two separate classes that are set up through their objects. Association relationship indicates how objects know each other and how they are using each other’s functionality. It can be one-to-one, one-to-many, many-to-one and many-to-many."*
>
> Choudary, A. 2019. What is Association in Java and why do you need it? [edureka.co](https://www.edureka.co/blog/association-in-java/)

Esimerkkejä erilaisista yhteyssuhteista on lukuisia, ja tutustut niihin tarkemmin mm. tietokantakurssilla. Tämän kurssin näkökulmasta voimme esimerkiksi ajatella yhteyssuhdetta `Henkilotieto`- ja `LocalDate`-luokkien välille siten, että `Henkilotieto` pitää sisällään tiedon yksittäisen henkilön syntymäajasta. `Henkilotieto`-oliot voivat käyttää tätä syntymäaikaa sisäisesti esimerkiksi henkilön iän laskemiseksi.

## Oppituntitallenne: Luokkien väliset yhteyssuhteet

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/b6aa4193-13dd-4261-bcb9-49c71aff5f52?autoplay=false&amp;showinfo=true" allowfullscreen style="border:none;"></iframe>

[MS Stream: Luokkien väliset yhteyssuhteet](https://web.microsoftstream.com/video/b6aa4193-13dd-4261-bcb9-49c71aff5f52)


Toteutimme tunnilla Henkilotieto-luokan siten, että tästä luokasta on yhteys `LocalDate`-luokkaan. Lisäksi toteutimme `laskeIka`-nimisen metodin, joka hyödyntää syntymäaikaa iän laskemiseksi. Lopulta toteutimme myös `onTaysiIkainen`-metodin, joka kutsuu saman olion `laskeIka`-metodia:

```java
import java.time.LocalDate;
import java.time.temporal.ChronoUnit;
import java.util.ArrayList;
import java.util.List;

public class Henkilotieto {

    private String nimi;
    private LocalDate syntymapaiva;

    public Henkilotieto(String nimi, int paiva, int kuukausi, int vuosi) {
        this.nimi = nimi;
        this.syntymapaiva = LocalDate.of(vuosi, kuukausi, paiva);
    }

    public String getNimi() {
        return this.nimi;
    }

    public boolean onTaysiIkainen() {
        int ika = this.laskeIka();
        return ika >= 18;
    }

    public int laskeIka() {
        return (int) ChronoUnit.YEARS.between(this.syntymapaiva, LocalDate.now());
    }

    @Override
    public String toString() {
        return this.nimi + ", " + this.laskeIka() + " v";
    }
}
```

# Oliot listoilla ja listoja olioissa

Omien luokkiemme käyttäminen listoilla ei eroa Javan valmiiden luokkien käyttämisestä, jota olemme jo harjoitelleetkin esimerkiksi String-luokan kanssa:

```java
List<String> nimet = new ArrayList<>();

List<Kaupunki> kaupungit = new ArrayList<>();
List<Yhteystieto> kontaktit = new ArrayList<>();
List<Henkilotieto> henkilotiedot = new ArrayList<>();
```

Listan tyyppi määritellään, kuten aiemmin, muuttujan tyypin yhteydessä (`List<Kaupunki>`). Listan luontikäskyssä kulmasulut voidaan jättää tyhjiksi, mikäli rivillä on selvää, minkä tyyppistä listaa ollaan luomassa:

```diff
+ List<Kaupunki> kaupungit = new ArrayList<>();
- List<Kaupunki> kaupungit = new ArrayList<Kaupunki>();
```

## Oppituntitallenne: olioita listoilla ja listoja olioissa

<iframe width="640" height="360" src="https://web.microsoftstream.com/embed/video/09b3a526-88f5-4b5a-a507-d8f53b452a5a?autoplay=false&amp;showinfo=true" allowfullscreen style="border:none;"></iframe>

[MS Stream: Oliot listoilla ja listat olioilla](https://web.microsoftstream.com/video/09b3a526-88f5-4b5a-a507-d8f53b452a5a)


Listat, kuten muutkin Javan kokoelmat, ovat itse asiassa olioita. Listamuuttujien määritteleminen oliomuuttujaksi ei käytännössä eroa mitenkään muiden tyyppisistä muuttujista:

```java
public class Henkilotieto {

    private List<Henkilotieto> lapset;

}
```

Vastaavasti kuin aikaisemmin määrittelimme `Henkilotieto`-luokalle yksittäisen päivämääräolion `LocalDate`-luokan avulla, voimme määritellä siihen useita `Henkilotieto`-olioita sisältävän listan kyseisen henkilön lapsista:

```java
import java.time.LocalDate;
import java.time.temporal.ChronoUnit;
import java.util.ArrayList;
import java.util.List;

public class Henkilotieto {

    private String nimi;
    private LocalDate syntymapaiva;
    private List<Henkilotieto> lapset = new ArrayList<>(); // voitaisiin kirjoittaa myös konstruktoriin

    public Henkilotieto(String nimi, int paiva, int kuukausi, int vuosi) {
        this.nimi = nimi;
        this.syntymapaiva = LocalDate.of(vuosi, kuukausi, paiva);
    }

    public String getNimi() {
        return this.nimi;
    }

    public void lisaaLapsi(Henkilotieto lapsi) {
        this.lapset.add(lapsi);
    }

    public int getSyntymaVuosi() {
        return syntymapaiva.getYear();
    }

    public void setSyntymaAika(int paiva, int kuukausi, int vuosi) {
        LocalDate syntyma = LocalDate.of(vuosi, kuukausi, paiva);
        if (!syntyma.isAfter(LocalDate.now())) {
            this.syntymapaiva = syntyma;
        } else {
            // TODO: Heitä poikkeus?
        }
    }

    public boolean onTaysiIkainen() {
        int ika = this.laskeIka();
        return ika >= 18;
    }

    public int laskeIka() {
        return (int) ChronoUnit.YEARS.between(this.syntymapaiva, LocalDate.now());
    }

    @Override
    public String toString() {
        String nimiJaIka = this.nimi + ", " + this.laskeIka() + " v";
        if (this.lapset.isEmpty()) {
            return nimiJaIka;
        } else {
            return nimiJaIka + ", " + this.lapset.size() + " lasta:\n" + this.muodostaLapsiLista();
        }
    }

    private String muodostaLapsiLista() {
        String lapsiLista = "";
        for (Henkilotieto lapsi : this.lapset) {
            String lapsenNimi = lapsi.getNimi();
            lapsiLista += "- " + lapsenNimi + "\n";
        }
        return lapsiLista;
    }
}
```

## Yksityiset apumetodit

Kuten tunnilla esitetyssä esimerkissä, luokkiin toteutetaan usein yksityisiä "apumetodeja", joiden avulla isommat kokonaisuudet saadaan pilkottua helpommin ymmärrettäviksi pienemmiksi kokonaisuuksiksi. Tästä on esimerkkinä yksityinen `muodostaLapsiLista`-metodi, joka on `toString`-metodin apumetodi.

Luokan kokeilemiseksi toteutimme oppitunnilla ohjelmaluokan:

```java
public class HenkilotietoOhjelma {

    public static void main(String[] args) {

        Henkilotieto aiti = new Henkilotieto("Cecilia Smith", 1, 6, 1975);

        Henkilotieto adam = new Henkilotieto("Adam Smith", 2, 3, 2000);
        Henkilotieto bob = new Henkilotieto("Bob Smith", 4, 5, 2003);

        aiti.lisaaLapsi(adam);
        aiti.lisaaLapsi(bob);

        System.out.println(aiti);

        System.out.println(adam);

        System.out.println(bob);
    }
}
```

Ohjelmaluokan tuloste:

```
Cecilia Smith, 45 v, 2 lasta:
- Adam Smith
- Bob Smith


Adam Smith, 20 v

Bob Smith, 17 v
```

# Viittauksen kopioiminen != olion kopioiminen

Kuten olemme kurssilla listojen yhteydessä huomanneet, olioita ei voi kopioida sijoittamalla niitä uusiin muuttujiin. Jos asetamme olion uuteen muuttujaan, kopioimme ainoastaan viittauksen. Tällöin samaan olioon viitataan vain usealla eri muuttujalla:

```java
Yhteystieto y1 = new Yhteystieto("Adam", "050123", "adam@example.com");
Yhteystieto y2 = y1; // ei kopioi, vaan viittaa samaan olioon

y1.asetaEmail("mr.adam@example.com");

System.out.println(y1);
System.out.println(y2); // email on muuttunut myös tässä!
```

Jos yllä olevassa esimerkissä kutsutaan `asetaEmail`-metodia muuttujan `y1` kautta, muuttuu sähköpostiosoite myös `y2`:ssa. Tämä johtuu siitä, että **olemme luoneet vain yhden olion, johon viitataan kahdella muuttujalla**. 

Olioiden kopioimiseksi ei ole yksittäistä yleistä tapaa, vaan mahdolliset kopiot täytyy luoda tilanteesta riippuen eri tavoilla. 

## Tuntiesimerkki: olion muuttaminen, kun olio on jo toisen olion listalla

Toteutetaan tunnilla pääohjelmaluokka, jossa luodaan hierarkia `Henkilotieto`-olioita. Tutkitaan mitä käy, kun muutamme eri olioiden sisältämiä tietoja.


<!--# Mahdollinen tuntiharjoitus: AddressBook ja Contact

## Contact

* name (`String`)
* email (`String`)
* phone (`String`)

## AddressBook

* search(String keyword)
* add(Contact newContact)
* remove(String keyword)
* list() // palauttaa merkkijonon koko sisällöstä
* (load)
* (save)

## Lisäominaisuudet

* Osoitekirjan muodostaminen *järkeväksi* merkkijonoksi
* Osoitekirjan tulostaminen nimien mukaisessa aakkosjärjestyksessä
* Yhteystietojen vertailu (`Contact.equals`)
* Osoitekirjaan lisääminen vain, jos sama yhteystieto ei ole vielä osoitekirjassa (`List.contains`)
-->

---


Tämän oppimateriaalin on kehittänyt Teemu Havulinna ja se on lisensoitu [Creative Commons BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/) -lisenssillä.

<script src="/tocbot/tocbot.min.js"></script>
<script src="/scripts.js"></script>
<link rel="stylesheet" href="/tocbot/tocbot.css">