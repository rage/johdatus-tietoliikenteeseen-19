---
path: '/osa-4/1-kuljetuskerros'
title: 'Kuljetuskerros'
hidden: false
---


<text-box variant='learningObjectives' name='Oppimistavoitteet'>

- Osaat kuvata kuljetuskerroksen tehtävät ja sen keskeiset protokollat.
- Osaat kertoa TCP:n ja UDP:n toimintaperiaatteet, samankaltaisuudet ja erot.

</text-box>

<!-- Osoitteet ja kerrokset -->
<quiz id="302a3048-1ea7-4e48-8feb-f64cf6b0053b"></quiz>



## Kuljetuskerros

Kuljetuskerros tarjoaa kuljetuspalvelun sovelluskerrokselle siten, että sovellusten tai oikeammin niitä toteuttavien prosessien ei tarvitse huolehtia viestien välityksestä vaan ne voivat vaan antaa viestin toimitettavaksi kuljetuskerrokselle. Viestin pitää toki antaa jollekin tietylle kuljetuskerroksen protokollalle, joka sitten huolehtii viestin vastaanottajalle.  Samalla koneella voi olla toiminnassa useita prosesseja. (Katso Tietokoneen toiminta -kurssin materiaalia prosesseihin ja niiden toimintaan liittyen.) Prosessit käyttävät pistokkeita (engl. socket), jotka liitetään johonkin tiettyyn tietoliikenteen porttiin. Wikipediassa on ihan [lyhyt termistösivu tietoliikenteen pistokkeisiin liittyen](https://fi.wikipedia.org/wiki/Pistoke_(tietotekniikka)). Pistoke-termiähän käytetään myös sähköverkoissa.

Tietoliikenteen [porteilla](https://fi.wikipedia.org/wiki/Portti_(tietoliikenne)) on porttinumerot, joiden avulla ne erotetaan toisistaan. Osa porttinumeroista on yhdessä sovittu tiettyjen sovellusten käyttöön ja osa on vapaasti käytettävissä. Porttinumeron avulla kuljetuskerros osaa tunnistaa sovelluskerroksen viestin vastaanottajan. Se on tavallaan paikallinen postiluukku, johon saapuvat viestit laitetaan. Lähettäjän täytyy siis tietää vastaanottavan koneen sovelluksen käyttämä porttinumero. Tämä on mahdotonta, jos meillä ei olisi etukäteen tietoa siitä mihin asiakkaan ensimmäinen viesti pitää toimittaa. Siksi yleisimmille sovelluksille on sovittu tietyt porttinumerot, joita ne käyttävät. Tällöin asiakas voi lähettää viestin 'arvaamalla', että palvelimella on käytössä nimenomaan tämä yhteisesti sovittu porttinumero.

<!-- Porttinumeroita -->
<quiz id="a3a4050f-824f-4d9a-b57b-d85137b3f786"></quiz>

##  TCP

TCP:n avulla sovelluskerroksen prosessit voivat muodostaa loogisen yhteyden lähettäjän ja vastaanottajan välille. Yhteys on kaksisuuntainen, joten molemmat voivat lähettää ja vastaanottaa viestejä samaa yhteyttä pitkin. Yhteys on looginen, koska meillä ei ole yhtä tiettyä kiinteää putkimaista reittiä, jota pitkin kaikki viestit aina kulkisivat lähettäjän ja vastaanottajan välillä.
Sovelluksen ja TCP:n välinen yhteys on sovittu käsiteltäväksi tavuvirtana, jolloin TCP:n ei tarvitse tietää sovelluksen sanomien rakennetta tai niiden kokoa etukäteen, vaan kaikki sovelluksen viestit tulevat TCP:lle pistokkeen kautta tavujonona, ihan samaan tapaan kuin tiedostoissa on vain tavuja.

TCP:n keskeinen tehtävä on huolehtia sovellukselta tulevan viestijonon jaottelusta sopivan kokoisiin datagrammeihin, jotka sitten annetaan verkkokerrokselle toimitettavaksi vastaanottajan koneelle. Näihin datagrammeihin liitetään otsake, jossa on sekä porttinumero että vastaanottavan koneen IP-osoite. Vastaanottajan päässä kuljetuskerros käyttää tätä datagrammin otsakkeessa olevaa porttinumeroa oikean vastaanottavan prosessin tunnistamiseen.


![erillisten ftp- ja www-prosessien lähettämä data lomittuu matkalla vastaanottajalle](../img/lomittuvat-alt.svg)


TCP-yhteyden ylläpitäminen edellyttää, että yhteys muodostetaan ja päätetään hallitusti. Yhteyden muodostaminen TCP-protokollassa tapahtuu erityisen kättelymenettelyn kautta. Myös yhteyden päättämiseen on oma kättelymenettelynsä. Kättelyssä yhteyttä avaavat osapuolet lähettävät protokollan mukaisia viestejä, joiden avulla ne sopivat yhteyden olemassaolosta ja vastaanottaja voi samalla kertoa miten paljon tietoa se voi ottaa vastaan sillä hetkellä. Yhteyden päättäminen hallitusti edellyttää, että kumpikin lähettää erityisen yhteyden päättämiseen liittyvän viestin.

TCP lupaa toimittaa viestit luotettavasti vastaanottajalle. Luotettava tiedonvälitys edellyttää, että lähettäjä voi olla varma siitä, että viesti on saapunut vastaanottajalle. Koska internetissä ei ole erillistä kontrolliväylää, on vastaanottajan lähetettävä erillinen kuittausviesti, jolloin lähettäjä voi tästä tietää viestin saapuneen.

Mitä lähettäjä sitten tekee, jos kuittausta ei saavu? Se ei voi tietää onko sen lähettämä alkuperäinen viesti kadonnut vai onko kadonnut vain kuittausviesti vai toimiiko verkko vain tavattoman hitaasti ja viestit ovatkin vielä matkalla. Tämä ongelma on keskeinen kaikelle tietoliikenteelle, joten pysähdytään tähän ihan hetkiseksi.


### Viestin katoaminen ja siihen reagointi

Viestin katoamiseen tai vahingoittumiseen on monta syytä. Jossain matkan varrella tai vastaanottajalla ei ole tilaa viestin vastaanottamiseen. Koska valo, sähkö tai radioaallot eivät voi odottaa matkalla, katoaa viesti aina, jos sitä ei ajoissa voida ottaa talteen johonkin. Toisaalta matkalla minkä tahansa kahden pisteen välillä signaali on myös alttiina erilaisille häiriöille. Auringon energiapurkaus, satunnainen muu säteily tai joku muu häiriö voi sekoittaa viestin bittejä, jolloin viesti ei enää olekaan alkuperäinen.
Tällainen vaurioitunut viesti pyritään aina tunnistamaan ja poistamaan, jolloin viesti ei taaskaan päädy vastaanottajalle.

Viestien ja kuittausten katoamista vastaan lähettäjät käyttävät ajastimia (timer). Kun ne lähettävät viestin, ne laittavat ajastimen käyntiin. Jos kuittausta ei ole saapunut siihen mennessä, kun ajastin laukeaa, lähettäjä olettaa viestin kadonneen ja lähettää sen uudelleen. Lähettäjää ei siis kiinnosta oliko kadonnut alkuperäinen viesti vai kuittaus. Sitä kiinnostaa ainoastaan se, että sillä ei ole varmuutta viestin perillemenosta.

Lähettäjän viestien uudelleen lähetyksestä valitettavasti seuraa se, että vastaanottaja saattaa saada saman viestin kahteen kertaan.
Näin käy aina, kun alkuperäinen viesti meni perille, mutta kuittaus katosi. Koska sovellus on kuitenkin lähettänyt vain yhden viestin, on tärkeää, että tämä monistunut viesti päätyy vastaanottavalle sovellukselle vain kertaalleen. TCP estää tämän näkymisen sovellukselle numeroimalla viestit ja näin se voi tunnistaa mahdolliset monistumiset ja poistaa ylimääräiset viestit ennen kuin ne pääsevät sovellukselle asti.


## UDP

UDP on yksinkertainen kuljetusprotokolla, joka ei välitä luotettavuudesta eikä tarjoa varmaa tiedonsiirtoa. Se ei muodosta yhteyttä ja käsittelee jokaisen sovellukselta tulevan viestin erillisenä datagrammina. Wikipediassa on [sivu UDP:stä](https://fi.wikipedia.org/wiki/UDP).

UDP yksinkertaisesti vain ottaa sovellukselta viestin välitettäväksi ja laittaa sen eteenpäin verkkokerrokselle. Toki UDP:kin laittaa viestiin oman kehyksen, jossa on myös vastaanottavan sovelluksen käyttämä porttinumero, jotta vastaanotettu viesti voidaan toimittaa oikealle sovellukselle.

UDP siis vain lupaa lähettää viestin, mutta ei anna mitään takuita viestin perille menosta eikä käytä kuittauksia tämän tarkistamiseen.

UDP:tä käytetäänkin yleensä silloin, kun sovellukselle ei ole merkitystä että kaikki viestit menevät sellaisenaan perille tai sovellus haluaa itse huolehtia mahdollisista uudelleenlähetyksistä. Näin on usein esimerkiksi erilaisten reaaliaikaisten sovellusten kuten verkkopelien tai videoiden kanssa. Ehkä tunnetuin UDP:tä käyttävä järjestelmä on nimipalvelu (Domain Name Service, DNS).

UDP jää tällä kurssillä hyvin vähälle huomiolle. Tärkeintä onkin tunnistaa termi ja muistaa, että kyse on kuljetuskerroksen yksinkertaisesta protokollasta.



## TLS

Alkuperäiset kuljetuskerroksen protokollat eivät tarjoa salausta tiedonsiirron turvallisuuden parantamiseksi. Sitä varten on kehitetty aluksi SSL ja siitä edelleen TLS (Transport Layer Security), jolla voidaan salata TCP-yhteyksissä kulkevaa dataa. Yksinkertaistetusti voidaan ajatella että TLS on vain salattu TCP-yhteys. Salauksessa haastavinta salausalgoritmien lisäksi on suunnitella ja toteuttaa luotettava avainten hallinta. Avainten hallinta kuuluu erilaisilla tietoturva-kursseilla ja siksi emme sitä tällä kurssilla käsittele enempää kuin jo aiemmin esillä olleet varmenteet edellyttivät.



<!-- kuljetuskerroksen tehtävistä essee -->
<quiz id="a9702473-86ed-4b36-b0d5-dffb15b68730"></quiz>
(Esseetehtävä vaihdettu 13.3.2019 - tehtäväksi anto lisätty.)
