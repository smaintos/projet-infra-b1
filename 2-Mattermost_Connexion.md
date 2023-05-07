# Pare-feu et connexions. 

Ici nous allons initier la connexion de la VM au World Wide Web. 

<img src="assests\9akfhcao.bmp"> - *The proper way to build a firewall*

#  Sommaire

 - [Sommaire](#sommaire) 
 - [I. T'as internet ?](#i-tas-internet)
 - [II. Ouvre le sas Michel !](#ii-ouvre-le-sas-michel)
 - [III. On brave le videur](#iii-on-brave-le-videur)
 - [IV. Finalisation.](#iv-finalisation)
 - T'as des nouvelles du Service RH ? 
 - Quel service RH ?
 - Nan y a que 4 parties.

 # I. T'as internet ? 

 Dans un premier temps, nous allons nous assurer que la VM Mattermost a accès à internet.

 On va donc ping depuis la VM, Google, youtube, peu importe : 
 ```
 ping google.com // youtube.com // 1.1.1.1 // 8.8.8.8
 ```
 
 Pour le coup choisissez, c'est à votre envie et goût de qui vous allez embêter. 

 # II. Ouvre le sas Michel !

C'est sympa de savoir qu'on peut faire "toc-toc" chez Google mais ça va pas nous aider des masses. 

 Ce que nous allons faire ici fait partie du plus simple. 

 Nous allons utiliser directement l'interface de VirtualBox afin de "déplacer" notre VM - MattermostWeb - directement dans votre LAN.

 On va utiliser un principe de "pont" entre la carte réseau de la VM et votre box. Ainsi sans passer "directement" par votre ordinateur, la VM pourra communiquer avec votre box puis, le monde extérieur.

 Pour se faire, suivez le [guide](https://wiki.dave.eu/index.php/VirtualBox_Network_Configuration). 
 Ou quelqu'un d'autre si vous préférez ou que vous êtes paranos, une petite recherche (en anglais de préférence) et c'est dans la poche :smile:


 # III. On brave le videur.

 <img src="assests\7m4xxbbs.bmp">
 On va donc maintenant se lancer dans le paramètrage de la box. Pourquoi ?

 Afin de pouvoir communiquer avec le monde extérieur en toute sécurité pardi ! 

Pour ceci vous aurez besoin de : 

 - Vos accès à la box.
 - Des oeufs.
 - De la farine.
 - Un peu de courage.
 - De la patience. 
 - Du Lait.


Dépendant de votre FAI (Fournisser d'Accès Internet) vous aurez une interface de paramétrage de votre box différente. 

Le but étant ici de laisser entrer une connexion sur un Port extérieur choisis afin de la rediriger vers un port interne qui sera celui destiné à la VM. Vous suivez ? :grimacing: 

Concrêtement ouvrez un port définis côté IP publique, et redirigez celui vers un port interne à votre LAN. C'est très vague comme instruction, mais tout dépendra de l'interface de votre box. 

# IV. Finalisation.

Nous aurons besoin d'une dernière manipulation afin de faire fonctionner tout ce petit réseau ! 

Nous allons aborder le principe de "Port Forwarding". Nous allons ici l'utiliser sur VirtualBox (ou l'interface de votre utilisation).

C'est simple à nouveau, suivez le [guide](https://www.it-connect.fr/configurer-le-port-forwarding-sur-une-vm-virtualbox%EF%BB%BF/) ! 

:warning: N'oubliez pas d'ouvrir les ports choisis, sur votre OS, dans votre VM ! :warning:

A ce stade vous devriez pouvoir recevoir des requêtes d'adresses IP distantes à votre LAN. 
Bravo et bon courage pour la suite ! 

<img src="assests\51vda2jn.bmp">

Vous pouvez maintenant passer à la [suite](3-Securite_du_serveur_ovh_partie_1.md).