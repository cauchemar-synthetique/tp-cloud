# TP1 : Conteneurs

## I. Docker
### 1. Installer

🌞 **Installer Docker sur la machine**  
Installation du service :

```
$ sudo dnf install docker-ce docker-ce-cli conteneurd.io docker-buildx-plugin docker-compose-plugin
```
Démarrage du service :
```
$ sudo systemctl start docker
```
Ajout de mon utilisateur au groupe docker :
```
$ sudo usermod -aG docker $(whoami)
```
### 3. Lancement de conteneurs
🌞 **Utiliser la commande docker run**  
Lancement du conteneur ```NGINX```
```
$ docker run --name web -v /home/admin/tp_docker/nginx/test.conf:/etc/nginx/conf.d/test.conf -v /home/admin/tp_docker/nginx/index.html:/ usr/share/nginx/html/index.html -p 8888:80 --memory=512m --cpus=0.5 -d nginx
```
Contenu de ```test.conf``` :
```
$ cat /home/admin/tp_docker/nginx/test.conf
serveur {
  écoutez 9999 ;
  racine /var/www/tp_docker ;
}
```
## II. Images
### 2. Construisez votre propre Dockerfile
🌞 **Construisez votre propre image**
```
$ fichier docker chat
DEPUIS Ubuntu : le dernier

EXÉCUTER apt update -y

EXÉCUTER apt install -y apache2

RUN fait écho à "Bienvenue cauchemar." > /var/www/html/index.html

COPIER apache2.conf /etc/apache2/apache2.conf

CMD ["apache2", "-D", "PREMIER PLAN"]
```
La conf d'apache2 :
```
$ chat apache2.conf
Écoute 80

LoadModule mpm_event_module "/usr/lib/apache2/modules/mod_mpm_event.so"
LoadModule dir_module "/usr/lib/apache2/modules/mod_dir.so"
LoadModule authz_core_module "/usr/lib/apache2/modules/mod_authz_core.so"

DirectoryIndex index.html
DocumentRoot "/var/www/html/"

Journal des erreurs "/var/log/apache2/error.log"
Avertir le niveau de journalisation
```
Le fichier docker :
```
$ docker build . -t mon fichier docker
[+] Bâtiment 2.3s (10/10) TERMINÉ
[...]
```
```
$ docker run -d -p 8888:80 mon fichier docker
0f96bd565ad56e5600abccf58affe89a2875efcc4596abdea12054a29ab1ce95
```
```
$ curl hôte local : 8888
 Bienvenue cauchemar.
$ boucle 192.168.56.4:8888
 Bienvenue cauchemar.
```
