# Tehtävä 2 

## Tehtävä 1: Hyper-V: uuden Windows Server -virtuaalikoneen luominen

Toistaiseksi kaikki tehtävät ovat olleet aika suoraviivaisia. Tehtävään annetaan ohjeet, jotka ovat ns. Step-by-step ohjeet.
Toisinsanoen, tehtävää tehdessä tulen mahdollisesti mainitsemaan useaan otteeseen, että etenen ohjeiden mukaisesti. Ongelmatilanteet ovat ne, jotka tuon esiin ja miten toimin.

Ensinmäinen vaihe on asentaa HyperV:n uusi palvelinroolissa toimiva virtuaalikone. Tämä onnistuu kaikessa yksinkertaisuudessaan painamalla Hyper-V managerin oikeasta laidasta Actions-kohdasta painamalla "new" ja "new Virtual Machine".

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/dc7f365f-4727-44ef-9f1c-85c2777ff9b5)

Tästä jatketaan ohjeiden mukaisesti. Virtuaalimallikoneelle annetaan nimeksi WindowsServerTemplate. Specify Generation kohdasta valitaan generation 1. Assign Memory kohdassa tehdään ensinmäinen isompi säätö. Alkuperäisen Startup memoryn (1024MB) sijaan annetaan kolminkertainen määrä, eli 3072MB. Lisäksi checkataan "Use Dynamic Memory for this virtual machine."

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/517744b6-4f5b-4423-990c-8c6a66b5abcd)

Connection kohdassa valitaan aikaisemmin luotu "HyperVVSwitch".

Connect Virtual Hard Disk kohdassa valitaan "Create a virtual hard disk" ja sille annetaan nimeksi "WindowsServerTemplate.vhdx. Lisäksi levyn kooksi annetaan 30GB.

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/981c036d-2a00-445a-ac30-272ad3987181)

Installation Options kohdasssa valitaan "Install an operatin system from a bootable CD/DVD-ROM" ja valitaan työpöydältä löytyvä Windows_Server.iso tiedosto.

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/6841371e-f60b-45bc-b0d4-4420d9af7f67)

Näiden kohtien jälkeen ollaan valmiita ja painetaan Finish.

Seuraavaksi muutetaan prosessoriytimien määrää. Tämä onnistuu siten, että valitaan Hyper-V Managerista "WINDOWSLABSERVERI" ja taas oikealta "Actions" kohdan alta "Settings". Tämän jälkeen aukeaa valikko, jossa näkyy eri asetuksia. Meitä kiinostaa tässä "Hardware" kohta ja tarkemmin "Processor" kohta. Tästä kohdasta muutamme ylintä kohtaa, eli "Number of virtual processors". Tähän syötetään 4. Ei muita muutoksia. Apply ja Ok.

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/511219fd-d068-4bbd-bcd1-b5f1a0fcb1c3)

Ensinmäinen vaihe on valmis.

## Tehtävä 2: Windowsin asennus

Seuraava vaihe alkaa siten, että Hyper-V managerista valitaan "Actions" kohdasta "WindowsServerTemplate" kohdan alapuolelta "Connect" ja käynnistetään virtuaalikone. Ohjeissa neuvotaan muokkaamaan ikkunan skaalausta, joka onnistuu valitsemalla virtuaalikoneen yläkulmasta "view" ja muuttamalla Zoom-level 100%.

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/49bdd22d-3aff-44bf-86fb-831a757f9d30)

Kieleksi valitaan Englanti, "Time and currency format" sekä "Keyboard or input method" Finnish. Itse vältyin ongelmatilanteetlta, mutta ohjeissa mainitaan, että jos hiirtä ei voi käyttää virtuaalikoneesa, niin virtuaalikone tulisi sammuttaa Hyper-V Managerista "Turn Off" painikkeella.

Asennus on aika yksiselitteistä. Hyväksytään "license terms". Installation type kohdassa valitaan "Custom: Install Windows only (advanced). Seuraavassa näkymässä voidaan luoda uusi levytila, mutta käytämme aikasemmin luotua 30gb levyä. 

Asetukset ovat valmiit ja itse asennus alkaa nyt. Tässä menee ohjeiden mukaan n. 10-15min.

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/6416c509-0f21-42f3-ac00-9b1e1496d0a8)

Kun asennus on valmis käynnistyy virtuaalitietokone uudelleen. Tästä en saanut kuvaa, sillä en ollut paikalla. Kun virtuaalikone on käynnistynyt uudelleen, aukeaa "Customize settings" ikkuna jossa luodaan admnistrator käyttäjälle salasana.

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/ad5ed4a3-117b-4018-ac55-b3d4a7ebe38e)

Salasanaksi annetaan "Qwerty789". Lopuksi Finish.

Kun päästään windows lukitusruutuun valitaan virtuaalikoneen Hyper-V ikkunasta "Action" ja ctrl+alt+delete. Täten voidaan syöttää aikaisemmin annettu salasana ja kirjautua admin käyttäjällä sisään.

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/9d59ac7f-a2b7-4017-ae18-429da7891a5a)

Kun kaikki on valmista, pitäisi ikkunan näyttää tältä.

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/b6d0273b-52c8-4deb-a1f8-3a51c6ac0022)

## Tehtävä 3: Server Manager: Tutustuminen palvelimen hallintanäkymään

Tässä tehtävässä tutustutaan palvelimen hallintanäkymään. Käydään läpi eri kohtia Server Managerissa. Erikseen mainitaan Dashboard näkymä

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/2b88144c-eb25-4d49-bd65-04cd8cd2a315)

Local Server näkymä

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/92ee5b2e-ada0-4a34-8a1c-018434c2da03)

Manage & Tools -valikot jotka löytyvät Server Managerin yläpalkista oikealta (sinisellä ympäröity):

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/2c9d878f-e035-4901-88b1-6c33a0c5877e)

Siinä se.

## Tehtävä 4: Mallinnus: Windows-palvelinkoneen alustus

Tässä osassa ajetaan alustus palvelinkoneelle. Tähän käytämme avuksi sysprep-työkalua joka on Windowsin sisäänrakennettu työkalu.

Aluksi avaamme virtuaalikoneella komentorivi ja valitaan "Run as Administrator" oikeaclikkaamalla Command prompt kuvaketta.

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/91741edc-1038-4bcc-a974-827d0e98c065)

Sen jälkeen syötetään komento "C:\windows\System32\sysprep\sysprep.exe /generalize /shutdown" Komento siis hakee tiedoston "sysprep.exe". En tiedä mitä "generalize" tarkoittaa, mutta oletan että shutdown sulkee virtuaalitietokoneen sysprep.exe ohjelman toimintojen jälkeen.

Kun komento on syötetty, aukeaa "System Preparation Tool" ikkuna, jossa checkataan "Generalize" (tähän ilmeisesti tarvitaan /generalize komentoa).

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/52d0fe7d-6ff4-4db1-a76c-a7238bfda375)

Tämän jälkeen painetaan Ok.

Kun Sysprep oli kesken, muistin, etten ollut tehnyt Tehtävä 2. vaihe 10/13 joka on Irroittaa asenuksess käytetty "iso" levykuva tietokoneen DVD-asemasta. Se onnistui avaamalla virtuaalikoneen (ei windowsin) yläkulmasta painamalla "Media" -> "DVD Drive" -> Eject.

Harmillisesti jouduin tehdä kaiken alusta tästä johtuen. Joudun siis poistamaan Windows serverin ja luoda asetukset uudelleen. Tästä en tee raportointia... 

Raportoin sen verran, että kun luodaan uusi Virtual hard disk, niin siinä ilmeni errori, joka ei suostunut luomaan uutta virtual hard diskiä. Tämä johtui siitä, että vanha virtual disk oli jo olemassa, niin käytän sitä. Toivon, että tämä riittää. 

Itseasiassa teen siten, että poistan vanhan virtual diskin myös, että saan täysin puhtaan asennuksen nyt 2. kerralla.

Nyt ollaan takaisin nykyhetkessä ja voidaan jatkaa. Uudelleen käynnistyksen jälkeen syötetään näppäimistön kieli ja luodaan salasana. Käytän näissä samoja arvoja, kuin aikaisemmin, eli Finnish ja "Qwerty789". Lopuksi Finish.

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/369882ea-35cb-4406-a8e6-1f96942e2ef7)

Tämän jälkeen voidaan sulkea virtuaalikone ja siirtyä tehtävään 5.

## TEHTÄVÄ 5: Mallikoneen käyttäminen useamman palvelinkoneen pohjana

Seuraavaksi tallennetaan "muottikone". Valitaan HyperV Managerin "Virtual Machines" valikosta virtuaalikoneemme oikeaclickkaamalla ja valitaan "Export...".

Locationiksi valitaan "C:\Users\Admin123456\Desktop\HyperV\. Kyseistä kansiota ei ole olemassa, mutta kirjoittamalla polun Location kohtaan, luodaan kansio automaattisesti. Lopuksi "Export". 
Voi myös tietenkin luoda kansion valmiiksi ja valita sen painamalla "browse", mutta teen tämän ohjeiden mukaan.

Seuraavaksi Mennään polkuun "C:\Users\Admin123456\Desktop\HyperV\WindowsServerTemplate\Virtual Hard Disks". Sieltä löytyy virtuaalikoneen kiintolevytiedosto. 

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/e57fbe55-00fa-4ad2-a189-4cd0a84dd43e)

Tänne kopioidaan virtuaalikovalevytiedosto "WindowsServerTemplate" kahdeksi uudeksi tiedostoksi polkuun: "C:\Users\Admin123456\Desktop\HyperV\ nimillä "WindowsServer_DC.vhdx" ja "WindowsServer_FileServer.vhdx".

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/8c357540-ead5-48d6-9ba5-41c615f51ac5)

Ja näin olemme valmiita.
