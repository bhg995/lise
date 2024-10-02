# Hello Django

## [Django](https://www.djangoproject.com/)

"_Django is a high-level Python web framework that encourages rapid development and clean, pragmatic design. Built by experienced developers, it takes care of much of the hassle of web development, so you can focus on writing your app without needing to reinvent the wheel. It’s free and open source._" - Django [[1](https://www.djangoproject.com/)]

"_Django is a free and open-source, Python-based web framework that runs on a web server. It follows the model–template–views architectural pattern. It is maintained by the Django Software Foundation, an independent organization established in the US as a 501 non-profit._" - Wikipedia [[2](https://en.wikipedia.org/wiki/Django_(web_framework))]

Avoimeen lähteeseen perustuva Django on web-kehys joka toimii Pythonilla. Django on helppo käyttää ja ottaa käyttöön, ja Django tarjoaa kaiken mahdollisen tarvittavan ohjelmiston tai web-sovelluksen kehitykseen. [[3](https://www.tieturi.fi/koulutusala/ohjelmistokehitys/ohjelmoinnin-viitekehykset/)]

## [PostgreSQL](https://www.postgresql.org/)

"_PostgreSQL (pgsql) on SQL-kieltä tukeva avoimen lähdekoodin tietokantamoottori._" - Linux.fi-wiki [[4](https://www.linux.fi/wiki/PostgreSQL)]

# Laitteisto

- Näyttö: AOC G2490VXA, 24" QHD(1440p), 144Hz
- Raspberry Pi 4 model B 4 Gt
- Käyttöjärjestelmä: Raspberry Pi OS 32bit kernel (based on Debian)
- CPU: Broadcom BCM2711 SoC with a 1.8 GHz 64-bit quad-core ARM Cortex-A72 processor, with 1 MB shared L2 cache.
- Näytönohjain: Broadcom VideoCore VI @ 500 MHz
- Muisti: 4 Gt
- Tallennustila: 32 Gt

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

Koodipätkä on tiedostossa `crm/admin.py`. Koodista puuttui `from . import models`. Lisäsin sen 

    from django.contrib import admin
    from . import models

    admin.site.register(models.Customer)

Tarkistin uudelleen:

    ./manage.py runserver

Sain tulokseksi:

![Näyttökuva 2024-9-28 kello 13 02 21](https://github.com/user-attachments/assets/db5b6237-8bfd-4800-bbb8-b075264bce5a)

Tässä vaiheessa en ollut varma että toimiiko Django niinkuin pitäisi.

    curl -s localhost|grep title # access without GUI

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

Lopetin 28.9 17:35

Tulin illemmalla takaisin, kokeilin vielä kerran Djangon käyttöönottoa onnistumatta.

Päätin aloittaa tyhjältä pöydältä.

Poistin Djangon, sille luomani ympäristön ja Apachen. Epäilin että Apachella olisi vaikutusta. # https://stackoverflow.com/questions/30670759/run-django-without-apache-using-runserver-on-port-80-and-accessible-outside-lan

Sitten kokeilin uudestaan, seuraamalla opettajan ohjeita.

![Näyttökuva ](https://github.com/user-attachments/assets/9c330bf9-1e7c-4f0d-85d1-55bb90c0609f)

![Näyttökuva 2](https://github.com/user-attachments/assets/ab17daf1-ee9d-4b05-b9f0-68f3c2c89ff8)

![Näyttökuva 3](https://github.com/user-attachments/assets/d4488fdb-59bc-4f55-9116-a048ba5dfa01)

29.9 klo 0:11 Djangon raketti näkyi selaimella.

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

[[7](https://stackoverflow.com/questions/20239232/django-server-error-port-is-already-in-use)] [[8](https://man7.org/linux/man-pages/man2/kill.2.html)]

Kokeilin mitkä portit ovat estämässä. Vahingossa suljin selaimen, mutta samalla varmistuin että syntaksi toimii:

![Näyttökuva 6](https://github.com/user-attachments/assets/f3135e0c-9089-4db3-8d31-8568e036b1d9)

![Näyttökuva 7](https://github.com/user-attachments/assets/662b118d-2e08-40ed-b8e5-6a07bdc78f27)

![Näyttökuva 8](https://github.com/user-attachments/assets/e3b7ee7e-fe11-4ead-9daf-7335fdc45019)

![Näyttökuva 10](https://github.com/user-attachments/assets/1ff9ffc8-b0b9-438d-bee4-d7689d44cd74)

CRM toimii. Selailin Djangoa ja lisäsin uuden käyttäjän.

## b) Tee Djangon tuotantotyyppinen asennus

Aloitin klo 29.9 22.24. Seuraan opettajan [ohjeita](https://terokarvinen.com/2022/deploy-django/)

Päivitin koneen ja käynnistän Apachen.

    sudo apt-get update
    sudo systemctl start apache2

Tein uuden kansion:

    mkdir -p publicwsgi//tuotantoDjango/static/

Valmistelin `.html` tiedoston:

    echo "Statically see you at llanga.live."|tee publicwsgi/tuotantoDjango/static/index.html


Lisäsin konfiguraatioasetuksiin polun

    Alias /static /home/uhse/publicwsgi/tuotantoDjango/static/
    <Directory /home/uhse/publicwsgi/tuotantoDjango/static/>
        Require all granted
    </Directory>

Sivuasetukset:

    sudo a2dissite 000-default.conf 
    sudo a2ensite llanga.live.conf
    
![Näyttökuva 2024-9-29 kello 23 14 09](https://github.com/user-attachments/assets/f065c5a8-18ec-4d56-9e02-5a2aa40ee65d)

![Näyttökuva 2024-9-29 kello 23 14 53](https://github.com/user-attachments/assets/5d50d535-4bc6-4355-af41-2eafd97328cf)

**Django virtuaaliympäristön asennus**

    echo "Statically see you at llanga.live."|tee publicwsgi/tuotantoDjango/static/index.html
    cd publicwsgi/
    virtualenv -p python3 --system-site-packages env
    source env/bin/activate

Pääsin virtuaaliympäristöön, josta pääsin asentamaan Djangon.

    pip install -r requirements.txt

    Successfully installed django-4.2.16

Sitten aloitin Django projektin:

    django-admin startproject tuotantoDjango
    micro /etc/apache2/sites-available/llanga.live.conf

Muokkasin opettajan esimerkkiä ja vaihdoin kansion nimen, sekä polun:

    Define TDIR /home/uhse/publicwsgi/tuotantoDjango
    Define TWSGI /home/uhse/publicwsgi/tuotantoDjango/wsgi.py
    Define TUSER uhse
    Define TVENV /home/uhse/publicwsgi/env/lib/python3.9/site-packages


    <VirtualHost *:80>
        Alias /static/ ${TDIR}/static/
        <Directory ${TDIR}/static/>
                Require all granted
        </Directory>

        WSGIDaemonProcess ${TUSER} user=${TUSER} group=${TUSER} threads=5 python-path="${TDIR}:${TVENV}"
        WSGIScriptAlias / ${TWSGI}
        <Directory ${TDIR}>
             WSGIProcessGroup ${TUSER}
             WSGIApplicationGroup %{GLOBAL}
             WSGIScriptReloading On
             <Files wsgi.py>
                Require all granted
             </Files>
        </Directory>

    </VirtualHost>

    Undefine TDIR
    Undefine TWSGI
    Undefine TUSER
    Undefine TVENV

Apachen moduuli virtuaaliympäristössä:

    sudo apt-get -y install libapache2-mod-wsgi-py3
    /sbin/apache2ctl configtest

![Näyttökuva 2024-9-29 kello 23 39 58](https://github.com/user-attachments/assets/596af884-552a-49a0-b9c9-7d0d20e3ed20)

    sudo systemctl restart apache2
    curl -s localhost|grep title

Virhe:

    <title>404 Not Found</title>

Tarkistin lokista:

    sudo tail -f /var/log/apache2/error.log

Loki:

    Mon Sep 30 00:10:04.536650 2024] [wsgi:error] [pid 4838:tid 4847] [client ::1:59554] Target WSGI script not found or unable to stat: /home/uhse/publicwsgi/tuotantoDjango/wsgi.py
    [Mon Sep 30 00:12:11.162752 2024] [wsgi:error] [pid 4838:tid 4852] [client 127.0.0.1:44910] Target WSGI script not found or unable to stat: /home/uhse/publicwsgi/tuotantoDjango/wsgi.py

Tarkemmin:

    Target WSGI script not found or unable to stat: /home/uhse/publicwsgi/tuotantoDjango/wsgi.py

Eli Django ei päässyt käsiksi `wsgi.py` tiedostoon. Tarkistin missä tiedosto on -> /home/uhse/publicwsgi/tuotantoDjango/tuotantoDjango/wsgi.py.

Ajoin `django-admin startproject` komennon _tuotantoDjango_ kansion sisällä, joka loi uuden samannimisen kansion , jossa kyseinen tiedosto oli.

Kävin vaihtamassa `.conf` tiedostossa poluksi /home/uhse/publicwsgi/tuotantoDjango/tuotantoDjango/wsgi.py.

![Näyttökuva 2024-9-30 kello 0 29 48](https://github.com/user-attachments/assets/4f97f94c-af01-49b1-af95-b9c3600d2d3e)

![Näyttökuva 2024-9-30 kello 0 31 53](https://github.com/user-attachments/assets/3e20100d-d511-4025-bd88-4cdc212154a5)

Django käynnistyi.

Debug ottaminen pois käytöstä. Näin rikolliset tai muut eivät pääse näkemään tarkasti virheviestejä.

    micro tuotantoDjango/settings.py

Vaihdoin `ALLOWED_HOSTS` muuttujan `True`:ksi

    ALLOWED_HOSTS = ["localhost", "llanga.live"]

Sekä lisäsin:

    import os

ja:

    STATIC_ROOT = os.path.join(BASE_DIR, 'static/')

Sen jälkeen:

    touch tuotantoDjango/wsgi.py
    sudo systemctl restart apache2

![Näyttökuva 2024-9-30 kello 0 38 59](https://github.com/user-attachments/assets/c5e47f6a-1a3c-46ef-b1f0-da6867b5ef58)

![Näyttökuva 2024-9-30 kello 0 59 08](https://github.com/user-attachments/assets/1c8942a1-88bf-440c-be99-dde8767923dd)

Tein uuden käyttäjän `leonardo`, jotta pääsen käyttämään Djangoa.

![Näyttökuva 2024-9-30 kello 1 01 01](https://github.com/user-attachments/assets/814ce177-1bef-4569-befa-52f602a1857c)

Klo 01:00 tuotantotyyppinen Django oli valmis

![Näyttökuva 2024-9-30 kello 1 03 14](https://github.com/user-attachments/assets/d7abc332-7473-4f21-b8c7-822b097eb991)

## PostgreSQL

Tehtävä osoittautui hankalaksi, ja kokeilin CHATGPT.

Prompt:

> PostgreSQL käyttöönotto Djangossa (env) ympäristössä

Vastauksena sain ohjeet:

Asenna psycopg2-kirjasto, joka mahdollistaa Djangon yhteyden PostgreSQL:ään:

    pip install psycopg2

Avaa projektisi settings.py-tiedosto ja muuta tietokantakonfiguraatiota PostgreSQL:ksi :

    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql',
            'NAME': 'your_db_name',
            'USER': 'your_db_user',
            'PASSWORD': 'your_db_password',
            'HOST': 'localhost',  # tai '127.0.0.1'
            'PORT': '5432',       # Oletusportti
        }
    }

Siirry PostgreSQL komentoikkunaan:

    sudo -u postgres psql

Luo uusi tietokanta:

    CREATE DATABASE your_db_name;
    CREATE USER your_db_user WITH PASSWORD 'your_db_password';
    ALTER ROLE your_db_user SET client_encoding TO 'utf8';
    ALTER ROLE your_db_user SET default_transaction_isolation TO 'read committed';
    ALTER ROLE your_db_user SET timezone TO 'UTC';
    GRANT ALL PRIVILEGES ON DATABASE your_db_name TO your_db_user;

Poistu PostgreSQL-komentoriviltä:

    \q

Luo malleja models.py-tiedostoon ja suorita migraatiot:

    # myapp/models.py
    from django.db import models

    class MyModel(models.Model):
        name = models.CharField(max_length=100)
        value = models.IntegerField()

Suorita seuraavat komennot:

    python manage.py makemigrations
    python manage.py migrate

Avaa Python shell Djangossa ja testaa tietojen tallentamista:

    python manage.py shell

    from myapp.models import MyModel

    # Luo uusi objekti
    obj = MyModel(name='Test', value=123)
    obj.save()  # Tallenna tietokantaan

Voit tarkistaa tiedot PostgreSQL komentoikkunasta:

    sudo -u postgres psql your_db_name
    SELECT * FROM myapp_mymodel;  -- Varmista, että objekti tallentui

-------------CHATGPT vastaus loppuu -----------

<br>

![Näyttökuva 2024-9-30 kello 2 13 52](https://github.com/user-attachments/assets/c47bfeef-64e6-4c10-9707-53d889f9c623)

settings.py

![Näyttökuva 2024-9-30 kello 2 03 04](https://github.com/user-attachments/assets/95acbeca-402b-4052-99c4-7aa23ef8c2d5)

./manage.py migrate

![Näyttökuva 2024-9-30 kello 2 39 42](https://github.com/user-attachments/assets/6620fcbd-49a9-4862-9e45-25cbd5d74b79)

Huomasin että PostgreSQL sisällä komentojen käyttö oli vaikeata, sain usein syntaksivirheitä. Epäonnistuin luomaan käyttäjän oikealla tavalla, josta tuli myöhemmin virheitä kun yritin ajaa komennon `./manage.py migrate`. Esim. 

        psycopg2. OperationalError: FATAL: password authentication dailed for user "leonardo" 
        FATAL: password authentication failed for user "leonardo"

[[9](https://pimylifeup.com/raspberry-pi-postgresql/)] [[10](https://www.postgresql.org/docs/current/user-manag.html)]

Näin että ongelma oli salasanassa, mutta muuten PostgreSQL pitäisi toimia. Yritän kokeilla myöhemmin uudelleen.

Lopetin klo 30.9 02:40

**PÄIVITYS 2.10.2024 klo 16:50**

Yritin saada PostgreSQL-tietokannan toimimaan Djangossa, ennen tuntia. En ymmärtänyt missä vika oli, vaihdoin `settings.py`-tiedostossa salasanan, olin jo kokeillut ilman salasanaa sekä salasanalla, jota varmasti käytin luodessani käyttäjän.

Ei onnistunut, sain edelleen saman virheviestin:

    django.db.utils.OperationalError: FATAL:  password authentication failed for user "leonardo"
    FATAL:  password authentication failed for user "leonardo"

Kirjoitin saman virheviestin googleen, poistin oman käyttäjänimen ja kansionimen. Löysin [StackOverFlow:sta](https://stackoverflow.com/questions/43060857/postgresql-fatal-password-authentication-failed-for-user-douglas) vastaavan kysymyksen. Ensimmäinen vastaaja ehdotti salasanan vaihtamista PostgreSQL:ssä, kokeilin sitä ensin myös:

![Näyttökuva 2024-10-2 kello 17 24 24](https://github.com/user-attachments/assets/f0b2555d-b567-4238-9a5a-b2fbaefbbd54)

[[11](https://stackoverflow.com/questions/43060857/postgresql-fatal-password-authentication-failed-for-user-douglas)]

Suljin tietokannan, ja kokeilin `./manage.py makemigrations` uudelleen, ja sain saman virhekoodin. Tämä ei kuitenkaan toiminut, sillä syntaksini oli väärä.

Tietokantojen komennoissa, oikeinkirjoitus ja `;` merkki ovat tärkeitä. 

SQL- harjoituksista oli jo vähän aikaa, ja ennenkuin tajusin edes virhettä. Päätin poistaa käyttäjän.

Mieleeni tuli poistaa kyseinen käyttäjä, ja luoda uusi. Näin voisin ainakin saada tietokannan toimimaan.

Etsin tietoa googlesta hakemalla:

    Google: how to delete users in postgres

Löysin PosgreSQL: sivuilta `dropuser` komennon, mutta ihmettelin syntaksia, komennot olivat kirjoitettu pienellä. 
[[12](https://www.postgresql.org/docs/current/app-dropuser.html)]

Avasin uudelleen tietokannan ja yritin poistaa käyttäjän `leonardo`:

![Näyttökuva 2024-10-2 kello 17 29 03](https://github.com/user-attachments/assets/8095791c-b2e5-4373-8d60-73daa5c7499a)

Ensin oli syntaksivirheitä, sain ne korjattua. 

Toiseksi, en voinut poistaa käyttäjää koska siihen oli sidottu koko tietokanta. 

Samasta kysymysketjusta löysin

    What worked for me on AWS RDS (PostgreSQL 13) is the following:

    REVOKE ALL PRIVILEGES ON DATABASE <my_db> FROM <my_user>;

    I also had a similar error where the role was owner for tables so it couldn't be dropped, had to re-assign table owner with:

    ALTER TABLE <my_table> OWNER TO <trusted_role>;

    In fact, on RDS, AWS doesn't give you full superuser to your master user, so the following REASSIGN command fails:

    REASSIGN OWNED BY <olduser> TO <newuser>;

    edited May 6 at 11:34
    Eddie C.'s user avatar
    Eddie C.
    9961010 silver badges1818 bronze badges
    answered Sep 16, 2021 at 19:48
    Andrew's user avatar
    Andrew

Peruin `leonardo`-käyttäjän oikeudet, jonka jälkeen järjestelmä suostui poistamaan käyttäjän. Tarkistin vielä käyttäjän komennolla `\du`

Käyttäjä oli poistunut onnistuneesti. Nyt voisin kokeilla uudestaan tietokannan käyttöönottoa.

Päätin jatkaa myöhemmin, koska tunti oli alkanut jo.

**Tunnin aikana tein seuraavan:**

Tein käyttäjän uudelleen, käytin samaa käyttäjänimeä ja salasanaa, joten `settings.py`-tiedostoa ei tarvinnut muokkaa.

![Näyttökuva 2024-10-2 kello 19 12 02](https://github.com/user-attachments/assets/f637d602-fb9b-4caf-ab30-aa210c69bc87)

Tällä kertaa Django käynnistyi OK, mutta sain virhekoodin `[02/Oct/2024 16:09:09] "GET / HTTP/1.1" 400 143` kun yritin avata selaimella.

![Näyttökuva 2024-10-2 kello 19 17 04](https://github.com/user-attachments/assets/b23d556e-acb9-4e9f-91a3-522cf973bcf2)



1. https://www.djangoproject.com/
2. https://en.wikipedia.org/wiki/Django_(web_framework)
3. https://www.tieturi.fi/koulutusala/ohjelmistokehitys/ohjelmoinnin-viitekehykset
4. https://www.linux.fi/wiki/PostgreSQL
5. https://terokarvinen.com/2022/django-instant-crm-tutorial/?fromSearch=django
6. https://terokarvinen.com/2022/django-instant-crm-tutorial/
7. https://stackoverflow.com/questions/20239232/django-server-error-port-is-already-in-use
8. https://man7.org/linux/man-pages/man2/kill.2.html
9. https://pimylifeup.com/raspberry-pi-postgresql/
10. https://www.postgresql.org/docs/current/user-manag.html
11. https://stackoverflow.com/questions/43060857/postgresql-fatal-password-authentication-failed-for-user-douglas
12. https://www.postgresql.org/docs/current/app-dropuser.html
