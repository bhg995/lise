![IMG_0332](https://github.com/user-attachments/assets/40254afe-08ae-4a70-b9f3-d27b78ebb106)![IMG_0330](https://github.com/user-attachments/assets/fa94b9e7-8107-45b1-8675-13a370a24fff)# Dual boot Debian on Mac

## Tehtävänanto

a) Asenna Linux ~~virtuaalikoneeseen~~. Tässä raportissa asennetaan Linux Debian MacOS X:n rinnalle.
b) Tee ja raportoi jokin yksinkertainen toimenpide haluamallasi Linux-ohjelmalla.


## Laitteisto

Tietokone: MacBook Air (13-inch, 2017)
Käyttöjärjestelmä: macOS Monterey 12.7.5
Prosessori: 1,8 GHz Kaksiytiminen Intel Core i5
Muisti: 8 Gt 1600 MHz DDR3
Näytönohjain: Intel HD Graphics 6000, 1536 Mt

USB-tikku: Scandisk 128GB USB 3

## OS valmistelu

Tiedosto ladattu 22.8 klo 19:45 sivulta: https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/

debian-live-12.6.0-amd64-xfce.iso

Käytän BalenaEtcheria kirjoittamaan Debian käyttöjärjestelmä USB-tikulle: https://etcher.balena.io/

![Näyttökuva 2024-8-23 kello 23 30 27](https://github.com/user-attachments/assets/b40074bb-90dd-4954-a889-a856d8780942)

Näyttökuva 1. BalenaEtcher

## Mac valmistelu

Avaan levytyökalun (disk utility) ja lisään uuden osion kiintolevylle, jostain syystä tietokone herjaa kun yritän muuttaa tallennustilaa ext4 muotoon.
Käytän 50GB tallennustilaa ja MS-DOF(FAT) tallennusmuotoa. Vaihdan myöhemmin muodon kun pääsen muokkaamaan osioita Debian asennuksen yhteydessä.

![Näyttökuva 2024-8-23 kello 23 36 57](https://github.com/user-attachments/assets/47b2b0c6-874a-43fe-9875-165eca65b8bb)

Näyttökuva 2. Levytyökalu

## Asennus

Käynnistän Mac koneen uudelleen, ja pidän alt/option näppäintä (⌥ symboli näppäimistöllä).
Hetken kuluttua saan näkyviin Macin taltion, sekä EFI boot taltion. 
Vasemmalta oikealle valitsen keskimmäisen ensin, ei tapahtu mitään.
Valitsen toisen EFI boot taltion vasemmalta laidalta.

![Näyttökuva 2024-8-24 kello 13 10 43](https://github.com/user-attachments/assets/7cb67ec7-e093-4067-ae6f-732f13d0bf5d)

Näyttökuva 3. Taltiot

Tietokone lataa hetken, sitten avaa käynnistyslataajan näkymän, ja valitsen ensimmäisen vaihtoehdon "Live system (amd64)"

ja hetken kuluttua Debian työpöytä tulee näkyviin.

![Näyttökuva 2024-8-24 kello 13 11 01](https://github.com/user-attachments/assets/1889fb31-9439-4969-addb-25f585c931b7)

Näyttökuva 4. Debian Live työpöytä

Tässä kohtaa olen tyytyväinen live näkymään, ja voin aloittaa varsinaisen asennuksen.

Asennustyökalussa valitsen seuraavat vaihtoehdot
Kieli: Amerikanenglanti
Sijainti: Helsinki
Näppäimistökieli (asettelu): Suomi (Macintosh)
Osiointi: Valitsen levyosion jonka tein Macin levytyökalussa, sd3 joka on ''unknown''. Tiedän sen koosta että sen on levy jota haluan käyttää. Kuva alla
Käyttäjätiedot: Täytän kaikkiin kohtiin "uhse". Aikaisemmassa asennuksessa oli häikkää salasanan kohdalla, järjestelmä pyysi salasanaa kirjautuessani vaikka en asettanut sellaista.

![Näyttökuva 2024-8-24 kello 13 11 14](https://github.com/user-attachments/assets/548aa362-3f76-42fa-bf3e-5343df9e3bb2)

Näyttökuva 5. Debian asennus -osiointi.

![Näyttökuva 2024-8-24 kello 13 11 26](https://github.com/user-attachments/assets/37efc19d-c0bd-440f-bfb6-bae914d2b543)

Näyttökuva 6. Debian asennus -käyttäjät.

![Näyttökuva 2024-8-24 kello 13 11 41](https://github.com/user-attachments/assets/9275d533-3954-4c38-8874-bf5eb65e8090)

Näyttökuva 7. Debian asennus -kooste (osiointi).

![Näyttökuva 2024-8-24 kello 13 11 58](https://github.com/user-attachments/assets/2d7dad99-e377-4fd7-a352-cbb47a5f94d8)

Näyttökuva 8. Debian asennus -virheviesti osioinnista.

![Näyttökuva 2024-8-24 kello 13 12 12](https://github.com/user-attachments/assets/1837f3e6-fdbb-477d-8392-a3f4216238d4)

Näyttökuva 9. Debian työpöytä. Virheviestistä huolimatta Debian toimii normaalisti, ja kaikki näyttää olevan kunnossa.

![Näyttökuva 2024-8-24 kello 13 12 25](https://github.com/user-attachments/assets/71c58137-5aa5-4cf8-9e23-884cd2d6e2e3)

Näyttökuva 10. Debian pääte. Tarkistetaan polku, tarkistetaan sisältö, navigoidaan kansioiden välissä sekä luodaan uusi kansio sekä tiedosto.

