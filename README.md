# Welcome to FixOurWater

See https://github.com/mysociety/fixmystreet for the original FixMyStreet repo this project is based on.

# Installation instructions (with Mapit)

The following was attempted on Debian Wheezy running in AWS.

## FixMyStreet

```
sudo sed -e 's/$/ non-free/' -i /etc/apt/sources.list

sudo apt-get update

sudo apt-get install -y \
  git \
  sendmail \
  apache2 \
  libapache2-mod-fastcgi \
  lockfile-progs

sudo a2enmod rewrite proxy expires fastcgi headers

sudo sendmailconfig
```

Test that email works with:

```
echo "My test email being sent from sendmail" | /usr/sbin/sendmail myemail@domain.com
```

If you run into file permission issues, see http://askubuntu.com/questions/365087/grant-a-user-permissions-on-www-data-owned-var-www.

Now follow: http://fixmystreet.org/install/manual-install/.

### Notes

Before running `gem install` you might need to run:

```
PATH="`ruby -e 'puts Gem.user_dir'`/bin:$PATH"
```

## MapIt
```
sudo apt-get install -y \
  python-dev \
  python-pip \
  python-psycopg2 \
  binutils \
  libproj-dev \
  gdal-bin \
  apache2 \
  libapache2-mod-wsgi

  sudo pip install virtualenv django
```

Now follow: https://trac.osgeo.org/postgis/wiki/UsersWikiPostGIS20Debian70src.

To set up postgres:

```
sudo -u postgres psql
  CREATE USER mapit WITH PASSWORD 'a1b2c3d4e5' WITH SUPERUSER;
  CREATE DATABASE mapit WITH OWNER mapit;
  \c mapit
  CREATE LANGUAGE plpgsql;
  \q
```

And finally follow: http://mapit.poplus.org/docs/self-hosted/install/.

### Notes

Instead of `./manage.py migrate mapit` try `python ./manage.py migrate`.
