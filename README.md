#DEBIAN VPS SET UP NGINX 1.18.* HTTP2 HTTPS PHP 7.4* PYTHON 3.9.* LAST MYSQL PHPMYADMIN POSTGRESQL PHPPGADMIN  DJANGO 3.1.*



Проверяем обновы
apt update

Обновляем пакеты
apt upgrade


#СМЕНА ПАРОЛЯ
passwd 

##### Мониторинг сервера 
apt install htop -y
htop

##### АВТОЗАГРУЗКА 

apt install rcconf
rcconf

apt install curl wget nano git  tree -y

# Не обязательно Красивый шел для консоли Install oh-my-zsh:

apt install zsh -y

sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"


apt-get install -y redis-server nginx zlib1g-dev libbz2-dev libreadline-dev llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev liblzma-dev python3-dev python-imaging python3-lxml libxslt-dev python-libxml2 python-libxslt1 libffi-dev libssl-dev python-dev gnumeric libsqlite3-dev libpq-dev libxml2-dev libxslt1-dev libjpeg-dev libfreetype6-dev libcurl4-openssl-dev supervisor



##########-NGINX-##########

apt install ca-certificates apt-transport-https 

Add the following line to /etc/apt/sources.list:
deb https://nginx.org/packages/debian/ stretch nginx
Install GPG key of the repository:

# wget https://nginx.org/keys/nginx_signing.key
# sudo apt-key add nginx_signing.key
Update the package index:
# sudo apt-get update
Install nginx deb package:
# sudo apt-get install nginx

➜  ~ nginx -v
nginx version: nginx/1.18.0


ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/



##########-NGINX-##########

#### CERTBOR FOR SSL HTTPS #######

apt install certbot 

#certbot-python-nginx

certbot --nginx 

#### CERTBOR FOR SSL HTTPS #######



########-PHP-last-3######

apt install ca-certificates apt-transport-https 
wget -q https://packages.sury.org/php/apt.gpg -O- | apt-key add -
echo "deb https://packages.sury.org/php/ stretch main" | tee /etc/apt/sources.list.d/php.list

apt update
apt install php7.4


➜  ~ php -v
PHP 7.4.16 (cli) (built: Mar  5 2021 08:37:59) ( NTS )

# это не обязательно
#apt install php7.4-cli php7.4-common php7.4-curl php7.4-mbstring php7.4-mysql php7.4-xml

########-PHP-last-3######




######### --PYTHON 3.9.* --#########

apt install wget build-essential libreadline-gplv2-dev libncursesw5-dev \
     libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev 
     
Качаем питон , распаковываем, уствнавливаем по умолчанию

wget https://www.python.org/ftp/python/3.9.2/Python-3.9.2.tgz 

tar xzf Python-3.9.2.tgz 

cd Python-3.9.2
./configure --enable-optimizations 

#Это если хотите новый питон по умолчанию
#Python-3.9 in default
make install 

Это только если вам нужна алтернативная вессия
#Python-3.9 alternativa
#make altinstall 

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


django-admin startproject filmsapp 
&& cd filmsapp
python -m venv env 

#windows C:\Users\admin\Desktop\Back-django\filmsapp\env\Scripts\activate.bat

#linux env/bin source activate

pip install --upgrade pip

pip install django

pip install djangorestframework

pip install django-rest-knox

pip freeze > requirements.txt

python manage.py startapp films

tree -L 3

python manage.py runserver 0.0.0.0:8000
