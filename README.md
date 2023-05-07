# Projet-infra-B1A    - Groupe 10

Réalisation d'un projet dans le but de mettre en oeuvre nos connaissances accumulées pendant les cours.



### **Projet réalisé par :** 



BATISTA LOBATO DE SUZA Lucas - MARIAMON William - MARQUIE Médéric - MILLE Vendelin 

________________________________________________________________________________
## Présentation : 

Nous avons fait le choix de monter une solution permettant de chatter, d'échanger de lourds fichiers et s'organiser. 

Nous avons donc choisi d'utiliser **Mattermost**, un logiciel libre de messagerie instantanée et de collaboration d'entreprise.

<img src="assests\0kc8whai.bmp" width="100" height="100">

[Mattermost :](https://mattermost.com/)  C' est un logiciel libre de messagerie instantanée et de collaboration d'entreprise. 

Il est publié sous licence MIT et écrit en langage [Go](https://go.dev/). 

Il est distribué sous forme de logiciel libre avec des fonctionnalités de messagerie instantanée, de partage de fichiers et de vidéoconférence. 

Il est possible de l'installer sur un serveur privé et de l'utiliser comme alternative à [Slack](https://slack.com/intl/fr-fr/). 

Mattermost est disponible sous forme de clients pour les systèmes d'exploitation Windows, macOS et Linux, ainsi que pour les appareils mobiles Android et iOS. Il est également possible d'accéder à Mattermost via un navigateur Web.

____________________________________________________________________________

## Pré-requis : 

Nous avons dans notre groupe des utilisateurs de 2 OS différents : Windows (10 & 11) et Mac.  

**Pour notre installation**, nous utilisons [VirtualBox](https://www.virtualbox.org/wiki/Downloads). 

Une iso [Rocky Linux](https://rockylinux.org/fr/download) en version 9.1-minimal-architecture-x86_64.

Je vous renvoie vers ce [guide](https://gitlab.com/it4lik/b1-reseau-2022/-/blob/main/cours/memo/install_vm.md) d'installation de VM très complet. (Merci [Léo](https://gitlab.com/it4lik) :blossom:)

Assurez-vous de checker cette liste, ci-dessous, afin d'être sûres d'avoir les paramètres au top :chart_with_upwards_trend: ! 

 - Une IP locale, statique ou dynamique. 
 - Un hostname personnalisé.
 - Firewall actif. 
 - SSH fonctionnel.
 - Un accès à internet.
 - Un DNS en fonction.
 - SELinux en permissive.

Après avoir fini ci-précédemment, vous pourrez procéder à la suite ! 
____________________________________________________________________________

## Sommaire : 

  1. ### [Installation de Mattermost.](1-Mattermost_Installation.md)
  2. ### [Paramétrage du réseau.](3-Mattermost_Connexion.md)

  3. ### [Securité du serveur - Partie 1](3-Securite_du_serveur_ovh_partie_1.md)

  4. ### [Securité du serveur - Partie 2](3-Securite_du_serveur_ovh_partie_2.md)
  _________________________________________________________________________


  Un petit mot de la fin qui nous tient à coeur. 

  C'est le fruit d'un travail rigoureux et acharné, mais nous sommes fiers du résultat. N'hésitez pas à nous faire des retours sur ce guide. 

  Merci Léo pour tes enseignements et tes critiques. Nous continuerons à pousser, puis fleurir un jour, grâce à ces bases. :blossom: