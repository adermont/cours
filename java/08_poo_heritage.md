## Héritage

Lorsqu'on veut réutiliser les propriétés d'une classe, on peut la faire hériter
d'une classe existante avec le mot-clé `extends` :

```java
public class Humain extends Animal {
    // La classe Humain disposera de toutes les variables d'instance
    // définies dans la classe Animal ainsi que toutes ses méthodes.
}
```

On dit alors que `Humain` est une **sous-classe** de `Animal` et que `Animal` 
est la **super-classe** ou la classe parente de `Humain`.

En Java, si une classe ne définit aucune super-classe, elle hérite 
automatiquement de la classe `Object` (dont le nom complet est `java.lang.Object`).


**Règle n°1 : visibilité des variables et méthodes**
Quand une classe B hérite d'une classe A, elle aura les mêmes variables et les 
mêmes méthodes `public` ou `protected` de la classe A.

>Exemple (notation UML) :
>
>[![](https://mermaid.ink/img/pako:eNp9k1FvmzAQx78K8tOqkSgGmiaoL1M2bdJUrVoeKk28GLikJ5kzO9tSuyzffSZFLQw2v4D9_9_dzz77JCpTg8hFpZW1H1EdWTUFRWHcs6k9uuj292IR3SkHjKA_aagcmwZIHYH_Y_yCB5yRv3GNFCye7w07VWoo6MV2AXg1n14Wu_G-ZXyK8gjJDRap_EAEYD8rVuQQJoYabMXYOjQUtL1jpONAbhT_9PCXch6izG95SLZAqrGC79AGiBI1uglGb9kZsqZpVE8zJgXr-hQa3l1FpTEaFA0MR3DDBF8fHoPtNccsdHf8I9TWo7WKKniYItp9CAIThH_U9jo0LNTcGW14puq0q-PabCqwNsgznVhQuTNd5NA0BgxXcnJogestIqCN2ihi0QA3Cutwsy8khXCP0EAh8vBbw0F57QpRUGdV3pn9M1Uid-whFr6tw176tyDyg9I2rLaKfhgzmov8JJ5EfiOX2yRJk1WykduVzK5j8SzyRCbLdbZJbtYruUmv0yw7x-LXJYNcynUq11kmt2kmsyDHAmp0hu_6x9h9zn8AodIfbA?type=png)](https://mermaid.live/edit#pako:eNp9k1FvmzAQx78K8tOqkSgGmiaoL1M2bdJUrVoeKk28GLikJ5kzO9tSuyzffSZFLQw2v4D9_9_dzz77JCpTg8hFpZW1H1EdWTUFRWHcs6k9uuj292IR3SkHjKA_aagcmwZIHYH_Y_yCB5yRv3GNFCye7w07VWoo6MV2AXg1n14Wu_G-ZXyK8gjJDRap_EAEYD8rVuQQJoYabMXYOjQUtL1jpONAbhT_9PCXch6izG95SLZAqrGC79AGiBI1uglGb9kZsqZpVE8zJgXr-hQa3l1FpTEaFA0MR3DDBF8fHoPtNccsdHf8I9TWo7WKKniYItp9CAIThH_U9jo0LNTcGW14puq0q-PabCqwNsgznVhQuTNd5NA0BgxXcnJogestIqCN2ihi0QA3Cutwsy8khXCP0EAh8vBbw0F57QpRUGdV3pn9M1Uid-whFr6tw176tyDyg9I2rLaKfhgzmov8JJ5EfiOX2yRJk1WykduVzK5j8SzyRCbLdbZJbtYruUmv0yw7x-LXJYNcynUq11kmt2kmsyDHAmp0hu_6x9h9zn8AodIfbA)
>
>Dans cet exemple, les classes `MaterielElectromenager`, `MaterielHifi` et 
>`OrdinateurPortable` héritent de la classe `Produit` et voient donc tous ses
>attributs et méthodes publics. Le code suivant est donc valide :
>
>```java
>OrdinateurPortable lenovoLaptop = new OrdinateurPortable();
>lenovoLaptop.prix = 1500;
>```


**Règle n°2 : l'héritage N'EST PAS MULTIPLE** (contrairement au langage C++ par exemple).
Si une classe B hérite d'une classe A, elle ne peut plus hériter d'une autre classe.

>Exemple de code invalide:
>
>```java
>public class OrdinateurMachineALaver extends Ordinateur, MachineALaver{
>
>}
>```
>
>En général, on comprend assez bien ce concept car il faut se représenter l'héritage
>comme une relation "est". Un ordinateur EST un produit, une machine à laver EST un
>produit également, mais un ordinateur N'EST PAS une machine à laver et vice-versa. 


**Règle n°3 : méthodes et classes abstraites**
Une classe n'est pas obligée **d'implémenter** (retenez bien ce terme car il a une
vraie signification en programmation orientée objet) toutes ses méthodes. Il est 
possible de laisser certains méthodes **abstraites** avec le mot-clé `abstract`.
Dans ce cas, la classe devra être elle aussi déclarée avec le mot-clé `abstract`.

>Exemple :
>
>```java
>/**
> * Un Ordinateur générique qui hérite de la classe Produit.
> */
>public abstract class Ordinateur extends Produit {
>
>   /**
>    * Cette méthode indique s'il est possible de porter 
>    * l'ordinateur à une seule main.
>    */
>   public boolean isPortable(); 
>}
>
>/**
> * Un OrdinateurPortable qui hérite des caractéristiques d'un Ordinateur
> * et définit également une nouvelle variable 'poids' avec le getter associé.
> */
>public class OrdinateurPortable extends Ordinateur {
>
>   private int poids;
>
>   /**
>    * @return Le poids de l'ordinateur portable, en grammes.
>    */
>   public int getPoids() {
>       return this.poids;
>   }
>
>   /**
>    * Cette méthode retourne 'true' si le poids de l'ordinateur 
>    * est inférieur à 3kg.
>    */
>   public boolean isPortable() {
>       return getPoids() < 3000; // 3kg
>   }
>}
>```
>
>Une classe qui n'est pas abstraite est une classe **concrète**.

**Règle n°4 : classes abstraites sans méthodes abstraites**

On peut déclarer une classe avec le mot-clé `abstract` même si aucune de ses méthodes
n'est déclarée avec le mot-clé `abstract`.

>```java
>/**
> * Un Ordinateur qui hérite des caractéristiques d'un Produit
> * et implémente des méthodes utilisables par les sous-classes.
> * 
> * Cependant cette classe ne dispose pas d'assez d'informations pour qu'on puisse
> * l'exploiter alors on la déclare abstraite pour interdire de s'en servir directement.
> */
>public abstract class Ordinateur extends Produit {
>
>   protected int nbProcesseurs;
>   protected int quantiteRam;
>
>   /**
>    * @return Le nombre de processeurs de l'ordinateur.
>    */
>   public int getNbProcesseurs() {
>       return this.nbProcesseurs;
>   }
>
>   /**
>    * @return La quantité de RAM de l'ordinateur.
>    */
>   public int getQuantiteRam() {
>       return this.quantiteRam;
>   }
>}
>```

**Règle n°5 : les classes abstraites sont non instanciables**

On ne peut pas instancier une classe abstraite. Il n'est possible d'instancier que 
des objets dont la classe est concrète.

>Exemple en reprenant le code précédent :
>
>```java
>Ordinateur ordi = new Ordinateur(); // INTERDIT car Ordinateur est une classe abstraite
>```

### Les interfaces

Une interface est comme une classe abstraite (d'ailleurs une fois qu'une 
interface est compilée elle devient une classe abstraite) mais aucune de 
ses méthodes n'est implémentée.

Une interface se déclare avec le mot-clé `interface` au lieu de `class` :

>```java
>/**
> * Ici pour rester sur nos exemples de produits et d'ordinateurs, nous introduisons
> * le concept d'une entité qui dispose de processeurs et nous l'appelons "HasProcessors".  
> */
>public interface HasProcessors {
>
>   /**
>    * Quelle que soit la manière dont on les déclare, les méthodes d'une interface sont
>    * toujours "public", c'est forcé à la compilation. Inutile de mettre le mot-clé "public".
>    */
>   int getNbProcessors();
>}
>```

Maintenant que nous avons une interface `HasProcessor`, nous pouvons implémenter ses
caractéristiques à la fois dans la classe `Ordinateur` et ses sous-classes `OrdinateurPortable`
et `OrdinateurDeBureau`, mais aussi dans `MachineALaver` ! Car on peut **implémenter**
autant d'interfaces que l'on souhaite, contrairement à l'héritage qui nous contraint
à n'hériter que d'une seule classe.

Notez qu'on n'utilise plus `extends` mais plutôt **`implements`** pour hériter d'une interface.

>```java
>public class Ordinateur extends Produit implements HasProcessors {
>
>}
>public class MachineALaver extends Produit implements HasProcessors {
>
>   /**
>    *
>    */
>   int getConsommationKWh();
>}
>```

En résumé, une interface permet de définir un **comportement commun** plutôt qu'une 
nature d'objets. Une interface est comme un **contrat** qu'une classe peut décider 
d'implémenter ou non, pour offrir à ses clients toutes les méthodes de ce contrat.

On parlera parfois de "facettes" pour exprimer le fait qu'une classe puisse exposer
ou non les services définis dans une interface.

L'utilisation d'une interface est identique à l'utilisation d'une classe sauf
qu'on ne peut pas instancier une interface, il faut instancier une classe concrète qui
implémente cette interface :

>```java
>HasProcessors anyMachine = new HasProcessors(); // INTERDIT
>
>HasProcessors laptop = new Ordinateur(); // OK
>```

## [Chapitre suivant : Polymorphisme](08_poo_polymorphisme.md)