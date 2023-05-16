# Vinkkejä Viope-virhetilanteisiin

## "Could not find or load main class"

> <span style="color: red">Error: Could not find or load main class TerveMaailma
> Caused by: java.lang.NoClassDefFoundError: viikko1/perusteet/th/TerveMaailma (wrong name: TerveMaailma)</span>

Tämä virhe johtuu siitä, että Viope ei löydä toteuttamaasi luokkaa. Ongelma voi johtua joko virheellisesti nimetystä luokasta tai koodin alussa olevasta **package**-rivistä.

Vaikka ohjelmoisit omat ratkaisusi Eclipsessä hyvien käytäntöjen mukaisesti erillisiin paketteihin, tulee `package`-rivit poistaa aina palautettavien tiedostojen alusta. Viope ei tue paketteja tehtävien ratkaisuissa.

Vaikka ohjelma toimisi täysin oikein omalla Eclipselläsi, saattaa se aiheuttaa käännösvirheen, mikäli luokkasi nimi on eri kuin mitä Viope odottaa. Tarkista siis, että luokan nimi `public class Nimi { ... }` on kirjoitettu oikein kirjainkoko huomioiden.


## "Virhe tulostuksessa"

> Virhe tulostuksessa: ohjelmasi tulosti "maailma", vaikka tulostuksen olisi pitänyt olla "maailma!"

Vertaile merkki kerrallaan oman ohjelmasi tulostetta esimerkkitulosteeseen. Onko välimerkeissä tai numeroissa eroja? Entä kirjoitusvirheitä? Yllä olevassa esimerkkivirheessä oikeassa ratkaisussa on lopussa huutomerkki, joka puuttuu lähetetyn ratkaisun tulosteesta.


## "Virhe: ohjelmasi ei kääntynyt"

Jos luokassa on syntaksivirhe, ei kääntäjä pysty kääntämään ratkaisuasi eikä ohjelman suoritus ala lainkaan. Tällaisten tapausten välttämiseksi on tärkeää toteuttaa ja testata ratkaisusi aina ensin Eclipsessä, ja vasta sen jälkeen kopioida ainakin syntaksiltaan toimivaksi varmistettu ratkaisu Viopeen.

Nähdäksesi tarkemman virheilmoituksen Viopessa, avaa näkyville Java-kääntäjän antama virhe klikkaamalla "Kääntäjän viesti"-painiketta:

![Viopen kääntäjän viesti](/assets/viope_ohjelmasi_ei_kaantynyt.png)

Painike on Viopessa hieman hankala ymmärtää klikattavaksi sen tyylistä johtuen. Kääntäjän viesti kertoo missä kohdassa koodiasi virhe on.


<a href="https://video.haaga-helia.fi/media/K%C3%A4%C3%A4nt%C3%A4j%C3%A4n+virheilmoitukset+Viopessa/0_tpfd5pfd">Video: Kääntäjän virheilmoitukset Viopessa.</a>


## java.util.NoSuchElementException

![NoSuchElementException](/assets/NoSuchElementException.jpg)

Mikäli ohjelmasi vaikuttaa toimivan Eclipsessä moitteetta, mutta saat Viopessa virheen `java.util.NoSuchElementException`, varmista, että ohjelmasi ei jää odottamaan lisää syötteitä käyttäjältä.

Mikäli ohjelma pyytää syötettä vielä sen jälkeen, kun Viope on antanut sille kaikki esimerkkisuorituksessa annetut syötteet, syntyy tämä `NoSuchElementException`. Kuvassa virheilmoitus kertoo `nextInt`-kutsusta rivillä 17, joka kaatoi ohjelman, koska kaikki syötteet oli jo luettu.
