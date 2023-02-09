## Classes, instances et envoi de messages

Nous avons vu que les concepts de base en POO étaient les objets et les classes.
Revenons sur ces 2 entités fondamentales.

Une classe est composée d'un ensemble de variables et de méthodes. Pour pouvoir
utiliser les variables et les méthodes d'une classe à l'intérieur de cette même
classe, on peut faire appel aux notions qu'on a déjà apprises dans les
langages procéduraux comme le pseudo-code ou le C.

Maintenant, si nous voulons utiliser une classe depuis l'extérieur de
cette classe, par exemple pour déclarer une variable du type de cette classe,
il faut appeler son constructeur avec le mot-clé `new`. On dira qu'un objet est
aussi **l'instance** d'une **classe**.

`Object o = new Object();`

Nous pouvons également appeler une méthode qui est déclarée dans une autre
classe que celle dans laquelle on se trouve. Pour cela, nous devons avoir une
instance de la classe qu'on souhaite utiliser.

Par exemple, voici deux classes `Personne` et `Chien` avec chacune leurs
propriétés respectives. Nous voulons ici modéliser le fait que quelqu'un
puisse promener son chien :

```java
// Fichier Humain.java
// ---------------------
public class Humain {

    private Chien leChien = new Chien();

    /**
     * Cette méthode demande au chien d'aller courir.
     */
    public void promenerLeChien()
    {
        leChien.courir();
    }
}

// Fichier Chien.java
// ---------------------
public class Chien {
    private boolean besoinDeCourir;

    /**
     * Cette méthode ne fait courir le chien que s'il a besoin de courir.
     */
    public void courir()
    {
        if (besoinDeCourir) {
            System.out.println("Le chien court !");
            this.besoinDeCourir = false;
        } else {
            System.out.println("Le chien n'a plus besoin de courir.");
        }
    }
}
```

Maintenant notre programme :

```java
public class Balade {

    public static void main(String[] args)
    {
        Humain maitre = new Humain();
        maitre.promenerLeChien();
    }
}
```

Dans ce programme :

- `Chien` et `Humain` sont des classes.
- La classe `Humain` est composée d'une variable de type `Chien`
- La classe `Humain` propose une méthode publique `promenerLeChien()`
- La variable `maitre` est une instance de la classe `Humain`
- L'instruction `maitre.promenerLeChien()` est un **envoi de message**

> **IMPORTANT** : en POO, un appel de fonction est un envoi de message ! Il faut
> bien faire la distinction entre un simple appel de fonction (comme c'est
> le cas dans les langages impératifs comme le C) et les envois de messages en POO.
>
> Pour faire un envoi de message, il faut un **receveur**, contrairement à un
> simple appel de fonction qui se fait sans receveur. En d'autres termes, pour 
> appeler une fonction, il faut que l'appel soit reçu par un objet.
>
> En Java, quand on appelle une fonction déclarée à l'intérieur de la même classe 
> on ne précise pas l'objet sur lequel on appelle cette fonction PARCE QUE LE
> RECEVEUR EST IMPLICITE. Mais il existe toutt le temps et il s'agit du mot-clé 
> **`this`**.
>
>Exemple :
>
>```java
>   public void programmeDeLaJournee() {
>
>       // Ici le receveur de la méthode promenerLeChien() est l'objet 
>       // implicite 'this'
>       promenerLeChien();
>
>       // Le code suivant est équivalent et permet de voir explicitement le 
>       // receveur de l'appel de méthode promenerLeChien() :
>       this.promenerLeChien();
>    }
>```

Pour envoyer un message à un objet (ie. appeler une méthode de cet objet), on utilise 
**la notation pointée**, c'est à dire qu'on met le nom de la variable suivi d'un 
point et enfin le nom de la méthode qu'on veut appeler.

Exemples :

```java
this.promenerLeChien(); // receveur = this
monChien.courir();      // receveur = monChien
Integer.parseInt("5");  // Cas particulier : receveur = Integer.class
```

D'autre part, il est possible de chaîner les envois de messages. Voici l'exemple de
la classe `StringBuilder` permettant de concaténer des chaînes de caractères :

```java
StringBuilder sb = new StringBuilder();
String hello = sb.append("Hello").append(" ").append("world!").toString();
System.out.println(hello);
```

> Le caractère point '.' en Java signifie donc **ENVOI DE MESSAGE** et il est 
> <span style="color: red">**TOUJOURS**</span> précédé **soit d'un nom de 
> variable, d'une expression qui retourne un résultat (un appel de fonction
> par exemple, ou d'un nom de classe.**

## [Chapitre suivant : L'héritage](08_poo_heritage.md)