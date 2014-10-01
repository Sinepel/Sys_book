# Rkhunter #

**Rootkit Hunter** est un programme de détection de rootkits. Vous pouvez l'installer grâce à :

	apt-get install rkhunter

Il procédera à des détections journalières anti-rootkits et enverra des notifications par e-mail si nécessaire. Il est conseillé de l'installer très tôt car il calcule l'empreinte MD5 des programmes installés afin de détecter d'éventuels changements. Editez /etc/default/rkhunter pour indiquer l'adresse de notification et l'exécution journalière :

	vi /etc/default/rkhunter

	REPORT_EMAIL="monitoring@test.com"
	CRON_DAILY_RUN="yes"

En cas de fausses détections positives sur des répertoires ou fichiers existants et sains, éditez /etc/rkhunter.conf pour les ajouter à la liste des éléments autorisés.

	vi /etc/rkhunter.conf


	ALLOWHIDDENDIR=/dev/.udev
	ALLOWHIDDENDIR=/dev/.static

Vous pouvez également utiliser chkrootkit qui est un équivalent.