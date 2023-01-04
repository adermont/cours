# Java

Voici les sujets qu'il est important de connaître pour bien appréhender le cycle 
de développement d'applications en Java :

1) La syntaxe du langage et les structures de contrôle
2) Le kit de développement
3) Les librairies tierces
4) Le packaging et le déploiement d'applications

Java est un langage de programmation de _haut niveau_ (à l'opposé des langages 
dits "bas niveau"). Il est _compilé_ (par opposition aux langages "interprétés") 
et nécessite un kit de développement pour créer des applications. Le 
développement des applications se fait dans un éditeur de texte évolué qui 
s'appelle un **environnement de développement intégré** (IDE). 

Un IDE (ex : Eclipse, IntelliJ IDEA, Visual Studio Code...etc) est un éditeur de 
texte qui peut vérifier la syntaxe du langage Java en temps réel et marquer les 
éventuelles erreurs. Il peut aussi colorer les mots-clés, souligner les erreurs, 
générer du code à l'aide de raccourcis clavier...etc.) D'autre part, cet éditeur
est intégré avec le kit de développement.



## Programme minimal

Voici un premier programme qui est syntaxiquement minimal et correct, mais qui 
ne fait rien :

```java
	class MonProgramme {
		public static void main(String[] args) {
			// Ce programme ne fait rien
		}
	}
```

> Exécutez le programme avec la commande `java MonProgramme`

On peut modifier le programme pour qu'il affiche dans la console les paramètres 
de lancement :

```java
	class MonProgramme {
		public static void main(String[] args) {
			System.out.printf("%d%n", Arrays.toString(args))
		}
	}
```

Voyons comment compiler et lancer le programme :

	> javac MonProgramme
	> java MonProgramme argument1 arg2
	
Sortie affichée dans la console :
	
	> argument1 arg2

## Résumé

a) Un programme java doit respecter une syntaxe
b) Un programme java doit être compilé pour pouvoir être exécuté
c) Un programme peut être lancé dans la console avec des arguments séparés par des espaces
d) L'affichage par défaut d'un programme se fait dans la sortie standard de la console
e) L'entité minimale du langage s'appelle une *classe* et elle est composée de méthodes
f) Pour utiliser du code développé par des tiers, il faut l'importer
