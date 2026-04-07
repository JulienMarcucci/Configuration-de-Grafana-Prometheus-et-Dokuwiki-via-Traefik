Installation de Grafana

Mise à jour du serveur:
sudo apt-get update && sudo apt-get upgrade -y

Installation des outils nécessaire à l'ajout de dépôt:
sudo apt-get install -y apt-transport-https software-properties-common wget

Ajouter la clé de dépôt:
sudo wget -q -O /usr/share/keyrings/grafana.key https://apt.grafana.com/gpg.key

Installation des dépôts:
sudo echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

Mise à jour des paquets et installation:
sudo apt-get update && sudo apt-get install -y grafana

Démarrer le démon Grafana et faire en sorte qu'il démarre automatiquement:
systemctl daemon-reload
systemctl enable grafana-server
systemctl start grafana-server

Pour accéder à Grafana:
http://ip_VM:3000

Ici: 
http://192.168.253.139:3000 

Dans notre cas, on peut taper sur le navigateur: 
grafana.mediaschool.local

Pour ajouter prometheus sur Grafana: 
connections -> data sources -> add data sources -> choisir prometheus -> URL: http://prometheus:9090 -> save & test

Pour créer un Dashboard: 
new -> new Dashboard -> import Dashboard (https://grafana.com/grafana/dashboards/19268-prometheus/ -> copier l'id du Dashboard) -> coller id -> load -> import

Pour y accéder: 
Dashboards -> cliquer par exemple sur Prometheus All Metrics



Installation de Prometheus

Vérifier que le système est à jour:
sudo apt update && sudo apt upgrade -y

Installer Prometheus:
sudo apt-get install prometheus prometheus-node-exporter

Pour se connecter: 
http://192.168.253.139:9090

Dans notre cas:
prometheus.mediaschool.local



Installation de Dokuwiki

Installer Docker

1) Installer les dépendances de Docker

sudo apt-get update

sudo apt-get install apt-transport-https ca-certificates curl gnupg2



2) Ajouter le dépôt officiel Docker

sudo curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

sudo echo "deb \[arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb\_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list

sudo apt-get update



3) Installation des paquets Docker

sudo apt-get install docker-ce docker-ce-cli containerd.io

sudo systemctl enable docker



4) Vérification installation

sudo systemctl status docker

sudo docker run hello-world



5) Version

docker --version


6) Commandes Docker

Lister les containers Docker en cours d'exécution:

sudo docker ps


Lister tous les containers Docker enregistrés sur la machine, peu importe l'état:

sudo docker ps -a


Supprimer un container Docker:

docker rm id(ex: 3c745b055853)


Lister les images Docker (disponibles en local):

docker images

Supprimer une image Docker:

docker rmi hello-world


Démarrer un container Docker:

docker start id


Arrêter un container Docker:

docker stop id


Télécharger une image Docker à partir de Docker Hub:

docker pull httpd



Créer un dossier:

mkdir \~/dokuwiki-data


Lancer DokuWiki avec Docker et volume persistant:

sudo docker run -d -p 8080:8080 -v \~/dokuwiki-data:/storage --name dokuwiki dokuwiki/dokuwiki:stable


sudo docker ps


Ensuite:

http://ip_vm:8080

Ici: 

http://192.168.253.140:8080 ou encore http://wiki.mediaschool.local





