
# Nimekäs

_"Dig (Domain Information Groper) is a powerful command-line tool for querying DNS name servers.
Most DNS administrators use dig to troubleshoot DNS problems because of its flexibility, 
ease of use, and clarity of output. Other lookup tools tend to have less functionality than dig."_ - Linuxize [1]

`dig` Komento on hyödyllinen apuväline DNS-tietojen tarkisteluun. [2]

_"`host` is a simple utility for performing DNS lookups. It is normally used to convert names to IP addresses and vice versa."_ - Linux manual pages[3]

`scp` Komennolla voi kopioida tiedostoja turvallisesti verkon ylitse palvelimeen SSH-yhteydellä. `scp` voi pyytää salasanaa jos sitä tarvitaan. [4]

## Laitteisto

- Näyttö: AOC G2490VXA, 24" QHD(1440p), 144Hz
- Raspberry Pi 4 model B 4 Gt
- Käyttöjärjestelmä: Raspberry Pi OS 32bit kernel (based on Debian)
- CPU: Broadcom BCM2711 SoC with a 1.8 GHz 64-bit quad-core ARM Cortex-A72 processor, with 1 MB shared L2 cache.
- Näytönohjain: Broadcom VideoCore VI @ 500 MHz
- Muisti: 4 Gt
- Tallennustila: 32 Gt


## a) Kotisivu. Tee vähintään kolmen erillisen weppisivun kotisivu ja kopioi se näkymään palvelimellesi. 

Tein uuden virtuaalikoneen ja nimesin sen mansikaksi

![Näyttökuva 2024-9-24 kello 16 06 58](https://github.com/user-attachments/assets/01a77236-a660-4b4e-a277-b8fd73811725)

Valmistelin DNS asetukset namecheap:ssä

![Näyttökuva 2024-9-25 kello 0 58 19](https://github.com/user-attachments/assets/ded4fead-1c4d-426b-b70f-1c182da27e39)


Otin yhteyttä serveriin ja tein alkutoimenpiteet

    ssh root@167.99..210.231

  päivitys

    sudo apt update && sudo apt upgrade

  palomuurin asennus
  
    sudo apt-get install ufw
    
  avataan portti 22
  
    sudo ufw allow 22/tcp
    
  käynnistetään palomuuri
  
    sudo ufw enable

 latasin  työkalut
 
    sudo apt-get install openssh-server
    sudo apt-get install micro
    sudo apt-get install apache2

Tein uuden käyttäjän ja annoin sudo oikeudet.

![Näyttökuva 2024-9-24 kello 16 19 29](https://github.com/user-attachments/assets/2250a0a0-97b5-4d5a-ad63-25260a1c501a)

Kokeilin toiselta tietokoneelta että käyttäjä oli luotu ja minulla oli pääsy siihen.

![Näyttökuva 2024-9-24 kello 16 21 26](https://github.com/user-attachments/assets/0f161ad8-8e3e-4385-a3af-57939eaac763)

Yritin sulkea root käyttäjän, mutta sain viestin:

    usermod: user root is currently used by process 1

DigitalOceanin asetuksissa, valitsin palvelimen kirjautumismuodoksi SSH-avaimen. Löysin opiskelijan ohjeista `sudoedit /etc/ssh/sshd_config`, jolla suljin root oikeudet manuaalisesti. [5]


![Näyttökuva 2024-9-24 kello 16 32 06](https://github.com/user-attachments/assets/6261feb4-ad9b-4678-ba75-d34f9fe98210)

Sitten vielä lisäsin reijän palomuuriin

    sudo ufw allow 80/tcp

Sen jälkeen komennot

    sudo service ssh restart
    sudo apt-get update && sudo apt-get upgrade

Nyt voin alkaa tekemään verkkosivustot palvelimeen. Ensin katsoin että palvelin toimii ja localhost näyttää Apachen oletuskotisivua.

![Näyttökuva 2024-9-24 kello 16 40 01](https://github.com/user-attachments/assets/a28ac554-a185-452a-9056-6d025087833c)

    echo "Default|sudo tee /var/www/html/index.html"

![Näyttökuva 2024-9-24 kello 16 43 41](https://github.com/user-attachments/assets/9a4c8e9e-24e5-4dae-bfab-9ffd3f8b45d2)

Sitten tein hakemistot sivuille

![Näyttökuva 2024-9-24 kello 16 48 48](https://github.com/user-attachments/assets/e3fd4ebe-18fc-47dc-a6ca-b2e65fc5d1a4)

Tehtävän mukaan sivujen piti olla muokattavissa ilman pääkäyttäjän oikeuksia, siirsin käyttäjän public_html kansioon.

![Näyttökuva 2024-9-24 kello 23 56 33](https://github.com/user-attachments/assets/13c17bbb-975f-4da5-bbc9-ddf3a2824dcd)


Muutin Apachen VirtualHost-asetukset

    

Edellisessä tehtävässä [MaailmaKuulee](https://github.com/bhg995/lise/blob/main/h4/maailmaKuulee.md) käyttäjän oikeudet kansioiden kanssa oli hieman ongelmaa. Muokkasin kansioiden käyttöoikeuksia tässä vaiheessa..

    chmod o+x /home
    chmod o+x /home/immanuel

Sitten otin userdir käyttöön

    sudo a2enmod userdir
    sudo systemctl restart apache2

Loin virtualhost konfiguraatiot apachelle:

    sudo micro /etc/apache2/sites-available/llanga.live.conf
    sudo micro /etc/apache2/sites-available/site2.llanga.live.conf
    sudo micro /etc/apache2/sites-available/site3.llanga.live.conf

![Näyttökuva 2024-9-25 kello 0 23 50](https://github.com/user-attachments/assets/9d8f69d0-baf9-4a5c-b1f7-51b063f80679)

sivuille 2 ja 3 muutin ServerNameksi `site2.llanga.live` ja `site3.llanga.live`

Tämän jälkeen otin palvelimet käyttöön

    sudo a2ensite llanga.live.conf
    sudo a2ensite site2.llanga.live.conf
    sudo a2ensite site3.llanga.live.conf

Sitten käynnistin Apachen uudelleen

    sudo systemctl restart apache2

Tämän jälkeen aloin luoda HTML sivut ja linkitin toisiinsa:

    micro /home/immanuel/public_html/site1/index.html
    micro /home/immanuel/public_html/site2/index.html
    micro /home/immanuel/public_html/site3/index.html
    

![Näyttökuva 2024-9-24 kello 17 26 34](https://github.com/user-attachments/assets/7cafdd34-5144-47b8-9128-98295ec680b7)

Sivut toimivat selaimella

![Näyttökuva 2024-9-25 kello 0 29 36](https://github.com/user-attachments/assets/816df7f0-ff70-45ae-b877-9570996cb8f4)

Tein validit HTML5 sivut kannettavalla tietokoneellani, ja käytin `scp` komentoa kopioidakseni palvelimelleni.

![Näyttökuva 2024-9-25 kello 0 50 21](https://github.com/user-attachments/assets/c30340a2-0d6a-4650-8780-f360b702c4d9)

Kopiointi onnistui

![Näyttökuva 2024-9-25 kello 0 53 37](https://github.com/user-attachments/assets/eb205ba9-229d-4ee5-8bd6-538640089fdd)

Selaimella näytti OK!

![Näyttökuva 2024-9-25 kello 1 39 16](https://github.com/user-attachments/assets/fcdab75b-f019-45f4-9949-f62733b8b863)


## b) Alidomain

En ymmärtänyt tehtävää hyvin, voi olla että olin tehnyt a) tehtävän jälkimmäiset sivut osittain alidomainena?. Loin silti CNAME record luodakseen alidomaineja namecheapissä. Otan selvää seuraavalla tunnilla.

![Näyttökuva 2024-9-25 kello 1 11 24](https://github.com/user-attachments/assets/4a639787-9dd5-424c-9bb0-6fafcd3a0835)

## c) Pubkey

![Näyttökuva 2024-9-25 kello 1 18 43](https://github.com/user-attachments/assets/1bffe5bd-c970-4a96-9a2b-1e538df64c93)

Automatisointi

![Näyttökuva 2024-9-25 kello 1 34 38](https://github.com/user-attachments/assets/2ee10c53-5fca-484f-a8d5-a988ef89eceb)

## d) Tutki jonkin nimen DNS-tietoja 'host' ja 'dig' -komennoilla

En ymmärtänyt `dig` komennon tuloksia. Päätin että otan selvää seuraavalla tunnilla.

![Näyttökuva 2024-9-25 kello 1 43 21](https://github.com/user-attachments/assets/1cfbf668-3de1-4192-b868-bf9f93e5a2fc)


## Lähteet

1. https://linuxize.com/post/how-to-use-dig-command-to-query-dns-in-linux/
2. https://linux.die.net/man/1/dig
3. https://linux.die.net/man/1/host
4. https://linux.die.net/man/1/scp
5. https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/
6. https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/

- https://www.openssh.com/
