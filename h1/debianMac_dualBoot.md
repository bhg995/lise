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

![Näyttökuva 2024-8-23 kello 23 30 27](https://github.com/user-attachments/assets/b40074bb-90dd-4954-a889-a856d8780942).
Näyttökuva 1. BalenaEtcher

## Mac valmistelu

Avaan levytyökalun (disk utility) ja lisään uuden osion kiintolevylle, jostain syystä tietokone herjaa kun yritän muuttaa tallennustilaa ext4 muotoon.
Käytän 50GB tallennustilaa ja MS-DOF(FAT) tallennusmuotoa. Vaihdan myöhemmin muodon kun pääsen muokkaamaan osioita Debian asennuksen yhteydessä.

![Näyttökuva 2024-8-23 kello 23 36 57](https://github.com/user-attachments/assets/47b2b0c6-874a-43fe-9875-165eca65b8bb). 
Näyttökuva 2. Levytyökalu

## Asennus

Käynnistän Mac koneen uudelleen, ja pidän alt/option näppäintä (⌥ symboli näppäimistöllä).
Hetken kuluttua saan näkyviin Macin taltion, sekä EFI boot taltion. 
Vasemmalta oikealle valitsen keskimmäisen ensin, ei tapahtu mitään.
Valitsen toisen EFI boot taltion vasemmalta laidalta.

![IMG_0324](https://github.com/user-attachments/assets/c7e48ee7-98a4-4370-b429-a1f659c0a72e).
Näyttökuva 3. Taltiot

Tietokone lataa hetken, sitten avaa käynnistyslataajan näkymän, ja valitsen ensimmäisen vaihtoehdon "Live system (amd64)"

ja hetken kuluttua Debian työpöytä tulee näkyviin.

![IMG_0328](https://github.com/user-attachments/assets/da65a3b2-d703-4737-91bc-6b3d79f3b89c).
Näyttökuva 4. Debian Live työpöytä

Tässä kohtaa olen tyytyväinen live näkymään, ja voin aloittaa varsinaisen asennuksen.

Asennustyökalussa valitsen seuraavat vaihtoehdot
Kieli: Amerikanenglanti
Sijainti: Helsinki
Näppäimistökieli (asettelu): Suomi (Macintosh)
Osiointi: Valitsen levyosion jonka tein Macin levytyökalussa, sd3 joka on ''unknown''. Tiedän sen koosta että sen on levy jota haluan käyttää. Kuva alla
Käyttäjätiedot: Täytän kaikkiin kohtiin "uhse". Aikaisemmassa asennuksessa oli häikkää salasanan kohdalla, järjestelmä pyysi salasanaa kirjautuessani vaikka en asettanut sellaista.

![IMG_0329](https://github.com/user-attachments/assets/a4aa8172-e735-4045-ba32-7f8294ff7cd9).
Näyttökuva 5. Debian asennus -osiointi.


![IMG_0330](https://github.com/user-attachments/assets/9ed74a2b-f01b-418f-bdef-1c740bc03437).
Näyttökuva 6. Debian asennus -käyttäjät.

![IMG_0331](https://github.com/user-attachments/assets/fa5282b2-d715-40d7-a15b-50ca243c6794).
Näyttökuva 7. Debian asennus -kooste (osiointi).

![IMG_0332](https://github.com/user-attachments/assets/273f7682-da74-418d-bc24-ff63779d1adc).
Näyttökuva 8. Debian asennus -virheviesti osioinnista.

![IMG_0333](https://github.com/user-attachments/assets/95034640-2b51-4d2a-9edf-3d6434176a2a).
Näyttökuva 9. Debian työpöytä. Virheviestistä huolimatta Debian toimii normaalisti, ja kaikki näyttää olevan kunnossa.

![IMG_0334](https://github.com/user-attachments/assets/a1f3fefd-a881-479e-b363-adec7a73d011).
Näyttökuva 10. Debian pääte. Tarkistetaan polku, tarkistetaan sisältö, navigoidaan kansioiden välissä sekä luodaan uusi kansio sekä tiedosto.

