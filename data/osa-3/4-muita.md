---
path: '/osa-3/4-muita'
title: 'Muita esimerkkejä'
hidden: false
---

## Muita esimerkkejä sovelluskerroksen protokollista

WWW-palvelun ja tiedostopalvelujen lisäksi sovelluskerroksella on satoja muitakin palveluja ja niiden omia protokollia.  Yksi yleisimmistä on sähköpostin lähettämisessä käytetty SMTP.

## Sähköposti

Sähköpostipalvelu poikkeaa aiemmista palveluista siinä, että sähköpostin lähettämiseen sähköpostipalvelimelle käytetään SMTP-protokollaa (Simple Mail Transfer Protocol), mutta viestien noutamiseen lukemista varten käytetäänkin ihan eri protokollia. Tämä johtuu siitä, että aikoinaan sähköpostia luettiin vain kirjautumalla suoraan sähköpostipalvelimelle ja suorittamalla postin lukeminen paikallisesti palvelimelle. Siksi ei tarvittu muita protokollia, koska viestejä ei koskaan luettu tietoliikenneverkon avulla muualta. Nyt jo ihan tietoturvasyistä sähköpostipalvelimelle kirjautumista ei sallita, joten sähköpostien lukeminen on mahdollista vain erityisillä sähköpostin lukemiseen tarkoitetuilla sovelluksilla tai verkkoselaimen avulla. Verkkoselain käyttää WWW-palvelimen kanssa kommunikoidessaan aiemmin esiteltyä HTTP-protokollaa, minkä jälkeen WWW-palvelin yleensä toimii sähköpostiasiakkaana varsinaiselle sähköpostipalvelimelle. Sähköpostiohjelmat (kuten Thunderbird, Outlook sekä kännyköiden omat sähköpostisovellukset) kommunikoivat sähköpostipalvelimen kanssa yleensä joko IMAP- tai POP3-protokollilla. Nämä protokollat on kuvattu tarkemmin Wikipedian sivuilla: [IMAP (Internet Message Access Protocol)](https://fi.wikipedia.org/wiki/IMAP) ja vastaavasti [POP3 (Post Office Protocol version 3)](https://fi.wikipedia.org/wiki/POP3).

Sähköpostijärjestelmän eri vaiheiden protokollat käyttäytyvät eri tavalla. Lähetysvaiheessa käytettävä SMTP on niin sanottu PUSH-tyyppinen protokolla. Siinä sähköpostin lähettäjä 'työntää' tiedon sähköpostipalvelimelle ilman, että palvelin tekee aktiivisesti mitään. Aktiivinen toimija on siis postin lähettäjä. Lukuvaiheessa käytettävät protokollat IMAP ja POP3 ovat ns. PULL-tyyppisiä protokollia. Niissä  sähköpostin lukijan täytyy itse aktiivisesti ottaa yhteyttä palvelimeen ja 'vetää' sähköpostin sisältö palvelimelta itselleen. Tämä protokollien eri osapuolten aktiivisuus on myös seikka, joka palvelun ja protokollien suunnittelijoiden täytyy ottaa huomioon.

Roskapostin lähettäjät hyödyntävät vahvasti tätä sähköpostien lähettämisen PUSH-periaatetta. Ne voivat ottaa yhteyttä sähköpostipalvelimeen ja antaa sille sähköpostiviestin välitettäväksi sähköpostin vastaanottajalle. Alkuperäisessä SMTP:ssä sähköpostipalvelimen piti vastaanottaa kaikki sille annetut viestit. Nykyisin sähköpostipalvelimet suojautuvat mahdollisuuksien mukaan tällaisten asiattomien viestien välittämiseltä esimerkiksi pyrkimällä tunnistamaan viestin lähettäjän ja tarvittaessa kieltäytymällä viestin vastaanottamisesta.

## Pikaviestit

Pikaviestintä on selvästi sähköpostia uudempi tapa viestiä internetin käyttäjien kesken. Ensimmäisiä näistä oli [IRC](https://fi.wikipedia.org/wiki/IRC). Nykyisin paljon käytettyjä ovat esimerkiksi Whatsapp, Telegram, Yammer ja Slack. [Wikipedian pikaviestimiä käsittelevällä sivulla](https://fi.wikipedia.org/wiki/Pikaviestint%C3%A4) on lueteltu paljon muitakin pikaviestintäjärjestelmiä. Usein kukin järjestelmä on omalla tavallaan suljettu eli viestejä voi väittää vain kyseisen sovelluksen käyttäjien kesken.

Monet pikaviestintäjärjestelmät käyttävät sisäisesti viestien välittämiseen XMPP-protokollaa (Extensible Messaging and Presence Protocol), mutta muitakin, usein järjestelmän omia, protokollia on käytössä. XMPP on avoin protokolla, joten sen standardit on julkaistu. Niissä on varauduttu myös siihen, että XMPP:tä käyttävään järjestelmään voi erillisen yhdyskäytävän (gateway) kautta olla käyttäjiä myös muita protokollia käyttävissä järjestelmissä. Yhdyskäytävän tehtävänä on silloin tehdä tarvittavat protokollamuunnokset XMPP:n ja käyttäjän asiakasohjelman käyttämän protokollan välillä.


Emme millään pysty tutustumaan kaikkiin mahdollisiin internetin kautta saatavilla oleviin palveluihin ja niiden käyttämiin protokolliin. Tässä jäävät esimerkiksi erilaiset TV- ja videopalvelut kokonaan käsittelemättä. Jos erilaiset palvelut kiinnostavat laajemminkin, niin kannattaa itse aktiivisesti etsiä lisätietoja. Wikipediassa on yleensä ihan hyviä tiiviitä kuvauksia eri teemoista. Kannattaa lukea myös ihan perinteisiä lehtiä ja niiden artikkeleita. Suomenkielisiä lehtiä, joissa on paljon tietoliikenteeseen ja internetin palveluihin liittyviä artikkeleja ovat esimerkiksi Mikrobitti, MPC, Tekniikan maailma ja Scrolli. Lehtiä on toki paljon muitakin, mutta näitä selailen itse säännöllisesti.


## Virtuaalinen yksityisverkko


Virtuaalinen yksityisverkko (engl. virtual private network, VPN) on tapa muodostaa suojattu yhteys esimerkiksi työpaikan verkkoon silloinkin, kun käyttäjä todellisuudessa on jossain muualla. VPN-yhteyden avulla oman koneensa saa liitettyä työpaikan verkkoon siten, että koneella ovat käytettävissä ihan samat palvelut kuin työpaikallakin. Usein tietoturvan parantamiseksi organisaatiot rajoittavat palvelujen käyttöä ja näkyvyyttä siten, että ne ovat käytettävissä vain organisaation omassa verkossa.

Virtuaalinen yksityisverkko ei oikeastaan ole vain sovelluskerroksen asia, koska se vaikuttaa myös verkkokerroksen toimintaan. Käyttäjälle se on sovellus muiden joukossa ja siksi käsitellään jo tässä yhteydessä.

Esimerkiksi Helsingin yliopiston opiskelijoille ja henkilökunnalle on käytettävissä paljon enemmän palveluja yliopiston omassa verkossa kuin verkon ulkopuolella. Moni meistä on törmännyt tähän esimerkiksi tieteellisten artikkelien kanssa. Artikkeli on luettavissa ilman maksua, kun sen hakee yliopiston verkossa, mutta kun samaa artikkelia yrittää lukea kotiverkosta käsin, niin artikkelin julkaisija haluaakin maksun siitä. Tämä ero johtuu siitä, että yliopisto on jo maksanut artikkelien käyttöoikeudesta omassa verkossaan, muilta käyttäjiltä kustantaja haluaa edelleen maksun. Tällöin tilanne on helppo ratkaista muodostamalla ensin VPN-yhteys yliopiston verkkoon ja sitten hakemalla kyseinen artikkeli.

Ajatuksellisesti VPN-yhteys on siis jonkinlainen suojattu putki tai tunneli, joka johtaa omalta koneelta organisaation VPN-palvelimelle ja johon kukaan matkan varrella oleva ulkopuolinen toimija ei voi nähdä sisälle. Näin se on helppo vielä hahmottaa. Lisätään tähän vähän yksityiskohtia lisää. Putken sisällä liikenne on organisaation oman sisäisen verkon liikennettä, eli esimerkiksi www-selaimen lähettämiä pyyntöjä ja sen saamia vastauksia. Putken ulkopuolella liikenne puolestaan on julkisen internetin liikennettä. Sisäpuolella liikennöidään siis yrityksen sisäverkon IP-osoitteilla ja ulkopuolella julkisen internetin osoitteilla.

Lähettäjän sovellus lähettää viestin normaalisti ja protokollapinon eri kerroksilla siitä muodostetaan sisäverkon paketti. Koska sitä ei IP-osoitteidensa vuoksi voida suoraan lähettää julkiseen verkkoon, tämä paketti sijoitetaan ulkoverkon paketin sisään dataksi. Ulkoverkon paketti voidaan sitten lähettää VPN-palvelimelle. Palvelin avaa saamansa paketin ja ottaa sieltä tuon sisäverkon paketin, jonka se lähettää nyt sisäverkosta lopulliselle kohteelleen. Viestien paketointiin tutustutaan hiukan tarkemmin seuraavassa osiossa, jossa katsotaan muita protokollapinon kerroksia ja niiden toimintoja.

<quiz id="5c822c68244fe21455cbd3d8"></quiz>


## Yhteenveto

Tässä osiossa oli paljon asiaa, mutta se oli samalla vain pintaraapaisu.  Tutustuimme sovelluskerroksen yleisiin palveluihin, mutta jätimme tarkastelun aika yleiselle tasolle. Kaikki uudet verkkosovellukset tehdään nimenomaan sovelluskerroksen tasolla, tai jopa sen päälle. Erityisesti selaimissa toimivat palvelut siirtävät omat viestinsä HTTP-protokollan sisällä. Niillä on siis oma protokolla asiakkaan ja palvelimen väliseen viestintään ja tämä protokolla käyttää HTTP-protokollaa viestiensä siirtämiseen.

Tiedostojen siirtoon tai käyttäjien väliseen viestintään on tarjolla paljon erilaisia järjestelmiä. Tässä tutustuttiin niistä perinteisimpiin, koska ne ovat helpompia hahmottaa kuin uudemmat ja monipuolisemmat palvelut.

<quiz id="5c82321efd9fd71425c68e68"></quiz>
