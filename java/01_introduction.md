# Introduction au langage Java

Java c'est principalement 2 choses :
- [Des spécifications de langage](https://docs.oracle.com/javase/specs/jls/se19/html/index.html)
- [Des spécifications de JVM](https://docs.oracle.com/javase/specs/index.html)

Les spécifications du langage disent comment faire l'analyse syntaxique et 
sémantique des fichiers `.java`. Ce sont des règles de syntaxe et de 
compilation.  

Les spécifications de la JVM disent comment interpréter le format de fichier
`.class` défini par les spécifications de langage et produits par les 
compilateurs Java.

Voici les sujets qu'il est important de connaître pour bien appréhender le cycle 
de développement d'applications en Java :

1) La syntaxe du langage
2) Le kit de développement (`javac`, `java`, `javadoc`...)
3) L'API native du langage (module/package `java.lang`)
4) Les module complémentaires et les librairies tierces
5) Le packaging et le déploiement d'applications

## Langage
Java est un langage de programmation de _haut niveau_ (à l'opposé des langages 
dits "bas niveau"). Il est _compilé_ (par opposition aux langages "interprétés") 
et nécessite un kit de développement pour créer des applications. Le 
développement des applications se fait dans un éditeur de texte évolué qui 
s'appelle un **environnement de développement intégré** (IDE). 

## Environnement de développement intégré (IDE)

Un IDE (ex : Eclipse, IntelliJ IDEA, Visual Studio Code...etc) est un éditeur de 
texte qui peut vérifier la syntaxe du langage Java en temps réel et marquer les 
éventuelles erreurs. Il peut aussi colorer les mots-clés, souligner les erreurs, 
générer du code à l'aide de raccourcis clavier...etc.) D'autre part, cet éditeur
est intégré avec le kit de développement.

## Compilateur
Le compilateur Java (`javac`) est le programme qui transforme un fichier `.java`
en fichier `.class` contenant des **OPCODES**. L'IDE réalise la compilation
des fichiers grâce au programme `javac` lorsqu'on demande l'exécution d'une 
classe.

## Programme minimal

Voici un premier programme qui est syntaxiquement minimal et correct, mais qui 
ne fait rien :
```java
public class MonProgramme {
	public static void main(String[] args) {
		// Ce programme ne fait rien
	}
}
```

> Exécutez le programme avec la commande `java MonProgramme`

On peut modifier le programme pour qu'il affiche dans la console les paramètres 
de lancement :

```java
public class MonProgramme {
	public static void main(String[] args) {
		// Affichage des arguments du programme dans la sortie standard
		System.out.printf("%s%n", java.util.Arrays.toString(args));
	}
}
```

Voyons comment compiler et lancer le programme dans l'onglet "Terminal" 
d'IntelliJ :

> `javac MonProgramme.java`  
> `java MonProgramme arg1 arg2`
	
Sortie affichée dans la console :
	
> `argument1 arg2`

## Résumé

a) Un programme java doit respecter une syntaxe et doit être compilé en fichier 
`.class` pour pouvoir être exécuté.
b) Pour être exécuté, un programme doit déclarer une classe avec une méthode 
`public static void main(String[] args){}`.
c) Un programme peut être lancé dans la console avec des arguments séparés par 
des espaces.
d) L'affichage par défaut d'un programme se fait dans la console.