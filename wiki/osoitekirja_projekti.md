# AddressBook ja Contact -esimerkkiohjelma


## Data

**Contact**

* name (`String`)
* email (`String`)
* phone (`String`)

## Ominaisuudet

**AddressBook**

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


