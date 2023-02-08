## L'identité des objets

Quand on réalise l'opération `new AdressePostale()` on alloue en fait une quantité de
mémoire suffisante pour contenir toutes les variables de la classe `AdressePostale`.

Une fois cette allocation réalisée, la JVM appelle le **constructeur** de
l'objet, c'est à dire la méthode `AdressePostale()` qui est déclarée implicitement dans 
la classe `AdressePostale`.

Enfin, la JVM retourne ce qu'on appelle **une référence** (ie. une adresse) vers
la nouvelle variable qu'elle vient de créer. Cette adresse mémoire NE VA JAMAIS
CHANGER pendant toute la durée de vie d'un objet, elle restera toujours la même
et c'est ça qu'on appelle son **identité**.

Cependant, même si l'identité de notre objet ne change pas, nous pouvons créer
plusieurs variables qui copient la référence d'un objet. 

Dans l'exemple suivant, les variables `a1` et `a2` sont 2 variables qui référencent 
le même objet :

> ```java
>AdressePostale a1 = new AdressePostale();
>AdressePostale a2 = a1;
>```

Si on compare les deux variables avec le signe `==` nous aurons une égalité :

> ```java
>if ( a1 == a2 ) {
>   System.out.println("Les variables a1 et a2 sont égales");
>}
>``` 

L'opérateur **`new`** garantit que chaque objet a une identité unique. Vous
pouvez même essayer d'afficher son identité avec la
méthode `Object.identityHashCode()` qui retourne une valeur de type `int` :

> ```java
>public static void main(String[] args) {
>
>   // Création d'un objet
>   AdressePostale a = new AdressePostale();
>
>   // On calcule son identité et on la stocke dans une variable
>   int identity = System.identityHashCode(a);
>
>   // On affiche la valeur
>   System.out.println("L'identité de l'objet 'a' est " + identity);
>}
>```

## [Chapitre suivant : L'encapsulation](08_poo_encapsulation.md)