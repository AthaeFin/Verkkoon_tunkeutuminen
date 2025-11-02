# h2: Lempiväri: Violetti
## x) Lue ja selitä:
### Pyramid of Pain
####  https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html

- Pyramidin pohjalta ylöspäin hyökkääminen ja tekniikat vaikeutuvat; hash-arvoja ja IP-osoitteita on helppo muuttaa tunnistamisen estämiseksi, mutta pyramidin kärjessä olevia hyökkääjän
  toimintatapoja ja työkaluja on vaikeampi muuttaa.
- Puolustusnäkökannalla tärkeämpää on tunnistaa hyökkääjän toimintatavat (TTP=Tactics, Techniques, Procedures), ja kulkea pyramidin huipulta alaspäin.

### Diamond Model
#### https://www.threatintel.academy/wp-content/uploads/2020/07/diamond-model.pdf

- Malli koostuu neljästä komponentista; Capability (hyökkääjän TTP, taidot), Victim (hyökkäyksen uhri), Infrastructure (fyysinen ja looginen infra, IP- ja domain-osoitteet) ja Adversary (hyökkääjä)

## a) Apache log

Asensin virtuaalikoneelle Apachen komennoilla

    sudo apt update
    sudo apt install apache2

Asennuksen jälkeen virtuaalikoneen selaimella kirjoitin osoiteriville http://localhost. Apachen oletussivu avautui.
Tämän jälkeen lähdin tutkimaan Apachen logeja:

<img width="781" height="483" alt="image" src="https://github.com/user-attachments/assets/9ed03520-36b1-46ed-8e23-89fa595336ca" />

- 127.0.0.1 localhost-osoite
- "-" kertoo, että jotakin tietoa ei ole saatavilla. Tässä tapauksessa ensimmäinen "-" kertoo, että RFC-käyttäjäidentiteetti puuttuu, ja toinen "-" kertoo käyttäjänimen puuttuvan
- päivä, kellonaika ja aikavyöhyke
- "GET /HTTP/1.1" selain pyytää palvelimelta etusivua (juurta) HTTP-protokollalla (hassua kirjoittaa protokolla kahdesti, vähän niinkuin CD-levy tai Naan-leipä)
- 200 on serverin statuskoodi takaisin selaimelle. Onnistuneet pyynnöt alkavat koodilla 2, uudelleenohjatut alkavat 3, selaimen probleemat 4, ja serverin probleemat 5.
- 3383 kertoo objektin koon
- Mozilla/5.0 X11; Linux x86_64; rv:140.0 Gecko/20100101 Firefox/140.0 -> selain, versionumero, OS joilla lähetettiin pyynmtö palvelimelle

- lähteenä käytin Apachen omaa Manua: https://httpd.apache.org/docs/2.4/logs.html

## b) nmapped

Asensin virtuaalikoneelle nmapin

    sudo apt install nmap 
    
Otin virtuaalikoneen pois verkosta komennolla

    nmcli networking off

Tämän jälkeen lähdin tutkimaan localhost:in portteja

    sudo nmap -A localhost

<img width="487" height="74" alt="image" src="https://github.com/user-attachments/assets/299326b8-5552-4c3d-96c5-0c84eaff3b57" />

Tuloste kertoo, että portti 80 on auki, ja siellä on Apache-palvelin.

## c) skriptit

<img width="738" height="177" alt="image" src="https://github.com/user-attachments/assets/da784a5c-0ab0-45bb-9d91-20eb38f8f7d5" />


kohdan b nmap-komennossa annettiin parametri -A, joka näyttää käyttöjärjestelmän ja sen version, skriptit, reitityksen (tässä tapauksessa reitti on 0 hops, koska ollaan samalla virtuaalikoneella)

Nmapin manuaalissa lukee, että -A parametri on tunkeileva, sitä saa käyttää vain omiin vehkeisiin.

https://nmap.org/book/man-misc-options.html

## d) jäljet lokissa

<img width="771" height="374" alt="image" src="https://github.com/user-attachments/assets/fe02ffa9-c067-4d4a-94c6-fb20813f468f" />

Haistelun jäljet näkyvät, Nmap Scripting Engine (NSE) sekä nmap.org/book/nse.html

Pitkästä listasta pystyy etsimään tarkentamalla esimerkiksi 

    sudo cat /var/log/apache2/access.log | grep nmap

## e) Wire Sharking

<img width="1279" height="731" alt="image" src="https://github.com/user-attachments/assets/e6b99b82-b4d1-40f4-9409-abd84958bc3c" />

Omasta mielestä jännittävää, että hakusana nmap antaa kaksi osumaa, vaikka paketteja kulki 2834. Mutta edellisestä tehtävästä muistin, että kaksi porttia oli auki, joten oletan, että vastaus lienee tässä. 

- length, pituus
- GET pyyntö palvelimelle HTTP-protokollaa käyttäen

<img width="536" height="56" alt="image" src="https://github.com/user-attachments/assets/e3f99910-2c6c-4118-9327-812a754dcb3c" />

## f) net grep

Laitoin hetkellisesti verkon päälle että paketit tulee kotiin asti

    nmcli networking on
    sudo apt install ngrep
    nmcli networking off

Jonka jälkeen katsoin h2 vinkeistä komennon

    sudo ngrep -d lo -i nmap

Ja katsoin että onpas paska ja hidas ohjelma, menen keittämään kahvia. Lapioidessa kahvinpuruja keittimeen tajusin, että eihän liikennettä voi kaapata, jos on keittämässä kahvia eikä haistelemassa portteja,
(toisinsanoen user error) ja avasin uuden terminaaliruudun jossa ajoin komennon 

    sudo nmap -A localhost

Ja johan rupesi netgreppi kirjoittamaan:

<img width="765" height="431" alt="image" src="https://github.com/user-attachments/assets/21496c4a-0c7a-476f-a4e2-f049815201cb" />

54 osumaa:

<img width="228" height="23" alt="image" src="https://github.com/user-attachments/assets/83f825a5-a885-4605-b223-fe20cbf7bc0e" />



## g) Salainen agentti

Vaihdoin selaimen näyttämään samalta, kuin tehtävän A virtuaalikoneen surffailu, paitsi Geckosta tuli Kaktus:

    sudo nmap --script args http.useragent="Mozilla/5.0 (X11; Linux x86_64; rv:140.0) Kaktus" -A localhost

## h) Pienemmät jäljet 

<img width="1244" height="211" alt="image" src="https://github.com/user-attachments/assets/df37519f-784d-4c06-ae25-1bdd0fa2c8ed" />

NSE vaihtui feikkiselaimeen apachen logeissa.

<img width="735" height="434" alt="image" src="https://github.com/user-attachments/assets/d2c674f2-f8da-4186-a56f-c96d389877e8" />

2 osumaa, paljon vähemmän kuin aiempi 54 osumaa.

## i) LoWeR ChEcK

Lähdin siis etsimään, mistä löytyy nmaplowercheck

    grep -ir "nmaplower"


<img width="721" height="36" alt="image" src="https://github.com/user-attachments/assets/70b99be8-1192-4bfb-a429-102314186d9c" />


Hakemistossa /usr/share/nmap/nselib löytyi http.lua, jossa tärppäsi haku

    sudo nano http.lua


<img width="1266" height="762" alt="Screenshot 2025-11-02 174413" src="https://github.com/user-attachments/assets/dc161dad-1bc7-49fd-8857-d6ffbff6a970" />


Joten muokkasin rivin Kaktukseksi (yllättyneet parijonoon, saatte huomioliivit ja pääsette retkelle Korkeasaareen)


<img width="1281" height="769" alt="Screenshot 2025-11-02 174523" src="https://github.com/user-attachments/assets/b6ce7440-1fcc-4f52-b141-bc85d8fcceb2" />

Ajoin uudestaan ngrepin, ja tuloksena 0 osumaa

<img width="249" height="41" alt="image" src="https://github.com/user-attachments/assets/2a2ce39c-db72-4420-b4ee-b0965cbf0dde" />

## ajankäyttö

Arvioin käyttäneeni aikaa n. 7 tuntia mukaanlukien raportin teko, kahvinkeittimeen unohtunut kahvi, jonka join sitten kylmänä.

## Lähteet:

https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h2-lempivari-violetti T.Karvinen: tehtävänanto, luettu 2.11.2025

https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html D.Bianco: Pyramid of Pain, luettu 2.11.2025

https://www.threatintel.academy/wp-content/uploads/2020/07/diamond-model.pdf C.Betz, S.Caltagirone, A.Pendercast: Diamond Model, luettu 2.11.2025

https://httpd.apache.org/docs/2.4/logs.html Apachen käyttöohjeet, luettu 2.11.2025

https://nmap.org/book/man-misc-options.html Nmap käyttöohjeet, luettu 2.11.2025



















  
