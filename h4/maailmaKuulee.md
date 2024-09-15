
# VPS & Webserver. 15.9 klo 18:30

Tämä Github dokumentin kirjoitus alkoi klo 18:30. Tehtävää varten on tehty valmistelut heti viikkoluennon jälkeen, jotkut kohdat ovat tehty eri aikoihin ja lisätty tähän kirjoitusvaiheessa.

Tehtävä b) Tee alkutoimet omalla virtuaalipalvelimellasi & c) Asenna weppipalvelin omalle virtuaalipalvelimellesi oli aloitettu klo sunnuntaina 15.9 klo 18:50 ja lopettettu klo 20:13 onnistuneesti. www.llanga.live

## Laitteisto

- **Näyttö: AOC G2490VXA, 24" QHD(1440p), 144Hz**
- **Raspberry Pi 4 model B 4 Gt**
- Käyttöjärjestelmä: Raspberry Pi OS 32bit kernel (based on Debian)
- CPU: Broadcom BCM2711 SoC with a 1.8 GHz 64-bit quad-core ARM Cortex-A72 processor, with 1 MB shared L2 cache.
- Näytönohjain: Broadcom VideoCore VI @ 500 MHz
- Muisti: 4 Gt
- Tallennustila: 32 Gt

### x) Lue ja tiivistä

- Tavoitteena oli vuokrata virtuaalipalvelin, ja asentaa webbipalvelin virtuaalipalvelimelle.
- Susanna oli hyödyntänyt Github Education pakettia joka on suunnattu ohjelmistokehityksen opiskelijoille.
- Datakeskuksen sijainniksi hän valitsi Amsterdam, perustellen sen lähellä. Myös GDPR oli otettu huomioon.
- Autentikointimenetelmäksi Susanna valitsi vahvan salasanan, SSH-avain olisi ollut hänen mukaan parempia.
- Yhteys palvelimeen oli muodostettu ssh menetelmällä
- Susanna lisäsi uuden käyttäjän virtuaalipalvelimelle, samalla suojasi sen salasanalla
- `$ sudo apt-get update && sudo apt-get upgrade && sudo apt-get dist-upgrade`
  
### a) Vuokraa oma virtuaalipalvelin haluamaltasi palveluntarjoajalta.

Valitsin DigitalOceanin palvelimen palvelutarjoajaksi. Tero Karvinen ehdottaa sen käyttämistä kurssilla, olen nähnyt sen myös käytössä, ja uskoin että osaisin käyttää tai oppisin ainakin nopeasti.

![configs](https://github.com/user-attachments/assets/86266c34-c108-414a-9c6b-4e05278f52c0)


Virtuaalikone pitää ja kannattaa aina olla mahdollisimman lähellä käyttäjiä. Tätä tehtävää varten ei tämä ollut tärkeä, mutta valitsin kuitenkin Amsterdamin, joka sijaitsee Euroopassa sekä kuuluu GDPR:n piiriin.

![creatingDroplet](https://github.com/user-attachments/assets/9349c848-e6aa-434e-98de-d5bfda26d9fb)

Tämän jälkeen virtuaalipalvelimeni, jonka nimesin valdelmaksi, oli valmis ja sain ip osoitteen nimipalvelua varten.

![dropletti](https://github.com/user-attachments/assets/1bdf15c5-a92a-4b3f-8be3-fdcb2678c46f)

Valitsin domainnimen tarjoajaksi Namecheapiä. Tämä oli helppo valinta, opettaja on ehdottanut sen käyttöä ja se on varsin edullinen.

Ostaessani domainnimeä, olin niin innoissani tehtävästä että unohdin dokumentoida Namecheapin prosessin. Sain kuitenkin näyttökuvan sähköpostin vahvistuksesta ja tilauksestani.

![namecheapSuccess](https://github.com/user-attachments/assets/7788426f-df9b-4fbd-9985-46826bdd94d4)

![2024-09-15-221314_930x402_scrot](https://github.com/user-attachments/assets/1d173375-a750-4f86-ab37-50a299ec9f44)

### b) Tee alkutoimet omalla virtuaalipalvelimellasi. klo 18:50


Aloitin ottamalla yhteyttä palvelimeen

    $ ssh root@157.245.78.37

![2024-09-15-185407_655x254_scrot](https://github.com/user-attachments/assets/cb2c22b6-df15-4151-b7d4-55694e18aa84)

Ensin hain päivitykset 

        $ sudo apt-get update && sudo apt-get upgrade

Jonka jälkeen asensin palomuurin, avasin ensimmäisen portin ja kytkin palomuurin päälle

        $ sudo apt-get install ufw
        $ sudo ufw allow 22/tcp
        $ sudo ufw enable

![reikaPalomuuriin2024-09-15-190004_639x318_scrot](https://github.com/user-attachments/assets/bdb064e0-a129-4462-8df3-cb854aa803e4)

Lisäsinn uuden käyttäjän jolle loin vahvan salasanan, tein myös käyttäjästä sudoerin (sudo-oikeudet)

        $ sudo adduser leonardo 
        $ sudo adduser leonardo sudo

![uusiKaytt2024-09-15-190403_639x622_scrot](https://github.com/user-attachments/assets/7296ca30-1803-458f-97ee-74133046478e)

Sen jälkeen oli mahdollista kirjautua uudella käyttäjällä ja lukita juurikäyttäjä (root):

        $ ssh leonardo@157.245.78.37
        $ sudo usermod -lock root

Sitten laitoin päivitykset kuntoon kerralla

        $ sudo apt-get update && sudo apt-get upgrade && sudo apt-get dist-upgrade

Asensin Apachen virtuaalipalvelimelle ja tarkistin toimivuuden

        $ sudo apt-get install apache2
        $ sudo systemctl start apache2
        $ sudo systemctl status apache2

Kaikki näytti hyvältä, paitsi apache2.service näytti olevan disabled

![apacheSTATUS2024-09-15-191500_759x446_scrot](https://github.com/user-attachments/assets/8df61103-583a-48c0-9381-6cc570e0f551)
        
Ei ollut virhe, mutta korjasin sen

        $ sudo systemctl enable apache2
    
![apacheSTATUskorjattu2024-09-15-191547_759x254_scrot](https://github.com/user-attachments/assets/ab7e6244-e2a5-421c-ad1d-3a1f4aeb1408)

### c) Asenna weppipalvelin omalle virtuaalipalvelimellesi.

Tämän jälkeen toisen reijän palomuuriin

        $ sudo ufw allow 80/tcp

Korvasin Apache palvelimen oletussivut:

        $ echo HEI MAAILMA! KUULUUKO?|sudo tee /var/www/index.html

![OletussivuVaihdettu2024-09-15-192234_655x110_scrot](https://github.com/user-attachments/assets/1f148dc2-f767-48cc-ab61-b67b0657e6ef)

Otin `userdir`n käyttöön ja käynnistin palvelimen uudestaan

        $ sudo a2enmod userdir
        $ sudo systemctl restart apache2

Asensin micro editorin palvelimelle

        $ sudo apt-get install micro

Tein uuden kansion sivua varten

        $ mkdir -p /home/leonardo/public_html/llanga.example.com

Tein myös uuden .html tiedoston kotisivun näkymää varten

        $ micro /home/leonardo/public_html/llanga.example.com/index.html

Tähän tiedostoon kirjoitin HTML/CSS koodia, joka tulee näkymään sivulla llanga.live

Sen jälkeen laitoin sivuston asetukset kuntoon

        $ micro /etc/apache2/sites-available/llanga.example.com.conf

![AsetusTietosto2024-09-15-195054_655x334_scrot](https://github.com/user-attachments/assets/83c5d55e-8d6e-481c-ab5c-3437e6a8c185)

Sen jälkeen otin sivuston käyttöön ja käynnistin apachen uudelleen

        $ sudo a2ensite llanga.example.com.conf
        $ sudo systemctl restart apache2

Tämän jälkeen kokeilin komentoa `curl localhost`, mutta sain virhekoodin 403 HTTP-otsakkeeseen.

![Error403_2024-09-15-195600_655x254_scrot](https://github.com/user-attachments/assets/8c54350e-2e67-464d-be13-9622980ae356)

Etsin lokista tietoa

        $ sudo tail /var/log/apache2/error.log

Josta käy ilmi

        (13)Permission denied: [client 185.191.126.213:56244] AH00035: access 
        to / denied (filesystem path '/home/leonardo/public_html') because 
        search permissions are missing on a component of the path

Syötin virheviestin `(13)Permission denied: [client 185.191.126.213:56244] AH00035: access 
        to / denied (filesystem path '/home/leonardo/public_html') because 
        search permissions are missing on a component of the path` ChatGPT:n, ja vastaus oli

> The error message you shared provides a clear indication that the 403 Forbidden error is related to file system permissions. Specifically, Apache is trying to access /home/leonardo/public_html, but it is encountering a Permission Denied error due to missing search permissions on one of the directories in the path.
>
> Key Details in the Error:
>
>     Permission Denied (Error 13): This means Apache doesn't have permission to access one of the directories in the path leading to /home/leonardo/public_html.
>     Search Permissions: The search (or execute) permission (x on directories) allows Apache to "search" through directories to locate files.
>
> Likely Causes:
>
>     Permissions Issue on Parent Directories: One or more directories in the path (/home, /home/leonardo, or /home/leonardo/public_html) are missing the necessary execute (x) permissions for the web server user (typically www-data on Debian-based systems).
>     Directory Ownership: The directory may not be owned by the correct user, preventing Apache from traversing it.
>
> Solution:
>
> To fix this, you need to ensure that Apache has the necessary permissions on the directory path:
> Step 1: Check Permissions on the Path Components
>
> Run the following command to check the permissions on each directory in the path:
>
>        $ ls -ld /home /home/leonardo /home/leonardo/public_html
>
> This will show the current permissions for each directory in the path.
> Step 2: Grant Execute Permissions on Parent Directories
>
> If the directories `/home` or `/home/leonardo` are missing the `x` (execute) permission, you need to add it:
> 
>        $ chmod o+x /home
>        $ chmod o+x /home/leonardo

Olen tottunut näkemään luku/kirjoitus/execute liittyvissä komennoissa komennon joten kysyin ChatGPT:ltä

`difference between chmod 755 /home/leonardo/public_html and chmod o+x /home/leonardo?`

ChatGPT:

> The two commands you mentioned, chmod 755 /home/leonardo/public_html and chmod o+x /home/leonardo, have different purposes and > affect different parts of the file permissions. Here's the difference:
> 1. chmod 755 /home/leonardo/public_html
> 
> This command modifies the permissions of the /home/leonardo/public_html directory to 755. Here's what it means:
> 
>     7 (rwx): The owner (leonardo) has read, write, and execute permissions.
>     5 (r-x): The group (leonardo) and others (including Apache) have read and execute permissions but cannot write.
>
> So, this command allows everyone (owner, group, and others) to enter and read files in the public_html directory, but only the owner (leonardo) can modify the files.
> 2. chmod o+x /home/leonardo
> 
> This command adds the execute permission only for "others" (including Apache) on the /home/leonardo directory.
>
>    o+x: This gives "others" (anyone who is not the owner or in the group) permission to traverse (execute on directories means "can enter this directory").
>
> This command is necessary because Apache needs to traverse the /home/leonardo directory to reach /home/leonardo/public_html, but it doesn't give Apache permission to read the contents of /home/leonardo itself, which keeps it secure.
> Summary:
>
>     chmod 755 /home/leonardo/public_html: Allows anyone (Apache included) to access and read files within public_html, but only leonardo can modify the contents.
>     chmod o+x /home/leonardo: Grants only the minimal permission needed for Apache to "enter" the /home/leonardo directory and reach public_html, without exposing the contents of /home/leonardo.
> 
> Both permissions are important: 755 on public_html allows Apache to read files there, and o+x on /home/leonardo lets Apache traverse through /home/leonardo to get to public_html.

ChatGPT mukaan chmod o+x /home/leonardo näytti olevan tiukempi sallimaan oikeuksia, ja käytin sitä virheen korjauksessta.

Käynnistin apachen uudelleen, sen jälkeen kun olin syöttänyt ChatGPT:n ehdottamaa komentoa korjaamaan `Error 403`

Kokeilin uudestaan curl komentoa ja sain koodin 200!

Tarkistin että sivu toimii myös selaimen kautta

![kotisivut2024-09-15-214418_1000x727_scrot](https://github.com/user-attachments/assets/80a581da-44f6-4d62-8993-1195c8385283)

Sekä että toimii näkyy asianmukaisesti puhelimessa

![IMG_0411 3](https://github.com/user-attachments/assets/52149d34-8993-45ba-bc88-6224709e990a)

Klo 20:13 olin valmis ja sivu pyörii


## Lähteet
- https://terokarvinen.com/linux-palvelimet/
- https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/
- https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu#step-5-allowing-other-connections
