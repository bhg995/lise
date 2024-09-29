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

Tein [alkutoimet](https://github.com/bhg995/lise/blob/main/h4/maailmaKuulee.md#b-tee-alkutoimet-omalla-virtuaalipalvelimellasi-klo-1850).

Seurasin opettajan ohjeita: Django 4 Instant Customer Database Tutorial. [[5](https://terokarvinen.com/2022/django-instant-crm-tutorial/?fromSearch=django)]

Asensin virtuaaliympäristön palvelintietokoneelle:

    sudo apt-get -y install virtualenv

Tein uuden ympäristön Djangoa varten:

    virtualenv --system-site-packages -p python3 env/

![Näyttökuva 2024-9-28 kello 11 53 09](https://github.com/user-attachments/assets/4028c7e0-8b8d-4c07-aa55-a3e3d4b03821)

Nyt minulla oli uusi kansio `env/`, jossa tarvittavat paketit. Otin uuden ympäristön käyttöön komennolla:

    source env/bin/activate

Käyttäjätunnukseni edessä lukee (env), käytän eri ympäristöä.

![Näyttökuva 2024-9-28 kello 11 56 58](https://github.com/user-attachments/assets/d974dc28-2de8-4836-9d4b-06098f4d28c0)

    which pip
    /home/leonardo/env/bin/pip

Minulla oli jo Micro editori, versio `2.0.11`

Tein microdokumentti requirements.txt, kirjoitin  `django`, ja tallensin sen virtuaaliympäristöön

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

Tässä vaiheessa en ollut varma että toimiiko Django niinkuin pitäisi.

Sain osoitteen `http://127.0.0.1:8000/` josta olisin voin tarkistaa selaimella, mutta käytän Djangoa palvelimen kautta. Curl komennolla pitäisi näkyä että näkyykö sivu, mutta saan virheviestin:

    curl: (7) Failed to connect to 127.0.0.1 port 8000 after 0 ms: Couldn't connect to server

Klo 13:05 otan taukoa, ja palaan myöhemmin kokeilemaan eri keinoja, joilla saisin Django käynnistymään oikein.

Klo 15:55 aloitin uudelleen.

Päätin yrittää Djangon käynnistystä paikallisesti, Raspberry Pi -tietokoneella.

Aloitin käymällä läpi seuraavat sivut

- https://docs.djangoproject.com/en/5.1/intro/tutorial01/
- https://pimylifeup.com/raspberry-pi-django/

Seurasin opettajan ohjeita uudelleen. Käynnistys näytti onnistuvan.

    ./manage.py runserver
    
    Watching for file changes with StatReloader
    Performing system checks...

    System check identified no issues (0 silenced).

    You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
    Run 'python manage.py migrate' to apply them.
    September 27, 2024 - 17:29:11
    Django version 5.1.1, using settings 'folder.settings'
    Starting development server at http://127.0.0.1:8000/
    Quit the server with CONTROL-C.

Selaimessa kuitenkin:

![Näyttökuva _1](https://github.com/user-attachments/assets/5b952b1b-4de3-4424-8248-adc17445e861)

Lopetin 17:35

Tulin illemmalla takaisin, kokeilin vielä kerran Djangon käyttöönottoa onnistumatta.

Päätin aloittaa tyhjältä pöydältä.

Poistin Djangon, sille luomani ympäristön ja Apachen. Epäilin että Apachella olisi vaikutusta.

Sitten kokeilin uudestaan, seuraamalla opettajan ohjeita.

![Näyttökuva ](https://github.com/user-attachments/assets/9c330bf9-1e7c-4f0d-85d1-55bb90c0609f)

![Näyttökuva 2](https://github.com/user-attachments/assets/ab17daf1-ee9d-4b05-b9f0-68f3c2c89ff8)

![Näyttökuva 3](https://github.com/user-attachments/assets/d4488fdb-59bc-4f55-9116-a048ba5dfa01)

Kello 0:11 Djangon raketti näkyi selaimella.

**CRM** 

![Näyttökuva 4](https://github.com/user-attachments/assets/9fe2af18-29f8-4a57-b558-269d77d6d303)

Tässä välissä tein käyttäjän `leonardo`

![Näyttökuva 5](https://github.com/user-attachments/assets/269d389c-e828-424f-a044-d8cdc0a3caa7)

Lisäsin `settings.py` tiedostoon rivin `'crm'`

`models.py` tiedostoon lisäsin python koodin:

    from django.db import models
    
    class Customer(models.Model):
        name = models.CharField(max_length=160)

        def __str__(self):		# new
            return self.name	# new

`admin.py` tiedostoon:

    from django.contrib import admin
    from . import models

    admin.site.register(models.Customer)

Yritin käynnistää Djangon, mutta sain virheviestin `Error: that port is already in use`

Hain tietoa Googlesta, ja löysin ohjeen miten sulkea käynnissä olevat portit.

> A more simple solution just type sudo fuser -k 8000/tcp. This should kill all the processes associated with port 8000.

> EDIT:

> For osx users you can use sudo lsof -t -i tcp:8000 | xargs kill -9

> edited Nov 17, 2015 at 12:49
> answered Nov 27, 2013 at 10:53

> [Stackoverflow.com](https://stackoverflow.com/questions/20239232/django-server-error-port-is-already-in-use), [Mounir](https://stackoverflow.com/users/935241/mounir)

Kokeilin mitkä portit ovat estämässä. Vahingossa suljin selaimen, mutta samalla varmistuin että syntaksi toimii:

![Näyttökuva 6](https://github.com/user-attachments/assets/f3135e0c-9089-4db3-8d31-8568e036b1d9)


[[7](https://stackoverflow.com/questions/20239232/django-server-error-port-is-already-in-use)] [[8](https://man7.org/linux/man-pages/man2/kill.2.html)]

![Näyttökuva 7](https://github.com/user-attachments/assets/662b118d-2e08-40ed-b8e5-6a07bdc78f27)

![Näyttökuva 8](https://github.com/user-attachments/assets/e3b7ee7e-fe11-4ead-9daf-7335fdc45019)

![Näyttökuva 10](https://github.com/user-attachments/assets/1ff9ffc8-b0b9-438d-bee4-d7689d44cd74)



1. https://www.djangoproject.com/
2. https://en.wikipedia.org/wiki/Django_(web_framework)
3. https://www.tieturi.fi/koulutusala/ohjelmistokehitys/ohjelmoinnin-viitekehykset
4. https://www.linux.fi/wiki/PostgreSQL
5. https://terokarvinen.com/2022/django-instant-crm-tutorial/?fromSearch=django
6. https://terokarvinen.com/2022/django-instant-crm-tutorial/
7. https://stackoverflow.com/questions/20239232/django-server-error-port-is-already-in-use
8. https://man7.org/linux/man-pages/man2/kill.2.html
