# Bonnes pratiques pour l'installation d'un VPS #


----------

## Installation du serveur Web ##
- Apache2
- PHP5
- MySQL
- PHPMyAdmin
- Script « Newsite »
- PostFix
## Backup ##
- AutoMySQLBackup
- VEEAM (géré par OVH)
## Sécurité ##
- Créer utilisateur « dev » (le mettre dans le groupe www-data -> Group ID : 33)
- Interdire le « root » en SSH
- Mettre le port SSH à « 30000 »
- Installer Fail2Ban
- Créer un .htaccess pour PHPMyAdmin
- Installer « LogWatch » (récapitulatif des logs par Mail tous les matins)

## Liste des VPS ##
- vps13437.ovh.net
- vps36261.ovh.net
- vps55491.ovh.net
- vps74001.ovh.net
- vps79332.ovh.net
- vps91757.ovh.net