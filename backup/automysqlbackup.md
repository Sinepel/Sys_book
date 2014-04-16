# AutoMySQLBackup #


Pour sauvegarder son serveur, c’est souvent un peu chiant d’exporter les bases de données. Lorsqu’on utilise un outil comme backupPC, on est obligé de faire un peu de tuning plus ou moins propre.
Heureusement qu’un outil hyper simple est disponible pour sauvegarder chaque jour, chaque semaine, et chaque mois ses bases de données MySQL : AutoMysqlBackup
## Installation ##

Le paquet est présent dans les dépots debian/ubuntu :

	apt-get install automysqlbackup
## Configuration ##
Il n’y en a juste pas !!!
Par défaut, lors de l’installation, un nouveau fichier est crée : /etc/cron.daily/automysqlbackup
Il automatisera les sauvegardes quotidienne.
Si vous voulez personnaliser quelques paramètres, le fichier de configuration est ici :

	/etc/default/automysqlbackup 
Vous pourrez régler les notifications email, le dossier de sauvegarde, les bases de données à exclure…

Enfin, le répertoire de sauvegarde est dans :

	/var/lib/automysqlbackup/

Vous aurez alors 3 dossiers :

daily

weekly

monthly

Ne vous inquiétez pas si vous cherchez saturday dans daily, c’est en fait celle de weekly, pour éviter les doublons.

Les bases sont déjà compressées, et vous pouvez même les crypter.