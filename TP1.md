🌞 Ajouter votre utilisateur au groupe docker

```
sudo usermod -aG docker bossautruche
```
vérifier que vous pouvez taper des commandes docker comme docker ps sans avoir besoin des droits root

```
[bossautruche@localhost ~]$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED             STATUS             PORTS                                   NAMES
a1bff23d2adb   nginx     "/docker-entrypoint.…"   About an hour ago   Up About an hour   0.0.0.0:9999->80/tcp, :::9999->80/tcp   mystifying_shirley
```

ok pour l'instant c'est easy c'est cool c'est comprehensible 


🌞 Lancer un conteneur NGINX
```
[bossautruche@localhost ~]$ docker run -d -p 9999:80 nginx
b7ff7ab6758d5c2ed7a9538ce3222877c41aa29f2bb76a9c1d058dce93eb49b1
```

🌞 Visitons

vérifier que le conteneur est actif avec une commande qui liste les conteneurs en cours de fonctionnement :

```
[bossautruche@localhost ~]$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                   NAMES
b7ff7ab6758d   nginx     "/docker-entrypoint.…"   57 seconds ago   Up 57 seconds   0.0.0.0:9999->80/tcp, :::9999->80/tcp   laughing_kapitsa
```
afficher les logs du conteneur :

```
[bossautruche@localhost ~]$ docker inspect b7ff7ab6758d
```

afficher le port en écoute sur la VM avec un sudo ss -lnpt

```
[bossautruche@localhost ~]$ sudo ss -lnpt
[sudo] password for bossautruche:
State    Recv-Q   Send-Q       Local Address:Port       Peer Address:Port   Process
LISTEN   0        128                0.0.0.0:22              0.0.0.0:*       users:(("sshd",pid=693,fd=3))
LISTEN   0        4096               0.0.0.0:9999            0.0.0.0:*       users:(("docker-proxy",pid=2127,fd=4))
LISTEN   0        128                   [::]:22                 [::]:*       users:(("sshd",pid=693,fd=4))
LISTEN   0        4096                  [::]:9999               [::]:*       users:(("docker-proxy",pid=2132,fd=4))
```
ouvrir le port 9999/tcp (vu dans le ss au dessus normalement) dans le firewall de la VM

```
sudo firewall-cmd --add-port 9999/tcp
```
🌞 On va ajouter un site Web au conteneur NGINX

```
[bossautruche@localhost nginx]$ docker run -d -p 9999:8080 -v /home/bossautruche/nginx/index.html:/var/www/html/index.html -v /home/bossautruche/nginx/site.conf:/etc/nginx/conf.d/site.conf nginx
0f3f970e1bbc05ff7f0942c88e5b9d903e1399b3ad309f6e4c223a24e89f0516
```

🌞 Visitons

vérifier que le conteneur est actif:

```
[bossautruche@localhost nginx]$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS                                               NAMES
0f3f970e1bbc   nginx     "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp, 0.0.0.0:9999->8080/tcp, :::9999->8080/tcp   gracious_noether
```

j'ai visité le site avec mon pc, c'est super mignon y'a des chats partout trop kawai.

index.html : 
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chats et Meow</title>
    <style>
        body {
            background-color: #f5f5f5;
            font-family: 'Arial', sans-serif;
            color: #333;
            text-align: center;
            margin: 20px;
        }

        h1 {
            color: #ff6600;
        }

        img {
            width: 300px;
            border-radius: 15px;
            margin: 10px;
        }

        .meow {
            font-size: 24px;
            color: #cc3366;
        }
    </style>
</head>
<body>
    <h1>Le Monde des Chats</h1>
    <img src="https://placekitten.com/800/400" alt="Un Chat Mignon">
    <p class="meow">Meow ! Bienvenue dans le monde adorable des chats.</p>
    <img src="https://placekitten.com/700/350" alt="Un Autre Chat Mignon">
    <p class="meow">Meow, meow ! N'est-ce pas mignon ?</p>
    <img src="https://placekitten.com/600/300" alt="Encore un Chat Mignon">
    <p class="meow">Meow, meow, meow !</p>
</body>
</html>

```

🌞 Lance un conteneur Python, avec un shell


```
docker run -it python bash
```

ensuite je pipinstall aiohttpo et aioconsoel

j'ouvre un interpreteur python avec la commande "pyton"

j'import les deux pour check si j'ai bien import
c'est bon ca fonctionne

je sors de l'interpreteur
je me balade dans l'arborescence, ptite balade digestive c'est chill

je teste des pings y'a pas
ip a y'a pas  bref 
(y'a pas, c'est un "OS allégé")



🌞 Récupérez des images

```
[bossautruche@localhost nginx]$ docker pull python:3.11
3.11: Pulling from library/python

[bossautruche@localhost nginx]$ docker pull mysql:5.7
5.7: Pulling from library/mysql
no matching manifest for linux/arm64/v8 in the manifest list entries
[bossautruche@localhost nginx]$ docker pull mysql
Using default tag: latest
latest: Pulling from library/mysql

[bossautruche@localhost nginx]$ docker pull wordpress
Using default tag: latest
latest: Pulling from library/wordpress

[bossautruche@localhost nginx]$ docker pull linuxserver/wikijs
Using default tag: latest
latest: Pulling from linuxserver/wikijs

[bossautruche@localhost nginx]$ docker image ls
REPOSITORY           TAG       IMAGE ID       CREATED       SIZE
mysql                latest    8e409b83ace6   3 days ago    641MB
linuxserver/wikijs   latest    772abe6ffca7   6 days ago    459MB
wordpress            latest    4468dc043c37   2 weeks ago   739MB
python               3.11      f983f601e9a2   2 weeks ago   1.01GB
```

```
[bossautruche@localhost python_app_build]$ docker run python_app:version_de_ouf
Cet exemple d'application est vraiment naze 👎
[bossautruche@localhost python_app_build]$
```


