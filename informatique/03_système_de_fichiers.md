# Ordinateur : le système de fichiers

Un système de fichiers est une façon d'organiser les informations sur un support
de masse comme un disque dur ou une clé USB.

Le système de fichiers le plus connu est sans doute le FAT32 (File Allocation
Table 32 bits). Chaque système d'exploitation a son ou ses systèmes de fichiers.

Sous linux, on verra `ext4` par exemple, un système adapté aux nouveaux disques
dur SSD (Solid State Drive). Sous Windows il existe NTFS qui permet de gérer
les droits d'accès directement dans le système de fichiers et donc d'autoriser
ou non la lecture des fichiers en fonction de l'utilisateur connecté.

Le système de fichiers détermine la manière dont l'espace mémoire d'un disque
dur est utilisable. Il y a par exemple souvent une **taille de blocs** qui va
indiquer combien d'octets contigüs on peut utiliser en une seule fois. Cette
taille est fixe mais peut être paramétrée lors du **partitionnement** d'un 
disque dur. 

Chaque **bloc** de données contient des **données utiles** ainsi que des données
de la **table d'allocation**. Les données de la table d'allocation servent à 
chaîner les blocs entre eux pour former des **fichiers**. 

Un fichier est donc un ensemble de blocs qui peuvent être stockés physiquement 
à des endroits opposés d'un disque dur !

Pour simplifier, retenons que chaque bloc contient :
1. La taille des données utiles qu'il contient
2. Les données utiles du fichier
3. L'adresse du bloc suivant

> Exemple d'un fichier de 17Ko stocké sur 2 blocs de 16Ko :
>
> | Adresse |Taille utile | Données                 | Adresse du bloc suivant |
> |---------|-------------|-------------------------|-------------------------|
> | @0040A2 |  16Ko       | 0x40 0xFE 0x30 ...      | @FFCD20
> | @010D58 |  1Ko        | ...                     | NULL (0x000000)
>
>
> **NOTE** :
> La première conséquence qu'on peut voir ici, c'est qu'un fichier de 17ko de 
> données utiles prendra 32Ko d'espace sur le disque dur. Un système FAT32
> configuré avec une taille de bloc de 16Ko est donc plus adapté au stockage de 
> grands fichiers plutôt que plein de petits fichiers.