# Guide d'installation de Mattermost sur deux VMs Rocky Linux avec MySQL
Ce guide vous aidera à installer Mattermost sur deux machines virtuelles Rocky Linux en utilisant MySQL comme base de données. Les étapes sont divisées en deux parties : les prérequis et l'installation. Sachant que la base de données MySQL sera installée sur une machine virtuelle et Mattermost sur une autre.

## Prérequis

### Configuration matérielle
Pour installer Mattermost sur deux machines virtuelles Rocky Linux, vous aurez besoin de deux VMs distinctes. Chaque VM doit avoir au moins 2 Go de RAM et 2 cœurs de CPU pour fonctionner correctement.

### Configuration réseau
Pour que les deux machines virtuelles puissent communiquer entre elles, il est important de configurer leur réseau en conséquence. Vous pouvez utiliser un réseau privé virtuel (VLAN) pour connecter les deux machines virtuelles.

## Installation

### Installation de MySQL
Mattermost nécessite une base de données MySQL pour stocker les données. Vous pouvez installer MySQL en utilisant les commandes suivantes :
```
sudo dnf install mysql-server -y
sudo systemctl enable mysql
sudo systemctl start mysql
sudo mysql_secure_installation

```
Vous pouvez aussi sécuriser votre base de données en suivant l'instruction suivante :
```
sudo mysql_secure_installation
```
Et suivre les instructions.



### Étape 2 : Configuration de la base de données MySQL

Une fois MySQL installé, vous devez créer une base de données pour Mattermost. Connectez-vous à MySQL en tant qu'utilisateur root et créez une base de données et un utilisateur pour Mattermost : 
```
sudo mysql -u root -p 

CREATE DATABASE mattermost; 

CREATE USER 'mattermost'@'localhost' IDENTIFIED BY 'password';

GRANT ALL PRIVILEGES ON mattermost.* TO 'mattermost'@'localhost';

FLUSH PRIVILEGES;

EXIT;
```

### Étape 3 : Installation de Mattermost 

Téléchargez la dernière version de Mattermost à partir de leur site officiel. Vous pouvez le télécharger en utilisant la commande suivante :
```
wget https://releases.mattermost.com/5.34.2/mattermost-5.34.2-linux-amd64.tar.gz
```
Une fois le téléchargement terminé, extrayez l'archive téléchargée avec la commande suivante :
```
tar -xvzf mattermost*.gz
```
Ensuite, déplacez le répertoire Mattermost vers le répertoire /opt :
```
sudo mv mattermost /opt
```
Créez un répertoire de données pour Mattermost :
```
sudo mkdir /opt/mattermost/data
```

Ensuite, créez un utilisateur Mattermost et définissez le répertoire d'installation Mattermost comme propriétaire :
```
sudo useradd --system --user-group mattermost
 
sudo chown -R mattermost:mattermost /opt/mattermost

sudo chmod -R g+w /opt/mattermost

sudo restorecon -R /opt/mattermost
```
### Étape 4 : Configuration de Mattermost
Après avoir installé Mattermost, vous devez le configurer en éditant le fichier config.json dans le dossier /opt/mattermost/config/. Vous pouvez utiliser un éditeur de texte pour modifier ce fichier. Par exemple, vous pouvez utiliser l'éditeur nano pour modifier ce fichier :
```
sudo nano /opt/mattermost/config/config.json
```
Et dans ce fichier, vous devez modifier les lignes suivantes :
- Définissez "DriverName" sur "mysql"
- Définissez "DataSource" sur la valeur que vous avez définit lors de l'instalation de MySQL, en remplaçant "mmuser-password" et "host-name-or-IP" par les valeurs appropriées.
- Assurez-vous également que le nom de la base de données est correcte.

La ligne de configuration ressemblera à ceci :
```
"mmuser:<mmuser-password>@tcp(<host-name-or-IP>:3306)/mattermost?charset=utf8mb4,utf8&writeTimeout=30s"

```
Ensuite, enregistrez le fichier et quittez l'éditeur.

Vous pouvez testez le serveur Mattermost pour vous assurer que tout fonctionne :
```
cd /opt/mattermost
sudo -u mattermost ./bin/mattermost
```
Normalement vous pouvez communiquer avec la base de donner MySQL et Mattermost devrait fonctionner correctement.

### Étape 5 : Configuration du service Mattermost
Créez un fichier de service Mattermost avec la commande suivante :
```
sudo nano /etc/systemd/system/mattermost.service
```
Ajoutez le contenu suivant :
```
[Unit]
Description=Mattermost
After=syslog.target network.target postgresql.service

[Service]
Type=notify
WorkingDirectory=/opt/mattermost
User=mattermost
ExecStart=/opt/mattermost/bin/mattermost
PIDFile=/var/spool/mattermost/pid/master.pid
TimeoutStartSec=3600
KillMode=mixed
LimitNOFILE=49152

[Install]
WantedBy=multi-user.target
```	
Donnez les droits d'accès au fichier :
```
sudo chmod 664 /etc/systemd/system/mattermost.service
```

Enregistrez le fichier et quittez l'éditeur. Ensuite, démarrez le service Mattermost et activez-le pour qu'il démarre au démarrage :
```
sudo systemctl daemon-reload
sudo systemctl enable mattermost
sudo systemctl start mattermost
```

Pour accéder à votre Mattermost en local : `http://ip-de-Mattermost:8065`

Et voila ! Vous avez installé Mattermost sur vos VM's

Vous pouvez maintenant passer à la [suite.](2-Mattermost_Connexion.md)