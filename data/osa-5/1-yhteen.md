---
path: '/osa-5/1-yhteen'
title: 'Kaikki yhteen'
hidden: false
---


<text-box variant='learningObjectives' name='Oppimistavoitteet'>

- Osaat muodostaa kokonaisuuden kaikesta kurssilla käsitellystä.
- Osaat kuvata tietoliikenteen toimintaa eri tarkkuuksilla.
- Tiedät miten viestien välitys internetissä tapahtuu.

</text-box>


## Kaikki yhteen

Olemme käyneet läpi tietoliikenteen erilaisia osa-alueita, joitakin tarkemmin ja joitakin vain ohimennen.

Kootaan vielä kaikki asiat yhdeksi isommaksi kokonaisuudeksi. Tässä ei siis pitäisi enää tulla varsinaisesti uutta asiaa, vaan katsotaan kurssilla käsiteltyjen asioiden yhteistoimintaa.

![Kaavakuva missä viesti kulkee lähettäjältä vastaanottajalle useamman reitittimen kautta](../img/lahettaja-reititin-vastaanottaja.svg)



Lähdetään liikkeelle siitä, että käyttäjä kirjoittaa kotonaan www-selaimeen tietyn sivun URL-osoitteen (käytetään erimerkissä osoitetta http://www.helsinki.fi/opiskelijaksi


<!--  URL-osoite -->
<quiz id="44a72ec8-66d2-4116-83a7-40b5ecd154fa"></quiz>


Kuten muistamme, niin palvelimen nimi täytyy muuttaa IP-osoitteeksi, jotta pyyntö voidaan laittaa eteenpäin verkossa


<!--  verkkonimi IP-osoitteeksi -->
<quiz id="a9535cfa-86d6-4c87-9580-dfd50aa298ac"></quiz>


Nyt tiedetään jo palvelimen IP-osoite, joten sovelluskerroksella ei enää tehdä kovin paljoa.


<!--  HTTP ja kuljetuskerros -->
<quiz id="9e304b9a-7df8-464c-8573-d11c344dc324"></quiz>


Kuljetuskerroksen omissa otsaketiedoissa täytyy olla sovelluskerroksen palvelun/prosessin tunniste. Ajatellaan tätä siis kirjekuoreksi, jossa kuljetuskerroksen otsake on kirjekuoren päällä oleva osoite ja sovelluskerroksen viesti on kuoren sisällä oleva materiaali. (Sovelluskerros on jo voinut tehdä omasta viestistään erillisen kuoren ja antanut sen kuljetuskerrokselle. Uudemmissa verkkosovelluksissa tässä HTTP-protokollalta tulleessa viestissä voi olla jo useita sisäkkäisiä kuoria, mutta ne eivät näy kuljetuskerrokselle.)


<!--  prosessin tunnistaminen -->
<quiz id="adfc179d-8a8c-496a-9e82-e5fdb6ec5949"></quiz>


Nyt meillä on siis kuljetuskerroksen viestissä kuljetuskerroksen otsake ja sen data, joka sisältää sovelluskerroksen otsakkeen ja datan.

Seuraavaksi kuljetuskerros antaa verkkokerrokselle tämän viestin (kirjekuoren) välitettäväksi eteenpäin. Samalla se kertoo  verkkokerrokselle, sen tarvitsemat tiedot vastaanottavasta palvelimesta.


<!--  vastaanottaja verkkokerroksen otsakkeessa  -->
<quiz id="a530a00f-838b-4adc-9e74-da5d7de5a090"></quiz>


Nyt puolestaan verkkokerros laittaa kuljetuskerrokselta saamansa viestin omaa kirjekuoreen ja sen päälle tämän verkkokerroksen käyttämän osoitteen ja antaa tämän kuoren edelleen linkkikerrokselle.


<!--  vastaanottaja linkkikerroksen otsakkeessa -->
<quiz id="a707fee7-8503-40b8-895a-dccc9927715d"></quiz>


Ja linkkikerros lisää vielä yhden uuden kirjekuoren saamansa verkkokerroksen paketin ympärille. Tähän kuoreen kirjoitetaan päälle linkkikerroksen vastaanottajan osoite.

Todellisuudessa mitään kirjekuoria ei käytetä, vaan jokaisen kerroksen protokollalla on oma määritelty viestin rakenne, jonka alussa ovat kyseisen kerroksen otsaketiedot ja ylemmän kerroksen viesti otsakkeineen on tälle protokollalle vain välitettävää dataa.

Nyt vihdoin tuo välitettävä viesti on valmis poistumaan lähettäjän koneelta. Tämä lähtevä viesti on menossa www-palvelimelle, joka ei ole www-selaimen kanssa samassa aliverkossa. Esimerkiksi käyttäjä on kotona ja haluaa lukea www-sivun. Viesti pitää siis lähettää kotiverkosta ulos, mutta miten?

Tämä tapahtuu reitityksen avulla. Jokainen kone tietää oman oletusyhdyskäytävänsä IP-osoitteen.


<!--  Oletusyhdyskäytävä -->
<quiz id="9dada389-7d90-4591-b1fc-d06f7d29525c"></quiz>


Verkkokerros antaakin todellisuudessa linkkikerrokselle kirjekuoren, jonka päällä on IP-osoite, mutta haluaa, että linkkikerros toimittaa sen ensin ihan eri IP-osoitteella varustetulle reitittimelle. Tätä IP-osoitetta ei kirjoiteta verkkokerroksen kirjekuoren vastaanottajaksi, vaan vastaanottaja on edelleen tuo www-palvelimen IP-osoite. Siksi verkkokerroksen pitää tähän välityspyyntöön liittää nimenomaan yhdyskäytävänä toimivan reitittimen linkkikerroksen MAC-osoite.

Jos viesti olisi ollut menossa saman aliverkon laitteelle, esim. verkkokirjoittimelle, niin silloin linkkikerrokselle olisi annettu kyseisen laitteen MAC-osoite eikä reititystä olisi tarvittu. Tähän erotteluun käytetään aliverkon peitettä (network mask). Peitteen  avulla tietokone voi päätellä onko vastaanottaja samassa aliverkossa vai ei.
 

<!--  MAC-osoitteen selvittäminen -->
<quiz id="a8b24c90-8656-485e-b374-df00215a71e0"></quiz>


Näiden vaiheiden jälkeen viesti on vihdoin saatu siirrettyä yhden linkin verran eteenpäin kohti vastaanottajaa. Ensimmäisen linkin jälkeen viesti on siis päätynyt kotiverkon yhdyskäytävänä toimivalle reitittimelle.

Reitittimen linkkikerros poistaa viestistä linkkikerroksen kirjekuoren ja antaa verkkokerroksen kirjekuoren verkkokerrokselle tarkasteltavaksi. Reititin huomaa, että viesti ei ole sille tarkoitettu, joten se selvittää seuraavan vastaanottajan (usein joku toinen reititin) IP-osoitteen ja sen perusteella kyseisen laitteen linkkikerroksen osoitteen ja antaa viestin linkkikerrokselle välitettäväksi tälle laitteelle.

Näin viesti etenee vähitellen reitittimeltä toiselle, kunnes se saapuu Helsingin ylipiston reitittimelle.

Yliopiston reititin vastaanottaa viestin. Sekin tarkastelee vastaanottajan IP-osoitetta ja aliverkkopeitteen avulla havaitsee sen kuuluvan tiettyyn reitittimeen liitettyyn aliverkkoon, joten se lähettää viestin linkkikerroksen avulla sinne. Enää ei siis lähetetä viestiä jollekin välittävälle laitteelle vaan suoraan palvelimelle.

Näin viesti on monien vaiheiden kautta saapunut vastaanottajalle. Linkkikerros antaa oman kehyksensä datan verkkokerrokselle. Verkkokerros vielä tarkistaa, että viesti on tarkoitettu juuri tälle koneelle ja antaa sitten IP-paketin datan kuljetuskerrokselle. Kuljetuskerros katsoo oman viestinsä otsikoista vastaanottavan prosessin porttinumeron ja laittaa kuljetuskerroksen sanomassa olleen datan sinne. Näin sovelluskerros voi vihdoin saada itselleen lähetetyn sovelluskerroksen viestin ja käsitellä sen.

Koska kyseessä on www-palvelin ja viesti oli tiettyyn sivuun liittynyt GET-pyyntö, palvelin etsii kyseisen sivun ja muodostaa vastausviestin. Vastausviestin vastaanottajana on siis www-selain. Vastausviesti kulkee nyt päinvastaiseen suuntaan, mutta käy läpi samat vaiheet kuin pyyntöviesti. Nyt on tärkeä huomata, että reitti eri reitittimien kautta ei välttämättä ole sama kuin jota pitkin pyyntö tuli. Reitittimet tekevät jokaiselle paketille itsenäisen reitityspäätöksen, joten viestit voivat kulkea eri reittejä.


Palataan vielä lopuksi reitittimien toimintaan tarkemmin. Oheisessa kuvassa Reititin 1 vastaanottaa viestin, jonka alkuperäinen lähettäjä on käyttäjän tietokone ja lopullinen vastaanottaja reitittimen takana oleva palvelin (IP-osoite 111.112.113.56). Reititin 1 lähettää viestin edelleen reitittimelle 2, joka lähettää viestin palvelimelle.

![Kaavakuva missä viesti kulkee lähettäjältä (käyttäjän tietokone) vastaanottajalle (www-palveliin) kahden reitittimen kautta. Käyttäjän tietokoneen IP-osoite on 192.168.0.24 ja MAC-osoite A3-24-67-EF-11-A6. Reititin 1 on yhdistetty käyttäjän tietokoneeseen ja sen käyttäjän tietokoneen puoleinen IP-osoite on 192.168.0.3 ja MAC-osoite E6-E9-00-11-22-33. Reititin 1:n toisen puolen on IP-osoite on 242.242.242.42 ja MAC-osoite E6-E9-00-11-22-44. Reititin 1:n tämä puoli on yhdistetty Reititin 2:een. Reititin 2:n Reititin 1:n yhdistetyn puolen IP-osoite on 24.2.242.242.11 ja MAC-osoite C4:11:E3:EE:11:11. Reititin 2:n toisella puolella IP-osoite on 111.112.113.10 ja MAC-osoite C4:11:E3:EE:11:00. Reititin 2 on tältä puolelta yhdistettynä www-palvelimeen, jonka IP on 111.112.113.56 ja MAC AA:E1:86:11:3D:3E](../img/osa5-kuva.svg)


<!--  Reititin 1 -->
<quiz id="a408fd4b-82a0-4415-9d85-d8d6b095782e"></quiz>


## Yhteenvetona

Tietoliikenteessä on paljon toimijoita, mutta jokainen niistä hoitaa vain oman pienen tehtävänsä. Koko verkko toimii hyvin, kunhan jokainen sen pieni osa toimii hyvin. Verkon palveluja voi käyttää, vaikka ei verkon toimintaa täysin ymmärtäisikään. Oman kotiverkon ylläpito on helpompaa, kun tuntee siihen liittyvät käsitteet. IT-ammattilaisen, joka toteuttaa uusia verkkosovelluksia, on hyvä tuntea tietoliikenteen ja kommunikoinnin periaatteet, jotta oma sovellus toimisi tehokkaasti eikä kuormittaisi verkkoa tarpeettomasti.

Seuraavilla kursseilla tutustutaan tarkemmin eri protokollien toimintaan, niiden viestien rakenteisiin sekä erityisesti verkon kuormitukseen ja luotettavaan toimintaan liittyviin periaatteisiin.

Anna vielä lopuksi palautetta tästä kurssista. 

</quiz><!-- Palautetta -->
<quiz id="a18fe51a-80a8-41a7-99a5-d591ccba2f9a"></quiz>
