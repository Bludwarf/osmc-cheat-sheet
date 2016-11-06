# Read-only ([source][read-only])
Installer le programme suivant :

    sudo apt-get install hfsprogs

Vérifier le point de montage du disque (monté automatiquement par osmc) avec 

    mount
    
On doit voir apparaitre le point de montage en lecture seule "ro". Exemple :

    /dev/sda2 on /media/BluBook type hfsplus (ro,nosuid,nodev,relatime,umask=22,uid=0,gid=0,nls=utf8,uhelper=udisks)
  
Le remonter avec la commande :

    sudo mount -o remount,rw,force /mount/point
    
Vérifier que le disque est maintenant en lecture-écriture "rw". Exemple :

    /dev/sda2 on /media/BluBook type hfsplus (rw,nosuid,nodev,relatime,umask=22,uid=0,gid=0,nls=utf8,uhelper=udisks)
    
[read-only]: http://superuser.com/a/348870


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
