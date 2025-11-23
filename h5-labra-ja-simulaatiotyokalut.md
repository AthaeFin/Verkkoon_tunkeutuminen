# Laboratorio- ja simulaatiotyökalut hyökkäyksissä
## a) Evilginx

Taas aloitetaan puuhat lukemalla käyttöohjeita https://help.evilginx.com/community/getting-started/building. 

Asensin aluksi riippuvuudet:

    apt install git
    apt install golang
    git clone https://github.com/nvm-sh/nvm.git

Ja tämän jälkeen itse Evilginx:in

    git clone https://github.com/kgretzky/evilginx2.git

Tässä kohtaa jäin jumiin asennuksen jälkeen, mutta teoriassa seuraava osa tässä: 
https://help.evilginx.com/community/getting-started/deployment/local
    
Tutkittuani enemmän vaatimuksia, huomasin, että pitäisi olla käytössä domain kalastelua varten. Joten päätin tutustua itse ohjelmaan tarkemmin,
ja katsoin Kuba Gretzkyn haastattelun EvilGrinx PRO-työkalusta. **https://www.youtube.com/watch?v=eBKq1_L_tFE**

kohdasta 14:00 eteenpäin Gretzky demoaa EvilGrinx:in käyttöä, luo halvimman mahdollisen debian-pohjaisen palvelimen. Palvelin täytyy rekisteröidä lisensointipalvelimelle (Breakthedev), jotta saa sertifikaatit,
jotta kalastelua voi tehdä. Ohjelmaa käytetään kaksivaiheisen tunnistautumisen ohjaamiseen kalastelupalvelimelle.


## b) Mininet

Asensin WMVaren, 7zip:in opettajan erikoispaketoinnin avaamista varten ja mininet-virtuaalikoneen. 

Sen jälkeen lähdin tutkimaan, olisiko Youtubessa demoa SYN flood attackin tekemisestä, ja tätä lähdin katsomaan: https://www.youtube.com/watch?v=lFpDnPGXNwk

    ryu-manager ryu.app.simple_switch_13 

Käynnistää verkko-ohjaimen... ehkä. Tässä vaiheessa olen tehnyt koko tehtävää 6h, voin todeta, että suuren vuodesohvan kokoaminen yksin on paljon helpompaa kuin tämän kanssa taistelu. Tähän jäin jumiin,
tulen palaamaan tähän paremmin nukkuneena.



## Lähteet:
- https://help.evilginx.com/community/getting-started/building
  
- https://help.evilginx.com/community/getting-started/deployment/local
  
- https://www.youtube.com/watch?v=eBKq1_L_tFE
  
- https://www.youtube.com/watch?v=lFpDnPGXNwk

