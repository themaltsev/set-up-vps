# SET UP VPS UBUNTU DEBIAN for DJANGO 3.1.*


Проверяем обновы
apt update

Обновляем пакеты
apt upgrade


#СМЕНА ПАРОЛЯ
passwd 

apt install curl wget nano git  tree -y

# Не обязательно Красивый шел для консоли Install oh-my-zsh:

apt install zsh -y

sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"


sudo apt-get install -y redis-server nginx zlib1g-dev libbz2-dev libreadline-dev llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev liblzma-dev python3-dev python-imaging python3-lxml libxslt-dev python-libxml2 python-libxslt1 libffi-dev libssl-dev python-dev gnumeric libsqlite3-dev libpq-dev libxml2-dev libxslt1-dev libjpeg-dev libfreetype6-dev libcurl4-openssl-dev supervisor


#nginx

ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/

#install last python 3.9.*

api install python3.9

api install python3-pip

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
