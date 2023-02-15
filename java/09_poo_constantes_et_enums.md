# Les constantes et les énumérations

## Les constantes

En programmation il est parfois tentant de mettre des nombres "en dur" car pour nous ces valeurs
ont une signification précise. Or il arrive souvent que ces valeurs n'aient pas la même
signification pour tout le monde, voire pas de signification du tout quand on ne connait pas
bien le contexte d'un projet.

```java
Server myServer = new Server(80); // Qui saura dire à quoi correspond ce nombre 80 ???
                                  // Réponse : PERSONNE. On dit que ce nombre est "magique"
                                  // car il sort du chapeau du programmeur, on ne sait pas
                                  // comment il/elle a déterminé qu'il fallait utiliser le 
                                  // nombre 80 à cet endroit.
```

Donner un nom à une valeur permet d'une part de clarifier à quoi correspond cette valeur et 
d'autre part de réutiliser la même valeur à différents endroits de notre code sans devoir
réécrire toute la valeur.

```java
Server myHttpServer = new Server(DEFAULT_HTTP_PORT); // Voilà, c'est doublement mieux : on a 
                                                     // renommé la variable et on a utilisé une
                                                     // constante pour décrire que notre nombre
                                                     // était en réalité le numéro de port HTTP
                                                     // par défaut.
```

Imaginez un outil pour convertir des heures décimales en heures/minutes/secondes. Vous aurez
besoin de savoir combien il y a de minutes dans une heure et combien de secondes dans une 
minute. Plutôt que de faire le calcul à la calculatrice, aidez-vous des constantes pour donner
du sens à vos calculs :


>```java
>public class Convertisseur {
>   
>   public static final double UNE_SECONDE = 1;
>   public static final double UNE_MINUTE = 60 * UNE_SECONDE;
>   public static final double UNE_HEURE = 60 * UNE_MINUTE;
>
>   public static double convertirHeuresEnSecondes(double heures){
>       return heures * UNE_HEURE;
>   }
>   public static double convertirMinutesEnSecondes(double minutes){
>       return minutes * UNE_MINUTE;
>   }
>}
>```

<div style="padding: 10px; border: #D50 solid 5px; color: #D50">
    <strong>Règle de nommage :</strong> le nom d'une constante est entièrement en MAJUSCULES
    et les noms composés sont séparés par des caractères underscores "_".
</div>

## Les énumérations ou _enum_

Une énumération est une classe qui ne contient que des constantes (ou presque). Sa philosophie
est de pouvoir énumérer un ensemble de constantes qu'on utilisera comme valeurs dans les 
variables de notre programme.

Si nous reprenons notre exemple de la classe `Voiture`, nous voudrions maintenant ajouter une
variable `energie` pour savoir si elle roule au Diesel, au SansPlomb ou au GPL. Nous
pouvons créer une énumération car le nombre de valeurs possibles n'est pas infini et se cantonne
à quelques-unes (que nous compléterons au fil des besoins dans notre application) :

```java
public enum TypeCarburant {
    Diesel,       // les éléments sont séparés par une virgule ','
    SansPlomb95,
    SansPlomb98,
    GPL;          // Le dernier élément est suivi d'un point-virgule ';'
}
```

Je peux ainsi ajouter une variable `energie` de type `TypeCarburant` dans ma classe `Voiture` :

```java
public class Voiture extends Vehicule {

    private String marque;

    private TypeCarburant energie;
}
```

### Est-il possible d'ajouter des informations dans une enum ?

Oui ! Avec des variables d'instance, comme dans une classe tradidionnelle.

Exemple : 

```java
public enum TypeCarburant {

    Diesel, SansPlomb95, SansPlomb98, GPL;

    // Les variables d'instance doivent être déclarées APRES l'enum

    private int indiceOctane;
}
```

Il faut ensuite initialiser les variables dans le constructeur :

```java
public enum TypeCarburant {

    Diesel, SansPlomb95, SansPlomb98, GPL;

    private int indiceOctane;

    // ATTENTION : Les constructeurs sont TOUJOURS 'private' dans une enum !
    private TypeCarburant(int i) { 
        this.indiceOctane = i;
    }
}
```

Et ce n'est pas fini : comme nous venons de définir un constructeur avec 1 argument,
le constructeur par défaut qui était implicite jusqu'à présent, n'existe plus. Or
les constantes de l'enum sont des objets qui étaient initialisés grâce au constructeur
par défaut... Donc il faut appeler le nouveau constructeur, pour chacune des constantes :

```java
/**
 * Maintenant notre enum est complète, et même documentée ;)
 */
public enum TypeCarburant {
    /** Moteurs diesel. */
    Diesel(0),
    /** Moteurs à combustion au sans plomb 95. */
    SansPlomb95(95),
    /** Moteurs à combustion au sans plomb 98. */
    SansPlomb98(98),
    /** Moteurs à combustion au GPL. */
    GPL(89);

    private int indiceOctane;

    private TypeCarburant(int i) { 
        this.indiceOctane = i;
    }
}
```

### Comment modifier la façon dont sont affichées les enums ?

Parfois vous devrez afficher une variable de type enum, soit dans des logs pour
débugguer votre application ou bien dans une page web. Il est donc parfois utile 
de surcharger la méthode `toString()` dans une enum pour qu'lle soit affichée 
selon votre propre formalisme.

Imaginons le programme suivant :

```java
class Test {
    public static void main(String[] args){
        System.out.println(TypeCarburant.Diesel);
    }
}
```

Voici le résultat si je lance la classe `Test` :

> `> Diesel`

Si je veux voir apparaître l'indice d'octane, je dois surcharger la méthode `toString()` :

```java
public enum TypeCarburant {
   
    Diesel(0), SansPlomb95(95), SansPlomb98(98), GPL(89);

    private int indiceOctane;

    private TypeCarburant(int i) { 
        this.indiceOctane = i;
    }

    /**
     * Surcharge de la méthode toString() en utilisant la méthode name() de la classe Enum.
     */
    public String toString(){
        return name() + " (indice d'octane = " + indiceOctane + ")";
    }
}
```

Voici le nouveau résultat si je relance la classe `Test` :

> `> Diesel (indice d'octane = 0)`

### La méthode toString() est pratique mais comment faire mieux ?

Imaginons que dans mon entreprise on utilise ma librairie Java avec ma classe TypeCarburant
un peu partout dans tous les services pour différents logiciels.

Certains services ont besoin d'afficher l'indice d'octane systématiquement mais d'autres
services n'en ont absolument pas besoin et cette information est même jugée parfois trompeuse
par les salariés.

Dans ce cas vous devriez ne pas surcharger votre méthode `toString()` mais ajouter
un _getter_ permettant aux utilisateurs de votre enum de récupérer l'indice d'octane
pour l'afficher s'ils le souhaitent :

```java
public enum TypeCarburant {
   
    Diesel(0), SansPlomb95(95), SansPlomb98(98), GPL(89);

    private int indiceOctane;

    private TypeCarburant(int i) { 
        this.indiceOctane = i;
    }

    /**
     * Retourne l'indice d'octane du type de carburant.
     */
    public int getIndiceOctane(){
        return this.indiceOctane;
    }
}
```

Voici un exemple d'application du service des assurances :

```java
public class ServiceAssurance {
    
    public void assurerVoiture(Voiture v){
        ...
        System.out.println("Nous n'assurons pas les voitures roulant au " + v.getEnergie().name());
        ...
    }    
}
/*
        Résultat : 
        > Nous n'assurons pas les voitures roulant au GPL
*/
```

Et un autre exemple du point de vue du service mécanique :

```java
public class ServiceMecanique {

     public void diagnostiquerVoiture(Voiture v){
        
        System.out.println("Diagnostique d'un véhicule " + v.getEnergie().name() + " (indice d'octane = " + v.getEnergie().getIndiceOctane() + ")");

        ...
    }
}
/*
        Résultat :
        > Diagnostique d'un véhicule SansPlomb98 (indice d'octane = 98)
*/
```

### Comment transformer une chaîne de caractère en enum ?

Votre programme a peut-être reçu des données venant d'une base de données et vous souhaitez 
maintenant les transformer en un type Java enum.

Pour ceci il faut utiliser la méthode `Enum.valueOf(String)`. Cette méthode est `static`
donc vous pouvez l'appeler sans instancier d'objet.

Exemple :

```java
public class Database {

     public TypeCarburant getTypeCarburant(int voitureId){

        TypeCarburant typeCarburant = null;

        String sql = "SELECT type_carburant FROM voiture WHERE id=" + voitureId;

        ResultSet rs = executeSql(sql);
        if (rs.next()){
            String sTypeCarburant = rs.getString(1);

            // Trouve la bonne constante dans l'enum TypeCarburant :
            typeCarburant = TypeCarburant.valueOf(sTypeCarburant);
        }
         rs.close();

        return typeCarburant;
    }
}
```


## Pour aller plus loin

Entraînez-vous à créer des enum (reprenez vos TP de POO et voyez où vous pouvez utiliser des enum).
Lisez la [javadoc de la classe Enum](https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/lang/Enum.html) et listez les méthodes dont vous pourriez avoir besoin.