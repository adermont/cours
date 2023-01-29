# Java : Les structures de contrôle

Une structure de contrôle permet de modifier le flot d'exécution d'un programme.
Tant qu'il n'y a que des *statements*, le programme se déroule ligne après 
ligne. Une structure de contrôle permet de faire des "sauts" et des "boucles" 
pour aller à un autre endroit que l'instruction qui suit l'instruction courante.

## Les conditions `if/else if/else`

L'instruction `if` exprime une **condition** et permet de réaliser un 
**branchement conditionnel**. Si la condition déterminée entre les parenthèses 
est vraie (`true`), alors le code exécuté sera celui du 1er bloc entre les
accolades :

```java
	if (condition) {
		// Code exécuté seulement si la condition est true
	} else if (autreCondition) {
		// Code exécuté si `condition` est false ET que `autreCondition` 
		// est true
	} else {
		// Code exécuté dans tous les autres cas (ie. `condition` == false et 
		// `autreCondition` == false)
	}
```

**Remarque** : les accolades '{}' ne sont pas obligatoires mais il est 
**fortement recommandé** de les mettre systématiquement pour éviter les erreurs !



## Les boucles `for`

Une boucle `for` est une instruction particulière qui contient elle-même un bloc 
d'instructions à répéter plusieurs fois.

Il y a 4 éléments importants dans la boucle `for` :

A) L'instruction d'initialisation (exécutée obligatoirement **UNE SEULE FOIS**)
B) La condition d'entrée (évaluée **AVANT** d'entrer dans le bloc)
C) Le bloc de la boucle (exécuté **SEULEMENT SI** `B` est `true`)
D) L'instruction d'itération (exécutée **APRÈS** le bloc)

L'instruction se déroule dans cet ordre :

|Etape| Déroulement                                                          |
|-----|----------------------------------------------------------------------|
|1    | Le statement A est exécuté.
|2.1  | Si la condition B est vraie, alors le bloc C est exécuté 
|2.2  | Sinon, la boucle est interrompue et on passe à l'instruction suivante.
|3    | Le bloc D est exécuté puis on reprend à l'étape 2.1


Exemple de boucle :

```java
	for (int i=0; i < 10; i++) 
	{	
		// Ce code va être exécuté 10 fois
		// et à chaque fin de boucle, la variable 'i' est incrémentée.
	}
```

La syntaxe générale est :

```java
	for ( <condition_initiale> ; <condition_de_maintien> ; <incrément> ) {
		// Code à exécuter
	}
```

Il y a donc plein de façons d'utiliser une boucle for :

```java
	for (;;){
		// Ceci est une boucle infinie, équivalente à "while (true) { ... }"
	}

	int i=0;
	int[] tableau= new int[3]{0,0,0};
	for (/* pas de déclarations */ ; i<tableau.length ; /* pas d'instruction d'itération */) {
		tableau[i++] = i;
	}
	
	int[] tableau = new int[3]{0,0,0};
	for (int i=0 ; i<tableau.length ; i++){
		tableau[i] = i;
	}

	int[] tableau = new int[3]{0,0,0};
	for (int i=0; true ; i++){
		if (i == tableau.length) break; // Permet de sortir de la boucle quand i==3
		tableau[i] = i;
	}
```

## Les boucles `foreach`

Il s'agit d'une variante de la boucle `for` utilisée pour parcourir tous les 
éléments d'une liste ou d'un tableau.

Exemple :

```java

	// Chercher le nombre d'occurences du nombre 30 dans ce tableau
	int[] numbers = {10, 30, 30, 40, 100, 60};
	
	int result = 0;
	
	// Pour chaque élément 'n' du tableau 'numbers'
	for (int n : numbers) 
	// Faire :
	{
		if (n == 30) {
			result++;
		}
	}
	System. out.println("On a trouvé " + count30 + " fois le nombre 30");
```


## Les boucles `while` et `do while`

Pour la boucle `while ( <condition> ) { <code_to_execute> }` le code `code_to_execute` 
est exécuté uniquement si `<condition>` est vraie ET tant que cette condition reste vraie.

La condition d'une boucle `while` est vérifiée avant chaque itération.

Exemple :

```java
	int a = 0;
	while (a < 5) {
		a++;
		System.out.println("a = " + a);
		
		// Le programme affichera "a = 1" puis "a = 2" ...etc. jusqu'à "a = 5" puis s'arrêtera. 
	}
```

Pour la boucle `do { <code_to_execute> } while (<condition>);` le code `code_to_execute> 
sera exécuté une première fois quoiqu'il arrive mais ne sera réexécuté en boucle
que si la condition est vraie en début d'itération.

## Les branchements `switch`, `break`

L'instruction 'switch' est une instruction similaire à l'instruction `if`.

Exemple :

```java
	int moisDeLAnnee = 2;
	switch (moisDeLAnnee) {
		case 1: 
			System.out.println("janvier");
			break;
		case 2:
			System.out.println("février");
			break;
			
		// ...etc.
		
		default: 
			System.out.println("mois inconnu");
			break;
	}
```

Il faut bien comprendre que tout ce qui suit un bloc `case XXX:` sera exécuté
s'il n'y a pas d'instruction `break` :

```java
	int moisDeLAnnee = 7;
	switch (moisDeLAnnee) {
		case 7: // juillet
		case 8: // aout
			System.out.println("Vacances d'été");  // ce code sera exécuté
		
		default: 
			System.out.println("Période de travail"); // ce code est aussi exécuté !
			break;
	}
	
	// CE CODE A UN PROBLEME : il affichera les deux messages car il manque un `break`
	// après le code du bloc `case 8`.
```

## Les redirections `goto` et les labels

Ces instructions ne sont quasiment jamais utilisées et sont considérées comme de la bidouille.
Il faudra les utiliser uniquement pour du code "jetable" et à des fins personnelles.

```java
	for (;;) {
		reception:
		
		byte[] data = receiveData();
		if ( data.length == 0 ) {
			Thread.sleep(1000);
			
			goto reception; // on retourne à l'étiquette 'reception'
		}
		
		// Notez que ce code aurait pu être écrit de manière plus élégante !
		// C'est pour cela qu'on n'utilise pas ces instructions, héritées de vieux langages
		// tels que le BASIC ou le DOS.
	}
	
```

## Pour approfondir :

- Les structures de contrôle : [https://web.maths.unsw.edu.au/~lafaye/CCM/java/javacond.htm](https://web.maths.unsw.edu.au/~lafaye/CCM/java/javacond.htm)