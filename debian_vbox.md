# Install Debian on Virtualbox

## Tehtävänanto

a) Asenna Linux virtuaalikoneeseen.
b) Tee ja raportoi jokin yksinkertainen toimenpide haluamallasi Linux-ohjelmalla.

## Laitteisto

- Tietokone: MacBook Air (13-inch, 2017)
- Käyttöjärjestelmä: macOS Monterey 12.7.5
- Prosessori: 1,8 GHz Kaksiytiminen Intel Core i5
- Muisti: 8 Gt 1600 MHz DDR3
- Näytönohjain: Intel HD Graphics 6000, 1536 Mt

## Debian OS

Seuraavat tiedostot ladattu 22.8 klo 19:45 sivulta: 
https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/
- debian-live-12.6.0-amd64-xfce.iso.packages
- debian-live-12.6.0-amd64-xfce.iso.contents
- debian-live-12.6.0-amd64-xfce.iso

## VirtualBox

![Näyttökuva 2024-8-23 kello 14 16 17](https://github.com/user-attachments/assets/ab2c11b1-f5e3-4570-9b03-886d1969b00a)

## Asennus VirtualBoxiin

Valitsen Expert mode alhaalta

![1](https://github.com/user-attachments/assets/e5edd1ee-58ad-4a45-af92-abde357c07fe)

Jatketaan seuraavilla asetuksilla:

- Base memory: 2048 MB
- CPU: 1
- Hard Disk size: 60 GB
- Luodaan VDI (VirtualBox Disk Image)

![2](https://github.com/user-attachments/assets/62933fad-1d11-4c4e-b0e1-740be5ab987e)

![3](https://github.com/user-attachments/assets/3516341d-9794-4331-97f1-861862370d08)

![4](https://github.com/user-attachments/assets/94697404-2f87-4b88-a23c-ff510a9a6dae)

Debian OS nyt näkyy listalla.

![5](https://github.com/user-attachments/assets/10da0c21-4389-49a8-8abc-49c02bf44067)


## Käynnistys 

Käynnistetään virtuaalinen käyttöjärjestelmä 23.8.2024 klo 14:40, valitsemalla Live system (amd64)


![6](https://github.com/user-attachments/assets/9aaac595-a58b-4731-b6d2-bad23fc31787)


## Virhe

Ensin ilmestyy *ERROR* Failed to send host log message

![7](https://github.com/user-attachments/assets/2f24c8ec-4b0b-4e12-8517-ba7e07e3aa42)

sitten

![8](https://github.com/user-attachments/assets/bb40e462-5d6b-482e-ad46-e2fcd46c6d11)

Sen jälkeen näyttö on tummana hetken aikaa n. 2 min. Odotan hetken, kone saattaa suorittaa jotain taustalla.


Hetken odottelun jälkeen Debian live käynnistyy, ja Debian on asennettavissa

![9](https://github.com/user-attachments/assets/0e2db746-1efd-4a31-98d5-17c8f32caa97) 

## Debianin asennus 

Asennetaan Debian täysversio VirtualBoxissa

Ensiksi tulee varoitus "Untrusted application launcher"

![10](https://github.com/user-attachments/assets/e4b40c92-2fc7-4542-bd6b-5912a6a86b41)

jatketaan painamalla "Launch Anyway", ei kovin turvallista yleensä mutta olen virtuaaliympäristössä opettelemassa virtuaalikoneiden käyttämistä. En pidä mitään arkaluonteista tietokoneella.

Sitten valitsen kieleksi Amerikan englannin.
Sijaintitieto kelloa varten valitsen Helsinki.
Näppäimistökieleksi Suomi, ja asettelu Macintosh
Osionti kohdassa tyhjennän levyn asennusta varten, ja salaan koneen salasanalla.
Käyttäjät, täytän tiedot oma nimi (uhse), ja nimeän samalla tavalla myös kirjautumisnimen sekä tietokoneen nimen, mutta jätän salasanan pois tällä kertaa.
Yhteenvedosta tarkistan asetukset ja tiedot ovat oikein.

Asennus alkaa Host-koneen mukaan 15:20 ja on valmis 15:36

![11](https://github.com/user-attachments/assets/84cf90ff-b85a-4ee3-a246-05ce2b0a8d73)

## Ensimmäinen ongelma

Asennuksen jälkeen järjestelmä pyytää kirjautumaan sisään user käyttäjään salasanalla, vaikka nimesin tietokoneen "uhse" ja jätin käyttäjäsalasanan pois.

Nopean internet haun jälkeen käy ilmi että Debian ei käytä oletussalasanaa kuten Kali tai Raspberry.

## Uudelleenkäynnistys

Sammutan Debian virtuaaliympäristön valikosta painamalla "Shutdown" ja käynnistän uudelleen

Ongelma jatkuu joten etsitään lisää tietoa. Ensimmäiseksi yritän resetoida salasanan, ohjeet löytyivät. 
https://www.quora.com/How-do-I-reset-a-forgotten-password-on-Debian. 
kohta 10. Reboot your system: "reboot". ei toimi ja järjestelmä antaa virheviestin "System has not been booted with systemd as init system (PID 1). Can't operate. Failed to connect to bus: Host is down"

Lisää hakuja, ja löydetään  Sascha John Hesse joka kirjoitti Jul 9, 2022, 9:06 PM allaolevaan sivuun kommentin josta löydän komennon CTRL+R (macissa cmd+R). 
https://learn.microsoft.com/en-us/answers/questions/920172/bash-wsl-command-not-found 

Järjestelmä käynnistyy uudelleen, mutta ongelma jatkuu vieläkin pyytää salasanaa.

Poistan Debianin VirtualBoxista ja asennan uudelleen.
Teen kaiken samalla tavalla uudelleen, paitsi tällä kertaa klikkaan "älä kysy salasanaa kirjautuessa" vaihtoehtoa, jota en huomannut aikaisemmalla kerralla. Lopputulos on sama, en pääse kirjautumaan koska salasana on väärä.


## Lähteet
- https://terokarvinen.com/linux-palvelimet/
- https://terokarvinen.com/2023/create-a-web-page-using-github/
- https://terokarvinen.com/2021/install-debian-on-virtualbox/
- https://www.quora.com/How-do-I-reset-a-forgotten-password-on-Debian
- https://askubuntu.com/questions/1335269/host-is-down-text-showing-when-entering-command-reboot
- https://unix.stackexchange.com/questions/94466/didnt-have-to-specify-a-login-name-during-installation-now-it-asks-me-for-one
- https://learn.microsoft.com/en-us/answers/questions/920172/bash-wsl-command-not-found
