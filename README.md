# Read-only ([source][read-only])

Si c'est le cas désactiver la journalisation du disque HFS+ avec la commande :

    sudo diskutil disableJournal volumeName

Installer le programme suivant :

    sudo apt-get install hfsprogs

Vérifier le point de montage du disque (monté automatiquement par osmc) avec 

    mount
    
On doit voir apparaitre le point de montage en lecture seule "ro". Exemple :

    /dev/sda2 on /media/BluBook type hfsplus (ro,nosuid,nodev,relatime,umask=22,uid=0,gid=0,nls=utf8,uhelper=udisks)
  
Le remonter avec la commande :

    sudo mount -o remount,rw,force /mount/point
    
Si le démontage est bloqué parce qu'OSMC l'utilise, l'éjecter depuis l'interface OSMC. Puis le remonter manuellement... (détails ?)
    
Vérifier que le disque est maintenant en lecture-écriture "rw". Exemple :

    /dev/sda2 on /media/BluBook type hfsplus (rw,nosuid,nodev,relatime,umask=22,uid=0,gid=0,nls=utf8,uhelper=udisks)


# Mac Fusion

Installer OSXFuse (ex MacFUSE) puis Mac Fusion.
Monter ensuite /mount/point depuis MacFusion. Une connexion sshfs sera établie.
Via ssh ajouter les droits au dossier voulu avec

    sudo chmod o+w /mount/point/dossier

# [Date] (NTP)

Couper le service NTP et relancer le démon :

    sudo systemctl stop ntp
    sudo ntpd -qg

La correction appliquée à la date doit s'afficher. Relancer alors le service NTP :

    sudo systemctl start ntp

Vérifier la correction au bout d'une minute (une ligne préfixée * => synchro NTP) :

    ntpq -p

[date]: https://discourse.osmc.tv/t/fix-date-and-time/3120/13?u=bludwarf

# Node JS

Installation ([source][njsi]) :

    curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
    sudo apt install nodejs

# Sécurité

## SSH

Clé privée et clé publique :

    ssh-keygen

Certificat et clé privée ([source][cert]) :

    openssl req -x509 -nodes -newkey rsa:4096 -keyout myApp.key -out myApp.crt -days 365

L'option `-nodes` pour ne pas mettre de mot de passe à la clé privée.

# Scripts au démarrage

Utiliser le fichier rc.local ([doc][doc-rc])

    sudo nano /etc/rc.local

Ou utiliser cron :

    sudo apt-get install cron
    crontab -e
    
# Filesystem

Agrandir le filesystem à la carte SD : [lien](http://raspberrypi.stackexchange.com/a/501)

[njsi]: http://thisdavej.com/beginners-guide-to-installing-node-js-on-a-raspberry-pi/
[read-only]: http://superuser.com/a/348870
[cert]: http://stackoverflow.com/a/10176685/1655155
[doc-rc]: https://www.raspberrypi.org/documentation/linux/usage/rc-local.md
