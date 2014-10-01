## Comment marche Fail2Ban ? ##

Développé en langage Python, **Fail2Ban** est un logiciel libre permettant d'analyser des fichiers de logs et de déclencher des actions si certaines choses suspectes sont détectées. 

La grande force de Fail2Ban est sa grande modularité que cela soit au niveau des mécanismes de détections basées sur les expressions régulières ou sur les actions à mener qui peuvent aller de l'expédition d'un mail à la mise en place de règles de Firewall.


Fail2Ban se base sur un système de prisons (jails) que l'on peut définir, activer ou désactiver dans un simple fichier de configuration (/etc/fail2ban/jail.conf).


Une prison (jail) est composée, entre autres, des éléments suivants:

- Nom du fichier de log à analyser.
- Filtre à appliquer sur ce fichier de log (la liste des filtres disponibles se trouve dans le répertoire /etc/fail2ban/filter.d). Il est bien sûr possible de créer ses propres filtres.
- Paramètres permettant de définir si une action doit être déclenchée quand le filtre correspond ("match"): Nombre de "matchs" (maxretry), intervalle de temps correspondant (findtime)...
- Action à mener si nécessaire. La liste des actions se trouve dans le répertoire /etc/fail2ban/action.d. Il est également possible de créer ses propres actions.

## Installation de Fail2Ban ##

On commence par installer Fail2Ban sur son système. Il se trouve dans la grande majorité des distributions GNU/Linux et BSD. par exemple pour l'installer sur une machine Debian 6, il suffit de saisir la commande suivante (en root ou bien précédée d'un sudo):
Shell


	apt-get install fail2ban

## Protection contre les attaques "brute force" SSH ##

Un exemple étant toujours plus parlant, nous allons configurer notre Fail2Ban pour bloquer automatiquement les adresses IP des machines essayant des attaques de type "brute force" sur notre port SSH (cette attaque est à la portée de n'importe quel "neuneu". On trouve de très bon tutoriaux sur le sujet sur le net).

Si une machine cliente échoue 3 fois de suite lors de la saisie du couple login/password sur le serveur SSH alors on bloque l'accès au port TCP/SSH pendant 15 minutes. On analyse pour cela le fichier de log **/var/log/auth.log** en lui appliquant le filtre /etc/fail2ban/filter.d/sshd.conf puis, si nécessaire, l'action **/etc/fail2ban/action.d/iptables.conf**. La définition de cette prison (jail) est à faire dans le fichier **/etc/fail2ban/jail.conf**:

	# SSH
	# 3 retry ? > Ban for 15 minutes
	 
	[ssh]
	enabled = true
	port = ssh
	filter = sshd
	action = iptables[name=SSH, port=ssh, protocol=tcp]
	logpath = /var/log/auth.log
	maxretry = 3
	bantime = 900

