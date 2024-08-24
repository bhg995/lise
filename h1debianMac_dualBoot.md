# Dual boot Debian on Mac

## Tehtävänanto

a) Asenna Linux ~~virtuaalikoneeseen~~. b) Tee ja raportoi jokin yksinkertainen toimenpide haluamallasi Linux-ohjelmalla.


## Laitteisto

Tietokone: MacBook Air (13-inch, 2017)
Käyttöjärjestelmä: macOS Monterey 12.7.5
Prosessori: 1,8 GHz Kaksiytiminen Intel Core i5
Muisti: 8 Gt 1600 MHz DDR3
Näytönohjain: Intel HD Graphics 6000, 1536 Mt

USB-tikku: Scandisk 128GB USB 3

## Debian OS

Tiedosto ladattu 22.8 klo 19:45 sivulta: https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/

debian-live-12.6.0-amd64-xfce.iso

## BalenaEtcher

Käytän BalenaEtcheria kirjoittamaan Debian käyttöjärjestelmä USB-tikulle

## Mac esivalmistelu

Avaan levytyökalun (disk utility) ja lisään uuden osion kiintolevylle, jostain syystä tietokone herjaa kun yritän muuttaa tallennustilaa ext4 muotoon.
Käytän 50GB tallennustilaa ja MS-DOF(FAT) tallennusmuotoa. Vaihdan myöhemmin muodon kun pääsen muokkaamaan osioita Debian asennuksen yhteydessä.
