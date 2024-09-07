
# Name Based Virtual Host Support

## Laitteisto

- **Näyttö: AOC G2490VXA, 24" QHD(1440p), 144Hz**
- **Raspberry Pi 4 model B 4 Gt**
- Käyttöjärjestelmä: Raspberry Pi OS 32bit kernel (based on Debian)
- CPU: Broadcom BCM2711 SoC with a 1.8 GHz 64-bit quad-core ARM Cortex-A72 processor, with 1 MB shared L2 cache.
- Näytönohjain: Broadcom VideoCore VI @ 500 MHz
- Muisti: 4 Gt
- Tallennustila: 32 Gt

## x) Name-based Virtual Host Support

- Relies on the client (browser) to report the hostname as part of the HTTP headers
- This way, Host (server) can have many domain names on a single IP address
- Usually simpler, need only to configure DNS server to map each hostname to the correct IP address, <br>
  and then configure the Apache HTTP Server to recognize the different hostnames
- Eases the demand for scarce IP addressess

## Webbipalvelimen Asennus & Testi

**a) Testaa, että weppipalvelimesi vastaa localhost-osoitteesta. Asenna Apache-weppipalvelin, jos se ei ole jo asennettuna.**

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

Seuraavaksi testasin webbipalvelimen toimivuuden:

Ensin:

    $ curl localhost
    $ curl -I localhost

Käytin `localhost` tarkistamisessa lyhyttä muotoa. Pidempi muoto olisi...

>     $ curl http://localhost
>     $ curl -I http://localhost

... tämä latasi sivuston HTML-koodin kehotteeseen

![curlHost](https://github.com/user-attachments/assets/37782d6d-4bff-438b-a239-7332fc081d02)

`curl -I` komento näyttää lyhyesti, että webbipalvelin toimii. Koodi `200` joka on `OK`. Perusvastaus hyväksytylle HTTP pyynnölle. Mukana myös muutakin tietoa, kuten sisällön muoto, viimeksi muokattu jne.

![curl_I_HOST](https://github.com/user-attachments/assets/fa2688dd-82f3-4f9b-a05f-ffd1f3d9f5f5)


<sub>Näyttökuva 2. CLI, Webbipalvelin HTML</sub>

Samalla tarkistin että se avautuu myös selaimella:

    $ firefox localhost

![2024-09-07-153736_1920x1080_scrot](https://github.com/user-attachments/assets/a7a6f231-b694-4a12-90cd-853ac7aec103)

<sub>Näyttökuva 3. Apache-palvelin Firefox selaimessa</sub>


## Loki

**Tehtävänanto b) Etsi lokista rivit, jotka syntyvät, kun lataat omalta palvelimeltasi yhden sivun. Analysoi rivit (eli selitä yksityiskohtaisesti jokainen kohta ja numero, etsi tarvittaessa lähteitä).**

Seuraavalla komennolla tarkistin lokitiedot

    $ tail -f /var/log/apache2/access.log

    ![accesLog](https://github.com/user-attachments/assets/3b532bc4-5708-42e1-af0a-bc69327fa750)


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

## Kysymykset & Kommenttit

### Sivun lataus omalta palvelimelta, Kysymys.

Tehtävänanto *`b) Etsi lokista rivit, jotka syntyvät, kun lataat omalta palvelimeltasi yhden sivun. 
Analysoi rivit (eli selitä yksityiskohtaisesti jokainen kohta ja numero, etsi tarvittaessa lähteitä).`* 



Sivustoja:

https://www.2kmediat.com/apache/apache_konfiguraatio12.asp

https://www.hostingpalvelu.fi/ohjeet/domain-ja-verkkotunnus-ohjeet/mika-on-domainin-nimipalvelinnimipalvelu-dns/

https://httpd.apache.org/docs/2.4/vhosts/name-based.html

https://www.digitalocean.com/community/tutorials/apache-configuration-error-ah00558-could-not-reliably-determine-the-server-s-fully-qualified-domain-name#setting-a-global-servername-directive
