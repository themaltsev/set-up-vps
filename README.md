# DEBIAN VPS SET UP NGINX 1.18.* HTTP2 HTTPS PHP 7.4*   PYTHON 3.9.* LAST MYSQL PHPMYADMIN POSTGRESQL PHPPGADMIN  DJANGO 3.1.* GUICONR VENV



Проверяем обновы
apt update

Обновляем пакеты
apt upgrade


#СМЕНА ПАРОЛЯ
passwd 


#locale
#убеждаемся что отсутствует русский язык
#Устанавливаем поддержку русского языка

apt-get install locales
locale-gen ru_RU.UTF-8

LANG="ru_RU.UTF-8"
после чего запускаем:

dpkg-reconfigure locales
Выбираем русский язык и другие параметры

apt-get install console-cyrillic
Выполняем настройку языкового пакета:

dpkg-reconfigure console-cyrillic


Если в PuTTy язык не сменился на русский попробуйте выполнить команду:
export LC_ALL=ru_RU.UTF-8
export LANG=ru_RU.UTF-8



##### Мониторинг сервера 
apt install htop -y


##### АВТОЗАГРУЗКА 

apt install rcconf


apt install curl wget nano git  tree -y

####last NODE JS ####

apt-get install curl software-properties-common
curl -sL https://deb.nodesource.com/setup_15.x | bash


# Не обязательно Красивый шел для консоли Install oh-my-zsh:

apt install zsh -y

sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"


apt-get install -y redis-server nginx zlib1g-dev libbz2-dev libreadline-dev llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev liblzma-dev python3-dev python-imaging python3-lxml libxslt-dev python-libxml2 python-libxslt1 libffi-dev libssl-dev python-dev gnumeric libsqlite3-dev libpq-dev libxml2-dev libxslt1-dev libjpeg-dev libfreetype6-dev libcurl4-openssl-dev supervisor

######--APACHE2--#########

apache2/ports.conf *:9000

000-default.conf

<VirtualHost *:9000>
ServerAdmin webmaster@localhost
DocumentRoot /var/www/back
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>


Убедитесь, что веб-сервер прослушивает нужный порт:

netstat -tlpn

Вывод команды должен выглядеть так:

Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      2498/sshd
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      8376/nginx: master
tcp6       0      0 :::22                   :::*                    LISTEN      2498/sshd
tcp6       0      0 :::9000                 :::*                    LISTEN      8042/apache2


/etc/php/7.0/apache2/php.ini
Шаг - 2: теперь нужно увеличить значения ниже в файле php.ini .

memory_limit = 1500MB

post_max_size = 1500MB

upload_max_filesize = 1500MB



######--APACHE2--#########


##########-NGINX-##########

###### Инсталлер nginx c модулями https://github.com/angristan/nginx-autoinstall


$ wget https://raw.githubusercontent.com/angristan/nginx-autoinstall/master/nginx-autoinstall.sh
chmod +x nginx-autoinstall.sh
./nginx-autoinstall.sh

./configure --prefix=$PWD --build="quiche-$(git --git-dir=../quiche/.git rev-parse --short HEAD)"  --with-http_v3_module --with-quiche=../quiche --with-openssl=../quiche/deps/boringssl --with-http_v2_module --with-http_ssl_module

#nginx.conf


user  www-data;
worker_processes  3; КОЛВО ЯДЕР *2 +1

ДОБАВИМ ПАПКУ БЕЗ ВСЯКИХ .CONF И БЕЗ ВСЯКИХ ССЫЛОК
include /etc/nginx/configs/*;

apt install ca-certificates apt-transport-https 

Add the following line to /etc/apt/sources.list:
deb https://nginx.org/packages/debian/ stretch nginx
Install GPG key of the repository:

wget https://nginx.org/keys/nginx_signing.key
 apt-key add nginx_signing.key
#Update the package index:

apt-get update
#Install nginx deb package:
apt-get install nginx

➜  ~ nginx -v
nginx version: nginx/1.18.0


МУТИМ ЧЕРЕ АПАЧИ 
location ~ \.php$ {
proxy_pass http://server-ip:9000;
proxy_set_header Host $host;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto $scheme;
}

МУТИМ ЧЕРЕЗ СОКЕТ

location ~* \.php$ {
root /var/www/back; ОБЯЗАТЕЛЬНО ПУТЬ ЕБАЛСЯ ПОЛ-ДНЯ!!!!!
fastcgi_split_path_info ^(.+\.php)(/.+)$;
fastcgi_pass unix:/run/php/php7.4-fpm.sock; # подключаем сокет php-fpm
fastcgi_index index.php;
fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
include fastcgi_params;
}


##
# Gzip Settings
##
gzip on;
gzip_disable "msie6";
gzip_vary on;
gzip_proxied any;
gzip_comp_level 6;
gzip_buffers 16 8k;
gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript;

# создаём папку configs в etc/nginx/
# и добавляем строку ниже для автоподключения конфигов без символьных ссылок

include /etc/nginx/configs/*;


#СИМВОЛКА ЕСЛИ НУЖНА
$ ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/



##########-NGINX-##########


#### CERTBOR FOR SSL HTTPS #######

apt install certbot 

#certbot-python-nginx

certbot --nginx 

$ nano /etc/letsencrypt/renewal/example.com.conf

Вставьте в конец файла строку:

renew_hook = systemctl reload nginx


#### CERTBOR FOR SSL HTTPS #######


------------- On Debian and Ubuntu -------------
$ cat /var/log/nginx/error.log
$ cat /var/log/php7.4-fpm.log


########-PHP-last-3######

apt install ca-certificates apt-transport-https 
wget -q https://packages.sury.org/php/apt.gpg -O- | apt-key add -
echo "deb https://packages.sury.org/php/ stretch main" | tee /etc/apt/sources.list.d/php.list

apt update
apt install php7.4

№перенаправить» на другую альтернативу можно, например, так:

update-alternatives --config php

➜  ~ php -v
PHP 7.4.16 (cli) (built: Mar  5 2021 08:37:59) ( NTS )

# это не обязательно
#apt install php7.4-cli php7.4-common php7.4-curl php7.4-mbstring php7.4-mysql php7.4-xml

Если проблемы удаляем php 8.0

########-PHP-last-3######



######### --PYTHON 3.9.* --#########

$ apt install build-essential checkinstall
$ apt install libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev

apt install wget build-essential libreadline-gplv2-dev libncursesw5-dev \
     libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev 
     
Качаем питон , распаковываем, уствнавливаем по умолчанию

wget https://www.python.org/ftp/python/3.9.2/Python-3.9.2.tgz 

tar xzf Python-3.9.2.tgz 

$ cd Python-3.9.2

$ ./configure --enable-optimizations 

#Это если хотите новый питон по умолчанию
#Python-3.9 in default
$ make install 

Это только если вам нужна алтернативная вессия
#Python-3.9 alternativa
$ make altinstall 

cd /


➜  / python3 -V
Python 3.9.2


#UPGRADE PIP 

apt install python3-pip
pip3 install --upgrade pip

➜  / pip3 -V
pip 21.0.1 from /usr/local/lib/python3.9/site-packages/pip (python 3.9)


######### --PYTHON 3.9.* --#########


# Не обязательно я делаю алиас чтобы последний пинот был доступен по вызову python
#переходим в root добавляем в этот файл ".bashrc" строку ниже

alias python='/usr/bin/python3.9'

#для pip

alias pip='/usr/bin/pip3'

$ mkdir djangoprojectname
$ cd djangoprojectname/
$ virtualenv env
$ source ./env/bin/activate


$ pip install django gunicorn psycopg2-binary djangorestframework

$ django-admin startproject back
pip freeze > requirements.txt

tree -L 3

$ nano ~/back/back/settings.py

ALLOWED_HOSTS = ['*']

Запускаем Django

$ python3.9 manage.py runserver 0.0.0.0:8000

проверяем - работает?

ctrl+c

Миграции

$ python3.9 manage.py makemigrations
$ python3.9 manage.py migrate


$ gunicorn --bind 0.0.0.0:8000 back.wsgi

проверяем - работает?

ctrl+c


Должны получить 
(venv) ➜  back gunicorn --bind 0.0.0.0:8000 back.wsgi
[2021-03-25 10:16:25 +0000] [800] [INFO] Starting gunicorn 20.0.4
[2021-03-25 10:16:25 +0000] [800] [INFO] Listening at: http://0.0.0.0:8000 (800)
[2021-03-25 10:16:25 +0000] [800] [INFO] Using worker: sync
[2021-03-25 10:16:25 +0000] [801] [INFO] Booting worker with pid: 801


### УЗНАТЬ ПУТЬ для Gunicorn.service в виртуалке
$ which gunicorn
#/home/back/env/bin/gunicorn


Выходим с виртуалки
$ deactivate


#### DATA BASE #######
pip install --upgrade setuptools
apt install gcc libssl-dev
apt-get install python3-dev default-libmysqlclient-dev build-essential
pip install mysqlclient




#### DATA BASE #######

$ back python3 manage.py makemigrations
$ back python3 manage.py migrate

python3 manage.py startapp "new__app"


#########--GUNICORN--############

$ nano /etc/systemd/system/gunicorn.socket ### Добавить содержимое

[Unit]
Description=gunicorn socket

[Socket]
ListenStream=/run/gunicorn.sock

[Install]
WantedBy=sockets.target


$ nano /etc/systemd/system/gunicorn.service ### Добавить содержимое



[Unit]
Description=gunicorn daemon
Requires=gunicorn.socket
After=network.target

[Service]
User=root
Group=www-data
WorkingDirectory=/home/back/back
ExecStart=/home/back/env/bin/gunicorn \
          --access-logfile - \
          --workers 3 \
          --bind unix:/run/gunicorn.sock \
          back.wsgi:application

[Install]
WantedBy=multi-user.target


$ systemctl start gunicorn
$ systemctl enable gunicorn

И обязательно тестируем, что всё работает!

$ systemctl status gunicorn.socket

$ journalctl -u gunicorn.socket


$ chown -R www-data:www-data /home/back/back
$ usermod -aG www-data mad
$ chmod go-rwx /home/back/back
$ chmod go+x /home/back/back
$ chgrp -R www-data /home/back/back
$ chmod -R go-rwx /home/back/back
$ chmod -R g+rwx /home/back/back




### debag #####

curl --unix-socket /run/gunicorn.sock localhost
tail -F /var/log/nginx/error.log
journalctl -u gunicorn
systemctl status gunicorn.socket
systemctl status gunicorn
### debag #####


### restart ####
systemctl daemon-reload
systemctl restart gunicorn.socket
systemctl restart gunicorn
### restart ####


#### СКрипт который задаёт права для папок и файлов 
#!/bin/bash

dir=/var/www/site
user=root

echo "Set permissions for $dir...";
echo "CHOWN files...";
chown -R $user:$user "$dir";
echo "CHMOD directories...";
find "$dir" -type d -exec chmod 0755 '{}' \;
echo "CHMOD files...";
find "$dir" -type f -exec chmod 0644 '{}' \;

