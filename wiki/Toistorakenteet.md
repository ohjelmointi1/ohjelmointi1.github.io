[&larr; Takaisin etusivulle](/)

<h1 class="js-toc-ignore">Toistorakenteet</h1>

Ehtorakenteiden tavoin toistorakenteilla voidaan vaikuttaa koodin suorituksen etenemiseen. Toistorakenteiden avulla tietyt koodirivit voidaan toistaa eri logiikoilla tai tarvittaessa jopa "ikuisesti". 

Tällä opetusviikolla harjoittelemme pääasiassa koodin toistamista tietyn määrän kertoja sekä käymään läpi kokonaislukuja. Toistorakenteita hyödynnetään myöhemmin myös listojen ja taulukoiden yhteydessä, jolloin käymme läpi niissä olevia arvoja yksitellen.

Tänään opettelemme

* käyttämään while- ja for-toistorakenteita
* toistamaan koodia tietyn määrän kertoja
* toistamaan koodia kunnes tietty ehto toteutuu
* käymään läpi olemassa olevia arvoja toiston avulla.

**Sisällysluettelo**

<div class="js-toc"></div>


<!--
Tehtäväideat:

* piste- ja arvosana-asteikon läpikäynti toistorakenteen avulla
    - Mahdollisesti CSV-datan generointi?
    - toisessa luokassa olevan metodin kutsuminen!

* <option>-rakenteen generointi
    - vuosiluku
    - hinta
    - esimerkki nettiauto.com:ista!

-->

# While-toistokäsky

While-toistokäsky on yksinkertaisin tapa toistaa koodia Javalla. `while`-avainsanan jälkeen annetaan ehto sekä koodilohko, jota toistetaan niin kauan, kuin ehto on tosi:

```java
while (ehto) {
    // Toistetaan, jos ehto == true ja 
    // lopetetaan, kun ehto == false
}
```

## while vs. if

Syntaksin puolesta `while` ja `if` ovat hyvin samankaltaiset:

```java
while (ehto) {
    // Toistetaan *niin kauan kuin* ehto on tosi
}

if (ehto) {
    // Suoritetaan *kerran*, jos ehto on tosi
}
```

## Ehdon muuttaminen toistettavassa koodilohkossa

Jotta toistoehto muuttuisi jossain vaiheessa epätodeksi, tehdään toistettavassa koodilohkossa tyypillisesti operaatioita, jotka vaikuttavat toistoehtoon. 

Koodia halutaan esimerkiksi usein suorittaa tietty määrä kertoja, jolloin käytetään laskuria, joka pitää kirjaa suorituskerroista. Tässä esimerkissä `luku`-muuttujaa käytetään rajoittamaan suorituskertoja siten, että ruudulle tulostetaan vuorollaan luvut 1, 2, 3, 4 ja 5:

```java
public static void main(String[] args) {
    // alustetaan laskuri
    int luku = 1;

    // toistetaan kunnes luku saa arvon 6
    while (luku < 6) {
        System.out.println(luku);
        luku++; // sama kuin: luku = luku + 1;
    }
}
```

<iframe width="560" height="315" src="https://www.youtube.com/embed/us9GXUZ60ws" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Tämä esimerkki videoineen on lainattu Helsingin yliopiston Agile Education Research -tutkimusryhmän ohjelmointikurssilta ja se on lisensoitu Creative Commons BY-NC-SA-lisenssillä. [https://2017-ohjelmointi.github.io/part2/#section-40-toistolauseen-ehto-toiston-lopettajana](https://2017-ohjelmointi.github.io/part2/#section-40-toistolauseen-ehto-toiston-lopettajana)


## While-toistokäskyn hyödyntäminen

Tehdään oppitunnilla pieni Java-ohjelma, joka generoi HTML: `<select>`-elementin. Elementin idea on peräisin [nettiauto.com:in](https://www.nettiauto.com/) hakutyökalusta, jossa haettavan auton hintaa voidaan rajoittaa vastaavalla tavalla.

Tämän yksinkertaistetun esimerkin avulla voit valita hinnan ylä- ja alarajan 500 euron välein väliltä 0-5&nbsp;000 euroa:

<fieldset>
    <legend>Hinta</legend>
    <select name="min">
        <option>Minimi</option>
        <option value="0">0 €</option>
        <option value="500">500 €</option>
        <option value="1000"> 1 000 €</option>
        <option value="1500"> 1 500 €</option>
        <option value="2000"> 2 000 €</option>
        <option value="2500"> 2 500 €</option>
        <option value="3000"> 3 000 €</option>
        <option value="3500"> 3 500 €</option>
        <option value="4000"> 4 000 €</option>
        <option value="4500"> 4 500 €</option>
        <option value="5000"> 5 000 €</option>
    </select> - 
    <select name="max">
        <option>Maksimi</option>
        <option value="0">0 €</option>
        <option value="500">500 €</option>
        <option value="1000"> 1 000 €</option>
        <option value="1500"> 1 500 €</option>
        <option value="2000"> 2 000 €</option>
        <option value="2500"> 2 500 €</option>
        <option value="3000"> 3 000 €</option>
        <option value="3500"> 3 500 €</option>
        <option value="4000"> 4 000 €</option>
        <option value="4500"> 4 500 €</option>
        <option value="5000"> 5 000 €</option>
    </select>
</fieldset>

Yllä olevat HTML-valintaelementit muodostetaan [select](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select-) sekä [option](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/option)-tagien avulla seuraavasti:

```html
<select name="min">
    <option>Minimi</option>
    <option value="0">0 €</option>
    <option value="500">500 €</option>
    <option value="1000"> 1 000 €</option>
    <option value="1500"> 1 500 €</option>
    <!-- ... -->
    <option value="5000"> 5 000 €</option>
</select>
```

Tässä tuntiesimerkissä kokeilemme itse generoida HTML-elementit Javan toistorakenteen avulla.


# For-toistokäsky

While-toistokäskyn lisäksi on olemassa myös for-toistokäsky. For on tyypillinen esimerkiksi silloin, kun haluttu suoritusten määrä on jo alussa tiedossa. Tällöin laskurin alustaminen, kasvattaminen ja toistoehto saadaan kirjoitettua kompaktiin muotoon samojen sulkujen sisään:

```java
for (alustus; ehto; kasvatus) {
    // Tähän lohkoon kirjoitettu koodi 
    // Toistetaan, kunnes ehto == false
}
```

For-rakenteessa suoritetaan ensin alustus. Sen jälkeen tarkastetaan onko ehto tosi, ja jos on, suoritetaan koodilohko. Koodilohkon suorittamisen jälkeen suoritetaan aina kasvatusoperaatio, jonka jälkeen ehto tarkastetaan uudestaan.

Jos haluamme esimerkiksi tulostaa luvut yhdestä viiteen, kuten edellä teimme `while`-toistokäskyn kanssa, se voisi tapahtua seuraavasti:

Kirjoitetaan alustukseen `int luku = 1`:

```java
for (int luku = 1; ehto; kasvatus) {
    System.out.println(luku);
}
```

Sen jälkeen määritellään, millä ehdolla toistoa jatketaan. Nyt haluamme toistaa koodia luvuille yhdestä viiteen:

```java
for (int luku = 1; luku < 6; kasvatus) {
    System.out.println(luku);
}
```

Jotta toisto etenee aina kierroksittain luvusta seuraavaan, täytyy `luku`-muuttujan arvoa kasvattaa:

```java
for (int luku = 1; luku < 6; luku++) {
    System.out.println(luku);
}
```

## For- ja while-toistorakenteet

Loogisesti samat toistorakenteet on mahdollista toteuttaa sekä while- että for-toistorakenteina. Rakenteeksi kannattaakin valita aina tapauskohtaisesti tarkoitukseen paremmin sopiva.

```java
for (int i = 0; i < 3; i++) {
    System.out.println(i); 
}
```

Sama while-toistokäskyllä:

```java
int i = 0; // toistossa käytettävän muuttujan alustus 

while (i < 3) { // toistoehto 
    System.out.println(i); 
    i++; // muuttujan päivitys
}
```

Tämä esimerkki on lainattu Helsingin yliopiston Agile Education Research -tutkimusryhmän ohjelmointikurssilta ja se on lisensoitu Creative Commons BY-NC-SA-lisenssillä. [https://2017-ohjelmointi.github.io/part6/#section-35-for-toistolause](https://2017-ohjelmointi.github.io/part6/#section-35-for-toistolause)

Molemmat oheisista esimerkeistä tulostavat ruudulle luvut 0, 1 ja 2. Ainoa ero on se, että while-esimerkissä muuttuja `i` on olemassa myös toistolauseen jälkeen.

# Toistolauseesta poistuminen eli (`break`)

Varsin usein haluamme suorittaa koodia toistaiseksi, kunnes käyttäjä esimerkiksi antaa tietyn syötteen. Tällöin voi olla hyödyllistä tehdä "ikuinen silmukka" eli:

```java
while (true) {
    // "ikuisesti" toistettava koodi
}
```

Toistolauseesta voidaan poistua tarvittaessa kesken toistettavan lohkon suorituksen komennolla `break`. Komento `break` on tyypillisesti toistolauseen lohkon sisällä olevassa ehtolauseessa, jossa tarkastellaan, haluaako käyttäjä poistua toistolauseesta tai onko tapahtunut jokin muu toiston keskeyttävä tapahtuma.

```java
/* 
 * Tämä esimerkki on lainattu Helsingin yliopiston Agile Education Research -tutkimusryhmän
 * ohjelmointikurssilta ja se on lisensoitu Creative Commons BY-NC-SA-lisenssillä. 
 * https://2017-ohjelmointi.github.io/part2/#section-47-toistolauseesta-poistuminen 
 */
Scanner lukija = new Scanner(System.in);

while (true) {
  System.out.println("osaan ohjelmoida!");

  System.out.print("jatketaanko (ei lopettaa)? ");
  String komento = lukija.nextLine();
  if (komento.equals("ei")) {
    break;
  }
}

System.out.println("kiitos ja kuulemiin.");
```

## Tehtävä 1: sademäärien kysyminen toiston avulla

Tuntitehtävä: kirjoitetaan ohjelma, joka kysyy päivittäisiä sademääriä ennalta tunnetun määrän yksi kerrallaan. Lopuksi tulostetaan lukumäärä, summa, minimi, maksimi sekä keskiarvo.


## Tehtävä 2: tuntemattoman ajanjakson sademäärien kysyminen

Tuntitehtävä: Muutetaan ohjelmaa niin, että päivien lukumäärä ei ole ennalta tunnettu, vaan negatiivinen sademäärä lopettaa kysymisen.


---

Tämän oppimateriaalin on kehittänyt Teemu Havulinna ja se on lisensoitu [Creative Commons BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/) -lisenssillä.

<script src="/tocbot/tocbot.min.js"></script>
<script src="/scripts.js"></script>
<link rel="stylesheet" href="/tocbot/tocbot.css">