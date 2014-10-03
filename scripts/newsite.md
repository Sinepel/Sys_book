# Script "newsite"

## Améliorations à venir :
- Création de la BDD automatique
- Envoyer les informations par mail

## Code :

>     #!/bin/bash
>     echo -e "\n*** MDWEB - CREATION DE SITE ***\n"
>     echo "Adresse du site (sans http://) : "
>     read adresseSiteBrute
>     adresseSiteUnderscoree=${adresseSiteBrute//[.]/_}
>     
>     echo "<VirtualHost *:80>
>     DocumentRoot /var/www/$adresseSiteUnderscoree/
>     ServerName $adresseSiteBrute
>     <Directory /var/www/$adresseSiteUnderscoree/>
>     Options +Indexes +FollowSymLinks +MultiViews +Includes
>     AllowOverride All
>     Order allow,deny
>     allow from all
>     </Directory>
>     </VirtualHost>" /etc/apache2/sites-available/$adresseSiteBrute
>     echo "Création du VirtualHost [OK]"
>     
>     mkdir /var/www/$adresseSiteUnderscoree
>     chmod -R 770 /var/www/$adresseSiteUnderscoree
>     chown -R www-data:www-data /var/www/$adresseSiteUnderscoree
>     
>     a2ensite $adresseSiteBrute
>     echo "Activation du VirtualHost [OK]"
>     
>     /etc/init.d/apache2 restart
>     echo "Redémarrage d'Apache [OK]"
>     
>     motDePasseFTP=$(cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 20 | head -n 1)
>     #ftpasswd --passwd --name=$adresseSiteUnderscoree --home=/var/www/adresseSiteUnderscoree --shell=/bin/false --uid=33 --gid=33
>     echo $motDePasseFTP | ftpasswd --stdin --passwd --name=$adresseSiteUnderscoree --home=/var/www/$adresseSiteUnderscoree --shell=/bin/false --uid=33 --gid=33 --file=/etc/proftpd/ftpd.passwd
>     
>     echo -e "\nRécapitulatif :\n"
>     echo -e "   Adresse du site :   http://$adresseSiteBrute\n"
>     echo -e "   Serveur FTP :   $adresseSiteBrute"
>     echo -e "   Utilisateur FTP :   $adresseSiteUnderscoree"
>     echo -e "   Mot de passe FTP :  $motDePasseFTP\n"
>     echo -e "   Répertoire :/var/www/$adresseSiteUnderscoree\n\n"
