
# Name Based Virtual Host Support

## Laitteisto

- **Näyttö: AOC G2490VXA, 24" QHD(1440p), 144Hz**
- **Raspberry Pi 4 model B 4 Gt**
- Käyttöjärjestelmä: Raspberry Pi OS 32bit kernel (based on Debian)
- CPU: Broadcom BCM2711 SoC with a 1.8 GHz 64-bit quad-core ARM Cortex-A72 processor, with 1 MB shared L2 cache.
- Näytönohjain: Broadcom VideoCore VI @ 500 MHz
- Muisti: 4 Gt
- Tallennustila: 32 Gt

## x) Virtual Host Support


### Name-based

- Relies on the client (browser) to report the hostname as part of the HTTP headers
- This way, Host (server) can have many domain names on a single IP address
- Usually simpler, need only to configure DNS server to map each hostname to the correct IP address, <br>
  and then configure the Apache HTTP Server to recognize the different hostnames
- Eases the demand for scarce IP addressess

### IP-Based

## Webbipalvelimen Asennus & Testi

**a) Testaa, että weppipalvelimesi vastaa localhost-osoitteesta. Asenna Apache-weppipalvelin, jos se ei ole jo asennettuna.**

### Asentaminen

Latasin Apache palvelinohjelman ja käynnistin seuraavilla komennoilla.

Lataaminen:

    $ sudo apt-get install apache2

Tarkistin version:

    $ sudo apache2 -v

Sain tulokseksi:
  
    Server version: Apache/2.4.62 (Raspbian)
    Server built:   2024-08-15T01:18:37

Käynnistys:

    $ sudo systemctl start apache2

![cli_screenshot](https://github.com/user-attachments/assets/66758ff4-95b3-447a-8567-02b5073f9e8b)
<sub>Näyttökuva 1. CLI, Apachen käynnistys</sub>

Käynnistyksessä virhe. Virheen korjaus  [**Haasteet & Virheviestit**](https://github.com/bhg995/lise/blob/main/h3/HelloWebServer.md#haasteet--virheviestit) -osiossa.

### Sivuston Testaaminen

Seuraavaksi testasin webbipalvelimen toimivuuden:

Ensin:

    $ curl localhost
    $ curl -I localhost

Käytin `localhost` tarkistamisessa lyhyttä muotoa. Pidempi muoto olisi...

>     $ curl http://localhost
>     $ curl -I http://localhost

... tämä latasi sivuston HTML-koodin kehotteeseen

![curlHost](https://github.com/user-attachments/assets/37782d6d-4bff-438b-a239-7332fc081d02)
<sub>Näyttökuva 2. CLI, Webbipalvelin HTML</sub>

`curl -I` komento näyttää lyhyesti, että webbipalvelin toimii. Koodi `200` joka on `OK`. Perusvastaus hyväksytylle HTTP pyynnölle. Mukana myös muutakin tietoa, kuten sisällön muoto, viimeksi muokattu jne.

![curl_I_HOST](https://github.com/user-attachments/assets/fa2688dd-82f3-4f9b-a05f-ffd1f3d9f5f5)

<sub>Näyttökuva 3. CLI, HTTP Response Header</sub>

Samalla tarkistin että se avautuu myös selaimella:

    $ firefox localhost

![2024-09-07-153736_1920x1080_scrot](https://github.com/user-attachments/assets/a7a6f231-b694-4a12-90cd-853ac7aec103)

<sub>Näyttökuva 4. Apachen palvelimen oletussivu Firefox selaimessa</sub>


## Loki

**Tehtävänanto b) Etsi lokista rivit, jotka syntyvät, kun lataat omalta palvelimeltasi yhden sivun. Analysoi rivit (eli selitä yksityiskohtaisesti jokainen kohta ja numero, etsi tarvittaessa lähteitä).**

Seuraavalla komennolla sain lokitiedot

    $ sudo tail /var/log/apache2/access.log

  ![accesLog](https://github.com/user-attachments/assets/3b532bc4-5708-42e1-af0a-bc69327fa750)

<sub>Näyttökuva 5. CLI, Palvelimen lokitiedot</sub>

Otin tarkisteluun toisen rivin, jossa haettiin weppispalvelimen kotisivu:

    127.0.0.1 - - [07/Sep/2024:12:33:22 +0300] "GET / HTTP/1.1" 200 3382 "-" "Mozilla/5.0 (X11; Linux aarch64; rv:102.0) Gecko/20100101 Firefox/102.0"

Apachen sivustolla [Log Files](https://httpd.apache.org/docs/current/logs.html) selitetään jokaisen tiedon tarkoituksen.

- `127.0.0.1` on client (browser), eli asiakas tai selain joka tekee pyynnön palvelimelle (host)
- Puuttuva tieto merkitään `-` merkillä. Tässä tapauksessa tästä puuttuu [rfc1413](https://datatracker.ietf.org/doc/html/rfc1413)
- Seuraava puuttuva tieto on `käyttäjätunnus`. En ole asettanut vielä käyttäjätunnusta/palvelinohjaaja ei tarvitse käyttäjätunnusta
    - If the status code for the request (see below) is 401, then this value should not be trusted because the user is not yet authenticated.
- `[07/Sep/2024:12:33:22 +0300]`, on aika milloin loki on kirjattu
- `GET / HTTP/1.1`, on rivi jolla client pyytää tietoja. Tässä rivissä on tietoa
    - `GET`, pyytää tiedot
    - `/`, pyydettävä tieto. Tämä pyytää juurikansion. Pyyntö voisi olla myös esim. [/apache_pb.gif](https://httpd.apache.org/docs/current/logs.html)
    - `HTTP/1.1`, kertoo käytetyn protokollan tiedon pyytämiseen.
- `200`, kertoo että pyyntö on totetutettu ja tila on OK. 200 alkuiset tilakoodit merkitsevät onnistunutta pyyntöä.
- `3382`, kertoo kuinka paljon tietoa on lähetetty palvelimelta selaimelle. 
- Seuraava merkki `-` kertoo puuttuvasta tiedosta. Puuttuva tieto on pyydetyn tiedon sijainti (webosoite). Apachen sivuston esimerkin mukaan tämä tieto voisi olla seuraava `http://www.example.com/start.html`
    - Tällä sivulla sijaitsee esimerkkipyynnön .gif tiedosto ([/apache_pb.gif](https://httpd.apache.org/docs/current/logs.html))
- Viimeinen kohta `Mozilla/5.0 (X11; Linux aarch64; rv:102.0) Gecko/20100101 Firefox/102.0`, kertoo client (browser) järjestelmän ja käytössä olevan selaimen tieto
    - `Mozilla/5.0` on Mozillan valtuutus, joka on yleinen melkein kaikille selaimille. [lähde](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent/Firefox)
    - `X11; Linux aarch64; rv:102.0`, kertoo client (browser) tiedon
        - `X11` X windows System ikkunointijärjestelmä
        - `Linux aarch64` kertoo että käyttöjärjestelmä on Linux ja arkkitehti ARM 64-bittinen
        - `rv:102.0` koneen versio joka renderöi webbisivut
        - `Gecko/20100101` on [selainmoottori](https://fi.wikipedia.org/wiki/Gecko) jota käyttää Firefoxin lisäksi muita selaimia. 20100101 on moottorin versio.
        - `Firefox/102.0` on client (browser) käytössä oleva selain. Käytetään Firefox selainta jonka versio on 102

## Uusi etusivu

**c) Etusivu uusiksi. Tee uusi name based virtual host. Sivun tulee näkyä suoraan palvelimen etusivulla http://localhost/. Sivua pitää pystyä muokkaamaan normaalina käyttäjänä, ilman sudoa. Tee uusi, laita vanhat pois päältä. Uusi sivu on hattu.example.com, ja tämän pitää näkyä: asetustiedoston nimessä, asetustiedoston ServerName-muuttujassa sekä etusivun sisällössä (esim title, h1 tai p).**

Opettajan [sivulla](https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/) Oli helppo ja selkeä ohje.

Aloitin luomalla kansion webbisivujen sisältöä varten:

![2024-09-09-224703_1920x1080_scrot](https://github.com/user-attachments/assets/aa97d6d3-08db-4f26-85c8-32cfddf1bfc7)

<sub>Näyttökuva 6. Kansion luominen webbisivuille</sub>

Seuraavaksi lisäsin palvelimen asetustiedoston hakemistoon, muokkaamalla hieman komentoa opettajan sivuilta:

`sudo nano /etc/apache2/sites-available/hattu.example.com.conf`

Lisäsin seuraavan sisällön asetustiedostoon:

    <VirtualHost *:80>
        ServerName hattu.example.com
        ServerAlias localhost
        DocumentRoot /home/uhse/public_html/hattu.example.com

        <Directory /home/uhse/public_html/hattu.example.com>
            Require all granted
        </Directory>
    </VirtualHost>

Sitten lisäsin HTML sisältöä uuteen etusivuun komennolla:

    sudo nano /home/uhse/public_html/hattu.example.com/index.html

Samalla kirjoitin sen vastaamaan validia HTML5-sivua. Seuraavassa tehtävässä opettaja on pyytänyt tekemään validin HTML5 sivun.

![validiHTML](https://github.com/user-attachments/assets/d8dc0354-5b01-40a5-8234-e970e56920e8)

<sub>Näyttökuva 7. HTML5-koodia tekstieditorissa</sub>

Sen jälkeen otin sivuston käyttöön:

    sudo a2ensite hattu.example.com.conf
    sudo systemctl restart apache2

Sivusto näyttää toimivan oikein:

![curlTesti](https://github.com/user-attachments/assets/a113920a-e447-4fb9-9038-858352d20740)

<sub>Näyttökuva 8. hattu.example.com tekstieditorissa</sub>

## HTML5

### e) Tee validi HTML5 sivu.

HTML ja HTML5 erona on se että jälkimmäinen pystyy toistamaan audioita ja videoita. Modernit selaimet tukevat HTML5 koodia.

Käytin esimerkkina opettajan [sivulla](https://terokarvinen.com/2012/short-html5-page/)) olevaa lyhyttä esimerkkiä validista HTML5 koodista.



## Haasteet & Virheviestit

### Could not reliably determine the server's fully qualified domain name, AH00558

Törmäsin virheeseen Apachen käynnistyksessä, jossa se ilmoitti käynnistyksen yhteydessä:

`apachectl[22731]: AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 127.0.1.1. Set the 'ServerName' directive globally to suppress this message`

Googlasin koko tekstin ja löysin [DigitalOceanin](https://www.digitalocean.com/community/tutorials/apache-configuration-error-ah00558-could-not-reliably-determine-the-server-s-fully-qualified-domain-name) sivun, josta löysin:

![AH0058fix](https://github.com/user-attachments/assets/a5962e87-238b-4a50-ba56-adf163bac59e)

<sub>Näyttökuva 2. DigitalOceanin ohje virheelle AH00558</sub>

Toimin ohjeiden mukaan ja lisäsin koodin apache2.conf tiedostoon. Sen jälkeen käynnistin Apachen uudelleen käyttämällä komentoa `restart`. Samalla tarkistin että onko virhe enää näkyvissä.

    $ sudo systemctl restart apache2
    $ sudo systemctl status apache2

Tämän jälkeen Apache käynnistyi ilman virheitä:

![workinApache](https://github.com/user-attachments/assets/c50fcbb4-5b91-4742-aa56-18e537638ffc)

<sub>Näyttökuva 3. CLI, Apachen status</sub>

## Kysymykset & Kommentit

### Sivun lataus omalta palvelimelta, Kysymys.

Mitä eroa kansioilla `/var/www/html/index.html` ja ``


Sivustoja:

https://www.2kmediat.com/apache/apache_konfiguraatio12.asp

https://www.hostingpalvelu.fi/ohjeet/domain-ja-verkkotunnus-ohjeet/mika-on-domainin-nimipalvelinnimipalvelu-dns/

https://httpd.apache.org/docs/2.4/vhosts/name-based.html

https://www.digitalocean.com/community/tutorials/apache-configuration-error-ah00558-could-not-reliably-determine-the-server-s-fully-qualified-domain-name#setting-a-global-servername-directive
