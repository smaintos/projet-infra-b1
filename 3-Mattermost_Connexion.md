# Pare-feu et connexions. 

Ici nous allons initier la connexion de la VM au World Wide Web. 

[![FireWall Meme, yes indeed](assests\9akfhcao.bmp "This is the proper way to make a firewall")](https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.reddit.com%2Fr%2Fmemes%2Fcomments%2Fayn8uv%2Fthis_is_the_proper_way_to_make_a_firewall%2F&psig=AOvVaw1RnDTLpBTE1u8e8JNAcwyJ&ust=1683570797745000&source=images&cd=vfe&ved=0CA4QjRxqFwoTCPCYiZTu4_4CFQAAAAAdAAAAABAf)

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

 [![Hobbits](assests\7m4xxbbs.bmp "They're taking the Hobbits to Isengard !")](https://www.google.com/url?sa=i&url=https%3A%2F%2Fprogrammerhumor.io%2Fprogramming-memes%2Ffirewall-be-like-what-has-it-got-in-its-nasty-little-packetses%2F&psig=AOvVaw3mdrs75EeYEwyof1g5EHXI&ust=1683571813823000&source=images&cd=vfe&ved=0CA4QjRxqFwoTCLi_6fXv4_4CFQAAAAAdAAAAABAD)

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

[![Port-Forwarding meme, yes](assests\51vda2jn.bmp "Oh the irony")](https://www.google.com/url?sa=i&url=https%3A%2F%2Ftwitter.com%2Foverflow_meme%2Fstatus%2F1335458305280446466&psig=AOvVaw0K6I_jeYV6LemNSDbCOzEB&ust=1683571045554000&source=images&cd=vfe&ved=0CA4QjRxqFwoTCOC_8ZHt4_4CFQAAAAAdAAAAABAS)