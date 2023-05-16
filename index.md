---
title: Tervetuloa koodaamaan!
layout: default
nav_order: 0
---

# Tervetuloa koodaamaan!

Tervetuloa ohjelmointi 1 -opintojaksolle! Tältä sivustolta löydät kurssin oppituntien muistiinpanot, videotallenteet ja koodiesimerkit.
{: .fs-6 }


## Kurssin sisältö

Tunneilla opetellaan ohjelmoinnin perusteita sekä hyviä ohjelmointikäytäntöjä ja käydään läpi esimerkkejä. Lisäksi opiskelijat ohjelmoivat tuntitehtäviä ja saavat niihin ohjausta. Kurssin suorittamiseksi sinun tulee palauttaa hyväksytysti automaattisesti arvioitavia harjoitustehtäviä Viope-järjestelmään sekä suorittaa kurssin lopuksi järjestettävä koe. Koe sisältää harjoitustehtävien kaltaisia ohjelmointitehtäviä ja se tehdään tietokoneella.

[Opintojaksokuvaus](https://opinto-opas.haaga-helia.fi/course_unit/SOF005AS2A)


## Kehitys ohjelmistokehittäjänä

> "The biggest mistake I see new programmers make is focusing on learning syntax instead of learning how to solve problems."
>
> [V. Anton Spraul](https://medium.freecodecamp.org/how-to-think-like-a-programmer-lessons-in-problem-solving-d1d8bf1de7d2)

Tällä  kurssilla opetellaan Java-kielen syntaksia, mutta erityisesti pyrimme opettelemaan ohjelmistokehityksen kannalta hyödyllisiä ajatusmalleja ja ongelmanratkaisutapoja. Ajatusmallit ja ongelmanratkaisukyky ovat myöhemmin sovellettavissa eri ohjelmointikielillä ja eri tyyppisissä sovelluksissa.

**1. Think like a computer**
  * Opimme ymmärtämään "miten tietokone" toimii ja mitkä ovat Javan peruspilarit
  * Osaamme tuottaa tietokoneen näkökulmasta järkeviä ratkaisuja

**2. Think like a programmer**
  * Opimme soveltamaan oppimaamme ja tuottamaan myös ihmisen näkökulmasta järkeviä ratkaisuja
  * Ymmärrettävyys, jatkokehitettävyys, ylläpidettävyys, testattavuus

**3. Work like a programmer**
  * Opimme hyödyntämään ammattimaisen ohjelmistokehittäjien työkaluja kuten kehitysympäristöä, versionhallintaa ja yksikkötestausta (opettelu jatkuu Ohjelmointi 2:lla)


## Kurssin työmäärä

Opintojakso kestää 8 viikkoa ja on laajuudeltaan 5 opintopistettä, joten sen [laskennallinen työmäärä on noin 135 tuntia](https://www.haaga-helia.fi/fi/ects-jarjestelma-ja-tutkintotodistuksen-liite-eli-diploma-supplement). Viikkoa kohden työmäärä vastaa laskennallisesti jopa 17 tuntia, joten varaa kurssin suorittamiseen runsaasti aikaa joka viikko.

```java
public class KurssinTyomaara {

    public static void main(String[] args) {
        int kestoViikkoina = 8;
        int opintopisteita = 5;
        int tyomaaraPerPiste = 27;

        int kokonaistyomaara = opintopisteita * tyomaaraPerPiste;
        System.out.println(kokonaistyomaara); // 135 tuntia

        double tyomaaraPerViikko = 1.0 * kokonaistyomaara / kestoViikkoina;
        System.out.println(tyomaaraPerViikko); // 16.875 tuntia per viikko
    }
}
```

## Kurssin työkalut

### Java ja Eclipse IDE

Tarvitset Java-ohjelmien kehittämiseksi ja suorittamiseksi [Java JDK](https://www.oracle.com/java/technologies/downloads/):n.

Lähdekooditiedostojen editointiin ja ohjelmien suorittamiseen käytämme tällä kurssilla Eclipse-kehitysympäristöä, jonka voit ladata itsellesi [eclipse.org-sivustolta](https://www.eclipse.org/downloads/packages/). Valitse versio **Eclipse IDE for Enterprise Java and Web Developers**, jotta sama Eclipse toimii myös jatkokursseilla.

Saat käyttää myös muita työkaluja, mutta niihin ei voida tarjota käyttötukea.


### Viope

Kurssin harjoitustehtävien tehtävänannot löytyvät Viope-järjestelmästä, jonne tehtävät myös palautetaan. Viope tarkistaa tehtävät automaattisesti ja pitää kirjaa tehtäväpisteistä.

Rekisteröidy Viopeen osoitteessa [https://hh.viope.com/](https://hh.viope.com/). Rekisteröityessäsi valitse toteutus oman toteutuskoodisi perusteella. Mikäli sinulla on jo Viope-tunnukset, kirjaudu sisään olemassa olevilla tunnuksillasi.

**Teknisistä syistä johtuen Viopeen palautettavista lähdekoodeista täytyy aina poistaa mahdolliset package -lauseet luokan yläpuolelta.** Viope on myös muilla tavoin erittäin tarkka ohjelmien oikeellisuudesta, mikä saattaa aiheuttaa ensimmäisillä viikoilla hämmennystä. Tyypillisiä Viope-virhetilanteita ja niiden ratkaisuja on dokumentoitu [erilliselle sivulle](wiki/Viope), jota päivitetään kurssin edetessä.


### GitHub

Kurssin tehtäväpohjien ja malliratkaisujen jakelussa hyödynnetään ohjelmistokehityksen alalla erittäin vakiintunutta Git-versionhallintaa ja GitHub-palvelua. Voit tutustua kurssin esimerkkikoodeihin osoitteessa [https://github.com/ohjelmointi1/ohjelmointi1-3018](https://github.com/ohjelmointi1/ohjelmointi1-3018). Halutessasi voit myös "kloonata" esimerkit omaan Eclipseesi seuraavalla osoitteella (file &rarr; import &rarr; projects from Git):

    https://github.com/ohjelmointi1/ohjelmointi1-3018.git

Gitin käytön opetteluun voit käyttää esimerkiksi Helsingin yliopiston erinomaista "Tietokone Työvälineenä"-kurssin Git-materiaalia: [https://tkt-lapio.github.io/git/](https://tkt-lapio.github.io/git/). Vaikka Git tuntuisi aluksi vaikealta tai ahdistavalta, sinun ei tarvitse opetella kaikkea kerralla, vaan tee vain sen verran mistä on sinulle välitöntä hyötyä. Voit hyvin suorittaa tämän kurssin myös perehtymättä erikseen Gittiin.


## Tämän oppimateriaalin lisenssi

Tämän oppimateriaalin on kehittänyt Teemu Havulinna ja se on lisensoitu [Creative Commons BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/) -lisenssillä. Oppimateriaalissa on hyödynnetty myös lukuisia muita lähteitä, jotka on mainittu eri aiheiden yhteydessä.

Sivuston lähdekoodit löydät osoitteesta [https://github.com/ohjelmointi1/ohjelmointi1.github.io](https://github.com/ohjelmointi1/ohjelmointi1.github.io).

Sivuston sivupohjana käytetään [Just the Docs](https://github.com/just-the-docs/just-the-docs) -nimistä teemaa, joka on lisensoitu [MIT-lisenssillä](https://github.com/just-the-docs/just-the-docs/blob/main/LICENSE.txt).