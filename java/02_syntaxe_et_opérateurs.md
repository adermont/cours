# Java : la syntaxe

La syntaxe d'un langage est régie par ce qu'on appelle sa **grammaire**. Ce sont 
les règles qui disent quels mots on peut utiliser et dans quel ordre, comme une 
langue vivante.

La grammaire du langage Java est disponible à cette
[adresse](https://docs.oracle.com/javase/specs/jls/se7/html/jls-18.html) 
pour celles et ceux qui sont curieux de voir comment s'exprime la grammaire d'un 
langage de programmation.

Notez que la façon d'exprimer une grammaire suit elle aussi des règles de 
syntaxe particulières. En fait, la grammaire d'un langage de programmation est 
un **meta langage** car elle est auto-descriptive. Ceci permet de développer un 
programme dont le rôle est de vérifier si un texte respecte les règles de 
grammaire du langage ciblé. C'est ce que ce va faire un **parseur** (*parser*
en anglais).

En Java, un fichier valide contient au moins la déclaration d'une classe qui a 
pour nom le même nom que le fichier où elle est déclarée.

<ClassDeclaraction> ::= [<Modifier>] class <Texte> '{' [<Instructions>] }
<Modifier> ::= {}



## Les commentaires standards (privés)

En java, on peut écrire des indications dans le code pour aider à sa 
compréhension. Ces annotations s'appellent des commentaires (ou *comments* en 
anglais).

Un commentaire n'est jamais interprété, il sera ignoré par le compilateur, sauf 
s'il s'agit de commentaires de type `javadoc`.

Exemples :

```java
 // Ceci est une ligne de commentaire, tout caractère suivant le '//' est
 // interprété comme un commentaire. Le signe de début de commentaire doit être 
 // répété à chaque ligne.
 
 int i = 0; // On peut insérer un commentaire après une expression.
 
 /* Le code entre les balises '/*' et '*/' est un commentaire. */

  int i = /* on peut même commenter à l'intérieur du code */ 2 + 4 + 8 + 16;

 /* On peut même écrire un commentaire 
   sur plusieurs lignes.
 */
```

## Les commentaires javadoc (publics)

Un commentaire public est destiné à être vu par les utilisateurs de notre 
programme. En Java, le kit de développement contient un utilitaire qui s'appelle
`javadoc` et qui permet de générer des fichier HTML à partir des commentaires
publics trouvés dans notre code. Ceci permet d'harmoniser le look de la 
documentation des API écrits en Java.

Tout commentaire encadré par `/**` et `*/` est un commentaire public qui sera
interprété par l'utilitaire `javadoc` mais ignoré par le compilateur.

La 1ère phrase doit être concise et doit obligatoirement se terminer par un 
point (`.`).

Exemple : 

```java
 /** 
  * Cette classe permet de réaliser des calculs simples. La fonction 
  * "additionne" permet d'additionner deux nombres, la fonction....etc.
  *
  * @see #additionne(int,int)
  */
  public class Operations {
  ...
	/**
	 * Cette fonction additionne deux nombres.
	 *
	 * @return La somme de <code>nombre1</code> et <code>nombre2</code>.
	 */
	 public static int additionne(int nombre1, int nombre2) {
		return nombre1 + nombre2;
	 }
	 
	 ...
```

Documentation sur l'utilitaire `javadoc` : [https://docs.oracle.com/javase/8/docs/technotes/tools/windows/javadoc.html](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/javadoc.html)


Exemple de fichier produit par la commande `javadoc` : [https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/lang/System.html](https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/lang/System.html)




## Les variables et les constantes

Pour stocker des valeurs (des nombres, du texte ou des références), on utilise
des variables. C'est un moyen plus pratique que d'utiliser des adresses de la 
mémoire, car **les variables ont un nom** alors que les adresses sont des 
nombres parfois très grands.

Lorsqu'une variable est déclarée avec le mot-clé `final`, on dit que c'est une 
**constante**. Au cours du programme, la valeur d'une variable peut évoluer 
tandis que la valeur d'une constante, elle, reste **fixe**.

> **Note** :
> Dans les faits, une variable est un bloc contigu de 32 bits en mémoire. 
> Dans ce bloc de la mémoire, on stocke soit un nombre, soit une référence 
> (c'est à dire une adresse de la mémoire). 

Les variables et les constantes ont un **type** qui détermine les opérations 
qu'on peut réaliser dessus. Ainsi les opérations `+` ou `-` ne sont possibles 
qu'entre 2 variables de type numérique (`int`, `short`, `byte`, `long`...)

Il n'existe que 2 familles de variables/constantes : 

+ les **types primitifs**
+ les **références**

Les types de variables dits "primitifs" sont les suivants :

|Mot-clé   | Type                                                        |
|----------|-------------------------------------------------------------|
| `double` | nombre à virgule flottante sur 64 bits                      |
| `float`  | nombre à virgule flottante sur 32 bits (mauvaise précision) |
| `long`   | entier signé (positif ou négatif) sur 64 bits               |
| `int`    | entier signé sur 32 bits                                    |
| `short`  | entier signé sur 16 bits                                    |
| `byte`   | entier signé sur 8 bits                                     |
| `char`   | caractère ou entier non signé sur 16 bits                   |
| `boolean`| booléen vallant 'vrai' ou 'faux'                            |
| `String` | chaîne de caractères                                        |

**Remarque** : la JVM, c'est à dire la machine virtuelle qui interprète votre 
code, est une machine 32 bits. Elle manipule uniquement des zones mémoire de 32 
bits. Par conséquent, les opérations sur des types de données 64 bits sont 
délicates car il faut manipuler les données en 2 temps. D'autre part il faut 
noter que même si vous déclarez une variable avec le type "byte" (8bits), la JVM
va utiliser 32 bits au lieu de 8 (les 24 bits qui sont inutiles sont à zéro).

Les autres types de variables/constantes sont des **objets** (nous verrons ce 
concept plus tard).

La différence entre une variable et une constante, c'est le mot-clé `final`. Ce
mot-clé est utilisé en général pour interdire de modifier une valeur par mégarde.

Exemples :

```java
	// Variables :
	int a = 1;
	byte b = 0xFF
	a = 5;
	char c = 'a';
	String urlIsen = "http://www.isen.fr";
	urlsISen = "https://www.isen.fr";
	
	// Constantes :
	final boolean IS_OK = true;
	final double PI = 3.14159;
	PI = 3.14; // INTERDIT PAR LE COMPILATEUR CAR 'PI' est une constante
```



## Pour approfondir :

- Les types de données :  [https://web.maths.unsw.edu.au/~lafaye/CCM/java/javatype.htm](https://web.maths.unsw.edu.au/~lafaye/CCM/java/javatype.htm)

- Les variables :  [https://web.maths.unsw.edu.au/~lafaye/CCM/java/javavar.htm](https://web.maths.unsw.edu.au/~lafaye/CCM/java/javavar.htm)
