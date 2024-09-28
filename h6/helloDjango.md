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



1. https://www.djangoproject.com/
2. https://en.wikipedia.org/wiki/Django_(web_framework)
3. https://www.tieturi.fi/koulutusala/ohjelmistokehitys/ohjelmoinnin-viitekehykset
4. https://www.linux.fi/wiki/PostgreSQL
5. https://terokarvinen.com/2022/django-instant-crm-tutorial/?fromSearch=django
