# set up vps for django


apt update
apt upgrade
apt install curl nginx wget nano 

#good shel for console 
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"


Time to change your default shell to zsh:
Do you want to change your default shell to zsh? [Y/n] y
Changing the shell...
Shell successfully changed to '/usr/bin/zsh'.

         __                                     __
  ____  / /_     ____ ___  __  __   ____  _____/ /_
 / __ \/ __ \   / __ `__ \/ / / /  /_  / / ___/ __ \
/ /_/ / / / /  / / / / / / /_/ /    / /_(__  ) / / /
\____/_/ /_/  /_/ /_/ /_/\__, /    /___/____/_/ /_/
                        /____/                       
....is now installed!


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
C:\Users\admin\Desktop\Back-django\filmsapp\env\Scripts\activate.bat
env/bin source activate
pip install --upgrade pip
pip install django
pip install djangorestframework
pip install django-rest-knox
pip freeze > requirements.txt
python manage.py startapp films
tree -L 3
python manage.py runserver 0.0.0.0:8000
