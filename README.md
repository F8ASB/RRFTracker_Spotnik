# RRFTracker_Spotnik
Suivi temps réel de l'activité du réseau [RRF](https://f5nlg.wordpress.com/2015/12/28/nouveau-reseau-french-repeater-network/) (Réseau des Répéteurs Francophones) pour Spotnik. Une video du fonctionnement est visible sur [Youtube](https://www.youtube.com/watch?v=rVW8xczVpEo) ;)

## Principe de fonctionnement

Cette implémentation du RRFTracker permet de suivre en temps réel l'activité du réseau RRF, en utilisant un Rasbperry Pi ou un Orange Pi et un écran OLED 0.96" 128x64 type SH1106 ou SSD1306. Il fait suite à un premier projet, réalisé fin novembre 2018 à partir d'un Nodemcu ESP8266 et d'un écran LCD 16x2.

Ce dispositif peut donc être associé sans difficulté à un Spotniks Gamma, Delta, etc. afin de profiter d'un minimum de remontée d'informations, à l'image des Hotspots MMDVM type ZUMspot, Jumbo SPOT, etc. si precieux aux porteurs de casques de chantiers... j'ai nommé les DMRistes ;)

À noter qu'un projet plus évolué, porté par F8ASB (Juan), F5SWB (Dimitri) et F0DEI (Toufik), basé sur l'utilisation d'un écran type Nextion est également en cours de développement. Du fait des possibilités tactiles de l'écran, ce projet offre plus de possibilité en terme d'interactivité (changement de salon, etc.). 

Au repos, si aucune station n'est en émission, le RRFTracker affichera,

* l'indicatif des 2 derniers noeuds étant passés en émission,
* l'heure du dernier passage en émission.

Si un QSO est en cours, le RRFTracker affichera,

* l'indicatif des 2 derniers noeuds étant passés en émission,
* l'indicatif du noeud en cours d'émission.

En complement, sur la ligne centrale, au milieu de l'écran, on retrouve

* le nombre de passages en émission sur la journée (depuis 00h00),
* le temps depuis lequel fonctionne le RRFTracker (uptime),
* le nombre de passages en émission depuis l'allumage du RRFTracker,
* l'indicatif du link le plus actif avec le nombre de passage en émission.

Pour finir, en haut à droite de l'écran, le RRFTraker affiche l'heure. Et le bas de l'écran présente un histogramme du trafic dans la journée, heure par heure.

## Post installation sur Spotnik 1.9

En partant de la version 1.9 de Spotnik, il faut procéder à l'installation de quelques modules complémentaires. Depuis une connexion SSH, lancez les commandes suivantes:


`sudo apt-get install i2c-tools libi2c-dev python-smbus python-pip python-dev python-imaging`

`sudo apt-get install libfreetype6-dev libjpeg-dev build-essential`

`sudo pip install --upgrade setuptools`

`sudo -H pip install --upgrade luma.oled`

Enfin, si ce n'est pas déjà fait, il reste à activer le support du protocole I2C afin de pouvoir dialoguer avec l'écran OLED.

* Sur Raspberry Pi, utiliser raspbian-config
* Sur Orange Pi Zero, todo todo todo

Pour finir et vérifier que tout est pret, une fois l'écran connecté (voir schéma), exécutez la commande suivante:

`i2cdetect -y 0`

Cette commande devrait retourner quelque chose comme:

```
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- 3c -- -- --
40: -- -- -- -- -- -- -- -- UU -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
70: -- -- -- -- -- -- -- --
```

Votre écran utilise donc ici le port 0 et l'adresse 3c. Editer le code du RRFTracker (juste au début du main) en fonction de ce que vous retourne la commande. Et si elle ne fonctionne pas, essayez:

`i2cdetect -y 1`

Dans ce cas, le port à indiquer dans le code du RRFTracker sera 1.

## Liste des composants

Voici la liste des composants dont vous aurez besoin:

* 1 Raspberry Pi ou 1 Orange Pi
* 1 écran OLED 0.96" 128x64 type SH1106 ou SSD1306
* 4 cables Dupont femelle / femelle
 
## Schéma de montage

![alt text](https://github.com/armel/RRFTracker_Spotnik/blob/master/doc/RRFTracker.png)