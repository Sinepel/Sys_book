# Se connecter en ssh sans demande de mot de passe #

J'ai une machine (A), avec un compte "benjamin" à partir de laquelle je souhaite me connecter en root sur une autre machine (B) sans demande de mot de passe.

## Sur la machine A (en utilisateur benjamin) : ##

	ssh-keygen -t rsa, puis 3 fois Entrée
Cette commande me génère une clé publique et une clé privée (dans l'ordre, id_rsa.pub et id_rsa) dans le dossier /home/benjamin/.ssh
Ensuite, il faut copier la clé publique (id_rsa.pub) dans un fichier authorized_keys dans le dossier /root/.ssh de la machine B.


## Sur la machine B : ##

	sudo mkdir /root/.ssh
Créé le dossier /root/.ssh

## Sur la machine A : ##

	scp /home/benjamin/.ssh/id_rsa.pub 192.168.1.4:/root/.ssh/authorized_keys
En supposant que l'adresse IP de la machine B soit 192.168.1.4.
Il faut, uniquement cette fois, taper le mot de passe root de la machine B. Cette commande copie le fichier /home/benjamin/.ssh/id_rsa.pub dans le fichier /root/.ssh/authorized_keys de la machine B (même si ce fichier n'existe pas).
Toujours sur la machine A (en utilisateur benjamin) :

	ssh root@192.168.1.4 (puis confirmer avec yes)

Plus aucun mot de passe ne sera demandé.
Le fichier /home/benjamin/.ssh/known_hosts contient les 'identifiants' du pc sur lequel on a voulu se connecter.

Résumé :
> - Je génère une clé publique ssh avec le compte benjamin sur la machine A,
> - je la copie sur la machine B dans le fichier /root/.ssh/authorized_keys (si je veux avoir accès au compte root sans mot de passe),
> - à partir de la machine A (avec le compte benjamin) je me connecte en ssh sur la machine B (ssh root@adresse_ip_machineB)
> - il se créé donc un fichier /home/benjamin/.ssh/known_hosts contenant l'identité de la machine B.

----------


Note : Pour améliorer la sécurité de ces connexions par clé RSA, nous pouvons restreindre l'utilisation de la clé d'authentification à l'adresse IP de la machine A en ajoutant from="" devant la clé dans le fichier authorized_keys.
Ce dernier ressemblera donc à ceci :


from="192.168.1.2" ssh-rsa AB3NzaC1yc2EAzYABIwAb[...]


----------


Note 2 : Une fois que nos clés publiques/privées ont été générées sur la machine A (étape 1), il est possible "d'**automatiser**" tout le reste avec une seule commande : **ssh-copy-id**
Très simplement, sur la machine A, vous n'avez qu'à taper :

	ssh-copy-id root@192.168.1.4 
(pour reprendre notre exemple). Cette commande se chargera de créer le répertoire .ssh et de remplir le fichier authorized_keys automatiquement sur la machine distante.

Pour les connexions SSH sur un port autre que le port 22, il faut lancer la commande ssh-copy-id "-p 2224 root@192.168.1.4" Utilisez cette procédure avec prudence, en particulier avec les comptes root.
Laisser un accès libre à une machine en root est un manque de sécurité évident, malgré toutes les précautions préalables.