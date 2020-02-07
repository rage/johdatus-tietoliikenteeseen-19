---
path: '/osa-4/4-fyysinen-kerros'
title: 'Fyysinen kerros'
hidden: false
---


<text-box variant='learningObjectives' name='Oppimistavoitteet'>

- Ymmärrät miksi tämä kerros on mukana protokollapinossa

</text-box>


##  Fyysinen kerros

Käydään vielä täydellisyyden vuoksi hyvin lyhyesti läpi eri tavat kuljettaa viestejä paikasta toiseen tietoverkossa. Varsinaisesti fyysinen bittien siirtäminen paikasta toiseen ei enää ole osa tämän kurssin sisältöä, mutta usein on hyvä hiukan ymmärtää myös tätä osaa tietoliikennetekniikasta tai oikeastaan elektroniikasta.

Bittejä on kaksi: 0 ja 1. Ne täytyy erottaa toisistaan jollain tavalla. Yksi tapa on käyttää esimerkiksi jännitteitä ja niiden eroja kuvaamaan näitä kahta bittiä, jolloin erilaisista jännite-eroista voidaan päätellä kummasta bitistä kulloinkin on kyse. Valon kohdalla voidaan käyttää esimerkiksi eri väristä (eri spektri) valoa kuvaamaan eri bittejä.

Todellisuudessa bittien kuvaaminen sähkön, valon tai sähkömagneettisen säteilyn (=radioaaltojen) avulla on edellä kuvattua monimutkaisempaa, mutta tällä kurssilla riittää ymmärtää, että kummallekin bitille on oma kuvauksensa ja ne voidaan näin erottaa toisistaan. Tämä bittien koodaaminen tehdään yleensä jollakin [modulointitekniikalla](https://fi.wikipedia.org/wiki/Modulaatio_(elektroniikka)).

Bittien siirtonopeus riippuu toisaalta käytettävän materiaalin (esim kupari, valokuitu, ilma) sallimasta muutosnopeudesta ja toisaalta siitä kuinka pitkä ero kahden bitin kuvausten välillä pitää olla, jotta ne eivät sekoitu toisiinsa matkalla. Näistä saadaan kyseiselle materiaalille tai oikeastaan siitä tehdylle johtimelle liikennöintinopeus bitteinä sekunnissa.

Bitit voidaan koodata sähköisinä signaaleina. Tällöin yleensä käytetään joko [parikaapelia](https://fi.wikipedia.org/wiki/Parikaapeli) tai [koaksiaalikaapelia](https://fi.wikipedia.org/wiki/Koaksiaalikaapeli). Tyypillisesti kiinteistöjen omat dataverkot on toteutettu parikaapelilla. Aiemmin koaksiaalikaapeli oli yleisempi.

Tällä hetkellä on voimakas siirtymä kohti valokuituja, koska valolla saadaan paljon suurempi liikennöintinopeus. Merikaapelit ovat jo pitkään olleet valokuituja ja nyt muutkin kaapeloinnit ovat vähitellen siirtymässä valokuitupohjaisiksi. Tätä tukee voimakkaasti [liikenne- ja viestintäviraston määräys](https://www.traficom.fi/fi/viestinta/viestintaverkot/kiinteiston-sisaverkko), jonka mukaan vuodesta 2014 alkaen on uusiin ja peruskorjattaviin kiinteistöihin asennettava kuitu jokaiseen asuntoon.

Erilaiset fyysiset johtimet edellyttävät myös niihin liitettäviltä laitteilta kyseistä yhteystapaa tukevaa liitosta. Yleisin liityntätapa [parikaapelien](https://fi.wikipedia.org/wiki/Parikaapeli) kanssa on RJ45, tai oikeammin 8P8C. Yleensä näistä ethernet-liittimistä ja -parikaapeleista käytetään nimitystä rj45, on se sitten oikein tai väärin. Toinen parikaapeleihin liittyvät numeroryhmä on Cat5, Cat6 vai peräti Cat7. Tämä kategoria (category) kertoo miten hyvin kaapeli on suojattu erilaisilta häiriöiltä.


<!--  Osion 4 osaamistavoitteet -->

<quiz id="a3c24883-8267-4f32-91f5-d8793915f2d9"></quiz>



