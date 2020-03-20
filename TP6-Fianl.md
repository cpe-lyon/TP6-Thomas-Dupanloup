#TP6 - Gestion des disques,Bootn Gestion des logs.

##Dupanloup Shana - Thomas Pierrick

###Exercice 1

__1. Dans l’interface de configuration de votre VM, créez un second disque dur, de 5 Go dynamiquement
alloués ; puis démarrez la VM__

On créer un disque dur via l'interface de VM de 5Go. On a créé un nouveau disque virtuel de taille fixe ( un fichier vdi sur notre machine hôte)


__2. Vérifiez que ce nouveau disque dur est bien détecté par le système__

On vérifie que ce disque est bien présent avec ````lsblk```. On observe bien un disque /dev/sdb de taille 5go. 

__3. Partitionnez ce disque en utilisant fdisk : créez une première partition de 2 Go de type Linux (n°83),
et une seconde partition de 3 Go en NTFS (n°7)__ 

Pour partitionner ce disque on utilise la commande ```sudo fdisk /dev/sdb``` on créer ensuite nos partitions en calculant la bonne taille de segment.
On peut vérifier à l'aide de ```lsblk```que l'on a bien 2 partitions sdb1 et sdb2 qui sont faites. 

__4. A ce stade, les partitions ont été créées, mais elles n’ont pas été formatées avec leur système de fichiers.
A l’aide de la commande mkfs, formatez vos deux partitions (! pensez à consulter le manuel !)__

On formate notre deuxième partition à l'aide de la commande : ```sudo mkds -t ntfs /dev/sdb2```

__5. Pourquoi la commande df -T, qui affiche le type de système de fichier des partitions, ne fonctionne-telle pas sur notre disque ?__

Cette commande ne fonctionne pas nos disque car ces derniers ne sont pas montés pour notre système. Il faut donc les monter au préalable.

6. Faites en sorte que les deux partitions créées soient montées automatiquement au démarrage de la machine, respectivement dans les points de montage /data et /win (vous pourrez vous passer des
UUID en raison de l’impossibilité d’effectuer des copier-coller)

Pour monter nos deux partitions on va commencer par créer nos répertoires dans lesquels on veut les monter avec la commande ```sudo mkdir /data /win```
On va ensuite modifier le fichier /etc/fstab de façon monter nos partitions au moment du boot. 

On monte ensuite nos partitions avec les deux lignes suivantes :

```bash 
sudo mount /dev/sdb1 /data
sudo mount /dev/sdb2 /win 
```
__7. Utilisez la commande mount puis redémarrez votre VM pour valider la configuration__

Après avoir redémaré la VM si l'on tape la commande ```lsblk``` nos partitions sont bel et bien montés. 



