# Projet Trottinette électrique

Ce projet est concu conjointement par Jérémy Roy, Arthur Méot, l'équipe professorale du 
Cégep de Sherbrooke et Écomobilité Sherbrooke par l'intermédiaire de M.Gauthier

L'objectif est la création d'un tableau de bord à l'aide d'un PCB de notre conception faisant
le lien entre le controlleur d'une trottinette électrique et un Rasberry Pi 3 servant à l'affichage sur un 
écran HDMI.

Ce projet a pour but de permettre aux étudiants de travailler sur un système réel et intégré plutôt que 
sur des montages de laboratoire isolés et théorique.

## Fonctionnalités requises
Le projet devra présenter les aspects suivant tel qu'exigé par Écomobilité Sherbrooke:
- L'affichage en temps réel des données en provenance de la trottinette
- Une interface ergonomique 
- Fixation au guidon par un boitier imprimé en 3D
- Présence d'un manuel utilisateur
- Restrictions de composantes imposé par le client. (Voir prérequis)

## Prérequis

### Matériel
- Base de trottinette fonctionnel fournit par le client
- Rasberry Pi 3
- Écran compatible avec la communication HDMI (Rasberry Pi)
- Cable JST 10 pins à JST 10 pins (PCB STM32)
- Cables à breadboard femelle à femelles (PCB STM32 / Rasberry Pi)
- PCB concu par les étudiants (PCB STM32)
- Boitier fixable sur le guidon de la trottinette (Boitier 3D)

### Logiciel
- Grisement lors du freinage (Rasberry Pi)
- Affichage du mode de conduite (Rasberry Pi)
- Arrêt de l'accélération moteur lors du freinage (Rasberry Pi)
- Affichage en temps réel des données (Rasberry Pi)
- Interface ergonomique (Rasberry Pi)
- Réception données sous format UART (STM32)

### Limitations
- Le PCB doit être programmable par le connecteur USB-C
- Nous devons avoir un bouton reset dédié sur le PCB
- Nous devons utiliser la puce STM32U083MC 
- Power supply 5V de 2.5A pour l'alimentation du Rasberry Pi 4 model B
- Les Dels utiliser doivent utiliser de 5mA
- Alimentation maximale de 12V/0.5A
- La réception des données se fait par le format JSON sur un protocol UART en provenance du controleur 
- Dût à notre installation actuelle avec un écran HDMI, la station et fixe et ne peux pas être fixé sur la trottinette
- Le système ne possède présentement pas de sécurité en cas de chute qui stopperait le moteur.
- Le système ne peut fonctionner sur l'alimentation de la batterie car il n'y a plus de convertisseur à la sortie du 12V.

## Structure

### Schéma
Voir section "PCB" -> "Schémas" pour voir les schémas de concept et électrique du projet.

### Dossiers/codes
Voir section "Codes" pour visionner les codes nécessaire au fonctionnement du projet.
#### Section Rasberry Pi 
- Ce code est à insérer dans un Rasberry Pi 4 model B et sert à l'affichage des données traitées par le STM32 sous format UART ou I2C sur un écran par l'intermédiaire d'un port HDMI.
#### Section STM32
- Ce code est à insérer dans le module STM32 conçu pour ce projet est fait le traitement des données reçu en provenance du controlleur de la trottinette.  Il recoit des informations par UART sous le format JSON et les retourne par UART et I2C.  


### Tests/validation
[Plan_Test](https://github.com/FeuYage/Projet-integrateur/tree/main/PCB/Plan%20de%20test)

## Utilisation

### Pour un utilisateur
- Lors du démarrage, passage par 2 modes : initialisation / mode conduite.
- En mode conduite, l'utilisateur à accès à : Freins / Accélération / Interrupteur des lumières / Informations affichées sur l'écran (Vitesse en km/h, niveau charge batterie, état freins, indicateur de la clé, température drive, mode de vitesse, état lumière, état arrêt urgence)
- L'utilisateur n'a pas d'accès aux éléments de débuggages.

### Pour un developpeur
- Mettre le jumper sur les broches BOOT du PCB pour entrer dans le mode de démarrage programmation par USB OU, Brancher le port JTAG pour programmation.
- Programmation faite par l'intermédiaire du port USB-C ou JTAG du PCB fait par les étudiants et en passent par la logiciel CUBEIDE pour modification du code accessible dans la section STM32.
- Plusieurs éléments de débuggages sont présent sur le PCB pour diagnostiquer toutes erreurs possibles.  Les dels servent pour la vérification de l'alimentation avec les points de test et des broches Arduino sont accessible pour analyse avec un analyseur logique.
- Il est également possible d'ajouter de nouvelles fonctionalités à l'interface en modifiant le code dans la section Rasberry Pi du GitHub.

### Prochaines étapes (todo)
- Ajout d'une centrale inertielle pour sécurité aditionnelle.
- Conception d'un boitier fermé pour fixation sur guidon.
- Ajout d'un régulateur 12V pour permettre l'alimentation par le controlleur de la trottinette.
- Finalisation du code
- Test d'intégration
- Préparation présentation
