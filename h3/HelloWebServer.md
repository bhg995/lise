
# Name Based Virtual Host Support

## x) Name-based Virtual Host Support

- Relies on the client (browser) to report the hostname as part of the HTTP headers
- This way, Host (server) can have many domain names on a single IP address
- Usually simpler, need only to configure DNS server to map each hostname to the correct IP address, <br>
  and then configure the Apache HTTP Server to recognize the different hostnames
- Eases the demand for scarce IP addressess

## Weppipalvelimen Asennus & Testi

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

<sub>Näyttökuva 1. käyttöliittymä</sub>

Apache käynnistyi kuten odotetusti, mutta käynnistyksessä järjestelmä ilmoittaa

`apachectl[22731]: AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 127.0.1.1. Set the 'ServerName' directive globally to suppress this message`

Koitin selvittää mistä tämä johtuu. Aloitin Googlesta, ja kirjoitin koko tekstin hakukenttään. Listan kärjessä oli [DigitalOceanin](https://www.digitalocean.com/community/tutorials/apache-configuration-error-ah00558-could-not-reliably-determine-the-server-s-fully-qualified-domain-name) sivu, jossa se käsittelee juuri tätä aihetta.
<br>

An Apache `AH00558: Could not reliably determine the server's fully qualified domain name` message is generated when Apache is not configured with a global ServerName directive. The message is mainly for informational purposes, and an AH00558 error will not prevent Apache from running correctly.

DigitalOceanin sivulla oli ohje, miten sai tämän vian korjattua. Samalla oli myös tarkempi ohje kyseiselle vianmääritykselle.

Lyhyt ohje:

![2024-09-06-200742_1920x1080_scrot](https://github.com/user-attachments/assets/1fa5bc40-4ab9-45a4-b55b-180275129ea7)

<sub>Näyttökuva 2. DigitalOceanin ohje virheelle AH00558</sub>


Sivustoja:

https://www.2kmediat.com/apache/apache_konfiguraatio12.asp

https://www.hostingpalvelu.fi/ohjeet/domain-ja-verkkotunnus-ohjeet/mika-on-domainin-nimipalvelinnimipalvelu-dns/

https://httpd.apache.org/docs/2.4/vhosts/name-based.html
