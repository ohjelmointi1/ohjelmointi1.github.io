---
title: Muuttujien roolit
layout: default
parent: ''
---

# Muuttujien roolit

Ohjelmointi on usein ongelmanratkaisua, jossa tarvitsemme syntaksin osaamisen lisäksi taitoa nähdä ongelmia eri näkökulmista ja muotoilla ongelmia eri tavoilla.

Kun ymmärrämme miten muuttujat toimivat ja miten niitä käytetään, pystymme soveltamaan muuttujia erilaisissa käyttötarkoituksissa ratkaisemaan erilaisia ongelmia. [Jorma Sajaniemi](http://www.cs.joensuu.fi/~saja/var_roles/stud_vers/stud_Java_fin.html) on kehittänyt muuttujille oivallisen [luokittelun](http://www.cs.joensuu.fi/~saja/var_roles/stud_vers/stud_Java_fin.html), jonka avulla pystymme hahmottamaan erilaisia toistuvia rooleja, jotka muuttujilla on eri tyyppisten ongelmien ratkaisemisessa.

Tietokoneen näkökulmasta muuttuja on vain muuttuja, mutta ohjelmoijan näkökulmasta eri muuttujilla on erilaisia käyttötarkoituksia, kuten:

* askeltaja (`i`)
* yksisuuntainen lippu (`jatka`)
* tuoreimman säilyttäjä (`sademaara`)
* sopivimman säilyttäjä (`max`, `min`)
* kokooja (`summa`)
* kiintoarvo (`PI`, `lukija`, `desimaalit`)

Lue lisää näistä rooleista osoitteessa: [http://www.cs.joensuu.fi/~saja/var_roles/stud_vers/stud_Java_fin.html](http://www.cs.joensuu.fi/~saja/var_roles/stud_vers/stud_Java_fin.html)


## Alkuluku-esimerkki muuttujien roolien kera

Tässä esimerkkikoodissa hyödynnetään kiintoarvoa, yksisuuntaista lippua ja askeltajaa ja selvitetään, onko tietty luku alkuluku, eli onko se jaettavissa jollain muulla positiivisella kokonaisluvulla kuin yhdellä ja itsellään:

```java
public class Alkuluku {

    public static void main(String[] args) {
        // Koodissa on tarkoitus selvittää, onko tämä luku alkuluku.
        // Tätä lukua ei muuteta koodissa, joten sitä kutsutaan *kiintoarvoksi*.
        final int luku = 93;

        // *yksisuuntainen lippu* on alussa tietyssä arvossa, ja sitä muutetaan koodissa
        // ainoastaan yhteen suuntaan. Sen avulla tiedämme lopussa, onko alkuluku
        // osoitettu epätodeksi.
        boolean onAlkuluku = true;

        // *askeltaja* käy luvut läpi yksi kerrallaan: 2, 3, 4, 5, 6, ...., luku - 1
        for (int jakaja = 2; jakaja < luku; jakaja++) {
            // jos jako menee tasan, ei ole alkuluku
            if (luku % jakaja == 0) {
                onAlkuluku = false; // asetetaan lippu epätodeksi.

                // toisto voidaan nyt keskeyttää, koska luku on osoitettu ei-alkuluvuksi
                break;
            }
        }


        // jos lopussa *lippu* on edelleen tosi, ei löytynyt yhtään lukua, jolla jako menisi tasan
        if (onAlkuluku) {
            System.out.println("Luku " + luku + " on alkuluku");
        } else {
            System.out.println("Luku " + luku + " ei ole alkuluku");
        }
    }
}
```
