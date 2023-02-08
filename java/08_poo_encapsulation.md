## L'encapsulation

    Petit rappel :
    ------------
    En programmation impérative (ex. : langages C, Pascal, Basic...), on déclare des
    variables à l'intérieur des fonctions. Elles ne sont visibles QUE dans
    le **périmètre** de la fonction où elles sont déclarées. D'autre part les
    fonctions elles-mêmes sont visibles entre elles, rien n'interdit d'appeler
    une fonction à partir d'une autre.

En programmation objet, on a des **mécanismes de protection** pour éviter qu'une
variable soit modifiée par une fonction qui n'est pas définie dans le même
fichier. Et de la même façon il existe un mécanisme permettant de limiter la
visibilité des fonctions pour qu'on ne puisse pas les appeler depuis un fichier
extérieur.

Comme son nom l'indique, **l'encapsulation** permet d'encapsuler un ensemble de
variables et de fonctions à l'intérieur d'une **classe**.

Ceci nous autorise à déclarer des variables en dehors d'une fonction comme 
dans notre exemple précédent :

> ```java
>// Voici une classe contenant une seule variable
>public class AdressePostale {
>   public int codePostal; // Notez ici le mot-clé "public"
>}
>```

Pour pouvoir utiliser cette variable depuis l'extérieur de ma classe, je dois
créer un objet de type `AdressePostale` :

> ```java
>public class Main {
>
>   public static void main(String[] args) {
>
>       // Création d'un objet de type AdressePostale
>       AdressePostale myObject = new AdressePostale();
>
>       // On affiche la valeur de sa variable 'codePostal' en mettant un '.'
>       // après son nom :
>       System.out.println(myObject.codePostal); // Au début ce sera 0 !
>
>       // Maintenant on modifie la variable 'someVariable'
>       myObject.codePostal = 29200;
>
>       // On affiche la nouvelle valeur après modification
>       System.out.println(myObject.codePostal); 
>   }
>}
>```

On peut maintenant moduler la visibilité de notre variable (qui était déclarée
`public`) pour la rendre inaccessible. Nous devons la déclarer avec une
visibilité `private`, `protected` ou bien sans mot-clé (visibilité `package`,
déconseillée car complexe à comprendre et à mettre en oeuvre).

> ```java
>// Voici comment restreindre la visibilité de notre variable :
>public class AdressePostale {
>   private int codePostal; // Maintenant elle n'est visible que dans cette classe
>}
>```

Le code de notre programme `main()` ne fonctionne plus :

> ```java
>public class Main {
>
>   public static void main(String[] args) {
>
>       // Création d'un objet de type AdressePostale
>       AdressePostale myObject = new AdressePostale();
>
>       // ERREUR DE COMPILATION : la variable 'codePostal' est invisible !
>       System.out.println(myObject.codePostal);
>   }
>}
>```

Nous pouvons néanmoins permettre de lire notre variable en ajoutant une méthode
publique dans notre classe `AdressePostale` ; on appelle ce genre de méthodes des
*getters* :

> ```java
>public class AdressePostale {
>
>   private int codePostal; // La variable est privée
>
>   public int getCodePostal() { // La méthode est publique
>       return codePostal;
>   }
>}
>```

De cette manière, notre variable est **protégée** contre les écritures
accidentelles. Personne ne pourra modifier sa valeur en dehors de la classe
qui en est responsable. C'est ce principe qu'on appelle *encapsulation*.

## [Chapitre suivant : L'envoi de messages](08_poo_envoi_messages.md)