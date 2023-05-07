# Sécurité du serveur ovh partie 1.

Forcément pour que tout se porte bien il nous faut de la sécurité sur notre serveur ovh car c'est ici que les clients vont se connecter en premier avant d'être redirigés vers mattermost !

## Prérequis : 
    
* Un serveur VPS sous Rocky Linux 9.1 (abonnement le moins chère pas besoin de plus https://www.ovhcloud.com/fr/vps/ ;)
* Vérifier que la machine est à jour.
* Se connecter en SSH.
* Désactiver SELINUX.

____________________________________________________________________________

## On va commencer par la sécurité de base , FAIL2BANNNNNNN 

![](https://hackmd.io/_uploads/BynyWwSNh.jpg)

Avant tout de chose , on doit installer quelques petits packets donc : 

`sudo dnf install -y python3 bind-utils nmap nc tcpdump vim traceroute nano dhclient wget`

 ### Installation de fail2ban : 
 
` sudo dnf install epel-release -y`
` sudo dnf install fail2ban -y`

### Vérification du status (inactive) : 

`systemctl status fail2ban.service`

On passe maintenant à la configuration du service : 

`cd /etc/fail2ban`
`sudo cp jail.conf jail.local`

Ouvrir le fichier de conf créé juste avant "jail.local" avec l'éditeur de votre choix : 

`sudo nano jail.local`

Une fois dans le fichier de conf on va aller à la ligne "ignore ip" et la mettre en commentaire. 

Une fois cela fait vous pouvez maintenant configurer le fichier comme bon vous semble. 

Ici on a choisi d'appliquer un ban permanent du system si l'utilisateur à effectué 5 erreurs d'affilé pour la connexion en SSH, la conf doit ressembler à ça :

```
# ignorecommand = /path/to/command <ip>
ignorecommand =

# "bantime" is the number of seconds that a host is banned.
bantime  = -1

# A host is banned if it has generated "maxretry" during the last "findtime"
# seconds.
findtime  = 10m

# "maxretry" is the number of failures before a host get banned.
maxretry = 5

# "maxmatches" is the number of matches stored in ticket (resolvable via tag <matches> in actions).
maxmatches = %(maxretry)s
```

```
[sshd]
enabled=true
# To use more aggressive sshd modes set filter parameter "mode" in jail.local:
# normal (default), ddos, extra or aggressive (combines all).
# See "tests/files/logs/sshd" or "filter.d/sshd.conf" for usage example and details.
#mode   = normal
port    = ssh
logpath = /var/log/fail2ban.log
backend = %(sshd_backend)s
maxretry=5
bantime=-1
```

Une fois la conf fait plus qu'à lancer le service : 
`sudo fail2ban-client start`
`sudo fail2ban-client reload`

Une fois cela fait bah gg c'est config loul , pour voir les logs du service , le fichier se trouve dans **./var/log/fail2ban.log**.

Pour vérifier que tout marche bien , connectez vous au serveur en mettant un wrong password et l'erreur sera report.

___________________________________________________________________________

## Maintenant on va passer à un outils pour de l'hardening : [définition](https://fr.wikipedia.org/wiki/Durcissement_)

[![](https://hackmd.io/_uploads/rJs75uHVn.jpg)]


Et roulement de tambours cet outil c'est ......LYNIS ,
qui est un service qui va effectuer une série de tests sur votre machine et vous output un rapport par catégories des fails de sécurité présent sur votre système.

[![](https://hackmd.io/_uploads/rJLVcdBNh.png)]


## Pour l'installer : 

`git clone https://github.com/CISOfy/lynis `

(oui c'est un repo)

Et une fois cela fait attention magie... bah c'est bon , plus qu'à aller dans le dossier avec un  `cd /lynis` executez le avec un `./lynis audit system` et une fois cela fait il va se lancer et faire le retour d'analyse de votre machine. 

A partir de cela vous pouvez choisir de mettre l'accens sur quel type de fail.

---
## ModSecurity et nginx...

BON , c'est pas le plus opti mais c'est quand même efficace , je vous invite à faire des recherches sur le sujet car l'install peut-être plus ou moins différente en fonction des màjs de votre machine etc. 

C'est quoi [ModSecurity](https://fr.wikipedia.org/wiki/Modsecurity) ? Trois fois rien juste une sécurité qui va **GERER PLUSIEUR FAILs ET ATTAQUEs EN MEME TEMPS** comme les attaque xss ou injection sql par exemple :smile:.

[![](https://hackmd.io/_uploads/BJURhuSN2.png)]

Pour cette install il faudra beaucoup s'aider de la docs que [voici](https://www.atlantic.net/vps-hosting/how-to-install-modsecurity-with-nginx-on-rocky-linux-8/ ) 

vous pouvez passer la partie Actlantiv Cloud.
On a deja notre serveur ovh, malheuresement il n'y a pas tout ici , il y a quelques étapes qu'on rencontre à cause de soucis de packets un peu *boggés*. 

Une fois nginx installé et modsecurity ainsi que tous les paquets qu'il y a autour, c'est l'heure de lancer les scripts `./build.sh` ainsi que que `./configure`.

Si cela ne fonctionne pas cela vient de *l'instaler* qui ne veut pas se copier , il faudra donc le faire à la main avec la commande `sudo cp`.

Il n'y a aucune conf particulière à faire pour nginx.


### :warning: **TRES IMPORTANT !!** :warning: 

Les packages remies et `epel` seront sans doute non fonctionnels car lors de l'installation la dernière version n'est pas prise en compte.

Voici donc les bonnes versions à installer : 

`sudo dnf install https://rpms.remirepo.net/enterprise/remi-release-9.rpm`

`sudo dnf --enablerepo=remi install GeoIP-devel -y`

`sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm`


Une fois ces étapes suivient alors ModSecurity sera installé et opérationnel.

Première partie réalisé par Mariamon William.

Vous pouvez maintenant passer à la [suite](3-Securite_du_serveur_ovh_partie_2.md).
----











