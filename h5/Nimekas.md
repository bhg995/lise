
# Nimekäs

_"Dig (Domain Information Groper) is a powerful command-line tool for querying DNS name servers.
Most DNS administrators use dig to troubleshoot DNS problems because of its flexibility, 
ease of use, and clarity of output. Other lookup tools tend to have less functionality than dig"_ [1]

`dig` Komento on tehokas apuväline DNS-tietojen tarkisteluun. [2]

_"`host` is a simple utility for performing DNS lookups. It is normally used to convert names to IP addresses and vice versa"._ [3]

`scp` Komennolla voi kopioida tiedostoja turvallisesti verkon ylitse palvelimeen SSH-yhteydellä. `scp` voi pyytää salasanaa jos sitä tarvitaan. [4]

## Laitteisto

- MacBook Air (13-inch, 2017)
- Käyttöjärjestelmä: macOS Monterey 12.7.5
- Prosessori: 1,8 GHz Kaksiytiminen Intel Core i5
- Muisti: 8 Gt 1600 MHz DDR3
- Näytönohjain: Intel HD Graphics 6000, 1536 Mt


### a) Kotisivu. Tee vähintään kolmen erillisen weppisivun kotisivu ja kopioi se näkymään palvelimellesi. 

Aloitin tekemällä uuden virtuaalikoneen ja nimesin sen mansikaksi

![Näyttökuva 2024-9-24 kello 16 06 58](https://github.com/user-attachments/assets/01a77236-a660-4b4e-a277-b8fd73811725)

Otin yhteyttä serveriin ja tein alkutoimenpiteet

    sudo apt update && sudo apt upgrade
    sudo apt-get install ufw
    sudo ufw allow 22/tcp
    sudo ufw enable
    sudo apt-get install openssh-server
    sudo apt-get install micro
    sudo apt-get install apache2

Sitten tein uuden käyttäjän ja annan sudo oikeudet.

![Näyttökuva 2024-9-24 kello 16 19 29](https://github.com/user-attachments/assets/2250a0a0-97b5-4d5a-ad63-25260a1c501a)

Kokeilin toiselta tietokoneelta että käyttäjä oli luotu ja minulla oli pääsy siihen.

![Näyttökuva 2024-9-24 kello 16 21 26](https://github.com/user-attachments/assets/0f161ad8-8e3e-4385-a3af-57939eaac763)

Yritin sulkea root käyttäjän, mutta sain viestin että:

    usermod: user root is currently used by process 1

Ihmettelin hetken, muistin että valitsin palvelimen kirjautumismuodoksi SSH-avaimen, joten käytin komentoa `sudoedit /etc/ssh/sshd_config` ja suljin manuaalisesti. [5]



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

Edellisessä tehtävässä [MaailmaKuulee](https://github.com/bhg995/lise/blob/main/h4/maailmaKuulee.md) käyttäjän oikeudet kansioiden kanssa oli hieman ongelmaa. Ongelma korjaantui konfiguroimalla oikeuksia.

    chmod o+x /home
    chmod o+x /home/immanuel

Sitten otin userdir käyttöön

    sudo a2enmod userdir
    sudo systemctl restart apache2

Loin virtualhost konfiguraatiot apachelle:

    sudo nano /etc/apache2/sites-available/site1.llanga.live.conf
    sudo nano /etc/apache2/sites-available/site2.llanga.live.conf
    sudo nano /etc/apache2/sites-available/site3.llanga.live.conf

ja kirjoitin konfiguraatiot:

    <VirtualHost *:80>
      ServerAdmin admin@llanga.live
      ServerName site1.llanga.live
      DocumentRoot /var/www/site1.llanga.live/public_html
      ErrorLog ${APACHE_LOG_DIR}/error.log
      CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>

sivuille 2 ja kolme muutin ServerNameksi `site2.llanga.live` ja `site3.llanga.live`

Tämän jälkeen otin palvelimet käyttöön

    sudo a2ensite site1.llanga.live.conf
    sudo a2ensite site2.llanga.live.conf
    sudo a2ensite site3.llanga.live.conf

Sitten käynnistin Apachen uudelleen

    sudo systemctl restart apache2

Tämän jälkeen aloin luoda HTML sivut ja linkitin toisiinsa:

    micro /var/www/site1.llanga.live/public_html/index.html
    micro /var/www/site2.llanga.live/public_html/index.html
    micro /var/www/site3.llanga.live/public_html/index.html
    

![Näyttökuva 2024-9-24 kello 17 26 34](https://github.com/user-attachments/assets/7cafdd34-5144-47b8-9128-98295ec680b7)




## Lähteet

1. https://linuxize.com/post/how-to-use-dig-command-to-query-dns-in-linux/
2. https://linux.die.net/man/1/dig
3. https://linux.die.net/man/1/host
4. https://linux.die.net/man/1/scp
5. https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/
6. https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/


