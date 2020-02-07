---
path: '/osa-4/3-linkkikerros'
title: 'Linkkikerros'
hidden: false
---


<text-box variant='learningObjectives' name='Oppimistavoitteet'>

- Osaat kuvata linkkikerroksen tehtävät.
- Osaat perustella miksi linkkikerros keskittyy vain yhteen liikennöintiväliin
- Osaat yleisellä tasolla kertoa Ethernetin toimintaperiaatteen

</text-box>


Aiemmissa osioissa on jo ollut paljon materiaalia eri kerrosten osoitteista.

<quiz id="9e9179e8-7e45-4c81-b0e0-d19cab054a7f"></quiz>


##  Linkkikerros

Linkkikerroksen tehtävä on siirtää viesti yhden linkin sisällä lähettäjältä vastaanottajalle. Linkkikerros siis keskittyy vain viestin siirtoon fyysisen yhteyden yli yhdeltä solmulta toiselle solmulle. Linkkikerros ei siis välitä mitä viestin sisällä on tai minne sen lopulta pitää päätyä. Linkkikerros vain yksinkertaisesti siirtää viestin tämän yhden linkin yli seuraavalle laitteelle, joka usein on reititin.

Yhteys kahden laitteen välillä eli linkki voidaan toteuttaa usealla eri tavalla ja viestien siirtoon on myös useita vaihtoehtoisia protokollia. Tällä kurssilla tutustumme niistä vain ethernet-verkkoon, koska se on tyypillinen internetin linkkikerroksen toteutustapa.



## Ethernet

Ethernet on ensimmäinen ja varsin vakiintunut tapa toteuttaa lähiverkko. Esimerkiksi kotiverkot on yleensä aina toteutettu ethernet-verkkoina, jos niissä on kaapeloituja yhteyksiä laitteiden välillä.  Ethernet on muuttunut vuosikymmenten aikana. Kaapelointitekniikoita on muokattu ja verkon liikennöintinopeuksia on samalla saatu moninkertaistettua. Wikipediassa on [suhteellisen kattava artikkeli tästä kehityksestä](https://fi.wikipedia.org/wiki/Ethernet).

Tällä kurssilla keskitytään kuitenkin enemmän siihen, millaisia viestejä ethernet-verkossa välitetään ja miten ne verkossa liikkuvat. Jätetään tuleville kursseille verkon sanomien välitystekniikka CDMA/CS ja sen toiminnallisuus.

Ethernetissä kulkevia viestejä kutsutaan nimellä kehys (engl. frame). Kehyksen rakenne on määritelty tarkasti ja niillä on maksimipituus. IP-osoite oli verkkokerroksen vastaanottajan tunniste ja se kertoo lopullisen IP-paketin vastaanottavan koneen. Ethernet-verkossa viesti lähetetään aina saman verkon jollekin laitteelle, joten tässä verkossa käytetään MAC-osoitteita.

Kun verkkokerros pyytää linkkikerrosta välittämään IP-paketin, niin sen pitää kertoa mille paikallisen verkon koneelle tämä IP-paketti pitää toimittaa. Verkkokerroksella tiedetään oletusyhdyskäytävän tai reititystaulusta katsotun seuraavan reitittimen IP-osoite. Linkkikerros kuitenkin välittää kehyksiä MAC-osoitteiden perusteella. Näin ollen pyynnön yhteydessä täytyy selvittää vastaanottavan laitteen MAC-osoite. Tämä voidaan tehdä, joko suoraan omasta välimuistista, jos kyseisen koneen kanssa on viestitelty hiljattain, tai MAC-osoite voidaan kysyä ARP-protokollalla. ARP (Address resolution protocol) on monilähetysprotokolla, jolla lähettäjä kysyy kaikilta verkon laitteilta, mikä niistä käyttää kyseistä IP-numeroa. Kaikki saavat viestin, mutta vain laite, jolla tuo IP-numero on, vastaa ja kertoo oman MAC-osoitteensa. Tämä osoite voidaan tilapäisesti tallettaa omaan välimuistiin niin sanottuun ARP-tauluun.  ARP-taulussa on siis tallennettuna IP-osoite ja MAC-osoite pareja, joille on vielä asetettu tietty voimassaoloaika.

Ethernet lisää kehyksen alkuun (ja loppuun) omat otsake (ja lopuke) -tietonsa. Kehyksen varsinainen data sisältää välitettävän IP-paketin. Kehyksen otsakkeessa on lähettäjän ja vastaanottajan MAC-osoitteiden lisäksi myös joitakin muita kenttiä, mutta sivuutetaan ne tällä kurssilla.

Ethernet on suunniteltu monilähetysverkoksi, jossa kaikki verkon laitteet kuulevat kaiken liikenteen. Nykyiset verkot ovat jo niin laajoja, että vaikka ne loogisesti ovat edelleen monilähetysverkkoja, joissa kaikki kuulevat kaiken liikenteen, niin todellisuudessa niitä on pyritty osittamaan siten, että viestit eivät törmäilisi keskenään. Tähän osittamiseen käytetään nykyisin kytkimiä. Aiemmin käytettiin myös siltoja ja toistimia (repeater). 

<quiz id="9ecd2877-7e75-44ee-96f5-d1eb8fd17917"></quiz>



## Kytkin

Kytkin on lähiverkon laite, jonka tehtävänä on välittää liikennettä linkkikerroksen tasolla siten, että kaikki laitteet saavat kaiken niille kuuluvan liikenteen. Kytkimet ovat rakenteellisesti moniporttisia. Usein kotiverkon monitoimilaite on kaikkien muiden toimintojensa ohella myös esimerkiksi 4-porttinen kytkin. Siihen voidaan liittää 4 erillistä ethernet-kaapelia, jotka kuitenkin loogisesti ovat osa yhtä ja samaa lähiverkkoa. Isommissa organisaatioissa käytetään erillisiä kytkimiä, joilla ei ole muita toiminnallisuuksia. Tällaisissa kytkimissä voi olla jopa useita kymmeniä portteja.

Kytkin siis vastaanottaa liikennettä kaikista porteista ja välittää sitä myös kaikkiin portteihin. Kaikille vastaanottajille tarkoitetut moni- ja yleislähetykset (multicast, broadcast) se lähettää kaikkiin portteihin. Vain yhdelle vastaanottajalle tarkoitetut yksilähetykset (unicast) välitetään siihen porttiin, jossa kytkin tietää kyseisen vastaanottajan sijaitsevan. Jos se ei tätä jo tiedä, niin se lähettää myös yksilähetyksen kaikkiin portteihin.

Kytkin kirjaa omaan kytkintauluunsa välittämistään viesteistä niiden lähettäjän MAC-osoitteen ja sen mistä portista kehys saapui. Näin se vähitellen oppii, minkä portin kautta mikin MAC-osoite liikennöi.


### Reititin, kytkin ja toistin - erot

Erilaiset verkkolaitteet on kaikki suunniteltu välittämään pakettikytkentäisen verkon viestejä, kutsutaanpa niitä millä nimellä tahansa.

Reititin tekee tätä välitystyötään verkkokerroksen tasolla ja päättää mihin suuntaan (seuraavan reitittimen IP-osoite) IP-paketti pitää lähettää, jotta se aikanaan pääsisi lopulliselle vastaanottajalleen.

Kytkin tekee välitystyötä linkkikerroksella ja päättää kehyksen vastaanottajan MAC-osoitteen perusteella, mihin porttiin kyseinen kehys pitää välittää.

Toistin (repeater) on näistä yksinkertaisin. Se vain välittää kaikki viestit kahden eri segmentin välillä. Toistimia käytetään esimerkiksi pitkillä yhteyksillä signaalin vahvistamiseen. Sen voidaan ajatella toimivan fyysisellä kerroksella, koska se ei millään tavalla tutki välittämänsä sanoman sisältöä. Se vain toistaa viestin bitit sellaisenaan seuraavaan segmenttiin.


<quiz id="a1dbfb46-80e4-4b18-ae80-d5f66102e887"></quiz>
