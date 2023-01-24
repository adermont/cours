# Java : les méthodes

> **Préambule**
> 
> Une méthode est aussi appelée fonction dans d'autres contextes. L'appellation
> "méthode" est propre au Java et il nous fait presque oublier que le
> terme "fonction" est issu des mathématiques... En effet, rappelez-vous des 
> fonctions affines : `f(x) = a.x + b`
>
> Dans cet exemple, `f` est une fonction et `x` est un paramètre de `f`. Ce qui 
> signifie littéralement que la valeur de "`f` est **fonction** de la valeur de
> `x`". En Java on dira que `f` est une méthode qui prend un argument `x` et 
>retourne la valeur `a.x + b`.


## Pourquoi déclarer une méthode ?

En programmation, lorsqu'on a des éléments répétitifs à réaliser, on peut les 
exécuter à l'intérieur d'une boucle (`for`, `while`...) mais parfois ces 
opérations sont longues à écrire et tiennent sur plusieurs dizaines voire 
centaines de lignes de code. 

Pour qu'il soit plus facile de se repérer, on divise notre programme en
**méthodes**. Une méthode est une sous-partie de notre programme qui ne fait
que certaines choses. On pourrait voir ça comme les différentes étapes d'une 
recette de cuisine, elles-mêmes divisées en plusieurs sous-étapes.

Mais une méthode ne sert pas seulement à diviser notre code en plusieurs 
chapitres : elle sert aussi à pouvoir **réutiliser** une suite d'opérations
qu'on a besoin de faire régulièrement, SANS LES ECRIRE PLUSIEURS FOIS.

Exemple :

> Voici une opération mathématique que je dois écrire à plusieurs reprises 
> dans mon programme :  
> ```java
> int resultat1 = Math.sqrt((a + b) * (a - b)) / ((a * a) + (b * b))
> ...  
> // un peu plus loin :
> int resultat2 = Math.sqrt((a + b) * (a - b)) / ((a * a) + (b * b))
>```
> Si je n'utilise pas de méthode pour réaliser cette opération, je vais devoir
> réécrire le **MÊME CODE** à chaque fois ! En contexte professionnel, c'est
> **INTERDIT** pour la simple et bonne raison que si j'ai fait une erreur, je 
> vais devoir la corriger à chaque endroit où j'ai fait cette erreur !!! Pire :
>
> Il faut donc écrire une méthode qui réalise ce calcul et retourne le résultat :  
>
>```java
>int monCalcul(int a, int b) {
>    return Math.sqrt((a + b) * (a - b)) / ((a * a) + (b * b));
>}
>```
> On l'utilisera ainsi :
>```java
>int resultat1 = monCalcul(a,b);
>int resultat2 = monCalcul(a,b);
>```
> Et comme ça si j'ai une erreur dans mon calcul, je n'ai qu'à corriger la 
> méthode et le reste de mon code ne sera pas impacté.
>


## Où déclarer une méthode ?

Une méthode doit toujours être déclarée à l'intérieur d'une classe (c'est à
dire entre les deux accolades de la classe dans laquelle vous voulez déclarer 
votre méthode) :

```java
public class MaClasse {
	public void methodeBienDeclaree(){
		// OK
	}
}

// INTERDIT car on est en dehors des accolades de "MaClasse"
public void methodeMalDeclaree(){
	
}
```


## Comment déclarer une méthode ?

Quand vous déclarez une méthode, vous devez lui donner :
- un ou plusieurs **modificateurs** optionnel (ou *modifier* en anglais)
- un **nom**
- un **type de retour**
- et éventuellement des **paramètres**

Exemple :

```java
// Note : le code entre crochets est optionnel (dépend du type de la méthode)

[<modifier>] <type de retour> <nomDeLaMéthode>(<arguments>) {
	[return <résultat>;]
}
```

### Comment nommer ses méthodes ?

Pour nommer une méthode, il existe une convention appelée **notation hongroise**
aussi appelée **camel case** : quand un nom est composé de plusieurs mots, on 
débute chaque mot par une majuscule.

Exemples :

```java
	int calculerLaSommeDeDeuxNombres(int nombre1, int nombre2) {
		return nombre1 + nombre2;
	}
	void methodeSansRetour(){
		// Cette méthode ne retourne pas de valeur
	}
```

D'autre part, **contrairement aux noms de classes** les noms de méthodes 
doivent **toujours commencer par une minuscule**. Faites attention car le 
compilateur ne fera aucune erreur, c'est autorisé (même si c'est tordu) de
déclarer une méthode dont le nom commence par une majuscule.

<blockquote style="color: red;">
<b>NOTE</b> : il existe une exception pour ce qu'on appelle les *constructeurs*. 
Les constructeurs ne sont cependant pas des vraies méthodes, nous les verrons en
détail lors du module de Porgrammation Orientée Objet (POO). Et dans leur cas,
le nom doit être strictement identique au nom de la classe, donc comme le nom 
des classes commencent par une majuscule, le nom des constructeurs commence 
aussi par une majuscule.
</blockquote>


### Les *access modifiers* (visibilité d'une méthode)

La **visibilité** d'une méthode détermine le périmètre à l'intérieur duquel
votre méthode sera visible. La visibilité est un 
*access modifier* (c'est-à-dire qu'elle conditionne l'accès à la méthode).

Il existe 4 *access modifiers* qui régissent la visibilité d'une méthode : 

|Visibilité                   | Effet                                                                          |
|-----------------------------|--------------------------------------------------------------------------------|
|**private**                  | Visible seulement à l'intérieur de la classe.                                  |
|**protected**                | Visible dans la classe, ses sous-classes et les autres classes du même package.|
|**public**                   | Visible depuis n'importe quelle classe.                                        |
|(*rien*)                     | Visible seulement par les classes du package mais pas les sous-classes.        |


> Exemples :
>```java
> public void maMethodePublic() {
>	// Méthode visible par tout l'univers
> }
> public void maMethodeProtected() {
>	// Méthode visible à l'intérieur de la classe, des sous-classes et des classes du même package
> }
> public void maMethodePrivate() {
>	// Méthode privée, réservée à la classe uniquement, même les sous-classes n'y ont pas accès
> }
> public void maMethodePackage() {
> 	// Visibilité "package" : seules les classes du même package peuvent la voir mais pas les sous-classes
> }
>```

### Les *non-access modifiers*

Il existe 4 modificateurs/*modifiers* :

|Modifier         | Effet                                                                                  |
|-----------------|----------------------------------------------------------------------------------------|
|**static**       | Possibilité d'appeler la méthode en mettant le nom de la classe devant, avec un point. |
|**final**        | Rend la méthode non surchargeable par les sous-classes.                                |
|**abstract**     | Rend la méthode abstraite (implémentable uniquement dans les sous-classes              |
|**synchronized** | Ne sera pas abordé pour l'instant, concerne le multithreading                          |
|**volatile**     | Ne sera pas abordé pour l'instant, concerne le multithreading.                         |

Exemples :

> La méthode `Integer.parseInt(String)` définie dans la classe `Integer` est 
une méthode `static`. On peut donc l'appeler sur la classe directement.



## Comment exécuter/appeler une méthode ?

Pour exécuter le code d'une méthode, il faut l'appeler. En programmation 
orientée objet, quand on appelle une méthode on parle d'un **envoi de message**.
Le message dont on parle est reçu soit :

- Une classe (si la méthode est déclarée avec le mot-clé `static`)
- Un objet (ie. une variable créée avec le mot-clé `new`).

Pour l'instant nous allons nous concentrer sur les appels de méthodes statiques.

>```java
> public class Test {
>
> 	// Voici une méthode statique qui fait un calcul quelconque à partir de 2 variables :
> 	public static int monCalcul(int parametre1, int parametre2) {
>		return parametre1 - (parametre1 / parametre2);
> 	}
>
> 	// Voici maintenant la méthode main de notre programme
> 	public static void main(String[] args){
>
> 		// On appelle la méthode "monCalcul()" en lui passant 2 valeurs
> 		int resultat = maMethodeStatic(5,10);
>   	System.out.println(resultat);
> 	}
> }
>
>```

## Les méthodes particulières 

Il existe 2 types de méthodes un peu particuliers : les méthodes `main` et les 
constructeurs (que nous verrons plus tard en POO).

### La méthode main()

En Java, pour exécuter un programme il faut ce qu'on nomme un **point d'entrée**.
La machine virtuelle va toujours chercher à exécuter le code qui se trouve dans 
la méthode `main()`.

La méthode main() se déclare comme suit :

```java
public static void main(String[] args){
	// Les instructions de votre programme vont ici.
	// Il est possible d'appeler d'autres méthodes à partir de la méthode main().
}
```

Quelques éléments importants de cette méthode :

- Elle doit être déclarée avec le mot-clé **`static`**
- Son type de retour est obligatoirement **`void`**
- Elle prend 1 seul argument : un tableau de chaines de caractères **`String[]`**
