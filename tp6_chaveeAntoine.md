 # TP 6 - Gestion des disques /Tâches d’administration 


<h1>Exercice 1. Disques et partitions
</h1>

<ol>
<li><h3>Vérifiez que ce nouveau disque dur est bien détecté par le système<h3></li>

*cette commande permet de visualiçser tout les disk de notre vm*
<code>
ll /dev/sd*
</code>

*pour plus d'information sur les disks*

<code>
sudo fdisk -l
</code>

<li><h3>Partitionnez ce disque en utilisant fdisk : créez une première partition de 2 Go de type Linux (n°83),
et une seconde partition de 3 Go en NTFS (n°7)
<h3></li>

*Lancer l’interface de partitionnement fdisk en ligne de commande, en précisant le disque à modifier :*
<code>
fdisk /dev/sdb
</code>

*On va alors créer une première partition primaire, de 40 Go (soit 40960 mo), via la touche n :*
<code>
Command action
e extended
p primary partition (1-4)
p
Partition number (1-4): 1
First cylinder (1-19452, default 1):
Using default value 1
Last cylinder or +size or +sizeM or +sizeK (1-19452, default 19452): +2G
</code>

*Mes deux partitions sont bien créées correctement, il ne reste plus qu’à sauvegarder les modifications (touche w) et quitter :*

<code>
Command (m for help): w
The partition table has been altered!
Calling ioctl() to re-read partition table.
Syncing disks. 
</code>


<li><h3>A ce stade, les partitions ont été créées, mais elles n’ont pas été formatées avec leur système de fichiers.
A l’aide de la commande mkfs, formatez vos deux partitions ( pensez à consulter le manuel !)
<h3></li>

<code>
# mkfs -t ext3 /dev/sdb1
mke2fs 1.32 (09-Nov-2002)
Filesystem label=
OS type: Linux
...
Writing inode tables: done
Creating journal (8192 blocks): done
Writing superblocks and filesystem accounting information: done 

</code>

*nous allons typer notre partition en NTFS*

<code>
sudo mkfs.ntfs /dev/sdb2
</code>
<li><h3>Pourquoi la commande df -T, qui affiche le type de système de fichier des partitions, ne fonctionne-telle pas sur notre disque ?
</h3></li>

*on ne peut pas afficher les information car on na pas monter notre systéme de fichier*

<li><h3>Faites en sorte que les deux partitions créées soient montées automatiquement au démarrage de la
machine, respectivement dans les points de montage /data et /win (vous pourrez vous passer des
UUID en raison de l’impossibilité d’effectuer des copier-coller)
</h3></li>

*Le fichier de configuration dans ce cas est / etc / fstab . Il contient des options pour chaque lecteur et les paramètres de montage au démarrage. Vérifiez votre fichier / etc / fstab. Il devrait ressembler à ceci*

*Listez les partitions*
<code>
$ sudo fdisk -l
</code>
*Récupère l'UUID de la partition*
<code>
$ sudo blkid
</code>
*maintenant on rajooute uid et les 6 autres information pour monter notre file système dans notre vm*
<code>
$ sudo nano /etc/fstab
</code>

<li><h3>Utilisez la commande mount puis redémarrez votre VM pour valider la configuration
</h3></li>
<code>
$ sudo mount -a
</code>

</ol>

<h1>Exercice 2. Partitionnement LVM
</h1>
<ol>


<li><h3>On va réutiliser le disque de 5 Gio de l’exercice précédent. Commencez par démonter les systèmes de
fichiers montés dans /data et /win s’ils sont encore montés, et supprimez les lignes correspondantes
du fichier /etc/fstab
</h3></li>

*pour enlever le systéme de fichier nous allons utiliser*

<code>
sudo amount /data
</code>

*et maintenant nous allons supprimez les lignes dans fstab*

<code>
sudo nano /ect/fstab
with  ctlr k
</code>


<li><h3>Supprimez les deux partitions du disque, et créez une patition unique de type LVM
</h3></li>

*pour supprimer les deux partitions nous allons faire*

<code>
sudo fdisk /dev/sdb
 commande d
 selection num part
</code>

*on va créer une partition*

<code>
sudo fdisk /dev/sdb
 commande d
 selection num part
</code>

</ol>
