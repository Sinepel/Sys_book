# ncftpget : copie récursive de fichiers depuis un serveur FTP #


**ncftpget** est un utilitaire en ligne de commande qui permet de copier **récursivement** une arborescence de fichiers d’un serveur **FTP** distant. Quand on n’a pas d’autres moyens d’accès que le FTP c’est un petit programme bien pratique.

On peut le télécharger ici http://www.ncftp.com/ncftp/, pour Debian et Ubuntu on fera :

	sudo aptitude install ncftp


Exemple d’utilisation :

Pour copier tous les fichiers du répertoire **/var/www** du serveur **www.exemple.com** avec le user FTP « **machin** » vers le répertoire **/var/www/sitemachin** de la machine locale :

	ncftpget –R –v –u "machin" www.exemple.com /var/www/sitemachin /var/www


avec :

	-R : copie récursive
	-v : mode verbeux
	-u "machin" : nom de l'utilisateur FTP

Lien : [Linux: Download all file from ftp server recursively](http://www.cyberciti.biz/tips/linux-download-all-file-from-ftp-server-recursively.html)