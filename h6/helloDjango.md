# Hello Django

## [Django](https://www.djangoproject.com/)

"_Django is a high-level Python web framework that encourages rapid development and clean, pragmatic design. Built by experienced developers, it takes care of much of the hassle of web development, so you can focus on writing your app without needing to reinvent the wheel. It’s free and open source._" - Django [[1](https://www.djangoproject.com/)]

"_Django is a free and open-source, Python-based web framework that runs on a web server. It follows the model–template–views architectural pattern. It is maintained by the Django Software Foundation, an independent organization established in the US as a 501 non-profit._" - Wikipedia [[2](https://en.wikipedia.org/wiki/Django_(web_framework))]

Avoimeen lähteeseen perustuva Django on web-kehys joka toimii Pythonilla. Django on helppo käyttää ja ottaa käyttöön, ja Django tarjoaa kaiken mahdollisen tarvittavan ohjelmiston tai web-sovelluksen kehitykseen. [[3](https://www.tieturi.fi/koulutusala/ohjelmistokehitys/ohjelmoinnin-viitekehykset/)]

## [PostgreSQL](https://www.postgresql.org/)

"_PostgreSQL (pgsql) on SQL-kieltä tukeva avoimen lähdekoodin tietokantamoottori._" - Linux.fi-wiki [[4](https://www.linux.fi/wiki/PostgreSQL)]

# Tehtävät

## a) Tee yksinkertainen esimerkkiohjelma Djangolla.

Aloitin tehtävän la 28.9 klo 11:25

Minulla oli tehtävää varten valmiina virtuaalinen palvelin.

Olin jo valmiiksi tehnyt käyttäjän sudo-oikeuksilla, päivittänyt palvelimen root sekä käyttäjän komentokehotteesta, sulkenut root käyttäjän sekä asentanut palomuurin ja tehnyt reijät portteihin 22 ja 80.

Aloitin seuraamalla opettajan ohjeita: Django 4 Instant Customer Database Tutorial. [[5](https://terokarvinen.com/2022/django-instant-crm-tutorial/?fromSearch=django)]

Asensin virtuaaliympäristön palvelintietokoneelle:

    sudo apt-get -y install virtualenv

Tein uuden ympäristön Djangoa varten

    virtualenv --system-site-packages -p python3 env/

![Näyttökuva 2024-9-28 kello 11 53 09](https://github.com/user-attachments/assets/4028c7e0-8b8d-4c07-aa55-a3e3d4b03821)

Nyt minulla oli uusi kansio `env/`, jossa on uusimmat paketit. Otin virtuaalisen ympäristön käyttöön komennolla:

    source env/bin/activate

Nyt käyttäjätunnukseni edessä lukee (env).

![Näyttökuva 2024-9-28 kello 11 56 58](https://github.com/user-attachments/assets/d974dc28-2de8-4836-9d4b-06098f4d28c0)

    which pip
    -> /home/leonardo/env/bin/pip

Minulla oli jo Micro editori, versio `2.0.11`

Tein microdokumentti requirements.txt ja kirjoitin siihen `django` ja tallensin sen virtuaaliympäristöön

Sen jälkeen komento:

    pip install -r requirements.txt

Sain ladattua djangon

![Näyttökuva 2024-9-28 kello 12 11 13](https://github.com/user-attachments/assets/1b63967e-7b2e-4dd7-a0f3-5874379144af)

![Näyttökuva 2024-9-28 kello 12 18 30](https://github.com/user-attachments/assets/8d1e14bc-497b-44c0-93e3-595b32633733)

![Näyttökuva 2024-9-28 kello 12 26 55](https://github.com/user-attachments/assets/549a2d48-cbab-42fb-9691-14937bed6c98)

### Tietokanta

![Näyttökuva 2024-9-28 kello 12 27 57](https://github.com/user-attachments/assets/3f62a1ce-a272-49ad-a5fd-8afcc3d982c9)

![Näyttökuva 2024-9-28 kello 12 25 58](https://github.com/user-attachments/assets/dfcee407-998b-45f9-881a-c94081fb9b2a)

    micro crm/models.py

Lisäsin models.py esimerkkikoodia opettajan esimerkistä:

    from django.db import models

    class Customer(models.Model):
        name = models.CharField(max_length=160)

        def __str__(self):		
            return self.name	

Lähde terokarvinen.com. [[6](https://terokarvinen.com/2022/django-instant-crm-tutorial/)]

    ./manage.py makemigrations
    ./manage.py migrate

![Näyttökuva 2024-9-28 kello 12 41 03](https://github.com/user-attachments/assets/ac481f01-48ed-4da0-83e4-7854f4feacd9)

Rekisteröin tietokannan:

    micro crm/admin.py
    
ja lisäsin tiedostoon seuraavan pätkän:

    admin.site.register(models.Customer)

Lähde terokarvinen.com. [[6](https://terokarvinen.com/2022/django-instant-crm-tutorial/)]

Olin lukenut opettajan ohjeet loppuun, tässä vaiheessa halusin kokeilla mitä sain aikaiseksi.

Käytin komentoa:

    ./manage.py runserver

Sain virheviestin

![Näyttökuva 2024-9-28 kello 12 51 07](https://github.com/user-attachments/assets/64b9f6ed-29e2-417e-ad9b-32918036c00d)

        admin.site.register(models.Customer)
                        ^^^^^^
        NameError: name 'models' is not defined

Tämä oli helppo korjata, koodipätkä on tiedostossa `crm/admin.py`. Koodista puuttui `from . import models`. Lisäsin sen 

    from django.contrib import admin
    from . import models

    admin.site.register(models.Customer)

Tarkistin uudelleen:

    ./manage.py runserver

Sain tulokseksi:

![Näyttökuva 2024-9-28 kello 13 02 21](https://github.com/user-attachments/assets/db5b6237-8bfd-4800-bbb8-b075264bce5a)

Tässä vaiheessa en voinut varmistua että toimiiko Django ja sovellus niinkuin pitäisi.

Sain osoitteen `http://127.0.0.1:8000/` josta olisin voin tarkistaa selaimella, mutta käytän Djangoa palvelimen kautta. Curl komennolla pitäisi näkyä että näkyykö sivu, mutta saan virheviestin:

    curl: (7) Failed to connect to 127.0.0.1 port 8000 after 0 ms: Couldn't connect to server

Klo 13:05 otan taukoa, ja palaan myöhemmin kokeilemaan eri keinoja saada Django toimimaan juuri kuten haluan.


1. https://www.djangoproject.com/
2. https://en.wikipedia.org/wiki/Django_(web_framework)
3. https://www.tieturi.fi/koulutusala/ohjelmistokehitys/ohjelmoinnin-viitekehykset
4. https://www.linux.fi/wiki/PostgreSQL
5. https://terokarvinen.com/2022/django-instant-crm-tutorial/?fromSearch=django
6. https://terokarvinen.com/2022/django-instant-crm-tutorial/
