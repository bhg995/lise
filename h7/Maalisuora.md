# Ohjelmointi

"_Python on ohjelmointikieli, jolle on tunnusomaista hyvä luettavuus, korkea abstraktiotaso ja kehittyneet kirjastot monilla eri sovellusalueilla. Python on niin kutsuttu tulkattu kieli, mikä tarkoittaa että sen suorituskyky on alhaisempi kuin käännetyn kielen._" [1]

"_Java on Java (ohjelmointikieli) on yleiskäyttöinen ohjelmointikieli, jonka avulla ohjelmoijat voivat kirjoittaa koodia, joka kääntäessä toimii kaikilla Javaa tukevilla alustoilla ilman tarvetta kääntää koodia uudelleen._" [2]

"_C on yleiskäyttöinen, imperatiivinen ja rakenteinen käännettävä tietokoneiden ohjelmointikieli._" [3]

## Laitteisto

- Tietokone: MacBook Air (13-inch, 2017) **INTEL**
- Käyttöjärjestelmä: macOS Monterey 12.7.5
- Prosessori: 1,8 GHz Kaksiytiminen Intel Core i5
- Muisti: 8 Gt 1600 MHz DDR3
- Näytönohjain: Intel HD Graphics 6000, 1536 Mt

- Ympäristö: DigitalOcean VPS
- Käyttöjärjestelmä: Debian 12, arm64

## a) Kirjoita ja aja "Hei maailma" kolmella kielellä. su 6.10.2024

tämä osio klo 18:20 - 19:00

Hyödynsin opettajan sivuilla olevia ohjeita.

Ensin Java kielellä

![kello 18 38 30_javaCode](https://github.com/user-attachments/assets/b6969e0e-b655-4b0b-8d1e-f333cae238ff)

Testi:

![18 39 18_helloWorldJavalla](https://github.com/user-attachments/assets/fd175348-9bf0-4002-a397-4cddf37ae2d7)

Sitten C:llä

![18 44 59_cCode](https://github.com/user-attachments/assets/b06b0341-886d-4f09-8447-42ef7b34ce69)

Testi:

![18 50 26_helloWorldClla](https://github.com/user-attachments/assets/b6a0aaa6-8366-43f1-96ed-c301184e90e5)

C kieli oli täysin vieras kieli minulle, hieman kompuroin ennenkuin sain tervehdyksen toimimaan.

Viimeiseksi Pythonilla

![19 01 19_pythonCode](https://github.com/user-attachments/assets/f6724f06-e81f-4a26-9837-9fc4c3a3f030)

Pythonissa kirjoitin koodin niin, että ohjelma kysyy käyttäjältä vaihtoehtoja 1 tai 2. Käyttäjän valinnan jälkeen ohjelma tervehtii joko 1: suomeksi tai 2: englanniksi.

Testi:

![19 01 58_HelloWorldPythonilla](https://github.com/user-attachments/assets/67c505b1-25eb-43d8-896d-b6252548d0c1)

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

Tämän jälkeen kopioin sen pääkäyttäjänä kansioon /usr/local/bin/, unohdin että pitää sudottaa, sekä kompuroin salasanan kanssa vielä.

![19 25 57_bashKomennoksi](https://github.com/user-attachments/assets/93486179-535a-463c-8b34-60062ed8809d)

Kirjauduin ulos `leonardo`-käyttäjänä, ja kirjauduin testiä varten tekemääni `galileo`-käyttäjänä.

Testi: `galileo`

![19 30 46_kokeilua](https://github.com/user-attachments/assets/6d1622af-cc81-4248-b22b-c2484804241b)

Testi: `immanuel`

![20 30 30_kokeilua_immanuel](https://github.com/user-attachments/assets/cd4bc8ff-75ca-449b-bc81-2a27fe6b593e)


Komento `hei.sh` toimii nyt eri käyttäjillä.

## c) Ratkaise vanha arvioitava laboratorioharjoitus soveltuvin osin.

Tämä osio 20:30 - 21.20

Teen harjoituksen käyttäjänä `leonardo`, ja testaan sitä käyttäjällä `immanuel`

Valitsin edellisen toteutuksen labraharjoituksen osan:

"_c) Ei kolmea sekoseiskaa_"

    Suojaa raportti Linux-oikeuksilla niin, että vain oma käyttäjäsi pystyy katselemaan raporttia

[7]

Tein tiedoston `salaista.txt`, ja kirjoitin sisältöä siihen.

Tämän jälkeen muutin tiedoston oikeuksia `chmod 600 salaista.txt`, joka antaa käyttäjälle `leonardo` oikeudet lukea ja kirjoittaa mutta ei ajaa(execute). Muille käyttäjille ei ole oikeuksia lainkaan.

![20 50 39_salaiseksi](https://github.com/user-attachments/assets/110ea56d-1141-4158-ae64-63125b995b0f)

Kokeilin päästä `leonardo`-käyttäjän kansioon, ja järjestelmä ilmoitti että ei ollut siihen oikeuksia. Vvaihdoin käyttäjän `leonardo`-kansion oikeuksia niin, että muilla käyttäjillä on on vain luku oikeus, kun taas `leonardo`-käyttäjällä on täydet oikeudet.

![Näyttökuva 2024-10-6 kello 21 08 25](https://github.com/user-attachments/assets/1306e66b-6827-4cc0-aa46-174e31de2302)

Komento on `chmod 744 /home/leonardo`

Tarkistin tiedoston ja kansion oikeudet komennolla `ls -l`

![21 03 39_oikeudet](https://github.com/user-attachments/assets/fd4bc445-c2bd-469f-9b2b-696f242a80c3)

Huomasin että, `leonardo`-käyttäjän kansion sisältö oli aika lailla evätty, etenkin tiedostojen kohdalla. Komentoni muuttaa oikeuksia `salaista.txt`-tiedostoon toimivat, koska siinä ei ole samat oikeudet kuin muissa tiedostoissa, mutta oikeudet vastaavat mitä oli komennetty `chmod 600 salaista.txt`

Seuraavaksi kirjauduin käyttäjällä `immanuel` ja kokeilin päästä käsiksi tiedostoon.

![Näyttökuva 2024-10-6 kello 21 16 56](https://github.com/user-attachments/assets/756c22a8-5969-4944-80bf-2c05166a0822)

Järjestelmä antoi vastaukseksi `permission denied` kun yritin avata `immanuel`-käyttäjällä `leonardo`-käyttäjän tiedostoa. Katsoin vielä `leonardo`-käyttäjän kansiota, johon muillakin oli lukuoikeus, järjestelmä kertoi vielä että tiedostoihin ja kansioihin ei ole asiaa.

Aloitin tehtävät klo 18:20 ja olin valmis 21:20

[8]

## Lähteet

1. https://fi.wikipedia.org/wiki/Python_(ohjelmointikieli)
2. https://fi.wikipedia.org/wiki/Java
3. https://fi.wikipedia.org/wiki/C_(ohjelmointikieli)
4. https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/
5. https://terokarvinen.com/2007/12/04/shell-scripting-4/
6. https://github.com/jerebjo/Linuxi/blob/main/h7.md
7. https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-linux-palvelimet/
8. https://www.linode.com/docs/guides/modify-file-permissions-with-chmod/
