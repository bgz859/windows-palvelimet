# 3. Toimialueen ohjauspalvelin

## TEHTÄVÄ 1: Ohjauspalvelimen rungon määritys

Alkutilanne: Tarkistan, onko viimetehtävässä tehty WindowsServer_DC.vhdx tiedosto vielä tallessa.

Lähden etenemään tehtävän mukaisesti. Raportoin ongelmatilanteet ja tilanteet, jotka vaativat sitä. 
Luodaan uusi virtual machine. Nimeksi WindowsServer_DC. Muistia annetaan 3072 MB ja kytketään päälle dynaaminen muistin aallokointi. Verkkoyhteyden adapteriksi HyperVVSwitch.

Virtual Hard disk kohdassa käytetään viimeksi luotua WindowsServer_DC.vhdx levyä. Lopuksi Finish.

Kun virtuaalikone on luto mennään asetuksiin. Prosessoreja annetaan taas 4. 

## TEHTÄVÄ 2: Ohjauspavelimen määrityksiä

Connectilla virtuaalikone päälle ja Start.

Jostain syystä en aluksi saanut yhteyttä. Piti painaa restart connection ja virtuaalikone käynnistyi normaalisti. Omituista.

Mielestäni olin alustanut virtuaalikoneen sysprep-työkalulla, mutta seuraavia ohjeiden vaiheita minun ei tarvinnut tehdä. Toivon, että olen luonut tiedoston oikein. Tein sen kuitenkin 2. kertaa. Eli ohjeissa määritetään alkuasetukset, kuten näppäimistön kieli yms. Mutta minulla ei ollut noita asetuksia ollenkaan, kirjauduin suoraan sisään tietokoneelle.

Seuraava osio on minulle IP-osoitteen määritys. Avataan Command prompt ja syötetään "ipconfig /all" komento.

Sieltä otetaan talteen IPv4 Address, Subnet Mask ja Default Gateway.

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/abae81ae-0d63-4fa6-bf77-953151da6d52)

Minulla ne ovat seuraavat: IPv4 Address: 169.254.234.209 Subnet Mask: 255.255.0.0 Default Gateway: on tyhjä? Toivon, että tämä ei haittaa. Nämä määritetään uudelleen manuaalisesti.

Seuraavaksi asetetaan IPv4-tietoihin uudet asetukset:

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/c15b0fa8-6905-419f-aa23-3c59007e9f59)

Ja hyväksytään painamalla Ok. Tämän jälkeen annetaan vaihtoehdoksi yes tai no. Jos valitsen Yes, voin ohittaa tehtävän 2.3. Valitsen Yes.

Seuraavaksi testataan, että verkkoyhteys toimii. Komentoriviin syötetään komento nslookup haaga-helia.fi. Onnistunut suoritus antaa seuraavanlaisen tuloksen: 

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/0862e196-b2f8-4ef4-b7f1-ea594d319ff5)

Kohdassa 2.5 N/A - Tilannekatsaus DHCP-Palvelimellasi tuottaa ongelmia, sillä en ole käyttänyt tai luontu DHCP:tä. Selvitän tätä nyt edellisistä tehtävistä ja katson, olenko missannut tehtävän. Ilmeisesti Azure Lab virtuaalikoneessa DHCP-palvelimessa pitäisi näkyä windowsserver, mutta minulla ei näy mitään. Yritän ratkaista tämän.

No tehtäviä tarkemmin luettuna kävi ilmi, ettei meillä ole DHCP määrityksiä. Eipä kertaus haitaksi ole. Jatketaan..

Seuraavaksi annetaan uusi nimi ohjauspalvelimelle. Uudeksi nimeksi annetaan Controller-Bannat. Nimi lyhennetään 15. Merkkiin, eli Controller-Bann. Jotta muutokset saadaan voimaan, käynnistetään virtuaalikone uudelleen.

Koska lukitusruudun aktivointi vie paljon aikaa, poistetaan se käytöstä. Se toimii syöttämällä hakuun "gpedit.msc" Sieltä "Do not display the lock screen" ja Enabled. Ohjeiden mukaisesti.

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/62503d10-8828-480b-8742-d7aa50877c9f)

Seuraavaksi aktivoidaan Windows. Tällä varmistetaan windowsin toimintakelpoisuus riittävän pitkäksi ajaksi kurssilla. Tähän käytetään avuksi työkalua "slmgr.vbs".

Windowsin aktivointiin ei riitä pelkkä "slmgr.vbs" komento, vaan tarvitaan muutama lisäkomento. 2. vaihtoehdosta valitsin vaihtoehto 2. joka on "slmgr /skms ***.***.***.***" Tähtien tilalle syötetään IP-osoite, jonka näkee syöttämällä "nslookup kms.core.windows.net" komennon. Komentoni siis oli "slmgr /skms 20.118.99.224"

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/be7492a2-048c-49fb-b266-cfb7a45b186c)

Tämän jälkeen syötetään komento "slmgr /ato" ja jos komennon suorittaminen onnistui, tulee seuraavanlainen ilmoitus:

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/8464479a-04db-4931-80a3-57dfd20b2a2f)

Valmis.

## TEHTÄVÄ 3: Ohjauspalvelimen palvelinohjelmisto

Windowsohjauspalvelimen palvelinohjelmistojen asennus ja varsinainen ohjauspalvelimen roolin määritys.

Taas mennään ohjeiden mukaan. Raportoin kohtia, jotka tuottavat haasteita, tai ovat uusia / tärkeitä huomioida.

Tässä kohtaa valitaan SErver Roles kohdasta "Active Directory Domain Services" ja asennetaan se. Kun asennus on valmis painetaan "close".

Seuraavaksi korotetaan virtuaalikone ohjauspalvelimen rooliin. Ohjeiden mukaisesti. Toimialueen nimeksi annetaan sukunimi.lan eli bannat.lan. Pienellä. Salasanaksi sama kuin virtuaalikoneen ylläpitäjän salasana, eli Qwerty789.

Kun kaikki ok, lopuksi Install ja tietokone käynnistyy uudelleen asennuksen valmistuttua.

## TEHTÄVÄ 4: Tutustuminen toimialueelle kirjautumiseen

Nyt voidaan kirjautua joko adminina adminkäyttäjällä, tai toimialueelle käyttäen uutta bannat.lan käyttäjää. Tapoja on 2.
BANNAT\Administrator tai Administrator@bannat.lan salasana on aikaisemmin syötetty Qwerty789.
Käytin BANNAT\Administrator tapaa. Kirjauduttua sisään näen, että active directory on nyt asennettu ja varoituskolmio kadonnut. Kaikki on siis nyt ok.
