# Java : Les opérateurs

## Les opérateurs de comparaison

Un opérateur de comparaison permet de comparer deux variables ou deux nombres.
Le résultat d'une comparaison est **toujours un booléen** (`true` ou `false`).

Les opérateurs de comparaison sont utilisés pour exprimer des **conditions** 
dans des **assignations de variables**, dans des **blocs** `if`, dans des 
**boucles** `for` et `while` ou plus rarement dans des **expressions ternaires**
(dont on déconseille l'usage parce qu'il y a souvent des confusions dans leur 
compréhension). 

- En d'autres termes, on ne peut pas écrire une comparaison seule, il faut 
forcément l'utiliser dans une autre expression.


| Opérateur | Exemple   | Résultat                                 |
| --------- |-----------| -----------------------------------------|
|    ==     | a == b    | Vrai si 'a' égale 'b'                    |
|    !=     | a != b    | Vrai si 'a' est différent de 'b'         |
|     >     | a > b     | Vrai si 'a' est supérieur à 'b'          |
|     <     | a < b     | Vrai si 'a' est inférieur à 'b'          |
|    >=     | a >= b    | Vrai si 'a' est supérieur ou égal à 'b'  |
|    <=     | a <= b    | Vrai si 'a' est inférieur ou égal à 'b'  |
|    &&     | a && b    | Vrai si 'a' et 'b' sont vrais tous les 2 |
|    \|\|   | a \|\| b  | Vrai si 'a' ou 'b' est vrai              |

Exemples :

```java
	int a = 5;
	int b = 6;
	boolean isOk = a > b;
```


## Les opérateurs mathématiques

Un opérateur mathématique retourne un résultat de calcul.

| Opérateur | Exemple   | Résultat                                                        |
| --------- |-----------| ----------------------------------------------------------------|
|     +     | a + b     | Ajoute 'a' et 'b'                                               |
|     -     | a - b     | Soustrait 'b' à 'a'                                             |
|     *     | a * b     | Multiplie 'a' par 'b'                                           |
|     /     | a / b     | Divise 'a' par 'b'                                              |
|     %     | a % b     | 'a' modulo 'b' (le reste de la division entière de 'a' par 'b') |

Exemples :

```java
	// Opérations standards
	int nombre1 = 1;
	int nombre2 = 2;
	int somme = nombre1 + nombre2; // Résultat : 3
	int difference = nombre 1 - nombre 2; // Résultat : -1
	int multiplication = nombre1 * nombre2; // Résultat : 2
	int division = nombre1 / nombre2; // Résultat : 0
	
	// Incrémentation ++ et décrémentation --
	int nombre = 0;
	nombre++; // Résultat : nombre vaut 1
	++nombre; // Résultat : nombre vaut 2
	nombre--; // Résultat : nombre vaut 1
	--nombre; // Résultat : nombre vaut 0
	
	// Quand la ligne ne contient qu'une seule instruction ++ ou --, 
	// l'ordre n'a pas d'importance.
	// Mais si on réalise une opération ++ ou -- dans un appel de fonction, 
	// il faudra faire attention.
	//
	int nombre = 5;
	int mult = nombre++ * 2; // Résultat : nombre est incrémenté APRES la multiplication !
```
	
>_Attention aux débordements_ :
>
>```java
>	int max = Integer.MAX_VALUE; // 2147483647
>	max++; // débordement de capacité, la prochaine valeur après l'entier max est l'entier Integer.MIN_VALUE (c'est à dire -2147483648)
>```

## Les opérateurs d'assignation

Un opérateur d'assignation permet de modifier la valeur d'une variable ou la valeur 
initiale d'une constante.

| Opérateur | Exemple   | Résultat                                                        |
| --------- |-----------| ----------------------------------------------------------------|
|     =     | a = b     | Opérateur d'assignation : `a` prend la valeur `b`               |
|    +=     | a += b    | Equivalent à `a = a + b`                                        |
|    -=     | a - b     | Equivalent à `a = a - b`                                        |
|    *=     | a * b     | Equivalent à `a = a * b`                                        |
|    /=     | a / b     | Equivalent à `a = a / b`                                        |
|    %=     | a % b     | Equivalent à `a = a % b`                                        |

Exemples :

```java
	int a = 2;
	int b = 5;
	boolean egalite = (a == b); // false
	int c = a % b; // 2
	
```



## Les opérateurs logiques

Un opérateur logique permet de faire une opération de logique booléenne. Par conséquent
le résultat d'une opération de ce type sera aussi un booleén.


| Opérateur | Résultat                                 |
|-----------| -----------------------------------------|
| a && b    | Vrai si 'a' et 'b' sont vrais tous les 2 |
| a \|\| b  | Vrai si 'a' ou 'b' est vrai              |

Exemples :

```java

	// ET logique
	boolean jeSaisCompter = ((5+5) == 10) && ((2+2) == 4); // la variable 'jeSaisCompter' est vraie
	
	// OU logique
	boolean a = true;
	boolean b = false;
	if ( a || b ) { 
		System.out.println("Une des deux variables est vraie"); // Ce code sera exécuté
	}
	
```


## Les opérateurs "bit à bit"

Ces opérateurs sont utilisés pour faire des opérations sur la valeur binaire en faisant
des décalages ou des masquages de bits.

| Opérateur | Résultat                                                                                    | 
| --------- | --------------------------------------------------------------------------------------------|
| >>        | Décale les bits vers la droite. Les bits 'perdus' sont remplacés par des zéros.             |
| <<        | Décale les bits vers la gauche. Les bits 'perdus' sont remplacés par le bits de poids fort. |
| >>>       | Décale les bits vers la droite. Les bits 'perdus' sont remplacés par des zéros.             |
| \|        | Opération logique OU bit à bit.                                                             |
| &         | Opération logique ET bit à bit.                                                             |
| ^         | Opération OU EXCLUSIF bit à bit.                                                            |


## Pour approfondir :

- Les opérateurs :  [https://web.maths.unsw.edu.au/~lafaye/CCM/java/javaop.htm](https://web.maths.unsw.edu.au/~lafaye/CCM/java/javaop.htm)
