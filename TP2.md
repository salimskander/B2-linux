🌞 Récupérez des images

petit "docker pull"

```
docker pull wordpress
docker pull mysql
docker pull python
docker pull linuxserver/wiki js
```
listez les images que vous avez sur la machine avec une commande docker

```
[bossautruche@localhost ~]$ docker image ls
REPOSITORY           TAG       IMAGE ID       CREATED       SIZE
mysql                latest    73246731c4b0   3 days ago    619MB
linuxserver/wikijs   latest    869729f6d3c5   7 days ago    441MB
python               latest    fc7a60e86bae   2 weeks ago   1.02GB
wordpress            latest    fd2f5a0c6fba   2 weeks ago   739MB
nginx                latest    d453dd892d93   8 weeks ago   187MB
```


🌞 Lancez un conteneur à partir de l'image Python

[bossautruche@localhost ~]$ docker run -it python bash
root@a5de99f71902:/# python
Python 3.12.1 (main, Dec 19 2023, 20:14:15) [GCC 12.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
>>> exit()
root@a5de99f71902:/#


 🌞Ecrire un Dockerfile pour une image qui héberge une application Python

 ```
[bossautruche@localhost ~]$ cd python_app_build/
[bossautruche@localhost python_app_build]$ ls
Dockerfile  app.py
 ```

 🌞 Build l'image