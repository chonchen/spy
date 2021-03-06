spy
======
## Docker
### Mac OS
#### docker-machine
https://docs.docker.com/machine/get-started/
### Commands
#### Build
```
docker build -t tom/spy .
```
#### Run Docker Container
```
docker run -p 42221:22 -p 42222:8888 -d --name spy tom/spy /sbin/my_init --enable-insecure-key
```
#### Configure SSH
```
cat << EOF >> ~.ssh/config
Host spy
    IdentityFile ~/.ssh/insecure_key
    Port 42221
    ForwardAgent yes
    User root
    Hostname localhost
EOF
```
#### Setup Repo
```
ssh otherhost << EOF
  mkdir ~/src;
  cd ~/src;
  git init
  git checkout -b dummy
EOF
git push --set-upstream docker master
```
##### Initialize Server
```
cd ~/src
npm install
./node_modules/.bin/webpack --config webpack.config.js
./manage.py makemigrations spy
./manage.py migrate
```
##### Run Django
```
python manage.py runserver 0.0.0:8888
```

## Dev Notes
### Setup Django
https://realpython.com/learn/start-django/
##### Django + Webpack
http://owaislone.org/blog/webpack-plus-reactjs-and-django/
##### Django REST
http://www.django-rest-framework.org/tutorial/1-serialization/
http://www.django-rest-framework.org/tutorial/2-requests-and-responses/


