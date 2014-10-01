# Interdire le ssh de root #
## Sécuriser son serveur en interdisant la connexion de l'utilisateur root ##

La première chose à faire est de créer un utilisateur qui pourra se connecter. Débile comme remarque ? Un âne averti en vaut deux ;)

Donc la commande de création de mon utilisateur est :

	root@home:~# useradd -m -d /home/monutilisateurtropbien/ -s /bin/bash monutilisateurtropbien

Ensuite je change le mot de passe de monutilisateurtropbien :

	root@r16721:~# passwd monutilisateurtropbien
	Enter new UNIX password:
	Retype new UNIX password:
	passwd : le mot de passe a été mis à jour avec succès

**VÉRIFIEZ** que vous pouvez bien vous connecter en tant que **monutilisateurtropbien**.

Maintenant, il ne reste plus qu'à configurer le démon ssh pour qu'il n'accepte plus l'utilisateur root :

### Interdire le login de root via ssh ###

Édition du fichier de configuration de sshd :

	root@home:~# vi /etc/ssh/sshd_config

Remplacer :

	PermitRootLogin yes
Par: 
	
	PermitRootLogin no


On redémarre le démon :

	root@home:~# /etc/init.d/ssh restart

### Autoriser le login de root via ssh uniquement via une clé ###

Vous pouvez aussi autoriser le login root uniquement à l'aide d'une clé ssh avec la directive suivante dans le fichier /etc/ssh/sshd_config :

	PermitRootLogin without-password

Encore une fois pour que les modifications soient prises en compte il faut redémarrer le démon sshd :
	
	root@home:~# /etc/init.d/ssh restart



