[&larr; Takaisin etusivulle](/)

<h1 class="js-toc-ignore">Toistorakenteet</h1>

Ehtorakenteiden tavoin toistorakenteilla voidaan vaikuttaa koodin suorituksen etenemiseen. Toistorakenteiden avulla tietyt koodirivit voidaan toistaa eri logiikoilla tai tarvittaessa jopa "ikuisesti". 

Tällä opetusviikolla harjoittelemme pääasiassa koodin toistamista tietyn määrän kertoja, toiston keskeyttämistä, sekä käymään läpi kokonaislukuja. Toistorakenteita hyödynnetään myöhemmin myös listojen ja taulukoiden yhteydessä, jolloin käymme läpi niissä olevia arvoja yksitellen.


**Sisällysluettelo**

<div class="js-toc"></div>


# While-toistorakenne

While-toistorakenne on yksinkertaisin tapa toistaa koodia Javalla. `while`-avainsanan jälkeen annetaan ehto sekä koodilohko, jota toistetaan niin kauan, kuin ehto on tosi:

```java
while (ehto) {
    // Toistetaan, jos ehto == true ja 
    // lopetetaan, kun ehto == false
}
```

Vuokaaviona while-toistorakenteen logiikka on seuraava:

![While loop flow diagram](assets/While-loop-diagram.svg)

Kuva: P. Kemp. While loop flow diagram. CC0. [Wikipedia](https://commons.wikimedia.org/w/index.php?curid=894438)


## while vs. if

Syntaksin puolesta `while` ja `if` ovat hyvin samankaltaiset:

```java
if (ehto) {
    // Suoritetaan *kerran*, jos ehto on tosi
}
```

```java
while (ehto) {
    // Toistetaan *niin kauan kuin* ehto on tosi
}
```

Ehtorakenteesta poiketen toistorakenteessa toistettavassa lohkossa tehdään tyypillisesti muutoksia, jotka vaikuttavat tarkistettavaan ehtoon. Näiden muutosten avulla toisto saadaan tyypillisesti päättymään, kun haluttu logiikka on saatu valmiiksi.


## Ehdon muuttaminen toistettavassa koodilohkossa

Jotta toistoehto muuttuisi jossain vaiheessa epätodeksi, tehdään toistettavassa koodilohkossa tyypillisesti operaatioita, jotka vaikuttavat toistoehtoon. Operaatio on usein jonkin muuttujan arvon kasvattaminen.

Kun koodia halutaan suorittaa tietty määrä kertoja, käytetään tyypillisesti muuttujaa, joka pitää kirjaa suorituskerroista. Tällaisesta muuttujasta käytetään myös termiä askeltaja. Seuraavassa esimerkissä `luku`-muuttujaa käytetään rajoittamaan suorituskertoja siten, että ruudulle tulostetaan vuorollaan luvut 1, 2, 3, 4 ja 5:

```java
// https://2017-ohjelmointi.github.io/part2/, CC BY-NC-SA
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

Voit katsoa myös videolta selostuksen yllä olevan koodin toiminnasta:

<iframe width="560" height="315" src="https://www.youtube.com/embed/us9GXUZ60ws" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Tämä esimerkki videoineen on lainattu Helsingin yliopiston Agile Education Research -tutkimusryhmän ohjelmointikurssilta ja se on lisensoitu Creative Commons BY-NC-SA-lisenssillä. [https://2017-ohjelmointi.github.io/part2/#section-40-toistolauseen-ehto-toiston-lopettajana](https://2017-ohjelmointi.github.io/part2/#section-40-toistolauseen-ehto-toiston-lopettajana)


# While-toistokäskyn hyödyntäminen

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

Yllä olevat HTML-valintaelementit muodostetaan [select](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select-) sekä [option](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/option)-tagien avulla kutakuinkin seuraavasti:

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

Tässä tuntiesimerkissä kokeilemme itse generoida HTML-elementit Javan toistorakenteen avulla. Aikaisemmasta esimerkistä poiketen emme kasvatakaan lukua yhdellä, vaan 500:lla. Muuten koodi on hyvin samankaltainen. Lukujen muotoilussa hyödynnetään DecimalFormat-luokkaa siten, että muotoilussa on käytetty tuhaterotinta (`.`) ja ehdollisia numeroita (`#`): `#,### €`.


# For-toistokäsky

While-toistokäskyn lisäksi on olemassa myös for-toistokäsky. For on tyypillinen esimerkiksi silloin, kun haluttu suoritusten määrä on jo alussa tiedossa. Tällöin laskurin alustaminen, kasvattaminen ja toistoehto saadaan kirjoitettua kompaktiin muotoon samojen sulkujen sisään:

```java
for (alustus; toistoehto; kasvatus) {
    // Tähän lohkoon kirjoitettu koodi 
    // Toistetaan, kunnes ehto == false
}
```

For-rakenteessa suoritetaan ensin alustus. Sen jälkeen tarkastetaan onko toistoehto tosi, ja jos on, suoritetaan koodilohko. Koodilohkon suorittamisen jälkeen suoritetaan aina kasvatusoperaatio, jonka jälkeen ehto tarkastetaan uudestaan.

Jos haluamme esimerkiksi tulostaa luvut yhdestä viiteen, kuten edellä teimme `while`-toistokäskyn kanssa, se voisi tapahtua seuraavasti:

Kirjoitetaan alustukseen `int luku = 1`:

```java
for (int luku = 1; toistoehto; kasvatus) {
    System.out.println(luku);
}
```

Sen jälkeen määritellään, millä ehdolla toistoa jatketaan. Nyt haluamme toistaa koodia luvuille yhdestä viiteen, eli `luku < 6`:

```java
for (int luku = 1; luku < 6; kasvatus) {
    System.out.println(luku);
}
```

Jotta toisto etenee aina kierroksittain luvusta seuraavaan, täytyy `luku`-muuttujan arvoa kasvattaa joka kierroksen jälkeen yhdellä, eli `luku++`:

```java
for (int luku = 1; luku < 6; luku++) {
    System.out.println(luku);
}
```

## For- ja while-toistorakenteet

Loogisesti samat toistorakenteet on mahdollista toteuttaa sekä while- että for-toistorakenteina. Rakenteeksi kannattaakin valita aina tapauskohtaisesti tarkoitukseen paremmin sopiva. Tyypillisesti for-toistorakenne on oivallinen tilanteissa, joissa käymme jonkin ennalta tunnetun luku- tai arvojoukon läpi. While-rakenteella on puolestaan luontevaa toteuttaa toistaiseksi toistettavaa logiikkaa, jonka toistojen määrä tai käsiteltävä arvojoukko ei ole ennalta tiedossa.

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

# For-toistokäskyn hyödyntäminen

Toteutetaan vertailun vuoksi toistorakenne, joka muodostaa [nettiauto.com:in](https://www.nettiauto.com/) hakutyökalun mukaisen vuosiluvun valintaan käytettävän HTML-rakenteen. Aikaisemmasta esimerkistä poiketen tässä elementissä luvut ovat laskevassa järjestyksessä, ja suurin arvo vaihtuu aina kuluvan vuoden mukaan:

<fieldset>
    <legend>Vuosimalli</legend>
    <select name="min">
        <option>Minimi</option>
        <option value="2022">2022</option>
        <option value="2021">2021</option>
        <option value="2020">2020</option>
        <option value="2019">2019</option>
        <option value="2018">2018</option>
        <option value="2017">2017</option>
        <option value="2016">2016</option>
        <option value="2015">2015</option>
        <option value="2014">2014</option>
        <option value="2013">2013</option>
        <option value="2012">2012</option>
        <option value="2011">2011</option>
        <option value="2010">2010</option>
    </select> - 
    <select name="max">
        <option>Maksimi</option>
        <option value="2022">2022</option>
        <option value="2021">2021</option>
        <option value="2020">2020</option>
        <option value="2019">2019</option>
        <option value="2018">2018</option>
        <option value="2017">2017</option>
        <option value="2016">2016</option>
        <option value="2015">2015</option>
        <option value="2014">2014</option>
        <option value="2013">2013</option>
        <option value="2012">2012</option>
        <option value="2011">2011</option>
        <option value="2010">2010</option>
    </select>
</fieldset>

Yllä olevat HTML-valintaelementit muodostetaan [select](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select-) sekä [option](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/option)-tagien avulla kutakuinkin seuraavasti:

```html
<select name="min">
    <option>Minimi</option>
    <option value="2022">2022</option>
    <option value="2021">2021</option>
    <!-- ... -->
    <option value="2011">2011</option>
    <option value="2010">2010</option>
</select>
```

For-toistorakenteeksi muutettuna läpikäytävät arvot ovat nyt vuosilukuja. Vuosilukujen alkuarvo on nyt esimerkiksi `int vuosi = 2022` ja toisto jatkuu niin kauan, kuin vuosi on vähintään 1886: `vuosi >= 1886`. Toistokertojen välissä ei tällä kertaa kasvateta, vaan vähennetään vuotta yhdellä `vuosi--`.

Yllä pienimpänä vuosilukuna käytettiin vuotta 1886, [jota pidetään nykyaikaisten autojen syntymävuotena](https://en.wikipedia.org/wiki/Car), mutta lopetusehdossa voi hyvin olla mikä vain vuosiluku.


## Oikean vuosiluvun käyttäminen

Toiston alustuksessa ei kannata käyttää kovakoodattua vuosilukua, vaan Javan valmiita `Year`- tai `LocalDate`-luokkia. Nykyisen vuosiluvun saat selville esimerkiksi seuraavalla koodilla:

```java
Year nykyinenVuosi = Year.now();
int vuosiluku = nykyinenVuosi.getValue();
```

`Year`-luokan käyttämiseksi joudut myös lisäämään luokkasi alkuun `import`-käskyn:

```java
import java.time.Year;
```

# Toistolauseesta poistuminen eli **break**

Varsin usein haluamme suorittaa koodia toistaiseksi, kunnes käyttäjä esimerkiksi antaa tietyn syötteen. Tällöin voi olla hyödyllistä tehdä "ikuinen silmukka" eli:

```java
// ehto on kovakoodattu, eli se ei tule koskaan muuttumaan epätodeksi:
while (true) {
    // "ikuisesti" toistettava koodi
}
```

Yllä esitetystä toistorakenteesta voidaan poistua tarvittaessa kesken toistettavan lohkon suorituksen komennolla `break`. Komento `break` on tyypillisesti toistolauseen lohkon sisällä olevassa ehtolauseessa, jossa tarkastellaan, haluaako käyttäjä poistua toistolauseesta, tai onko tapahtunut jokin muu toiston keskeyttävä tapahtuma.

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

Tässä esimerkissä merkkijonoja vertaillaan `equals`-metodilla, jota käsittelemme tarkemmin seuraavalla oppitunnilla.

# Tehtäviä tunnille

## Arvosana-asteikko

Tässä tehtävässä hyödynnämme kurssin etusivulla esitettyä `OsasuoritustenArviointi`-luokkaa ja laskemme kaikille mahdollisille pistemäärille (0-25) niitä vastaavat koearvosanat. Opimme samalla kutsumaan omassa projektissamme määritettyä metodia.

**Metodin kutsuminen**

Olemme aikaisemmin kutsuneet Javan valmiita metodeja, esim:

```java
double halvempi = Math.min(hinta1, hinta2);
```

Tässä `min` on **metodi**, joka sijaitsee `Math`-**luokassa**. `hinta1` ja `hinta2` ovat metodille annettavia **parametriarvoja**. `min` palauttaa tuloksena `double`-tyyppisen luvun, joka yllä olevalla rivillä asetetaan talteen `halvempi`-muuttujaan. Käyttääksemme tätä metodia meidän ei tarvitse tietää, miten sen koodi on sisäisesti toteutettu.

Samalla logiikalla voimme kutsua omassa koodissamme olevaa metodia. Luokassa `OsasuoritustenArviointi` on metodi nimeltä `laskeArvosana`. Kyseinen metodi tarvitsee kaksi `int`-kokonaislukua: saadut pisteet ja maksimipisteet. Lopputuloksena metodi palauttaa liukuluvun väliltä 0-5, joka on annetuilla pisteillä saatava arvosana. Näillä tiedoilla osaamme kutsua metodia seuraavasti:

```java
double arvosana = OsasuoritustenArviointi.laskeArvosana(omatPisteet, maksimiPisteet);
```

Tehdään seuraavaksi toistorakenne, joka käy läpi kaikki mahdolliset pistemäärät ja tulostaa niitä vastaavat arvosanat kokeessa, jossa maksimipisteet ovat 25.

## FizzBuzz

FizzBuzz-tehtävä on ohjelmistokehittäjien työhaastatteluiden klassikko, jossa yllättävän ison osan haastatelluista kerrotaan epäonnistuvan. Tehtävä on ratkaistavissa tämän ja kahden aikaisemman oppituntimme perusteella.

> The "Fizz-Buzz test" is an interview question designed to help filter out the 99.5% of programming job candidates who can't seem to program their way out of a wet paper bag. The text of the programming assignment is as follows:
>
> *"Write a program that prints the numbers from 1 to 100. But for multiples of three print “Fizz” instead of the number and for the multiples of five print “Buzz”. For numbers which are multiples of both three and five print “FizzBuzz”."*
>
> [http://wiki.c2.com/?FizzBuzzTest](http://wiki.c2.com/?FizzBuzzTest)

## Sademäärien kysyminen toiston avulla

Kirjoitetaan ohjelma, joka kysyy päivittäisiä sademääriä ennalta tunnetun määrän yksi kerrallaan. Lopuksi tulostetaan lukumäärä, summa, minimi, maksimi sekä keskiarvo.


## Tuntemattoman ajanjakson sademäärien kysyminen

Muutetaan ohjelmaa niin, että päivien lukumäärä ei ole ennalta tunnettu, vaan negatiivinen sademäärä lopettaa kysymisen.




---

Tämän oppimateriaalin on kehittänyt Teemu Havulinna ja se on lisensoitu [Creative Commons BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/) -lisenssillä.

<script src="/tocbot/tocbot.min.js"></script>
<script src="/scripts.js"></script>
<link rel="stylesheet" href="/tocbot/tocbot.css">

