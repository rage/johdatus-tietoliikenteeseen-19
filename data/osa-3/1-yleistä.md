---
path: '/osa-3/1-yleistä'
title: 'Verkkosovellus'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

- Tutustut sovelluskerroksen toimintoihin.
- Osaat kuvata, miten http protokollalla viestien vaihto tapahtuu. Osaat kertoa, miksi https-protokolla on http-protokollaa parempi tietyissä tilanteissa.

</text-box>


Nyt lähdetään tutustumaan tietoliikenteen toiminnallisuuteen protokollapinon eri kerroksilla. Tässä osiossa vuorossa on pinon ylin kerros -sovelluskerros. Se on lähimpänä käyttäjää ja käyttäjän sovelluksia. Osa toiminnallisuuksista onkin jopa toteutettuna sovelluksen sisällä tai sovelluksen käyttämissä aliohjelmakirjastoissa. Ensin tarkastellaan asiaa verkossa toimivien sovellusten tarpeiden kautta.


## Verkkosovellus

Tietoverkon näkökulmasta sovelluskerroksella mietitään asioita vain kahden tai useamman keskenään kommunikoivan elementin kannalta. Kaikkien muiden protokollapinon kerrosten tehtävänä on omalta osaltaan huolehtia viestin siirtämisestä lähettäjältä vastaanottajalle. Tällä kerroksella täytyy oikeasti miettiä, mitä asiaa lähettäjällä on ja miten se pitäisi 'sanoa', jotta vastaanottaja voi sen ymmärtää.

Verkkosovelluksessa on siis useita eri paikoissa suoritettavia osia, jotka kommunikoivat keskenään tietoverkon välityksellä. Kukin sovelluksen palanen sekä lähettää että vastaanottaa viestejä muilta paloilta. Verkkosovellus voidaan toteuttaa monella eri tekniikalla ja hyvin erilaisilla abstraktiotasoilla. Perinteisessä internetin protokollapinossa ne kaikki kuuluvat sovelluskerrokselle, vaikka todellisuudessa osa näistä menetelmistä käyttää tiettyjä muita sovelluskerroksen palveluja oman toimintansa pohjana. Esimerkiksi web-sovellukset suoritetaan selaimessa, joka käyttää alun perin tekstipohjaisten www-sivujen siirtoon kehitettyä http-protokollaa oman kommunikointinsa pohjana.

Uudempia sovelluskerroksella tapahtuvia asioita ovat esimerkiksi esineiden internetiin (Internet of Things, IoT) liittyvät erilaiset ideat ja toteutukset, kuten ajatus siitä, että autot voisivat kommunikoida keskenään ja välittää esimerkiksi ruuhka- ja kelitietoja automaattisesti toisilleen. Näissäkin kommunikointi pohjautuu samoihin periaatteisiin, joita käymme tämän kurssin puitteissa läpi vähän perinteisemmillä esimerkeillä.

Verkkosovelluksen toteuttajalla, tekeepä hän web-sovellusta tai autojen välistä viestintää, on vastuullaan suuri joukko erilaisia päätöksiä sovelluksen toimintaan liittyen. Hänen täytyy miettiä sovelluksen arkkitehtuurin lisäksi myös osien välistä kommunikointia. Täytyy päättää mm. viestien rakenne ja sisältö, viestien välitysjärjestys, millaista välityspalvelua kuljetuskerrokselta halutaan, jne.  Viestien välitykseen liittyy mm. siirtoon kuluva aika, siirrettävän tiedon tarvitsema kapasiteetti, siirron luotettavuus ja mahdollisesti tarvittava salaus. Lisäksi on mietittävä saako viestejä kadota ja jos saa, niin miten sovellus silloin reagoi. Entä sallitaanko suuret viipeet siirrossa, ja mikä on tarvittava siirtokapasiteetti tai verkon läpäisykyky (throughput). Tällä kurssilla emme käy läpi sovelluksen suunnittelun tai toteutuksen näkökulmaa. Niitä käsittelevät muut kurssit, kuten esimerkiksi verkkosovellusten toteuttaminen tai web-sovellusohjelmointi.

## Verkkosovelluksen arkkitehtuuri

Vaikka emme tällä kurssilla opettelekaan varsinaisesti verkkosovellusten toteuttamista, niin joidenkin tietoliikenneratkaisujen ymmärtäminen on helpompaa, kun hahmottaa millaisia vaihtoehtoja sovelluksen toteutukselle on. Perinteisesti verkkosovellukset ovat käyttäneet asiakas-palvelija -mallia, jossa eri osilla sovellusta on keskenään erilaiset roolit. Esimerkiksi WWW-palvelussa, meillä on www-selain asiakkaan roolissa ja www-palvelin palvelijan roolissa. Asiakkaat ottavat yhteyttä palvelimeen ja palvelin vastaa niille.

Vertaistoimijamalli (peer to peer) on malli, jossa verkkosovelluksen osilla ei ole erilaisia rooleja, vaan kaikki ovat vertaisia ja niillä on samat toiminnallisuudet. Suomenkielessä usein puhumme suoraan vertaisverkosta (peer-to-peer network), jolloin ilman muuta oletetaan, että vertaiset ovat verkostoituneet keskenään. Wikipedian [suomenkielisellä sivulla](https://fi.wikipedia.org/wiki/Vertaisverkko) on lyhyt kuvaus aiheesta. [Englanninkielisellä sivulla](https://en.wikipedia.org/wiki/Peer-to-peer) on paljon laajempi selvitys.

Tämän kurssin kannalta noiden termien asiakas-palvelija ja vertaisverkko tunnistaminen riittää.


## Kuljetuskerroksen palvelut

Sovelluksille, joiden toiminta edellyttää, että kaikki viestit pääsevät perille, kuljetuskerros tarjoaa luotettavaa tiedonsiirtopalvelua. Se takaa, että viestit menevät perille samassa muodossa kuin ne on lähetetty, että ne eivät monistu matkalla ja että ne toimitetaan perille ennemmin tai myöhemmin. Jos esimerkiksi kaivinkone on katkaissut kaapelin tai palvelinkone on päivityksen vuoksi poissa käytöstä, niin viestiä ei voida toimittaa saman tien, vaan viestin toimitusviive voi olla hyvinkin pitkä. Sovellus voi toki asettaa aikarajan viestin välitykselle, mutta silloin voi olla, että viestiä ei saada toimitettua perille, kun vastaanottajaa ei tavoiteta ajoissa.

Jotkut sovellukset, kuten esimerkiksi verkkopelit, eivät puolestaan siedä pitkiä siirtoviiveitä tai suurta vaihtelua viestien kulkunopeuksissa. Sama koskee myös esim. videoiden katselua, silloinkin datan pitäisi siirtyä mahdollisimman tasaisesti. Videot tarvitsevat paljon siirtokapasiteettia, jolloin verkon nopeuden pitäisi olla mahdollisimman suuri. Tieverkossa puhutaan läpäisykyvystä (throughput) eli kuinka paljon liikennettä mahtuu kyseistä tietä pitkin kulkemaan. Tietoverkoissakin tämä olisi oikeampi termi, mutta yleisesti kuitenkin on otettu käyttöön termi 'verkon nopeus' vaikka verkko ei itse mihinkään liiku. Verkon maksimisiirtonopeus, esimerkiksi 1 Gb/s, asettaa teoreettisen maksimin verkon läpäisykyvylle, koska sitä suurempaa siirtonopeutta ei kyseisessä verkossa ole mahdollista saada. Käytännössä todelliset siirretyt datamäärät ovat huomattavan paljon pienempiä, koska verkossa liikkuu muitakin viestejä ja siirretyn datan määrään ei lasketa mukaan viestin otsakkeita.



Kuljetuskerroksen palveluja valittaessa sovelluksen suunnittelijan pitää siis päättää ainakin
<ul>
   <li> tarvitaanko luotettavaa kommunikointia vai riittäisikö epäluotettavampi?
   <li> onko viestin perille menon ajankohdalla väliä vai voiko viesti viipyä matkalla pidempään?
   <li> onko tarvittavalla siirtokapasiteetilla joku minimialaraja vai voidaanko ohjelman toiminta sopeuttaa käytettävissä olevaan verkon läpäisykykyyn?
   <li> kuinka turvallista kommunikointia tarvitaan vai voiko vain lähettää siten, että kaikki voivat nähdä viestit?
</ul>

Eri verkkosovelluksissa on tehty erilaisia ratkaisuja ja siksi ne toimivat eri tavoin.

Kuljetuskerroksella on käytössä kaksi vaihtoehtoista protokollaa TCP ja UDP, joiden toimintaan tutustutaan tarkemmin hiukan myöhemmin. Nyt kuitenkin katsotaan niiden tarjoamien palvelujen erot, koska sovelluksen täytyy valita kumpaa kuljetusprotokollaa se minkäkin viestin kanssa käyttää.

TCP on näistä monipuolisempi. Se tarjoaa luotettavan kuljetuspalvelun. Se lisäksi ylläpitää yhteyttä kommunikoivien osien välillä, joten peräkkäiset viestit voivat kulkea samaa loogista yhteyttä pitkin. Tietoliikenneverkon kannalta TCP pyrkii myös toimimaan kuormittamatta verkkoa tarpeettomasti. Siksi siihen on toteutettu myös vuonvalvonta (lähettää vain sen verran kuin vastaanottaja ehtii käsitellä) ja ruuhkanhallinta (lähettää vain sen verran kuin verkko ehtii välittää). Mikäli vastaanottaja tai verkko ei ehdi vauhtiin mukaan, niin TCP hiljentää lähetysvauhtia ja lähettää siis dataa hitaammin.

UDP puolestaan on yksinkertaisempi. Se vain ottaa viestin kuljetettavaksi, mutta ei välttämättä lupaa toimittaa sitä perille. UDP lupaa vain yrittää parhaansa (best-effort), mutta viestin välitys voi silti epäonnistua, jolloin viesti ei menekään vastaanottajalle. Mahdollinen viestin uudelleen lähetys on sovelluskerroksen vastuulla. UDP ei myöskään ota kantaa viestein välitysnopeuksiin, vaan se laittaa kaikki sovellukselta saamansa viestit saman tien eteenpäin. Taas mahdollinen sopeutuminen verkon välityskyvyn mukaan jää sovelluskerrokselle tehtäväksi.

Kumpikaan kuljetuskerroksen protokollista ei lupaa mitään viestin välityksen ajankohtaan liittyen. Mitään aikatakeita ei sovelluskerrokselle ole tarjolla. Ne eivät myöskään salaa viestejä. Salausta varten on erikseen SSL (secure socket layer) -kirjasto, joka salaa viestit ensin ja käyttää sitten TCP:tä viestien kuljettamiseen.

<quiz id="5c7e56533972a91474108c67"></quiz>
