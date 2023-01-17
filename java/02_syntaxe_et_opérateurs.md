# Java : la syntaxe

La syntaxe d'un langage est régie par ce qu'on appelle sa **grammaire**. Ce sont 
les règles qui disent quels mots on peut utiliser et dans quel ordre, comme une 
langue vivante.

La version 19 des spécifications du langage Java est disponible à cette
[adresse](https://docs.oracle.com/javase/specs/jls/se19/html/index.html) 
pour celles et ceux qui sont curieux de voir comment s'exprime la grammaire d'un 
langage de programmation.

Notez que la façon d'exprimer une grammaire suit elle aussi des règles de 
syntaxe particulières. En fait, la grammaire d'un langage de programmation est 
un **meta langage** car elle est auto-descriptive. Ceci permet de développer un 
programme dont le rôle est de vérifier si un texte respecte les règles de 
grammaire du langage ciblé. C'est ce que ce va faire un **parseur** (*parser*
en anglais).

En Java, un fichier valide contient au moins la déclaration d'une classe qui a 
pour nom le **même nom que le fichier où elle est déclarée**.

>```
> ClassDeclaraction ::= [<Modifier>] class <Name> '{' [<Instructions>] '}'
> Modifier ::= public | protected | private | <Default>
> Default ::= <empty string>
>```


## Les commentaires standards (privés)

En java, on peut écrire des indications dans le code pour aider à sa 
compréhension. Ces annotations s'appellent des commentaires (ou *comments* en 
anglais).

Un commentaire n'est jamais interprété, il sera ignoré par le compilateur, sauf 
s'il s'agit de commentaires de type `javadoc`.

Exemples :

```java
 // Ceci est un commentaire "ligne".
 // Le signe de début de commentaire doit être répété à chaque ligne.
 //
 int i = 0; // On peut ajouter un commentaire ligne après une instruction mais pas avant.
 
 /* Le code entre les balises '/*' et '*/' est un commentaire "bloc". */

  int i = /* on peut mettre un commentaire-bloc à l'intérieur d'une expression */ 2 + 4 + 8 + 16;

 /* On peut aussi écrire un commentaire bloc
   sur plusieurs lignes.
 */
```

## Les commentaires javadoc (publics)

En Java, le kit de développement contient un utilitaire qui s'appelle
`javadoc` et qui permet de générer des fichier HTML à partir des commentaires
javadoc trouvés dans notre code. Ceci permet d'harmoniser le look de la 
documentation des API écrits en Java.

Tout commentaire encadré par `/**` et `*/` est un commentaire javadoc qui sera
interprété par l'utilitaire `javadoc` mais ignoré par le compilateur. Cependant
vous devez savoir que `javadoc` ne lira QUE les commentaires accolés à des 
membres publics. D'autre part il faut apprendre la syntaxe de ces commentaires 
car on ne peut pas écrire n'importe quoi n'importe où.

Exemple : la 1ère phrase doit être concise et doit obligatoirement se terminer par un 
point (`.`)
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
```

- [Spécification des tags javadoc](https://docs.oracle.com/en/java/javase/19/docs/specs/javadoc/doc-comment-spec.html)

- [Documentation sur l'utilitaire `javadoc`](https://docs.oracle.com/en/java/javase/19/docs/specs/man/javadoc.html)

- [Exemple de fichier produit par la commande `javadoc`](https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/lang/System.html)



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
qu'entre 2 variables de type numérique (`int`, `short`, `byte`, `long`...) ou
deux chaines de caractères (`String`).

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

**Remarque** : la JVM manipule les données par paquets de 32 bits. Les types qui
sont stockés sur 64 bits doivent être utilisés avec précaution en contexte 
multithread à l'aide des classes `AtomicDouble`, `AtomicLong`...

Les autres types de variables/constantes sont des **objets** (nous verrons ce 
concept plus tard).

La différence entre une variable et une constante, c'est le mot-clé `final`. Ce
mot-clé est utilisé en général pour interdire de modifier une valeur par mégarde.

Exemples :

```java
	// Variables :
	int a = 1;
	byte b = 0xFF;
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

- [Guide "débuter en Java"](https://www.data-transitionnumerique.com/apprenez-programmation-java)

