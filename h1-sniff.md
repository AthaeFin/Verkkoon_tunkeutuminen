# h1-Sniff
## x) Lue ja tiivistä
- Wiresharkin asennuksessa oleellista on sallia ei-root käyttäjät, ja lisätä käyttäjä wireshark-ryhmään. 
- Wiresharkin kaappaamaa liikennettä voi tallentaa, ja tutkia myöhemmin.
- Linuxin käyttämät liitäntöjen lyhenteet en - wired Ethernet, wl - wireless, lo - loopback adapter
- ip a -komento kertoo oman IP-osoitteen

## a) Debianin asennus

Omalla läppärilläni oli jo Debian 13 asennettuna, mutta aikaavievien mutkien kautta ajauduin pistämään Debianin virtuaalipurkkiin pöytäkoneelle.

Mutka 1. Rootin salasana on hukassa -> youtube auki ja katsomaan, kuinka saan oman läppärini korkattua, että ei tarvitse asentaa Debiania siihen uudestaan. 
Rootin salasana vaihtuu, kun painaa GRUB-valikossa "e",
ja kirjoittaa avautuvaan tekstipätkään "no quiet" -kohdan jälkeen " rw init=/bin/bash. 

    mount | grep -w /
    passwd

jonka jälkeen reboot pitäisi toimia.

Mutka 2. Liian hätäinen Wiresharkin asennus. Uudenkarheilla root-oikeuksilla lähdin soitellen asentamaan Wiresharkia, ja en antanut non-root -oikeuksia, jolloin Wireshark ei löytänyt mitään liikennettä.
Tässä vaiheessa olin nälkäinen, kiukkuinen ja sen myötä luovutin, ja siirryin keittiöstä olohuoneeseen ison tietokoneen kimppuun, latasin ISO-imagen ja laitoin VirtualBoxin tulille.
Sillä aikaa, kun virtuaalikone heräili henkiin, pizza saapui kotiovelle. Tutkin tätä Wireshark -asiaa myöhemmin, oletan, että kokonaan ohjelman purge läppäriltä toimii. Jos ei toimi, pitää tutkia paremmalla ajalla.

## b) Kalastus kielletty

<img width="564" height="270" alt="kalastusluvatkunnossa" src="https://github.com/user-attachments/assets/149f677b-43a8-453f-99e4-275e9af93661" />

terminaalissa voi katkaista ja käynnistää yhteyden komennoilla

    nmcli networking off
    nmcli networking on

## c,d) Wireshark, TCP/IP-protokollapino

<img width="1282" height="802" alt="pino" src="https://github.com/user-attachments/assets/f4d99bd9-ce19-498a-a9c2-d9e65c3be784" />

- sovelluskerros (application layer) TLS
- kuljetuskerros (transport layer) TCP
- verkkokerros (network layer) IPv4
- siirtoyhteyskerros (link layer) Ethernet II

## e) surfing-secure.pcap

 - viimeisen paketin 283 kohdalla aika näyttää 7,5 joten oletan kaappauksen kestoksi 7,5 sekuntia.
 - Protokollia on TCP, TLS, ARP (missä on x, kerro osoitteeseen y), DNS

   <img width="794" height="498" alt="laitteetjaportit" src="https://github.com/user-attachments/assets/3b6ee034-884f-454d-8c66-51dc97be262e" />

   kätevä listaus ipv4-osoitteista

## g) surffailijan NIC

Jäänee mysteeriksi, koska internet ei kerro, löytyykö vastaus Wiresharkista (itse en löytänyt mistään link layer -kerrokselta, vain MAC-osoite). MAC-osoitteen avulla voi tietää valmistajan ja merkin, vai voiko? 

<img width="980" height="561" alt="revin_hiukset_irti" src="https://github.com/user-attachments/assets/905905ce-0126-45c2-a316-ca1926242b68" />

## h) missä ollaan surffailtu

Kuten edellä mainitsin, liikennettä on google.com ja terokarvinen.com, vuohilaskuri (varmaan kävijälaskuri tjsp)

<img width="638" height="261" alt="image" src="https://github.com/user-attachments/assets/b12a76b8-f369-4766-8bf8-de7294c3fc94" />


## i) analysoi omaa liikennettä


<img width="1027" height="614" alt="tukkairti" src="https://github.com/user-attachments/assets/cad09fd2-1add-4781-a3c1-c0b1625798ea" />

<img width="755" height="129" alt="image" src="https://github.com/user-attachments/assets/6a8e93f5-f9a8-4602-8126-be674b17c060" />

DNS on Domain Name System, suomalaisittain nimipalvelujärjestelmä.
1. rivillä kysyn verkkotunnuksesta en.wikipedia.org

2. ja 5. rivillä kysyn DNS:ltä wikipedian IPv4-osoitetta
   
3. rivillä kysyn IPv6-osoitetta
   
4. rivillä DNS vastaa kyselyyn verkkotunnuksesta, CNAME on vaihtoehtoinen nimi, vähän niinkuin Tero Karvinen = Karvinen, Tero
   
6 ja 8. rivillä DNS vastaa CNAME ja IPv4-osoitteella kyselyyni
   
7. rivillä DNS vastaa CNAME ja IPv6-osoitteella kyselyyni


## Lähteet

https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h1-sniff tehtävä, T.Karvinen, luettu 26.10.2025

https://terokarvinen.com/network-interface-linux/ T.Karvinen, luettu 26.10.2025, x) tiivistelmä

https://terokarvinen.com/wireshark-getting-started/ T.Karvinen, luettu 26.10.2025, x) tiivistelmä

https://www.youtube.com/watch?v=LnRt-4rodtQ Linuxhelp, how to change root password from boot on Debian 11.3, katsottu 22.10.2025 a) debianin asennus

## ajankäyttö

yhteensä 9h, mukaanlukien mutkat matkassa, pizzan syöminen, dokumentointi.
    
