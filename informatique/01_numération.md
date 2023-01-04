# Quelques bases mathématiques en **numération**

La numération est la façon dont on forme des nombres. Par exemple, on ne compte
pas de la même façon quand on compte des heures (qui vont de 0 à 24) ou quand on
compte des minutes (de 0 à 60).


## Notation décimale (base 10)

Dans la vie usuelle, les nombres sont représentés en base 10, c'est à dire qu'ils sont
composés de plusieurs chiffres allant de 0 à 9 et dont le poids est exprimé en 
puissances de 10. Chaque chiffre en partant de la droite a un poids croissant.

Ce qu'on appelle le **poids** d'un chiffre est la puissance de 10 à laquelle il 
faut élever ce chiffre.  C'est son numéro de rang (unité = rang 0, dizaines = rang 1, 
centaines = rang 2...)

On peut ainsi décomposer le nombre 394 comme suit :

394 = **3** x 10<sup>2</sup> + **9** x 10<sup>1</sup> + **4** x 10<sup>0</sup>


## Binaire (base 2) et hexadécimal (base 16)

En informatique, les chiffres sont généralement exprimés en binaire (base 2) ou 
en hexadécimal (base 16). Chaque chiffre qui compose le nombre sera donc exprimé
soit en puissances de 2 ou en puissances de 16. **La valeur d'un nombre et sa 
représentation en base 2, 10 ou 16 sont indépendantes.**

> Exemple pour la valeur 42 :
>
> Décomposition en puissances de 2  : 42 = 32 (1x2<sup>5</sup>) + 8 (1x2<sup>3</sup>) + 2 (1x2<sup>1</sup>) = **101010**
>
> Décomposition en puissances de 16 : 42 = 32 (2x16<sup>1</sup> + 10x16<sup>0</sup>) = **2A**

Inversement, l'interprétation d'un nombre exprimé en binaire ou en hexadécimal 
se déroule comme suit :

10001011 = 1x2<sup>7</sup> + 1x2<sup>3</sup> + 1x2<sup>1</sup> + 1x2<sup>0</sup> = 128 + 8 + 2 + 1 = **139**

5F = 5x16<sup>1</sup> + 16x16<sup>0</sup>= 80 + 15 = **95**



## MSB et LSB

> Pour désigner les bits de poids fort ou de poids faible on parle de "MSB" 
(Most Significant Bit) ou "LSB" (Least Significant Bit). 


> **ATTENTION** : Dans certains types de fichiers, ** le MSB peut être à droite** ! Mais
en général le MSB est à gauche dans la plupart des systèmes et des fichiers.



## Codage de l'information

Coder l'information c'est donner un sens "humainement compréhensible" à des nombres,
et donc aux octets qui encodent ces nombres.

Un octet étant composé de 8 bits, le nombre entier maximum qui peut s'exprimer sur 8 bits
est 2<sup>7</sup> + 2<sup>6</sup> + 2<sup>5</sup> + 2<sup>4</sup> + 2<sup>3</sup> + 2<sup>2</sup> + 2<sup>1</sup> + 2<sup>0</sup> = 255.

La valeur d'un octet varie donc de 0 à 255, ce qui donne 256 valeurs possibles. En hexa, 
la valeur d'un octet varie de `00` à `FF`.

Très souvent on dira qu'un groupe d'octets est un **mot* (désigné par le mot-clé "WORD" 
ou parfois "DWORD" dans certains langages comme le C). On peut ainsi trouver des mots de 
4 octets, 8 octets voire 16 octets.

Naturellement, plus il y a d'octets pour encoder un nombre, plus on peut encoder de 
grands nombres.


## Comment sont exprimés les nombres négatifs ?

Par convention, on utilise le MSB pour encoder le signe d'un nombre.
Le premier bit désignera donc le signe (négatif s'il est à 1 et positif sinon) et le reste 
servira à exprimer la valeur. Le poids du premier bit "utile" d'un nombre signé
sur 1 octet sera donc 2<sup>6</sup> et non pas 2<sup>7</sup>.

Un nombre entier signé codé sur 1 octet va de -128 à 127.

Le plus petit nombre est 10000000 : le 1 signifie "nombre négatif" et la valeur est ... -128 !
Il faut bien comprendre que les nombres négatifs s'expriment dans l'ordre croissant
en partant du plus petit (-128<sub>10</sub> ou 10000000<sub>2</sub>) au plus grand (-1<sub>10</sub> ou 11111111<sub>2</sub>).

Trouver la valeur d'un nombre signé négatif n'est pas intuitif, il y a des règles.
Il faut réaliser le complément à 1 puis le complément à 2.

Le calcul se fait en deux étapes :

1) Calcul du complément à 1 = Remplacer tous les 0 par des 1 et tous les 1 par des 0.
2) Calcul du complément à 2 = Ajouter 1 au complément à 1


> Exemple  : comment écrire –4 en binaire ou en hexadécimal ? 
>
> +4 = 0000 0100<sub>2</sub>
>
> Le complément à 1 de ce code est 1111 1011<sub>2</sub>
>
> Ajoutons 1 pour obtenir son complément à 2 :
>
> 1111 1011<sub>2</sub> + 1 = 1111 1100<sub>2</sub> = FC<sub>16</sub> = -4


## Comment sont exprimés les nombres réels ?

Pour coder les nombres réels, on utilise le principe de la notation ingénieur. Car un nombre réel
ce n'est jamais qu'un entier multiplié par une puissance de 10.

Le codage de l'information en norme IEEE 754 fait donc comme suit : 

| 1 bit | 8 bits   | 23 bits |
| ----- | -------- | ------- |
| Signe | Exposant | Mantisse|

> **ATTENTION** :
>
> On ne peut pas représenter tous les nombres réels avec cette notation. C'est
> pourquoi parfois on obtient des imprécisions dans certains calculs, liées à des arrondis.
> **La précision des nombres flottants sur 16 bits est très faible**.


## Unités

Les bits qui codent une information sont groupés par 8, soit 1 octet. L'octet est 
la plus petite unité traitable par les registres d'un processeur. On ne peut jamais
manipuler moins que 1 octet à la fois. Cependant les microprocesseurs modernes traitent
généralement les données 4 voire 8 octets à la fois.

> **ATTENTION** :
Contrairement aux multiples en base 10, en binaire les multiples sont exprimés en
puissances de 2 également. Par exemple un kilo-octets ce n'est pas 1000 octets 
mais 2^10^ octets, soit **1024** octets.

- 1 ko = 2<sup>10</sup> octets = 1 024 octets
- 1 Mo = 1 048 576 octets = 2<sup>20</sup> octets
- 1 Go = 1 073 741 824 octets = 2<sup>30</sup> octets
- 1 To = 1 099 511 627 776 octets = 2<sup>40</sup> octets


## Algèbre booléenne

L'algèbre booléenne est l'ensemble des règles arithmétiques en binaire permettant
de réaliser des calculs dans un ordinateur.

Les 4 opérations de base sont : AND, OR, XOR et NOT. En électronique on parle de 
"portes" (porte "ET", porte "OU", porte "NON ET" ...etc) et on peut réaliser tout
un tas de portes composées de ces opérations de base. Les composants électroniques
à la base de ces opérations sont les **transistors**.

Une porte est un opérateur logique qui prend un ou deux opérandes en entrée et 
calcule un résultat de sortie, tout comme l'addition ou la soustraction en
algèbre.

Voici les 4 opérateurs de la logique booléenne :

>
>| AND     | 0  | 1  |
>| ------- | :-:| -- |
>|  **0**  | 0  | 0  | La sortie est à 1 si seulement si les deux entrées sont à 1.
>|  **1**  | 0  | 1  |

>| OR      | 0  | 1  |
>| ------- | :-:| -- |
>|  **0**  | 0  | 1  | La sortie est à 1 à partir du moment où au moins une entrée est à 1.
>|  **1**  | 1  | 1  |

>| XOR     | 0  | 1  |
>| ------- | :-:| -- |
>|  **0**  | 0  | 1  | La sortie n'est à 1 que si une et une seule entrée est à 1.
>|  **1**  | 1  | 0  |

>| NOT     | 0  | 1  |
>| ------- | :-:| -- |
>|         | 1  | 0  | La sortie est l'inverse de l'entrée.


On peut appliquer ces opérateurs sur des nombres binaires :

>|OR          | | | | |
>|-           |-|-|-|-|
>|Opérande A :|1|0|0|1|
>|Opérande B :|0|1|1|1|
>|Résultat :  |1|1|1|1|

>|XOR         | | | | |
>|-           |-|-|-|-|
>|Opérande A :|1|0|0|1|
>|Opérande B :|1|1|1|1|
>|Résultat :  |0|1|1|0|



# Pour approfondir
___
Cours :
- [https://www.faidherbe.org/tutoriel/numeration.htm](https://www.faidherbe.org/tutoriel/numeration.htm)
- [http://www.courstechinfo.be/Math_Info.pdf](http://www.courstechinfo.be/Math_Info.pdf)

Tutos vidéos :

- [https://fr.khanacademy.org/math/algebra-home/alg-intro-to-algebra/algebra-alternate-number-bases/v/number-systems-introduction](https://fr.khanacademy.org/math/algebra-home/alg-intro-to-algebra/algebra-alternate-number-bases/v/number-systems-introduction)
