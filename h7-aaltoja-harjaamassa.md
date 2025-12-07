# Aaltoja harjaamassa

Alkusanoina kerron, että olen päntännyt viimeisen viikon Ciscon tietoverkkojen kokeisiin (kyllä, kaksi kappaletta samana päivänä), ja tämän tehtävän tekeminen ajoittuu hetkeen, jolloin tekisi mieli vaan heittää läppäri
ja pöytäkone parvekkeelta alas ettei ikinä tarvitse ajatella verkkovehkeitä ja miten ne toimii. Teen tehtävää niin pitkälle kuin silmät pysyy auki.

Jollakin toisella samat fiilikset Ciscon vehkeistä (Twitchin chatti on kyllä välillä viihdyttävä):

<img width="1162" height="181" alt="image" src="https://github.com/user-attachments/assets/eaf33662-e39b-439b-b06a-465da0fa56e7" />


## x) Tiivistä

### Hubacek 2019: Universal Radio Hacker SDR Tutorial on 433 MHz radio plugs
https://www.youtube.com/watch?v=sbqMqb6FVMY&t=199s

- Videolla käydään läpi signaalin analysointia ja tallentamista, Hubmartin kertoo, että analysoitavaa signaalia ei kannata valita aivan keskeltä vaan sivusta.
- Parametrit pitää katsoa kuntoon; oikea modulaatio, bittien pituus täsmää suurinpiirtein kaapattuun signaaliin.

### Cornelius 2022: Decode 433.92 MHz weather station data
https://www.onetransistor.eu/2022/01/decode-433mhz-ask-signal.html

- Samaa asiaa mitä videolla, enemmällä pohdinnalla.
- https://triq.org/explorer/ -tietokanta rtl_433 lähdekoodille

## a) WebSDR

Valitsin pitkältä listalta (http://websdr.org/) Northern Utah WebSDR:n ja pääsin takaisin 90-luvulle:


<img width="1896" height="781" alt="image" src="https://github.com/user-attachments/assets/f7012b8f-d79d-4e1c-8579-5e205360a9cb" />


Rullaamalla alaspäin tulee vesiputousnäkymä ja heti suoraan sain signaalin (mitään säätämättä) missä miehet keskustelee säästä, Pearl Harborista, lukuja ja armeija-aakkosia (pelaavat varmaan shakkia). 
Vaihdoin taajuutta (ja haarukkaa) ja löysin keskustelukanavan, missä miehellä on paksu aksentti (lapsi kysyy että miksi nauran kun mies sanoo hwai (miksi)). Sitten löysin Meksikolaisen kanavan, keskustelevat ihmisistä, musiikista,
Los Angelesista ja ilmeisesti ollaan jossain tapahtumassa, koska taustalla kuuluu hälinää. 


<img width="1183" height="881" alt="image" src="https://github.com/user-attachments/assets/49c86cf9-c17b-4650-95e3-72baea432ae5" />

## b) rtl_433

Vinkeistä katsoin, että ensin pitää asentaa oheiskamat:


    sudo apt-get -y install atool wget libssl-dev libtool libusb-1.0-0-dev librtlsdr-dev rtl-sdr libsoapysdr-dev


<img width="806" height="109" alt="image" src="https://github.com/user-attachments/assets/1b07d236-c174-4107-b655-f1757d41df1d" />


Seuraavaksi hakea githubista tuorein paketti:


    wget https://github.com/merbanan/rtl_433/releases/download/25.02/rtl_433-soapysdr-openssl3-Linux-amd64-25.02.zip


<img width="802" height="125" alt="image" src="https://github.com/user-attachments/assets/f9da1024-ebc5-4c1b-a477-c48aa3ce346c" />

Paketti auki:


    aunpack rtl*.zip


<img width="803" height="71" alt="image" src="https://github.com/user-attachments/assets/ab1e973b-5846-4393-8e5f-2befd1f4ea5b" />


Lopuksi katsotaan menikö kaikki oikein (näemmä meni)


<img width="802" height="86" alt="image" src="https://github.com/user-attachments/assets/abaeb312-589f-4421-90ed-feca6465fe6e" />

## c) Automaattinen analyysi

Tässä kohtaa jäin jumiin ja kävin katsomassa edellisen toteutuksen läpipeluuohjeen: https://github.com/nurminenkasper/Verkkoon-tunkeutuminen-ja-tiedustelu/blob/main/h3/h3-Aaltoja-harjaamassa.md

wgetillä pitää hakea Tero Karvisen sivuilta näyte, 


    wget https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/samples/Converted_433.92M_2000k.cs8
    

<img width="801" height="234" alt="image" src="https://github.com/user-attachments/assets/9b2ffed7-757f-4628-a7c5-38ca70797a6a" />


    ./rtl_433 -r Converted_433.92M_2000k.cs8


<img width="798" height="444" alt="image" src="https://github.com/user-attachments/assets/abdacc0b-5e3d-40a8-807f-ee246f59a6c3" />

Syötteessä kolme eri lähdettä; Nexa-Security, KlikaanKlikUit-Switch, Proove-Security (joka oikeasti on yksi kaukosäädin, koska id/housecode on sama ja aikaleima tasan sama).

... Tässä kohtaa on se hetki kun silmät tuntuu todella raskailta, jatkan tätä myöhemmin (kokeiden jälkeen)


## ajankäyttö

4h (päivitän myöhemmin)

## lähteet:

- https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h7-aaltoja-harjaamassa T.Karvinen, läksyt

- https://www.youtube.com/watch?v=sbqMqb6FVMY&t=199s Hubacek 2019: Universal Radio Hacker SDR Tutorial on 433 MHz radio plugs

- https://www.onetransistor.eu/2022/01/decode-433mhz-ask-signal.html Cornelius 2022: Decode 433.92 MHz weather station data

- http://websdr.org/ WebSDR-kanavat

- http://websdr1.sdrutah.org:8901/index1a.html N.Utah WebSDR

- https://github.com/nurminenkasper/Verkkoon-tunkeutuminen-ja-tiedustelu/blob/main/h3/h3-Aaltoja-harjaamassa.md K. Nurminen 2025, Aaltoja Harjaamassa

  













  


