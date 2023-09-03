# Hyper-V Määritykset

## Asennus

Tehtäväksi anto oli asentaa windows palvelimeen Hyper-V Manager ja luoda määritykset.
Avasin azurelabista windows palvelimen ja aloin töihin. Kun Windows palvelin oli auennut, avasin moodlesta ohjeet ja aloin töihin.

Kun palvelin oli auennut, ohjeiden ensinmäinen kohta oli "Klikkaa työpöydälläsi näkyvää kuvaketta Install hyper-V". Yllätyksekseni olin ilmeisesti edellisellä tunnilla ollut turhan innokas ja suorittanut asennuksen jo.
Sen jälkeen asennettin Hyper-V pohjainen virtuaalikytkin. Tälle annettiin nimeksi HyperVVSwitch. 

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/0e302e3f-c8bf-42e9-9c2c-f77d281e3a91)

Seuraavaksi kokeiltiin windows Powershellillä tulostaa järjestelmän verkkokortit. Minulle powershell täysin uusi asia, en ole ennen sitä käyttänyt.

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/11c931c0-b88d-410f-a935-3f6bd3ac7a69)

Powershell näytti toimivan ohjeissa toivotulla tavalla, eli voidaan jatkaa.

## Vaihe 2

Seuraavaksi määritetään virtuaaliselle verkkokortille "virtuaalireititin" IPv4-osoite.

Eli Network and Sharing Center -> vEthernet (HyperVVSwitch) status -> Properties -> Internet Protocol Version 4 (TCP/IPv4) Properties.

Määritimme IP-osoitteeksi 10.208.0.1 ja subnet maskiksi 255.255.255.0

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/8ba62209-4197-441e-93e1-ffb8a72a03ba)

Seuraavaksi luodaan Virtuaaliverkon osoitteenmuutos (NAT). Tämän pitäisi auttaa yhteyden luomisessa tulevaisuudessa asennettavien Hyper-V virtuaalikoneiden ja muun verkon välillä.

Avasimme PowerShellin adminoikeuksilla ja syötimme seuraavat komennot:
- $netNAT = "HyperVNAT"
- New-NetNat -Name $netNAT -InternalIPInterfaceAddressPrefix 10.208.0.0/24

Lopputulos oli seuraavanlainen:

![image](https://github.com/bgz859/windows-palvelimet/assets/143337738/867746f4-73ed-4f84-a9f3-3982d27137ff)

Määritimme siis verkkokortin 10.208.0.1 oletusyhdyskäytäväksi HyperV Virtuaalikoneille. NAT-määritys mahdollistaa toimivan ulospäin ja sisäänpäin kulkevan verkkoliikenteen HyperV koneiden ja ulkoverkon välillä "https://hhmoodle.haaga-helia.fi/pluginfile.php/3351688/mod_resource/content/10/1_Virtuaalikoneiden_kayttoalusta_Hyper-V_3.1.pdf".

(opettajalle, en osaa tehdä lähdeviittauksia, ainakaan täysin oikein. Otan mielelläni palautetta lähdeviittauksista. Käytin tehtävänteossa ainoastaan ohjetta, joka on yllämainittu. Merkitsin sen ylös, sillä lainasin siitä NAT-määrityksestä kertovan lauseen.)
