# Oliot listoilla ja listoja olioissa

Aiheen toisella oppitunnilla käsittelemme omien luokkiemme käyttämistä listoilla, sekä listojen määrittelemistä olioiden oliomuuttujiksi.

```java
List<Kaupunki> uusimaa = new ArrayList<Kaupunki>();
List<Yhteystieto> kontaktit = new ArrayList<Yhteystieto>();
```


# Datan kapselointi (encapsulation)

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


# Viittauksen kopioiminen != olion kopioiminen

Olioita ei voi kopioida sijoittamalla niitä uusiin muuttujiin. Tällöin viitataan vain samaan olioon usealla eri muuttujalla:

```java
Yhteystieto y1 = new Yhteystieto("Adam", "050123", "adam@example.com");

// ei kopioi, vaan viittaa samaan olioon:
Yhteystieto y2 = y1;
```

Jos yllä olevassa esimerkissä kutsutaan `asetaEmail`-metodia muuttujan `y1` kautta, muuttuu sähköpostiosoite myös `y2`:ssa. Tämä johtuu siitä, että **olemme luoneet vain yhden olion, johon viitataan kahdella muuttujalla**.

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



# AddressBook ja Contact -esimerkkiohjelma

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


---


Tämän oppimateriaalin on kehittänyt Teemu Havulinna ja se on lisensoitu [Creative Commons BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/) -lisenssillä.

<script src="/tocbot/tocbot.min.js"></script>
<script src="/scripts.js"></script>
<link rel="stylesheet" href="/tocbot/tocbot.css">