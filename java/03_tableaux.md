# Les tableaux en Java

Les tableaux sont des types de variables particuliers. Ce qu'on appelle tableau
est en réalité un ensemble de variables qui sont stockées de manière contigües
en mémoire, c'est à dire les unes à la suite des autres.

Quand on crée un tableau, on réserve un espace en mémoire, capable de stocker
un certain nombre de variables : ce nombre est la taille du tableau.

## Déclarer un tableau à 1 dimension

On déclare un tableau comme n'importe quelle variable : on écrit d'abord le
type des éléments qui seront rangés dedans (avec des crochets), puis son nom :

> ```java
> int[] monTableau; // ici je déclare un tableau de nombres entiers
>```

La différence avec une variable simple, ce sont les crochets `[]`, qui indiquent
qu'on a affaire à un tableau à 1 dimension.

Ensuite pour **initialiser** le tableau, je dois lui préciser :
- soit sa taille,
- soit directement son contenu (et sa taille sera calculée automatiquement).

Par exemple voici comment déclarer un tableau de 5 éléments de type `byte` :

>```java
> byte[] tableau = new byte[5];
>```

Si je veux déclarer un tableau contenant 10 nombres réels `double` je devrais 
écrire :

>```java
> double[] tableau = new double[10];
>```

Pour initialiser un tableau avec les valeurs 10, 20, 66, 47 et 85 par exemple, 
voici comment faire (les 2 façons sont autorisées) :

>```java
> int[] tableau = {10, 20, 66, 47, 85};          // Forme simple
> int[] tableau = new int[]{10, 20, 66, 47, 85}; // Forme complète
>```

## Déclarer un tableau à 2 dimensions

Il est possible de stocker des variables dans des tableaux à 2 dimensions. 
Cependant gardez en tête que si vous avez de nombreuses valeurs, l'espace 
mémoire consommé pour un tableau à 2 dimensions sera le carré de l'espace 
consommé par le même tableau à 1 dimension.

Exemple de déclaration pour un tableau qui fait 5 lignes et 2 colonnes :

```java
int[][] dim2array = new int[5][2];
```

Vous pouvez vous représenter le tableau précédent comme une matrice :
>```java
> int[][] dim2array = {
>    {0, 0}, // Ligne 0 : 2 colonnes numérotées de 0 à 1
>    {0, 0}, // Ligne 1 : 2 colonnes numérotées de 0 à 1
>    {0, 0}, // Ligne 2 : 2 colonnes numérotées de 0 à 1
>    {0, 0}, // Ligne 3 : 2 colonnes numérotées de 0 à 1
>    {0, 0}  // Ligne 4 : 2 colonnes numérotées de 0 à 1
> };
>```

> **RAPPEL** : Les dimensions d'un tableau sont fixes. Un tableau n'est pas 
redimensionnable. Pour augmenter la taille d'un tableau, on n'a pas d'autre 
choix que de déclarer une nouvelle variable de taille N+1 et de recopier les 
éléments de notre tableau initial dans le nouveau tableau.


### Comment utiliser un tableau ?

Les tableaux en Java sont des objets un peu particuliers. Ils ont une propriété
cachée qui s'appelle `length` et qui permet de connaitre leur taille.

Ainsi si j'écris : `array.length` cela signifie "nombre d'éléments de `array`".
C'est indispensable de connaître la taille d'un tableau pour parcourir tous 
ses éléments.

D'autre part il faut savoir que **la numérotation des éléments d'un tableau 
commence à 0** et non à 1. Donc pour obtenir le 1er élément d'un tableau, il
faut utiliser l'indice 0.

Pour obtenir la valeur située dans la case n°i d'un tableau, il faut utiliser la 
notation entre crochets :

>```java
> int[] array = {1, 2, 3, 4, 5}
>
> int i = 2; // numéro de la case qu'on cherche (3ème case vu qu'on part de zéro)
> 
> // La valeur de l'élément situé dans la case n°i est :
> int valueAtIndex_i = array[i]; // Ce sera la valeur 3
>```

Voici le même exemple mais avec un tableau à 2 dimensions :

>```java
> int[][] array = {
>                     {1, 10}, 
>                     {2, 20}, 
>                     {3, 30},
>                     {4, 40}, // 3ème ligne
>                     {5, 50}
>                 };
>
> int line = 3;
> int column = 1;
> 
> // La valeur de l'élément situé dans la case [column,line] est :
> int valueAtIndex_line_col = array[line][column];
>```

> **ATTENTION** : si vous tentez d'obtenir le 3ème élément d'un tableau qui n'en
compte que deux, vous obtiendrez une erreur `ArrayIndexOutOfBoundsException`.