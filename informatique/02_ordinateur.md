# Fonctionnement d'un ordinateur

Le composant de base d'un ordinateur est le **transistor**. Un transistor est un
composant électronique à 3 broches, qui permet de simuler des fonctions logiques
(ET, OU ...). Il agit un peu comme un interrupteur, commandé par une tension 
électrique. Lorsque qu'on applique une tension sur la borne de commande d'un 
transistor, il laisse passer le courant entre ses 2 autres bornes.

Un ordinateur transforme de l'énergie électrique en nombres binaires grâce à des
transistors. Quand un transistor est "passant", on interprète par la valeur 1.
S'il est "non passant", c'est la valeur 0. Ces nombres sont ensuite stockés dans
des registres (sortes de mémoires à court terme mais très rapides) pour qu'on
les utilise pour réaliser des opérations (addition, remise à zéro, 
multiplication...).

Ces nombres sont enregistrés sur un support électro-magnétique (disque 
dur, RAM) et sont utilisés pour créer de l'information (texte, images, vidéos) 
affichables sur un écran.


## Schéma d'un ordinateur

![Schéma d'un ordinateur](https://www.courstechinfo.be/Techno/Images/SchemaBloc.png)

[https://www.courstechinfo.be/Techno/ArchMat.html#SchemaBloc](https://www.courstechinfo.be/Techno/ArchMat.html#SchemaBloc)


## Rôle des composants

### Le microprocesseur

Le composant le plus important à comprendre est le microprocesseur. Il est
composé lui-même des milliards de **transistors**, agencés pour fournir des 
fonctionnalités évoluées, qu'on appelle un **jeu d'instructions**. Ces 
instructions ou fonctions sont souvent nommées par des acronymes de 3 ou 4 
lettres et dépendent de l'architecture du processeur (la plupart du temps ce 
sera Intel pour les PC).

Le **langage d'assemblage** est le langage de programmation qui utilise ces 
instructions directement compréhensibles par le microprocesseur. 
**L'assembleur** est le programme qui permet de traduire les mots-clés en 
chiffres (c'est plus simple qu'un compilateur).

Ceci permet de faire des opérations mathématiques mais aussi des opérations de 
déplacement de bits, permutations, effacements, initialations de mémoire à une 
valeur particulière,  sauts ...etc.

Un processeur réalise des opérations sur des **registres** (des éléments de 
mémoire internes au processeur et très rapides). Comme le nombre de registres 
est petit et limité, le processeur fonctionne en permanence avec la **mémoire 
vive** (RAM) pour aller lire et écrire des valeurs dont la durée de vie est plus
longue que l'opération en cours. Cependant la RAM s'efface quand l'ordinateur 
n'est plus sous tension.

On appelle **compteur ordinal** le numéro d'adresse qui contient l'instruction 
courante à exécuter. Ce qu'on appelle **un saut** est une instruction qui 
déplace ce compteur ordinal ailleurs dans la mémoire.

Concrètement, voici ce qui se passe en boucle dans le processeur :

	1) Initialisation du compteur ordinal à l'adresse mémoire initiale
	2) Lecture de l'instruction
	3) Lecture des opérandes
	4) Copie des opérandes sur la pile d'exécution
	5) Réalisation de l'opération
	6) Saut vers l'instruction suivante puis on recommence en 2)

_Exemples d'instructions (opcodes) avec leurs opérandes :_
>
> |Instruction & opérandes     | Commentaires                                             |
> |----------------------------|----------------------------------------------------------|
> |**INC** rcx                 | Cette opération incrémente la valeur du registre 'rcx'   |
> |**MOV** rcx, 1              | Envoie la valeur '1' dans le registre 'rcx'              |
> |**JMP** <_adresseXYZ_>      | Déplace le compteur ordinal à l'adresse '<_adresseXYZ_>' |
> |**ADD** rcx, rca            | Additionne les registres 'rcx' + 'rca' dans 'rcx'        |


*Pour approfondir sur le langage d'assemblage :* [https://www.esaracco.fr/documentation/assembly/assembly.pdf](https://www.esaracco.fr/documentation/assembly/assembly.pdf)


#### Fréquence du microprocesseur

On dit qu'un processeur est "cadencé" à une certaine fréquence car sur le plan 
électrique, il existe une **horloge à quartz** permettant d'envoyer un signal de
X impulsions par seconde vers le processeur. Il s'agit d'un *signal de commande*
(ie. ne véhicule pas d'informations car sa tension ne peut être que 0V ou 3V et 
sa fréquence est fixe). Il est simplement là pour **déclencher la prochaine 
opération automatiquement** sans intervention humaine. Les processeurs récents 
peuvent avoir une fréquence de plusieurs Giga Hertz (GHz).

#### 32 bits ou 64 bits ?

La famille la plus récente de microprocesseurs qui équipe les PC portables et 
les PC de bureau est la famille i686. De manière générale les différentes 
architectures récentes de microprocesseurs Intel se nomment x86 (386, 486, 586 
et 686, avec à chaque évolution l'ajout de nouvelles fonctions).

Comme un processeur est censé lire des valeurs en RAM, il faut qu'on puisse 
"adresser" ces valeurs, c'est à dire leur attribuer une adresse de stockage. Une
adresse est un numéro d'octet en mémoire et le nombre de bits du processeur va 
déterminer le numéro maximum que le processeur peut "atteindre". Aujourd'hui 
avec plusieurs dizaines de Giga Octets de RAM, il faut 64 bits pour pouvoir 
former des numéros d'adresses suffisamment grands et atteindre les octets dans 
ces mémoires. Pour rappel, sur 32 bits on ne peut adresser que 4 Go de RAM, d'où
l'apparition des processeurs 64 bits.


#### La pile d'exécution

La pile est un espace de stockage temporaire. On y empile des valeurs avec le 
mot-clé `push` et on les retire avec le mot-clé `pop`.

|Etat initial :|
|-----|
|vide |

	PUSH 10
	PUSH 20

|Nouvel état de la pile :|
|-----|
|20   |
|10   |

Exécution de l'opération "ADD"

	ADD # Cette opération enlève 2 opérandes de la pile et empile le résultat
	
|Nouvel état de la pile :|
|-----|
|30   |


## BIOS et séquence de boot

Le BIOS est le programme qui va permettre d'initialiser (boot) l'ordinateur avec
une séquence d'instructions toujours identiques. Il s'agit d'un programme 
inaltérable stocké dans une mémoire "morte" (ROM). A la mise sous tension, ce 
programme va être automatiquement copié en RAM et le processeur l'exécute.

Ce programme va scruter les contrôleurs d'entrées/sorties à la recherche d'une 
amorce. Le premier contrôleur trouvé avec une amorce valide est chargé en 
mémoire à la place du programme du BIOS.

Le programme d'amorçage est ensuite exécuté pour charger un système 
d'exploitation.

## Le chargement de l'OS

Le système d'exploitation ou OS (Operating System) est le premier et le 
principal programme exécuté par l'ordinateur. Il a pour objectif de communiquer 
avec les périphériques via des programmes subalternes qu'on appelle des pilotes 
et des contrôleurs d'entrées/sorties.


## Pour approfondir

[https://www.courstechinfo.be/Techno/index.html](https://www.courstechinfo.be/Techno/index.html)