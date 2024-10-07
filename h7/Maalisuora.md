# Ohjelmointi

"_Python on ohjelmointikieli, jolle on tunnusomaista hyvä luettavuus, korkea abstraktiotaso ja kehittyneet kirjastot monilla eri sovellusalueilla. Python on niin kutsuttu tulkattu kieli, mikä tarkoittaa että sen suorituskyky on alhaisempi kuin käännetyn kielen._" [1]

"_Java on Java (ohjelmointikieli) on yleiskäyttöinen ohjelmointikieli, jonka avulla ohjelmoijat voivat kirjoittaa koodia, joka kääntäessä toimii kaikilla Javaa tukevilla alustoilla ilman tarvetta kääntää koodia uudelleen._" [2]

"_C on yleiskäyttöinen, imperatiivinen ja rakenteinen käännettävä tietokoneiden ohjelmointikieli._" [3]

## Laitteisto

- **Tietokone: MacBook Air (13-inch, 2017) INTEL**
    - Käyttöjärjestelmä: macOS Monterey 12.7.5
    - Prosessori: 1,8 GHz Kaksiytiminen Intel Core i5
    - Muisti: 8 Gt 1600 MHz DDR3
    - Näytönohjain: Intel HD Graphics 6000, 1536 Mt

- **Virtuaalikone: VirtualBox Version 7.1.2 r164945 (Qt6.5.3)**
- **Ympäristö: Linux Debian 12 (cinnamon)**
    - DigitalOcean VPS, @nialo
    - Käyttöjärjestelmä: Debian 12, arm64

## a) Kirjoita ja aja "Hei maailma" kolmella kielellä. su 6.10.2024

tämä osio klo 18:20 - 19:00

Javan lataus:

    sudo apt-get install default-jre
    sudo apt-get install default-jdk

Hyödynsin opettajan sivuilla olevia ohjeita.

Ensin Java kielellä

![kello 18 38 30_javaCode](https://github.com/user-attachments/assets/b6969e0e-b655-4b0b-8d1e-f333cae238ff)

Testi:

![18 39 18_helloWorldJavalla](https://github.com/user-attachments/assets/fd175348-9bf0-4002-a397-4cddf37ae2d7)

Sitten C:llä

![18 44 59_cCode](https://github.com/user-attachments/assets/b06b0341-886d-4f09-8447-42ef7b34ce69)

Testi:

![18 50 26_helloWorldClla](https://github.com/user-attachments/assets/b6a0aaa6-8366-43f1-96ed-c301184e90e5)

C kieli oli täysin vieras kieli minulle, hieman kompuroin ennenkuin sain tervehdyksen toimimaan. Tiedoston nimessä oli häikkää. Vaihdoin tiedostonnimen `mv`-komennolla.

Viimeiseksi Pythonilla

![19 01 19_pythonCode](https://github.com/user-attachments/assets/f6724f06-e81f-4a26-9837-9fc4c3a3f030)

Pythonissa kirjoitin koodin niin, että ohjelma kysyy käyttäjältä vaihtoehtoja 1 tai 2. Käyttäjän valinnan jälkeen ohjelma tervehtii joko 1: suomeksi tai 2: englanniksi.

Testi:

![19 01 58_HelloWorldPythonilla](https://github.com/user-attachments/assets/67c505b1-25eb-43d8-896d-b6252548d0c1)

[4]

## b) Laita Linuxiin uusi komento niin, että kaikki käyttäjät voivat ajaa sitä.

Tämä osio klo 19:30 - 20:30

Testiä varten tein uuden käyttäjän `galileo`. Tämä käyttäjä ei kuulunut `sudo` ryhmään eikä `adm` ryhmään.

![18 21 08_listUsers](https://github.com/user-attachments/assets/d1f1c529-e8ee-426f-b974-ea744f9c2b27)

Käytin apuna opettajan sekä kurssin käyneen opiskelijan materiaaleja. [5][6]

Ensiksi tein muutoksen tekemääni `.py` tiedostoon, lisäämällä alkuun `#!/urs/bin/python3`. Näin terminaali voi tulkita koodipätkän komennoksi.

![19 04 04_pythonKomennoksi](https://github.com/user-attachments/assets/767b74f0-3462-413e-a79a-c324d1da6d85)

Ensin muutin tiedoston bash komennoksi `hei.py` -> `hei.sh`

Lisäsin tiedostoon ajo-oikeudet kaikille käyttäjille `chmod +x hei.sh`, testasin `./hei.sh`

![19 05 58_komentoPython](https://github.com/user-attachments/assets/ff2ba8f7-de49-46f0-afe0-54d3291dfe61)

Tämän jälkeen kopioin sen pääkäyttäjänä kansioon /usr/local/bin/, unohdin että pitää sudottaa.

![19 25 57_bashKomennoksi](https://github.com/user-attachments/assets/93486179-535a-463c-8b34-60062ed8809d)

Kirjauduin ulos `leonardo`-käyttäjänä, ja kirjauduin testiä varten tekemääni `galileo`-käyttäjänä.

Testi: `galileo`

![19 30 46_kokeilua](https://github.com/user-attachments/assets/6d1622af-cc81-4248-b22b-c2484804241b)

Testi: `immanuel`

![20 30 30_kokeilua_immanuel](https://github.com/user-attachments/assets/cd4bc8ff-75ca-449b-bc81-2a27fe6b593e)


Komento `hei.sh` toimii nyt eri käyttäjillä.

## c) Ratkaise vanha arvioitava laboratorioharjoitus soveltuvin osin. 

### Rinnakkaisarvioinnissa huomasin että tässä tehtävässä tein vain yhden tehtävän, harjoituksen kokonaisuudesta. Päätin että jatkan labraharjoituksia, ja lisään ne raporttiini ennen tehtävän deadlinea.

### Laboratorioharjoitus [Final Lab for Linux Palvelimet 2024 Spring](https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-linux-palvelimet/)

Tämä osio 20:30 - 21.20

Teen harjoituksen käyttäjänä `leonardo`, ja testaan sitä käyttäjällä `immanuel`

Valitsin edellisen toteutuksen labraharjoituksen osan:

"_c) Ei kolmea sekoseiskaa_"

    Suojaa raportti Linux-oikeuksilla niin, että vain oma käyttäjäsi pystyy katselemaan raporttia

Tein tiedoston `salaista.txt`, ja kirjoitin sisältöä siihen.

Tämän jälkeen muutin tiedoston oikeuksia `chmod 600 salaista.txt`, joka antaa käyttäjälle `leonardo` oikeudet lukea ja kirjoittaa mutta ei ajaa(execute). Muille käyttäjille ei ole oikeuksia lainkaan.

![20 50 39_salaiseksi](https://github.com/user-attachments/assets/110ea56d-1141-4158-ae64-63125b995b0f)

Kokeilin, `immanuel`-käyttäjänä tarkistella `leonardo`:n kansiota

![Näyttökuva 2024-10-6 kello 21 08 25](https://github.com/user-attachments/assets/1306e66b-6827-4cc0-aa46-174e31de2302)

Kokeilin päästä `leonardo`-käyttäjän kansioon, ja järjestelmä ilmoitti että ei ollut siihen oikeuksia. Vaihdoin käyttäjän `leonardo`-kansion oikeuksia niin, että muilla käyttäjillä on vain luku oikeus, kun taas `leonardo`-käyttäjällä on täydet oikeudet.

Komento on `chmod 744 /home/leonardo`

Tarkistin tiedoston ja kansion oikeudet komennolla `ls -l`

![21 03 39_oikeudet](https://github.com/user-attachments/assets/fd4bc445-c2bd-469f-9b2b-696f242a80c3)

Seuraavaksi kirjauduin käyttäjällä `immanuel` ja kokeilin päästä käsiksi tiedostoon.

![Näyttökuva 2024-10-6 kello 21 16 56](https://github.com/user-attachments/assets/756c22a8-5969-4944-80bf-2c05166a0822)

Järjestelmä antoi vastaukseksi `permission denied` kun yritin avata `immanuel`-käyttäjällä `leonardo`-käyttäjän tiedostoa. Katsoin vielä `leonardo`-käyttäjän kansiota, johon muillakin oli lukuoikeus, järjestelmä kertoi vielä että tiedostoihin ja kansioihin ei ole pääsyä.

[7]

### Seuraavat on suoritettu SSH- yhteyttä käyttäen. Mac tietokoneelta SSH-yhteydellä virtuaalipalvelimen Debian käyttöjärjestelmään

"_d) 'howdy'_"

- Tee kaikkien käyttäjien käyttöön komento 'howdy'
  - Tulosta haluamaasi ajankohtaista tietoa, esim päivämäärä, koneen osoite tms
  - Pelkkä "hei maailma" ei riitä
- Komennon tulee toimia kaikilla käyttäjillä työhakemistosta riippumatta

Tässä tehtävässä hyödynsin omaa raporttiani samanlaisesta [tehtävästä](https://github.com/bhg995/lise/edit/main/h7/Maalisuora.md#b-laita-linuxiin-uusi-komento-niin-ett%C3%A4-kaikki-k%C3%A4ytt%C3%A4j%C3%A4t-voivat-ajaa-sit%C3%A4). 

Päätin tehdä `howdy`-nimisen Python-komennon, joka käyttää Caesarin salakirjoitusmenetelmää. [8]

![0 49 45_howdyKOMENTO](https://github.com/user-attachments/assets/daff511a-4ce2-4047-82de-3cff699b90f8)

Tein tarvittavat toimet. `chmod a+x howdy`, joka antoi oikeuden kaikille ajaa komennon. `sudo cp howdy /usr/local/bin`, joka kopioi komennon kansioon, jotta kaikki voivat ajaa komentoa.

Ohjelma kysyy ensin salataanko vai puretaanko viestiä, pyytää viestin, pyytää kuinka monta siirtoa tehdään. Tämän jälkeen ohjelma tulostaa joko salatun tai puretun viestin.

![0 46 14_howdyKomento](https://github.com/user-attachments/assets/fb05835f-5b5e-4fd1-996f-f6b4f1be4b8d)

Komento toimii, komento salaa viestin Ceaserin salakirjoitusmenetelmällä.

![0 51 11_howdyKaytto](https://github.com/user-attachments/assets/fba27992-9c5d-4537-9bfb-e7090936eb97)

"_e) Etusivu uusiksi_"

- Asenna Apache-weppipalvelin
- Tee yrityksellemme "AI Kakone" kotisivu
- Kotisivu tulee näkyä koneesi IP-osoitteella suoraan etusivulla
- Sivua pitää päästä muokkaamaan normaalin käyttäjän oikeuksin (ilman sudoa). Liitä raporttiisi listaus tarvittavien tiedostojen ja kansioiden oikeuksista.

- Asenna Apache-weppipalvelin
  Tietokoneen valmistelu

        sudo apt-get update && sudo apt-get upgrade && sudo apt-get dist-upgrade -y
        sudo apt-get install ufw
        sudo apt enable ufw
    
    Apachen asennus & käynnistys:

        sudo apt-get install apache2
        sudo systemctl start apache2

    Apachen tilan tarkistus:

        systemctl status apache2
  
- Tee yrityksellemme "AI Kakone" kotisivu
  
  ![1 14 46_apacheStatus](https://github.com/user-attachments/assets/3f1afc8e-e27c-4250-921a-8dbefd1b034a)

  ![Näyttökuva 2024-10-7 kello 1 36 09](https://github.com/user-attachments/assets/73d8e2cd-5690-402d-b710-378d39d7b33f)

  ![Näyttökuva 2024-10-7 kello 1 34 40](https://github.com/user-attachments/assets/00f1ae2b-e11f-468b-9e09-fc8a3ce3c51a)

  ![Näyttökuva 2024-10-7 kello 1 36 09](https://github.com/user-attachments/assets/d7dae88d-3bbf-4b1e-a293-49071d81d03e)

  ![Näyttökuva 2024-10-7 kello 1 39 00](https://github.com/user-attachments/assets/a34b4052-7e9e-4239-88d8-97bbafaa4e5e)

  ![Näyttökuva 2024-10-7 kello 1 42 01](https://github.com/user-attachments/assets/24b1b8d5-7465-4a73-90f1-9aa897bbce2f)

  ![Näyttökuva 2024-10-7 kello 1 47 36](https://github.com/user-attachments/assets/b762354c-109f-4ce2-83da-ccd69193abe7)

  Virhe 403. Opettajan vinkki 

  "Kotisivu kielletty (403 Forbidden)? 'chmod ugo+x $HOME $HOME/public_html/', 'ls -ld $HOME $HOME/public_html/'" [9]

  Kokeilin sallia Apachelle oikeudet kansioon jossa kotisivun tiedosto on, komennolla `chmod ugo /home/leonardo/public_html`

  En onnistunut vieläkään siinä, huomasin `aikone.com.conf` tiedostossa pienen typon. vaihdoin aikoneen ip-osoitteen 127.0.0.1, aikaisemmin oli 127.0.1.1. Sekään ei auttanut joten virheloki esiin.

        sudo tail -f /var/log/apache2/error.log

  ja löysin lokista:

      [Sun Oct 06 22:56:15.382740 2024] [core:error] [pid 210410:tid 210418] (13)Permission denied: [client 127.0.0.1:34018] AH00035: access to / denied (filesystem path '/home/leonardo/public_html') because search permissions are missing on a component of the path

  Virhe AH00035: **access to / denied (filesystem path '/home/leonardo/public_html') because search permissions are missing on a component of the path**
  
  eli apachelta evätty oikeus `/home/leonardo/public_html`- polkuun.

  Annoin ajokomennon tällä kertaa `/leonardo`- kansioon, ja sivu näytti toimivan

  ![Näyttökuva 2024-10-7 kello 2 14 40](https://github.com/user-attachments/assets/7f239642-74bc-49d6-b349-327851706cb4)
  
- Kotisivu tulee näkyä koneesi IP-osoitteella suoraan etusivulla

  ![Näyttökuva 2024-10-7 kello 2 21 44](https://github.com/user-attachments/assets/1b2c8b8f-faae-4a9b-99da-7896a8141ff8)

  
- Sivua pitää päästä muokkaamaan normaalin käyttäjän oikeuksin (ilman sudoa). Liitä raporttiisi listaus tarvittavien tiedostojen ja kansioiden oikeuksista.

  ![Näyttökuva 2024-10-7 kello 2 18 02](https://github.com/user-attachments/assets/f1b365c8-13ef-4882-97f0-10f8e994708c)


"_g) Salattua hallintaa_"

- Asenna ssh-palvelin
- Tee uusi käyttäjä omalla nimelläsi, esim. minä tekisin "Tero Karvinen test", login name: "terote01"
- Automatisoi ssh-kirjautuminen julkisen avaimen menetelmällä, niin että et tarvitse salasanoja, kun kirjaudut sisään. Voit käyttää kirjautumiseen localhost-osoitetta

Tässä tehtässä käytin [raporttiani](https://github.com/bhg995/lise/blob/main/sshAuth.md) SSH- kirjautumisesta.

Asensin ssh-palvelimen

    sudo apt install openssh-client
    sudo apt install openssh-server

Luon avain turvallisen 4 kilotavuisen avainparin:

    ssh-keygen -b 4096 -t rsa

Tämä loi .ssh kansion käyttäjälle, jossa ovat avainparit, id_rsa sekä id_rsa.pub. id_rsa.pub sisältää julkisen avaimen jota voi jakaa, id_rsa on pidettävä aina salassa.

Teen uuden käyttäjän virtuaalikoneelle ja automatisoin kirjautumisen koneeltani.

Uusi käyttäjä `albert`

![Näyttökuva 2024-10-7 kello 2 44 36](https://github.com/user-attachments/assets/379d07a6-975f-4ead-ace3-ffb7147c8193)


Kopioin .pub tiedoston koneeltani, uudelle käyttäjälle.

    ssh-copy-id albert@146.190.237.216

![Näyttökuva 2024-10-7 kello 2 47 06](https://github.com/user-attachments/assets/7f2532af-4907-4561-802c-fce7b8ad0d52)

Lopetan 7.10.24 klo 2:45, palaan myöhemmin tekemään loput tehtävät

[10]

## Lähteet

1. https://fi.wikipedia.org/wiki/Python_(ohjelmointikieli)
2. https://fi.wikipedia.org/wiki/Java
3. https://fi.wikipedia.org/wiki/C_(ohjelmointikieli)
4. https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/
5. https://terokarvinen.com/2007/12/04/shell-scripting-4/
6. https://github.com/jerebjo/Linuxi/blob/main/h7.md
7. https://www.linode.com/docs/guides/modify-file-permissions-with-chmod/
8. https://fi.wikipedia.org/wiki/Caesarin_salakirjoitus
9. https://terokarvinen.com/linux-palvelimet/
10. https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-linux-palvelimet/
