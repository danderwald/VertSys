# Installation von saleor

Um saleor zu installieren und einzurichten, muss das Repository von github geklont werden.

    $ git clone git@github.com:mirumee/saleor.git

In den Einstellungen (saleor/settings.py) muss die Datenbank angepasst werden. Dafür werden die Default Einstellungen auskommentiert und mit den MySQL Einstellungen ersetzt.

    # SQLITE_DB_URL = 'sqlite:///' + os.path.join(PROJECT_ROOT, 'dev.sqlite')
    # DATABASES = {'default': dj_database_url.config(default=SQLITE_DB_URL)}
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',
            'HOST': 'IP',
            'NAME': 'DATENBANK_NAME',
            'USER': 'BENUTZER',
            'PASSWORD': 'PASSWORD'
        }
    }

Danach muss man in den saleor Ordner wechseln und das Image mit docker-compose bauen.

    $ cd saleor/
    $ docker-compose build

Wenn dies fertig ist, kann die Datenbank für Django eingerichtet werden. Dafür müssen zuerst die Migrationen eingespielt werden und die Datenbank mit Daten gefüllt werden.

    $ docker-compose run web python manage.py migrate
    $ docker-compose run web python manage.py populatedb --createsuperuser

Um den Shop zu benutzen, werden Pakete installiert, die für die Oberfläche benötigt werden.

    $ docker-compose run web npm install
    $ docker-compose run web grunt

Als vorletzten Schritt werden statische Dateiene (CSS, JS) in einem Ordner gesammelt.

    $ docker-compose run web python manage.py collectstatic

Nun kann man den Shop starten und ihn über die entsprechende IP und Port 8000 erreichen.

    $ docker-compose up
