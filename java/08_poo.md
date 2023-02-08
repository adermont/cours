# Programmation Orientée Objet (POO)

## Introduction

La programmation orientée objet est un paradigme apparu après celui de la
programmation procédurale. En programmation procédurale, on écrit un ensemble de
fonctions qui peuvent s'appeler les unes les autres sans contraintes. En POO, il
y a des contraintes permettant de mieux appréhender la complexité des grands
systèmes (plusieurs millions de lignes de code).

Une définition simple de la POO vous est donnée
[ici](https://www.lemagit.fr/definition/Programmation-orientee-objet).

## Concepts

La POO s'articule autour de 4 concepts fondamentaux que nous détaillerons plus loin :

- L'identité
- L'encapsulation
- Le polymorphisme
- L'envoi de messages

## Les notions de classe et d'objet

Jusqu'à présent nous avons manipulé des types "primitifs" comme `byte`, `short`, 
`int`, `float`, `double`...etc. Nous avons également travaillé avec des collections
d'objets : les tableaux `int[]`, `double[]` ... Mais si nous voulons des
types de données composés de plusieurs variables, nous devons créer de nouvelles
**classes**. 

### Classes
>**Premièrement** : une classe est un type de données qui permet d'étendre les 
capacités natives du Java.

>**Deuxièmement** : une classe contient toutes les méthodes qui permettentd'agir sur 
les données qu'elle contient (on appelle cela **l'encapsulation**). 

Exemple d'une classe `AdressePostale` contenant 4 **attributs** :

```java
public class AdressePostale {

    // Apprenez ces termes par coeur : 
    //
    // les variables suivantes sont des "variables d'instance"
    // aussi appelés des "attributs" ou "membres" de la classe.

    public int numeroDeRue;
    public String nomDeRue;
    public int codePostal;
    public String commune;
}
```

### Objets

La classe est en quelque sorte **le plan pour créer un objet** et l'objet est ce
qu'on appelle une **instance** de ce plan, une réalisation concrète de ce plan.

La classe déclare un type de données contenant des variables et les méthodes 
associées, tandis qu'un **objet** sera une **référence** vers un bloc en mémoire
qui contient les données décrites dans cette classe.

Un objet est une variable qui contient la référence ou l'adresse mémoire d'un
bloc de données où est stocké l'ensemble des variables de la classe à laquelle 
il appartient. On initialise un nouvel objet avec le mot-clé `new` suivi du
nom de sa classe :

> ```java
>AdressePostale a = new AdressePostale(); // La variable 'a' contient une référence vers un objet
>```
>
>- Le mot-clé `new` permet d'allouer un bloc de mémoire et renvoie une référence 
>vers ce bloc de mémoire.
>
>- Le nom de la classe (ici `AdressePostale`) sert à indiquer le type d'objet qu'on veut
>créer.
>
>- Le nom de la classe suivi des parenthèses indique qu'on appelle le 
>**constructeur** de la classe (ici c'est le constructeur par défaut, celui sans
>paramètres). 


## [Chapitre suivant : L'identité des objets](08_poo_identite.md)