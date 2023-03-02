# Conception Orientée Objet : méthodologie DDD

Parfois devant un énoncé on a l'angoisse de la page blanche car on manque de 
pratique en programmation ou dans un langage en particulier. Mais ça ne doit pas 
être un frein. Nous allons voir comment avancer quand on n'a pas encore une 
grande expérience en programmation, simplement avec quelques notions que sont 
les classes et les fonctions. Et quelques dessins :)

Les principes de conception qui sont proposés ici s'appellent **"Domain Driven
Design"** ou "Conception par la modélisation du domaine". Il en existe bien 
d'autres et on utilise souvent plusieurs approches sur un gros projet, en 
fonction du sous-système qu'on cherche à réaliser. La méthodologie DDD se prête
bien à l'apprentissage de la conception car elle est une approche assez 
naturelle.


## 1. Etude des spécifications

Etudiez vos User Stories avec attention pour essayer de déterminer 
quelles sont les données sur lesquelles vous allez devoir travailler. Relevez 
les noms (au sens grammatical) et les verbes qui reviennent souvent : Client, 
Achète, Produit, Fournisseur, Livraison, Commande, Facture ...etc.

Les **noms** se transforment souvent en **tables** de la base de données et en 
**classes** Java, tandis que les **verbes** se transformeront en **liens** entre 
vos classes ou en méthodes Java.

## 2. Modèle de données

Ensuite vous faites un brainstorming avec vos collègues dans le but de sortir 
un MPD (modèle physique de données), c'est à dire le diagramme relationnel `MySQL`
avec les relations entre vos tables, les clés primaires, étrangères et les index.

## 3. Diagramme de classes du domaine

Vous en déduisez ensuite logiquement un **diagramme de classes** du domaine.
C'est ce qu'on appelle le MCD ou Modèle Conceptuel de Données. Sur ce diagramme,
on devrait voir une classe par table de la BDD, sauf pour les tables de liens 
qui sont formalisées autrement. Les tables de liens doivent être modélisées sous 
forme d'un lien entre deux classes où chaque extrémité du lien comporte une 
cardinalité (aussi appelée "multiplicité") et le nom du lien sera souvent un 
verbe.

Par exemple pour Produit, Client et Commande vous ne modélisez que Produit et 
Client puis vous les reliez par un lien "commande >" allant de Client vers Produit
pour dire qu'un client peut commander 1 ou N produits. La cardinalité côté
Produit sera donc "1..N". Côté Client, comme une commande ne concerne qu'un seul 
client, donc la cardinalité sera "1".

## 4. Diagramme de classes de la logique métier

Une fois vos données déterminées et posées sur un diagramme de classes, vous aurez
une meilleure vision de ce que doit faire votre programme. Vous devrez alors compléter
votre diagramme de classes avec les classes de ce qu'on appelle la "logique métier".

C'est la partie la plus compliquée : imaginer quels sont les traitements à faire sur
les données. Pour faire cette étape, partez de vos user stories et détaillez chaque
étape progressivement. Par exemple pour un site e-commerce : 

1. Le cient parcourt la liste des produits
2. Il clique sur le bouton "Ajouter au panier"
3. Il valide son panier pour passer commande
4. Il saisit ses identifiants
5. Il valide le paiement
	
En partant de cette liste assez générale, demandez-vous comment :

1. Présenter une liste de produits à l'utilisateur ?

   1.1. Se connecter à la base de données  
   1.2. Exécuter une requête SQL pour obtenir la liste des produits  
   1.3. Afficher les produits à l'utilisateur  
	
Faites ceci pour chaque étape de votre processus et continuez à décomposer le plus
possible vos étapes jusqu'à obtenir une phrase que vous saurez coder de manière 
évidente. Dans mon exemple ci-dessus, toutes les étapes sont maintenant 
traduisibles en code de manière assez simple (à quelques détails techniques 
près) :

<ul><ul>
<li>
   1.1. La connexion se fait avec les classes `Database` et `MySqlDatabase` qui 
   permettent d'initialiser le driver MySQL et d'ouvrir des connexions.
</li>
<li>
   1.2. La méthode `Connection.createStatement()` permet de créer une 
   interaction avec la BDD puis `Statement.executeQuery("...")` permet 
   d'exécuter une requête SQL. Ensuite il faut faire le 
   **mapping objet-relationnel** en créant des objets de type `Produit` à partir 
   d'un objet `ResultSet` en appelant les méthodes `ResultSet.getInt()`, 
   `ResultSet.getString()`...etc.
</li>
<li>
   1.3. L'affichage dans la console se fait avec `System.out.println()` pour 
   chaque produit retourné par l'étape précédente.
</li>
</ul></ul>

Vous obtenez ainsi le squelette de votre application, sous forme de texte. 

Pour en faire un squelette de code, il n'y a qu'un pas : chaque étape est une 
fonction de votre futur programme ! Donc votre prochaine étape est de donner un 
nom de fonction à chaque étape.

<ul><ul>
<li>
   1.1. `getConnection()`
</li>
<li>
   1.2. `getAllProduits()`
</li>
<li>
   1.3. `displayProduits()`
</li>
</ul></ul>

Mais comme vous le savez, ce n'est pas suffisant. Il nous manque des 
informations pour déclarer nos fonctions en Java. Vous devez déterminer quels 
sont leurs **TYPES DE RETOUR** et leurs **PARAMETRES**.

Reprenons notre exemple :
<ul><ul>
<li>
1.1. Pour se connecter à la base de données, il faut utiliser la méthode 
   `DriverManager.getConnection(url,user,password)`. Donc votre méthode 
   `getConnection()` devra prendre en paramètre l'URL de la BDD ainsi que le 
   login/password d'un utilisateur autorisé à accéder à cette BDD. D'autre part 
   son type de retour sera le même que `DriverManager.getConnection()`, c'est à 
   dire une connexion de type `java.sql.Connection`.
   
> `public java.sql.Connection getConnection(String url, String login, String password)`
</li>
<li>		  
1.2. Pour obtenir la liste des produits, il n'y a pas besoin de paramètres
   puisqu'on est capable d'écrire la requête SQL à exécuter sans avoir 
   besoin d'infos supplémentaires : "SELECT \* FROM produits".
   Le type de retour sera une liste d'objets de classe "Produit".
   
> `public List\<Produit\> getProduits()`
</li>
<li>1.3. Pour afficher vos produits, votre fonction a besoin de prendre en paramètre 
   la liste des produits à afficher. Par contre, aucun type de retour car la 
   fonction n'a rien à calculer, on veut juste qu'elle fasse un affichage dans 
   la console.
   
> `public void displayProduits()`
</li>
</ul></ul>

## 5. Bien séparer les responsabilités

Prochaine étape de la conception : regrouper toutes vos méthodes dans des classes, ou
mieux : dans des interfaces. Certaines méthodes sont des méthodes purement techniques
(comme `getConnection()`) et d'autres sont des méthodes de la "logique métier" du e-commerce
(`getProduits()` et `displayProduits()`). Il faut **trouver qu'est-ce qui les relie entre elles**
et en général le nombre de réponses à cette question est infini car très subjectif.

Ce découpage est en partie subjectif, certes, mais il existe des principes
de conception et des bonnes pratiques qu'on regroupe sous un acronyme : **SOLID**.
Le principal à retenir est peut-être ceci : **chaque classe doit être spécialisée
pour faire le moins de choses possibles**. Car plus une classe (ou une méthode)
est compliquée, plus elle sera difficile à faire évoluer !

Rappelez-vous : on doit tester chacune de nos classes. Plus une classe fait de 
choses, plus son test sera compliqué. Et plus un test est compliqué, plus il 
devient une source d'erreurs ! Et moins il est maintenable par quelqu'un d'autre
car trop compliqué... D'ailleurs c'est un bon indicateur : si votre test devient
trop complexe à écrire, c'est qu'il y a probablement un problème de conception.

L'approche par objets sert à diviser les problèmes en sous-problèmes plus 
faciles à gérer.

Si une classe gère des commandes de produits, il y a fort à parier qu'elle devra
aussi gérer des clients. Peut-être serait-il bon dans ce cas d'avoir une classe
qui s'occupe de fournir des services pour gérer des produits, une autre classe 
pour gérer des clients et une classe pour passer des commandes. Mais ne pas 
faire une classe qui gère tous les types d'objets est une bonne pratique ! 
(Attention cependant, c'est toujours une histoire de compromis, car sur de 
petits projets (moins de 500 lignes de code) c'est souvent inutile de séparer 
autant les responsabilités dans plusieurs classes car ça prend du temps ; mais 
ce sera toujours plus clair et plus facile à comprendre, c'est indéniable.)

Encore une fois : tout est question de compromis. Vous travaillerez peut-être 
dans une équipe qui a beaucoup de mal à appliquer ces principes ou bien dans une
équipe qui les applique trop scrupuleusement. Tout ceci va compter dans vos 
décisions finales de conception et vous devrez parfois écrire des classes ne
contenant qu'une seule méthode publique qui ne rend qu'un seul service. En soi,
ça ne constitue pas du tout une mauvaise pratique, c'est juste très verbeux et
sur de gros projets vous vous retrouverez avec un nombre incroyable de classes.
Ce qui peut constituer un désavantage car le chargement d'une classe est coûteux
en Java par exemple. À vous de savoir où positionner le curseur pour choisir la
bonne "granularité", tout en sachant que moins une classe fait de choses mieux
on saura lui trouver un nom et plus ce sera facile de la tester et de l'utiliser.

Faites vos propres recherches sur les principes SOLID, pour ma part je vous 
recommande [ce lien](https://alexsoyes.com/solid/) pour débuter mais je vous 
invite à approfondir.

## 6. Diagrammes de séquence

Pour mieux appréhender le séquencement des opérations, c'est à dire dans quel 
ordre on appelle quelle méthode, il existe en UML un type de diagramme qui 
s'appelle le diagramme de séquence. Faites une veille sur ce sujet, je vous 
recommande par exemple cette [vidéo](https://www.youtube.com/watch?v=AZ4gwy-ZGC4).



