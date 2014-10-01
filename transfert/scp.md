# SCP : Transfert de fichier via SSH #

SCP est un protocole de transfert de fichiers de poste à poste basé sur SSH permettant de sécuriser les échanges.

En effet, il empêche que vos informations puissent être interceptées par d’autres personnes , la sécurité et l’authentification étant gérées par SSH.

J’utilise personnellement ce protocole pour les backup des fichiers sur mon serveur. Mais il m’arrive aussi de l’utiliser pour transférer des fichiers vers mon serveur quand je n’ai pas envie d’ouvrir un logiciel tel que Filezilla. Je vais donc vous apprendre (de manière succincte) à vous servir de SCP, pour plus d’informations , taper « man scp » dans votre terminal . Notez que dans cet article les dossier sont des dossiers sur système Unix (En effet, /home/jeremy/ est mon répertoire personnel sur mon ordinateur tournant sous Debian une distribution GNU/Linux).

## Backup de fichier ##

Serveur1 –> Serveur2 (Dans le cas d’envoi de dossier)

    scp -r -p mylogin1@myserveur1:dossier1/ mylogin2@myserveur2:dossier2/

Serveur –> Ordinateur (Dans le cas d’envoi de dossier)

    scp -r -p mylogin@myserveur:dossier/ /home/jeremy/dossier/

Serveur1 –> Serveur2 (Dans le cas d’envoi d’un seul fichier)

	scp -p mylogin1@myserveur1:dossier1/mon_fichier1.txt mylogin2@myserveur2:dossier2/mon_fichier2.txt

Serveur –> Ordinateur (Dans le cas d’envoi d’un seul fichier)

	scp -p mylogin@myserveur:dossier/mon_fichier.txt /home/jeremy/dossier/mon_fichier.txt

## Envoi de fichier ##

Si vous désirez envoyer un dossier de votre ordinateur vers votre serveur :

	scp -r -p /home/jeremy/dossier/ mylogin@myserveur:dossier/

Si vous désirez envoyer un fichier de votre ordinateur vers votre serveur :

	scp -p /home/jeremy/dossier/ mylogin@myserveur:dossier/

## Explications ##

Dans mes exemples j’ai introduit deux options en plus de la commande scp, que je vais vous expliquer directement.

L’option -r signifie « récursif », cela signifie que si vous envoyez un dossier (qui contient donc plusieurs fichiers et/ou sous-dossiers), scp parcourra tout ce dossier mais aussi les liens symboliques. Vous remarquerez que dans les commandes où je me contente de n’envoyer qu’un seul fichier, l’option -r disparaît car elle est bien entendu inutile.

L’option -p signifie que scp gardera les dates de modifications et de créations des fichiers et répertoires ainsi que leur droit en lecture et écriture.

Pour plus d’informations tournez vous vers les pages de manuel sur vos distributions en tapant tout simplement « man ssh » ou « man scp » dans un terminal. Ou alors rendez vous sur les pages wikipedia des deux protocoles SSH et SCP