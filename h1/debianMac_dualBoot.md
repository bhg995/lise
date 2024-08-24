# Dual boot Debian on Mac

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

![IMG_0324](https://github.com/user-attachments/assets/1ee5c1c3-b5bd-4e1b-b299-4ae0d693b6d6)
Näyttökuva 3. Taltiot

Tietokone lataa hetken, sitten avaa käynnistyslataajan näkymän, ja valitsen ensimmäisen vaihtoehdon "Live system (amd64)"

ja hetken kuluttua Debian työpöytä tulee näkyviin.

![IMG_0328](https://github.com/user-attachments/assets/1a3ba1e5-dbe3-48d8-9c59-e3f176499544)
Näyttökuva 4. Debian Live työpöytä

Tässä kohtaa olen tyytyväinen live näkymään, ja voin aloittaa varsinaisen asennuksen.

Asennustyökalussa valitsen seuraavat vaihtoehdot
Kieli: Amerikanenglanti
Sijainti: Helsinki
Näppäimistökieli (asettelu): Suomi (Macintosh)
Osiointi: Valitsen levyosion jonka tein Macin levytyökalussa, sd3 joka on ''unknown''. Tiedän sen koosta että sen on levy jota haluan käyttää. Kuva alla
Käyttäjätiedot: Täytän kaikkiin kohtiin "uhse". Aikaisemmassa asennuksessa oli häikkää salasanan kohdalla, järjestelmä pyysi salasanaa kirjautuessani vaikka en asettanut sellaista.

![IMG_0329](https://github.com/user-attachments/assets/38533573-218e-4e40-b005-c8ff21ddccf5)
Näyttökuva 5. Debian asennus -osiointi.

![IMG_0330](https://github.com/user-attachments/assets/901f4388-5657-44c0-9fbf-08b93ac825b4)
Näyttökuva 6. Debian asennus -käyttäjät.

![IMG_0331](https://github.com/user-attachments/assets/e9102204-f3dd-48bc-8d23-002cd02bbdc0)
Näyttökuva 7. Debian asennus -kooste (osiointi).

![IMG_0332](https://github.com/user-attachments/assets/a651e42e-f193-467f-a2b5-a40fa15451b3)
Näyttökuva 8. Debian asennus -virheviesti osioinnista.

![IMG_0333](https://github.com/user-attachments/assets/ab564323-00ab-4974-a74e-f4085bce1932)
Näyttökuva 9. Debian työpöytä. Virheviestistä huolimatta Debian toimii normaalisti, ja kaikki näyttää olevan kunnossa.

![IMG_0334](https://github.com/user-attachments/assets/701c2728-d3d5-47e2-837a-828dcc2c6c84)
Näyttökuva 10. Debian pääte. Tarkistetaan polku, tarkistetaan sisältö, navigoidaan kansioiden välissä sekä luodaan uusi kansio sekä tiedosto.

