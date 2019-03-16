---
path: '/osa-4/2-verkkokerros'
title: 'Verkkokerros'
hidden: false
---


<text-box variant='learningObjectives' name='Oppimistavoitteet'>

- Osaat kertoa mitä verkkokerroksen tehtävät ovat.
- Osaat kuvata IP-protokollan keskeisen toiminnan.
- Osaat yleisellä tasolla kertoa mikä reititin on ja miten se toimii viestien välityksessä

</text-box>


##  Verkkokerros

Verkkokerros on internetin keskeinen osa. Joissakin vertauksissa internetin verkkokerrosta ja erityisesti IP-protokollaa kuvataan symbolisesti tiimalasin kavennuksena. Verkkokerroksen yläpuolella sovelluskerroksella on paljon erilaisia protokollia ja sovelluksia, jotka kaikki puristetaan IP-protokollan mukaisten IP-pakettien sisään verkkokerroksella. Toisaalta taas verkkokerroksen alapuolella linkkikerroksella on paljon erilaisia linkkitoteutuksia, jotka kaikki kuljettavat sisällään näitä IP-paketteja. IP-paketteja kutsutaan joskus myös datagrammeiksi niiden englanninkielisen nimen mukaan.

Verkkokerros siis saa kuljetuskerrokselta viestin, johon verkkokerros lisää omat otsaketietonsa ja antaa sen sitten linkkikerrokselle siirrettäväksi seuraavaan käsittelypisteeseen.

Verkkokerros lupaa viedä kuljetuskerrokselta saamansa viestin vastaanottavan koneen kuljetuskerrokselle, mikäli mahdollista. Verkkokerros ei lupaa mitään viestin perillemenosta. Jos verkossa on ruuhkaa niin viesti saattaa kadota. Kuljetuskerroksen pitää itse huomata tämä, verkkokerros ei lupaa raportoida ongelmista. On verkkokerroksella toki erillinen ICMP-protokolla, jolla joitain tilanteita voi yrittää selvittää, mutta sitä emme käsittele, koska silläkään ei raporttia ongelmatilanteista luvata.

Me tutustumme tällä kurssilla vain IP-protokollaan ja siitäkin lähinnä sen vanhempaan IPv4 versioon.

## IP-protokolla

IP-protokolla on internetin kaikkein tärkein protokolla. Se liimaa sovellus- ja kuljetuskerrokset yhteen alemman linkkikerroksen kanssa. Kaikkien internetissä viestejä lähettävien ja vastaanottavien laitteiden on osattava IP-protokollaa. IP-protokollan yksityiskohtia on kuvattu Wikipediassa [vastaavalla sivulla](https://fi.wikipedia.org/wiki/IP). Protokollana IP ei ole kovin kummallinen: muodostetaan IP-paketti ja lähetetään se linkkikerroksen avulla matkalle kohti vastaanottajaa. Vastaanottajalla puolestaan verkkokerros saa IP-paketin linkkikerrokselta, poistaa siitä omat otsaketiedot ja antaa sen oikealle kuljetuskerroksen protokollalle käsiteltäväksi.

IP:n kuvaus usein keskittyykin kuvaamaan yksityiskohtaisesti mitä tietoa IP-paketti sisältää eli miten IP-paketin otsake on muodostettu. 
IP-paketille on ihan [oma Wikipedian sivu](https://fi.wikipedia.org/wiki/IP-paketti).


![Kuva IP-paketin otsaketiedoista](../img/ip-paketti.svg)


IP-paketin otsakkeessa on siis kuljetuskerroksen protokollan tunnistenumero, lähettäjän ja vastaanottajan IP-osoitteet sekä joukko erilaisia lisätietoja, jotka tässä ohitetaan. Ihan ensimmäisenä otsakkeessa on versionumero, jotta tiedetään miten otsakkeen muodostava bittijono pitää tulkita. IPv4:n ja IPv6:n otsakkeet ovat erilaiset jo ihan sen takia, että käytettävät IP-osoitteet ovat erimittaisia.


## Reititin

IP-protokollan keskeinen tehtävä  on huolehtia IP-paketin siirto lähettäjältä vastaanottajalle. Koska internet on toteutukseltaan etappivälitteinen, niin IP-paketit siirtyvät vaiheittain verkon sisällä lähettäjältä vastaanottajalle reitittimien muodostamaa verkostoa pitkin.  Muistat varmaan, että reitittimet yhdistävät eri aliverkkoja toisiinsa ja huolehtivat viestien välittämisestä aliverkkojen välillä.  Tämä sama malli laajenee koko internetiin. Kukin reititin huolehtii viestien kuljettamisesta vain omalta osaltaan. Se vastaanottaa viestejä kahdesta tai useammasta aliverkosta ja lähettää ne edelleen kohti vastaanottajaa, vaikka vastaanottaja ei olisikaan missään suoraan reitittimeen liitetyssä aliverkossa vaan jossain kauempana. Reitittimellä pitää siis olla tietoa siitä missä päin verkkoa erilaiset IP-numerot oikein ovat. Tätä kutsutaan reititykseksi (Wikipedian [sivulla](https://fi.wikipedia.org/wiki/Reititys) on paljon tähän liittyvää termistöä.)

Reitityksessä on kaksi erilaista toimintoa. Toinen on reittien määrittely, jota tehdään erilaisilla reititysalgoritmeilla. Toinen tämän kurssin kannalta tärkeämpi vaihe, on reitittimen vastaanottamien IP-pakettien lähettäminen edelleen seuraavalle reitittimelle. Reititysalgoritmeja emme käsittele, vaan oletamme, että reitittimellä on jo valmiina reititystaulu, jonka perusteella IP-paketin edelleenlähetys (engl. forwarding) tapahtuu.

Kun IP-paketti saapuu reitittimelle, niin reititin katsoo reititystaulustaan mihin linkkiin paketti pitää lähettää, jotta se aikanaan päätyisi vastaanottajalleen. IP-paketissa on vastaanottajan IP-numero, jonka avulla tämä reititystaulusta linkkitiedon poimiminen tehdään.  Yleensä reititystauluihin on määritelty oletusyhdyskäytävä (engl. default gateway), jolle annetaan kaikki ne saapuvat IP-paketit, joille ei ole määritelty tarkempaa suuntaa reititystaulussa. Tällä tekniikalla esimerkiksi kotiverkon ja  muun internetin yhdistävällä reitittimellä on varsin pieni reititystaulu. Kotiverkon osoitteet ovat kotiverkon puoleisessa linkissä ja kaikki muut ovat palveluntarjoajan verkkoon vievän linkin takana. Myös kaikkien verkkoon liitettävien laitteiden täytyy tietää vähintään oletusyhdyskäytävän osoite. Tosin niiden oletusyhdyskäytävä on oman aliverkon reititin. Tämän tiedon ne nykyisin saavat jo DHCP-kyselyn vastauksena. 

Reititin ei voi ylläpitää reititystaulussaan kaikkia mahdollisia IP-osoitteita, joten se tallettaa tietoja käyttäen IP-osoitteiden yhteisiä alkuosia. Jos esimerkiksi osoitteet 192.168.0.x on yhden linkin takana ja 192.168.1.x toisen, niin reititystaulussa on rivi kummallekin ryhmälle. Yhteinen alkuosa voi olla bittitasolla muuallakin kuin tavurajalla. Siksi tässä esimerkkitaulussa osoitteet on kuvattu bittitasolla eikä numeroina kuten muualla materiaalissa. 192.168.0.x bittitasolla 11000000 10101000 00000000 xxxxxxxx.

Reitittimen reititystaulu voisi näyttää vaikka seuraavanlaiselta:

<table>
  <tr>
    <th>Osoitteet</th> <th> Linkin numero </th>
  </tr>
  <tr>
    <th> 11000000 10101000 00000000 ******** </th> <th> 3 </th>
  </tr>
  <tr>
    <th> 11000000 10101000 00000001 ******** </th> <th> 2 </th>
  </tr>
  <tr>
    <th> 11000000 10101000 00010*** ******** </th> <th> 1 </th>
  </tr>
  <tr>
    <th> 11000000 10101000 ******** ******** </th> <th> 4 </th>
  </tr>
  <tr>
    <th> *                                   </th> <th> 0 </th>
  </tr>
</table>

Tämän taulun perusteella viesti, jonka vastaanottajan IP-numero on 11000000 10101000 00010101 00100010 ohjataan linkkiin 1, koska osoitteiden alkuosat ovat identtiset. Sitä ei ohjata linkkiin 4, koska sillä on pidempi yhteinen alkuosa linkkiin yksi menevien osoitteiden kanssa. Tähtien tilalla voi olla joko 0 tai 1, joten niiden kohdalla osoitteet voivat erota. Vastaavasti osoite, joka alkaa 01... ohjataan linkkiin 0, johon ohjataan kaikki viestit, joiden vastaanottajat eivät täsmää muiden osoitteiden kanssa.

<quiz id="a0b14163-7ff6-4cf2-8059-d46b7de88cdc"></quiz>

