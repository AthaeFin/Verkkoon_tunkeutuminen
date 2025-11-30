# NFC ja RFID

## 1. Tarkastele käytössäsi olevia RFID tuotteita, mieti miten hyvin olet suojautunut RFID urkinnalta?

Käytössäni on aika paljon RFID-tuotteita, esim. kotiavaimet, puhelin, älykello, pankkikortti. En ole suojautunut RFID-urkinnalta normaalia kansalaista enempää, tosin lähimaksun tultua itseä hirvitti
että nyt joku tulee lähelle ja vie rahat tililtä. Ei ole vielä vienyt, mutta silti tiukat päiväkohtaiset rajat olen omaan pankkikorttiini laittanut. Nykyään harvemmin kannan kortteja mukana, olen liittänyt pankkikortin
apple-walletiin joka haluaa nähdä naamani joka kerta kun jotain maksan.

## 2. Tutustu APDU komentojen rakenteeseen.

https://www.cardlogix.com/glossary/apdu-application-protocol-data-unit-smart-card/

APDU toimii niin, että päätelaite lähettää komennon ja kortti vastaa siihen. 
Komennon rakenne muodostuu neljästä tavusta otsikkoa (header) ja valinnaista sisältöä (body).

Otsikossa ohjekentät:
- CLA = tyyppi
- INS = mitä komento haluaa tehtävän
- P1-P2 = em. komennon parametrit

Sisällössä kentät: 
- Lc = määrittää datakentään koon tavuina (max. 255)
- Command Data = dataa (ylläri)
- Le = vastauksen koko tavuina

Vastaus koostuu sisällöstä ja lopusta (trailer). Lopun kaksi tavua kertoo annetun komennon tilan, esim. 90 00 = toteutunut.

## 3. Tutki ja kerro minkä mielenkiintoisen RFID hakkerointi uutiset löysit.

https://www.atlantanewsfirst.com/2025/11/25/new-ghost-tapping-scam-targets-holiday-shoppers-using-contactless-payments/

No okei ehkä mun foliohattu rapisi vuosia sitten ihan aiheesta :D 

Uutisessa kerrotaan, että taskuvarkaat ei mene enää taskuille vaan käyttää hyväkseen korttien lähimaksuominaisuutta. 







