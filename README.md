# AcePower Backend API

## Pre


```sh

# setup timezone in mysql, just change the `mysql` database
# https://stackoverflow.com/questions/21351251/database-returned-an-invalid-value-in-queryset-dates
mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql -D mysql -u root -p 
mysql -u root -p -e "flush tables;" mysql 


# setup the db
mysql -u root

CREATE DATABASE `acepower` CHARACTER SET utf8 COLLATE utf8_general_ci;
GRANT ALL ON `acepower`.* TO `acepower`@`localhost` IDENTIFIED BY 'acepower';
FLUSH PRIVILEGES;

# setup pyenv
pyenv virtualenv --copies 3.6.1 acepower

# install python libs
pip install -r requirements.txt

# setup model migration
python manage.py makemigrations
python manage.py migrate

# run it
python manage.py runserver 0.0.0.0:8090

# create login user
python manage.py createsuperuser

# open browser to test
open http://0.0.0.0:8090/

# http://django-reversion.readthedocs.io/en/latest/commands.html
# everytime registering a new model with django-reversion.
./manage.py createinitialrevisions
./manage.py createinitialrevisions your_app.YourModel --comment="Initial revision."

# should be in a crontab

./manage.py deleterevisions
# keep any changes from last 30 days
./manage.py deleterevisions your_app.YourModel --days=30
# keep 30 most recent changes for each item.
./manage.py deleterevisions your_app.YourModel --keep=30
# Keep anything from last 30 days and at least 3 from older changes.
./manage.py deleterevisions your_app.YourModel --keep=3 --days=30

# for oscar data fixtures trial
python manage.dev.py oscar_import_catalogue fixtures/*.csv
python manage.dev.py oscar_import_catalogue_images fixtures/images.tar.gz 
python manage.dev.py loaddata fixtures/*.json

# for ssh remote port forwarding
# https://gist.github.com/ace-han/8450817eecf868f086b59728d7ab62c5

# execute below command in local machine

ssh -fNTg -R 8090:localhost:8090 tinaam@tinaam.com

# this means 
# tinaam.com:8090 will redirect all dataflow to localhost:8090
```