# Dual boot Debian on Mac

## Debian OS Asennus USB-tikulla



## Laitteisto

- **USB-tikku: Scandisk 128GB USB 3**
- **Tietokone: MacBook Air (13-inch, 2017)**
- Käyttöjärjestelmä: macOS Monterey 12.7.5
- Prosessori: 1,8 GHz Kaksiytiminen Intel Core i5
- Muisti: 8 Gt 1600 MHz DDR3
- Näytönohjain: Intel HD Graphics 6000, 1536 Mt



## OS valmistelu

### Debian Live ISO

.iso tiedosto näkyy nimellä [debian-live-12.6.0-amd64-xfce.iso](https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid). [1]

Linkki vie kansioon, joka sisältää Debian GNU/Linux käyttöjärjestelmätiedostoja. 

_'These are files containing live images for the Debian GNU/Linux operating system. They are specifically for the amd64 architecture. There are multiple different files here, corresponding to the different desktop environments.'_ [1]


### BalenaEtcher

Käytän [BalenaEtcher](https://etcher.balena.io) ohjelmaa kirjoittamaan Debian [.iso](https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/debian-live-12.6.0-amd64-xfce.iso) kuva USB-muistiin. [2]

![Näyttökuva 2024-8-23 kello 23 30 27](https://github.com/user-attachments/assets/b40074bb-90dd-4954-a889-a856d8780942)

<sub>Näyttökuva 1. BalenaEtcher kirjoittamassa USB-muistiin, _flashing_.</sub>


## Mac valmistelu

Avaan levytyökalun (disk utility) ja lisään uuden osion kiintolevylle. Käytän 50GB tallennustilaa ja MS-DOS(FAT) tallennusmuotoa, tällä hetkellä levytyökalu suostuu vain siihen. Vaihdan myöhemmin muodon, kun pääsen muokkaamaan osioita Debian asennuksen yhteydessä sopivaksi muodoksi, ext4.

![Näyttökuva 2024-8-23 kello 23 36 57](https://github.com/user-attachments/assets/47b2b0c6-874a-43fe-9875-165eca65b8bb)

<sub>Näyttökuva 2. Osiointi levytyökalulla.</sub>


## Debianin Asennus Mac tietokoneelle

- Käynnistän Mac koneen uudelleen, ja pidän alt/option näppäintä (⌥ symboli näppäimistöllä).
- Tietokone antaa järjestyksessä vaihtoehdon käynnistää käyttöjärjestelmän, joko hDd taltiolta OS X:n, USB-tikulta Debian 12 tai aikaisemman luodun MS-DOS(FAT) taltiolta, joka on tyhjä.
- Valitaan USB-tikun Debian 12

![Näyttökuva 2024-8-24 kello 13 10 43](https://github.com/user-attachments/assets/7cb67ec7-e093-4067-ae6f-732f13d0bf5d)

<sub>Näyttökuva 3. Taltiot</sub>

Käynnistyslataajan näkymä tulee esiin, valitsen "Live system (amd64)", joka avaa Debian Live työpöydän näkymän.

![Näyttökuva 2024-8-24 kello 13 11 01](https://github.com/user-attachments/assets/1889fb31-9439-4969-addb-25f585c931b7)

<sub>Näyttökuva 4. Debian Live työpöytänäkymä</sub>

Tässä kohtaa olen tyytyväinen live näkymään, ja voin aloittaa varsinaisen asennuksen.

Asennustyökalussa valitsen seuraavat vaihtoehdot:
- Kieli: Amerikanenglanti
- Sijainti: Helsinki
- Näppäimistökieli (asettelu): Suomi (Macintosh)
- Osiointi: Valitsen levyosion jonka tein Macin levytyökalussa, sd3 joka on 'unknown'. Tiedän sen koosta että sen on levy jota haluan käyttää.
- Käyttäjätiedot: Täytän kaikkiin kohtiin "uhse". VirtualBox asennuksessa, Debian pyysi salasanaa kirjautuessani vaikka en asettanut sellaista.

![Näyttökuva 2024-8-24 kello 13 11 14](https://github.com/user-attachments/assets/548aa362-3f76-42fa-bf3e-5343df9e3bb2)

<sub>Näyttökuva 5. Debian asennus -osiointi.</sub>

![Näyttökuva 2024-8-24 kello 13 11 26](https://github.com/user-attachments/assets/37efc19d-c0bd-440f-bfb6-bae914d2b543)

<sub>Näyttökuva 6. Debian asennus -käyttäjät.</sub>

Asennuksen koosteesta näkyy tarkempi tieto osioinnista.

![Näyttökuva 2024-8-24 kello 13 11 41](https://github.com/user-attachments/assets/9275d533-3954-4c38-8874-bf5eb65e8090)

<sub>Näyttökuva 7. Debian asennus -kooste (osiointi).</sub>

Virheviesti tulee vastaan 'EFI file system creation failed'. Painan continue.

![Näyttökuva 2024-8-24 kello 13 11 58](https://github.com/user-attachments/assets/2d7dad99-e377-4fd7-a352-cbb47a5f94d8)

<sub>Näyttökuva 8. Debian asennus -virheviesti osioinnista.</sub>

Virheviestistä huolimatta Debian toimii normaalisti, kaikki näyttää olevan päältä päin kunnossa.

![Näyttökuva 2024-8-24 kello 13 12 12](https://github.com/user-attachments/assets/1837f3e6-fdbb-477d-8392-a3f4216238d4)

<sub>Näyttökuva 9. Debian työpöytä.</sub>


Tarkistetaan nykyyisen kansion polku ja sisältö, navigoidaan kansioiden välissä ja luodaan uusi kansio sekä tiedosto.

![Näyttökuva 2024-8-24 kello 13 12 25](https://github.com/user-attachments/assets/71c58137-5aa5-4cf8-9e23-884cd2d6e2e3)

<sub>Näyttökuva 10. Debian pääte.</sub>

## Lähteet

**1. Debian ISO**
Debian 2024. Index of /debian-cd/current-live/amd64/iso-hybrid/. _https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid_. filename: debian-live-12.6.0-amd64-xfce.iso, last modified: 2024-06-29 11:06. Luettu & Ladattu 22.8.2024 

**2. BalenaEtcher**
BalenaEtcher 2024. Flash images to SD cards & USB drives. _https://etcher.balena.io_. filename: balenaEtcher-1.19.21-arm64.dmg, last modified: 2024-05-30. Ladattu 18.7.2024
**3.**
**4.**

  **terokarvinen.com, Tero Karvinen**
_https://terokarvinen.com/_ Luettu 21.8.2024
_https://terokarvinen.com/2023/create-a-web-page-using-github/_. Luettu 21.8.2024
_https://terokarvinen.com/2021/install-debian-on-virtualbox/_. Luettu 21.8.2024
