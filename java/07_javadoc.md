# Javadoc

> Ce cours n'est qu'un petit aperçu des bases de Javadoc, la documentation officielle et complète est ici :  
> [https://www.oracle.com/technical-resources/articles/java/javadoc-tool.html](https://www.oracle.com/technical-resources/articles/java/javadoc-tool.html)

Quand vous écrivez une classe, il faut la documenter pour décrire comment 
elle fonctionne et savoir comment utiliser les différentes méthodes qui la 
composent.

Pour écrire la documentation d'une classe Java, il existe un standard qui 
s'appelle "Javacoc". En réalité, `javadoc` est l'outil qui vous permet de 
générer la documentation de vos classes en ligne de commande dans un Terminal.

Mais c'est également l'ensemble des règles qui régissent la manière dont on doit 
écrire les commentaires de notre code pour qu'ils soient interprétables par
l'outil `javadoc`.

> **NOTE** : `javadoc` ne sert à documenter que les éléments publics du code.
> Si une variable/méthode/classe est privée ou protected, elle n'apparaîtra 
> pas dans la documentation HTML générée par l'outil. 


## La commande `javadoc`

Dans IntelliJ, ouvrez le volet "Terminal" (View > Tools > Terminal) :

![View > Tools > Terminal](img/intellij-menu-view-terminal.png)

Créez un fichier d'exemple `Classe.java` dans le dossier `src`.

Puis tapez la commande suivante en remplaçant $NOM_DE_LA_CLASSE$ par le nom de 
la classe pour laquelle vous voulez générer la documentation :
> `$ javadoc -d javadoc src/$NOM_DE_LA_CLASSE$.java`
>
> **Note** : ne tapez jamais le premier caractère `$` au début d'une ligne de 
> commande car il s'agit d'une marqueur qui symbolise le "prompt" de votre 
> terminal.

Si la commande a bien fonctionné, vous verez un nouveau dossier `javadoc` créé
par la commande précédente. Il contient toute l'arborescence des fichiers HTML
pour documenter votre classe.

Vous pouvez également utiliser le menu `Tools > Generate javadoc ...` :  
![Menu Tools > Generate javadoc...](img/intellij-menu-tools-javadoc.png)  

![Generate javadoc...](img/intellij-fenetre-javadoc.png)

Voyons maintenant que mettre dans vos commentaires pour bien documenter vos 
classes !

## Les règles générales

1. Un commentaire `javadoc` commence par `/**` et se termine par `*/`.

2. Le texte d'un commentaire `javadoc` doit être écrit en **HTML**. Ca ne vous 
empêche pas de ne jamais mettre de balises HTML car du texte brut est du HTML
valide ;) Si vous voulez mettre du texte en gras, mettez-le entre des balises 
\<strong\> **et** \</strong\> par exemple.

3. Un commentaire `javadoc` doit être placé **DEVANT** l'élément
qu'il documente. C'est à dire que pour documenter une classe, le commentaire
doit être placé juste avant la ligne de déclaration de la classe :

	```java
	/**
	 * Ce commentaire résume ce que fait la classe.
	 */
	public class MyClass { ...
	```

4. Pour documenter une constante **publique** de la classe, idem :

	```java
	/** Ce commentaire décrit à quoi servira la constante. */
	public static final int MA_CONSTANTE = 42;
	```

5. L'outil `javadoc` traite tout ce qui se trouve entre le tag et le premier 
caractère point '.' comme un **résumé** de l'élément que vous documentez. Donc
si vous écrivez un commentaire de 3km, n'oubliez pas d'en faire un résumé et 
de finir votre phrase par un point :

	```java
	/**
	 * Ceci est le résumé de la méthode, mettez un point quand c'est fini.
	 * 
	 * Ensuite si la méthode est vraiment compliquée ou fait des traitements 
	 * bizarres, il faut prévenir l'utilisateur. Il est aussi important de bien 
	 * mettre des exemples d'utilisation lorsque la méthode fait beaucoup de 
	 * choses pour aider à sa compréhension.
	 *
	 * <TAGS> (rdv au chapitre suivant !)
	 */
	public MyClass myMethod() { ...
	```
	
	Regardez ce que produit la documentation du résumé de la méthode 
	`Integer.toBinaryString()` :  
	![Résumé de Integer.toBinaryString()](img/javadoc-integer-tobinstring-complete.png)
	
	Et la documentation complète de la même méthode :  
	![Doc complète de Integer.toBinaryString()](img/javadoc-integer-tobinstring.png)


## Les tags javadoc

Un tag javadoc est une balise qui commence par un `@` et est suivie par une 
valeur. Il existe des tags qui se mettent dans les entêtes de fichiers pour 
documenter le package, des tags prévus pour documenter la classe, des tags pour 
documenter les paramètres des méthodes ...etc.

```java
/**
 * Exemple de commentaire javadoc. Remplacez <TAG> et <VALEUR_DU_TAG> par des
 * vrais tags et des vraies valeurs ;)
 *
 * @<TAG> <VALEUR_DU_TAG>
 */
```

### Les tags d'une classe

| Tag          | Description                                             |
|--------------|---------------------------------------------------------|
| @version     | Décrit la date de création du fichier ou sa version.    |
| @author      | Décrit le nom de l'auteur de la classe.                 |
| @see         | Décrit une classe en lien avec la nôtre et qui peut aider à sa compréhension.|

Exemple :

```java
/**
 * MyClass is a class designed to blah blah........
 *
 * @date   23/01/2023
 * @author Some Name or Pseudonym
 * @see    otherpackage.OtherClass
 */
public class MyClass { ...
```

### Les tags d'une méthode

Les commentaires les plus importants sont ceux des méthodes de votre classe. 

| Tag              | Description                                        |
|------------------|----------------------------------------------------|
| @param \<nom\>   | Décrit un paramètre attendu par la méthode.        |
| @return          | Décrit ce que retourne la méthode.                 |

Exemple :

```java
/**
 * Cette méthode fait la moyenne des valeur d'un tableau de double[].
 *
 * @param tab Le tableau des valeurs dont on cherche à calculer la moyenne.
 * @return La moyenne des valeurs du tableau 'tab'.
 */
public class MyClass { ...
```


### Les tags un peu spéciaux ...


Dans un commentaire javadoc, on met parfois des liens internes vers la page de 
documentation courante ou vers une autre page d'une autre classe. Voici comment
mettre des liens, qu'ils soient internes ou externes :

- Pour une méthode "methodeInterne(int a, int b)" par exemple :  

```java
/**
 * Allez jeter un oeil à {@link #methodeInterne(int,int) cette méthode}
 */
```

- Pour une méthode "methodeExterne()" par exemple :  

```java
/**
 * Allez jeter un oeil à {@link autrepackage.AutreClasse#methodeExterne() cette méthode}
 */
```
