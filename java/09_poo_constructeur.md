# Les constructeurs

Dans le cours précédent, nous avons appris la différence entre une variable de type primitif
et une variable de type objet. On initialise une variable de type primitif de cette façon :


>```java
> <type_primitif> <nom> = <valeur>;
>```
 
Avec :
- `<type>` qui est un type primitif parmi `boolean`, `byte`, `short`, `int`, `float` ou `double`
- `<nom>` qui est un nom composé uniquement de **lettres, de chiffres et de underscores "`_`"**
- `<valeur>` qui est soit un nombre ou bien une expression équivalente à un nombre (une opération 
mathématique, un appel d'une méthode dont le type de retour est un type  ou une autre variable
du même type).

Exemples d'initialisations de variables primitives :

>```java
>int nombre5 = 5; // nombre "en dur"
>int nombreEntier = Integer.parseInt("512"); // appel d'une méthode qui retourne un 'int'
>float nombreFlottant = 2.3f + 6.1f; // opération mathématique
>byte octet = 0xff; // nombre "en dur"
>short petitNombre = 122; // nombre "en dur"
>double nombrePrecis = Math.PI; // référence à la constante 'PI' déclarée dans la classe 'Math'
>``` 

On initialise une variable de type objet de cette façon :

>```java
> <type_objet> <nom> = <valeur_objet>;
>```

Avec :
- `<type_objet>` qui est le nom d'une classe, d'une interface ou d'une enum
- `<nom>` qui est un nom de variable
- `<valeur_objet>` qui est un appel à un constructeur OU une référence à un objet existant 
(autre objet, appel de méthode qui retourne un objet compatible)

Exemples :
>```java
>// initialisation grâce au constructeur "vide" (ie. sans paramètres) de la classe Object
>Object o = new Object(); 
>
>// initialisation avec appel de la méthode valueOf de la classe Integer
>Integer objetNombre5 = Integer.valueOf(5); 
>
>// Initialisation grâce au constructeur à 1 argument de la classe String :
>String url = new String("http://www.simplon.fr");
>
>// Initialisation en référençant un object existant :
>String url2 = url;
>``` 

<div style="border: #D50 solid 5px; padding: 10px; color: #D50">
<strong>RAPPEL</strong> :
En java, la plupart du temps on déclare et on initialise les variables en même temps. 
Mais il faut bien dissocier les termes suivants :
<ul>
<li>
    <strong>Déclarer</strong> une variable = dire au compilateur qu'elle existe :
    <ul><li><pre>int maVariable; // déclaration seule</pre></li></ul>
</li>
<li><strong>Initialiser</strong> une variable = lui assigner une valeur avec le signe "="
    <ul><li><pre>maVariable = 5; // initialisation seule</pre></li></ul>
    <ul><li><pre>int maVariable = 5; // déclaration + initialisation</pre></li></ul>
</li>
</li>
<li><strong>Instancier un objet</strong> = créer un objet en appelant un des constructeurs 
de sa classe avec le mot-clé "new"
    <ul>
        <li>Ici un exemple de déclaration + initialisation + instanciation :
        <pre>Object anObject = new Object();</pre>
        </li>
    </ul>
</li>
</div>
<p></p>

Une variable n'est qu'un réceptacle, une boite qui peut contenir soit une valeur primitive
(ie. un nombre) ou une référence (ie. l'adresse mémoire) d'un objet.

Un objet est un bloc de mémoire contenant plusieurs variables, donc potentiellement d'autres
objets aussi. Il représente quelque chose du monde réel (ça peut être n'importe quoi, tout
concept dont on a besoin pour développer notre application).

En Java, on modélise un système informatique avec des objets plutôt qu'avec des variables 
primitives parce que c'est beaucoup plus modulaire et maintenable. Par exemple si je souhaite faire
un système de gestion d'une flotte de véhicules, je peux représenter les voitures ou les camions
du monde réel par des "objets" virtuels, de classe `Voiture` ou `Camion` et ainsi bien séparer
ce qui est lié aux voitures et ce qui est lié aux camions dans des fichiers séparés, plus faciles
à lire et à comprendre.

Pour donner vie aux concepts de mon système informatique (ie. les classes), il faut instancier des objets avec lesquels on pourra faire des calculs en appelant les méthodes définies dedans.

## À quoi sert un constructeur ?

Le constructeur est une méthode particulière qui permet d'initialiser vos variables d'instance.
Car pour pouvoir utiliser les variables d'un objet, elles doivent avoir été initialisées. C'est
le rôle du constructeur.

Imaginons par exemple le code suivant :

>```java
>/**
> * Au moment d'appeler la méthode 'addWagon(Wagon)' il y aura un problème
> * car la variable 'wagons' n'a pas été initialisée. En réalité vous apprendrez
> * que les variables d'instance (et uniquement elles, pas les variables locales) 
> * sont initialisées avec une valeur par défaut qui est 'null' pour les objets et
> * les tableaux, et zéro pour les variables de types primitifs.
> */
>public class Train {
>   private Wagon[] wagons; // initialisé à null par défaut
>   private int nbWagons; // initialisé à 0 par défaut
>
>   public void addWagon(Wagon w){
>       wagons[nbWagons] = w;
>       nbWagons++;
>   }
>}
>```

## Le constructeur par défaut

En Java, toute classe dispose d'un constructeur par défaut, c'est à dire un constructeur sans 
paramètres (j'utilise parfois le terme "arguments" mais considérez que c'est la même chose).
Si vous ne déclarez AUCUN CONSTRUCTEUR, un constructeur par défaut est créé automatiquement à
la compilation de la classe. 

Exemple :

>```java
>public class Train {}
>```

Cette classe aura un constructeur par défaut et je pourrai instancier un objet de cette classe
de cette manière :

>```java
>Train v = new Train();
>```

Si vous déclarez explicitement le constructeur par défaut, cela ne change rien sauf si vous 
**réduisez sa visibilité** de public vers `protected` ou `private`. En effet, certaines fois 
on peut vouloir interdire d'appeler le constructeur par défaut (c'est souvent le cas dans les 
classes où toutes les méthodes sont `static` car ça ne sert à rien d'instancier un objet
pour utiliser une méthode `static`) :

>```java
>public class StringUtils {
>
>    /** Constructeur par défaut invisible car déclaré avec visibilité 'private'.
>     *
>     * Il sera donc interdit d'écrire `new StringUtils()`. 
>     */
>    private StringUtils(){}
>
>    public static final String capitalize(String s) {...}
>    ...
>}
>```


## Super constructeur

En Java, **la première instruction** d'un constructeur doit **OBLIGATOIREMENT** être 
un appel à l'un des constructeurs de la super-classe. La plupart du temps, vous n'avez 
rien à faire car cet appel est ajouté AUTOMATIQUEMENT à la compilation de votre classe 
s'il est manquant.

>```java
>public class Vehicule {
>    public Vehicule(){
>        // appel implicite au constructeur par défaut de la classe Object
>    }
>}
>```

Voici comment appeler le super-constructeur par défaut (prenez le réflexe de **TOUJOURS** 
l'appeler **explicitement**, c'est une bonne pratique pour éviter les confusions) :

>```java
>// Fichier Vehicule.java (1 CLASSE = 1 FICHIER !)
>// -----------------------------------------------------------
>public class Vehicule {
>    // Aucun constructeur déclaré ==> présence implicite du constructeur par défaut
>}
>
>// Fichier Voiture.java
>// -----------------------------------------------------------
>public class Voiture extends Vehicule {
>    public Voiture(){
>        super(); // appel explicite au constructeur par défaut de la super-classe
>    }
>}
>```

Si le constructeur par défaut de la super-classe n'est pas adapté à ce que 
vous souhaitez faire, il faudra là aussi réaliser un appel explicite à un autre 
super-constructeur.


### _Cas particuliers_

Si votre classe hérite d'une super-classe **sans constructeur par défaut** ou bien 
s'il est déclaré avec la visibilité **private**, **vous devrez écrire un appel EXPLICITE** 
à un autre super-constructeur déclaré avec la visibilité **public** ou **protected**.

>```java
>// Fichier Vehicule.java
>// -----------------------------------------------------------
>public class Vehicule {
>   private String marque;
>
>   public Vehicule(String pMarque){
>       this.marque = pMarque;
>   }
>}
>
>// Fichier Voiture.java
>// -----------------------------------------------------------
>public class Voiture extends Vehicule {
>    public Voiture(){
>        super(null); // Obligation d'appeler le seul constructeur déclaré : c'est 
>                     // celui qui prend une chaîne de caractères en paramètre. On laisse
>                     // ce paramètre à 'null' pour le moment si on ne sait pas quoi mettre dedans.
>    }
>}
>```

Dans l'exemple ci-dessus, tout compile mais je risque de me retrouver avec une 
variable non initialisée. Pour initialiser correctement les variables de la 
super-classe, je dois modifier mon constructeur pour ajouter un paramètre `marque` 
comme dans la super-classe et appeler le constructeur de ma super-classe :

>```java
>public class Voiture extends Vehicule {
>    public Voiture(String marque){
>        // Maintenant on peut instancier une Voiture et il est obligatoire de 
>        // fournir la marque au constructeur pour respecter la philosophie de
>        // la super-classe 'Vehicule'.
>        super(marque);
>    }
>}
>```


## Surcharge de constructeurs

Dans la réalité, il arrive souvent qu'on ait plein de *variables d'instance* dans 
nos classes et que la plupart soient initialisées dans le constructeur grâce à des
paramètres. Par comodité, on crée donc des constructeurs qui prennent moins de 
paramètres, pour que ce soit plus rapide à écrire dans les cas standards.

Exemple :

>```java
>// Pour construire une chaîne de caractères, on devrait normalement préciser
>// son encodage (ie. son jeu de caractères) comme ceci :
>String excusezMoiEnIslandais = new String("Afsakið, Fyrirgefðu", Charsets.UTF_8);
>```

Mais comme la plupart du temps on écrit ses fichiers Java dans le jeu de caractères UTF8,
il n'est pas nécessaire de demander systématiquement un `Charset` en paramètre du constructeur
de `String`. Les concepteurs ont donc prévu ce cas de figure et proposent un constructeur
qui prend en argument une chaîne de caractères :

>```java
>// La chaîne entre guillemets suffit dans la majorité des cas :
>String excusezMoiEnIslandais = new String("Afsakið, Fyrirgefðu");
>```

### Quelle stratégie adopter pour déclarer ses constructeurs ?

L'idée est assez simple : on commence par écrire (ou générer avec IntelliJ !) 
le constructeur qui prend le plus de paramètres possibles et ensuite on écrit
des constructeurs plus simples qui appellent ce constructeur avec des valeurs
"par défaut".

>```java
>// Voici une ébauche de serveur Web qui écoutera sur le port 80 par défaut mais
>// on peut modifier ce numéro de port à la construction si on le souhaite.
>// On a aussi une variable pour configurer le nombre maximum de requêtes 
>// simultanées.
>public class HttpServer {
>
>    public static final int DEFAULT_PORT = 80;
>    public static final int DEFAULT_MAX_SIMULTANEOUS_REQUESTS = 20;
>
>    private int port;
>    private int nbMaxRequests;
>
>    /**
>     * Par convention on déclare le constructeur par défaut en premier.
>     */
>    public HttpServer(){
>        // appel au constructeur HttpServer(int,int)
>        this(DEFAULT_PORT, DEFAULT_MAX_SIMULTANEOUS_REQUESTS); 
>
>        // Notez que dans le cas où un constructeur en appelle un autre, on ne
>        // doit pas appeler le super-constructeur.
>    }
>
>    public HttpServer(int pPort){
>        this(pPort, DEFAULT_MAX_SIMULTANEOUS_REQUESTS);
>    }
>
>
>    public HttpServer(int pPort, int pNbMaxRequests){
>        super(); // Appel explicite au super constructeur de la classe Object
>        this.port = pPort;
>        this.nbMaxRequests = pNbMaxRequests;
>    }
>
>    /**
>     * Démarrage du serveur.
>     */
>    public void start(){
>        ...
>    }
>}
>```

La plupart du temps nous écrirons `new HttpServer()`, sauf si par exemple nous lançons
deux serveurs sur notre machine, ce qui créera un conflit d'utilisation du port 80. Dans
ce cas nous pourrons donc instancier nos serveurs avec le second constructeur :

>```java
>public static void main(String[]args){
>
>   HttpServer server1 = new HttpServer(8080);
>   HttpServer server2 = new HttpServer(8081);
>
>   server1.start();
>   server2.start();
>}
>```

Ce qui est strictement équivalent au code suivant :

>```java
>public static void main(String[]args)
>{
>   HttpServer server1 = new HttpServer(8080, HttpServer.DEFAULT_MAX_SIMULTANEOUS_REQUESTS);
>   HttpServer server2 = new HttpServer(8081, HttpServer.DEFAULT_MAX_SIMULTANEOUS_REQUESTS);
>
>   server1.start();
>   server2.start();
>}
>``
