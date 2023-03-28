# JavaScript / ECMAScript

Le JavaScript (ou plus précisément ECMAScript) est un langage de programmation
**objet, avec un typage faible (basé sur des prototypes) et interprété** :

- Objet : les variables sont des objets (ils ont des attributs et des méthodes)
- Typage faible : le type d'une variable est déterminé par inférence de son
  contenu
- Interprété : pas besoin de compiler le code

JavaScript est utilisé :

- **côté client** dans les pages HTML pour rendre le contenu des pages 
  dynamiques en fonction d'évènements venant du navigateur ou bien de
  l'utilisateur (clics de souris, focus, frappes au clavier...). 
- **côté serveur** depuis l'apparition des interpréteurs de JavaScript 
  autonomes comme `Node.js`. 

Tous les navigateurs Web disposent maintenant d'un interpréteur ECMAScript qui
fournit aux programmeurs une API leur permettant d'agir sur les éléments d'une
page HTML.

Concrètement, cela veut dire qu'on manipule les pages HTML grâce à des variables
prédéfinies (`document`, `window`, `console`...) et dont le type est issu 
d'une spécification qu'on appelle le **DOM** (pour *Document Object Model*).

## Déclarer un script

Il existe 2 façons de déclarer un script dans une page HTML :

```html
<!DOCTYPE html>
<html lang="fr">
<head>

    <!-- PREMIERE FACON : COMME FICHIER EXTERNE -->
    <script type="text/javascript" src="monFichier.js"></script>

    <!-- SECONDE FACON : INTEGRATION DIRECTE DANS LA PAGE -->
    <script type="text/javascript">
        /* Instructions */
    </script>

</head>
<body>

<!-- IL EST AUSSI POSSIBLE DE LE METTRE ENTRE LES BALISES BODY -->
<script type="text/javascript">
    /* Instructions */
</script>

</body>
</html>
```

## Débuter facilement

Le plus facile et le plus simple si vous n'êtes pas encore à l'aise avec un
environnement de développement Web est d'aller
sur [CodePen](https://codepen.io/pen/?editors=1111). Vous mettez votre code HTML
dans un éditeur, le code JavaScript dans un autre éditeur, et le résultat est
recalculé en temps réel, comme si votre page HTML était rechargée à chaque fois
que vous écrivez une nouvelle ligne de code.

Cela dit, la solution la plus ergonomique et performante est de coder dans
IntelliJ ou VSCode et de tester le résultat dans votre navigateur en affichant
votre page HTML car ces IDE disposent de mécanismes de rechargement à chaud à
chaque fois que vous sauvegardez votre fichier.

**Dans les 2 cas, vous disposez de l'auto-completion, donc servez-vous en !**

Commencez par écrire cette page HTML et enregistrez le résultat dans un 
fichier :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <script type="text/javascript">
        console.log("Bonjour");
    </script>
</head>
<h1>Titre de la page</h1>
</html>
```

Ouvrez ensuite votre fichier dans un navigateur et faites un clic 
droit puis "Inspecter". Affichez ensuite la console. Vous observerez que le 
message "Bonjour" s'est bien affiché dans la console.

L'instruction que vous venez d'écrire est équivalente
à `System.out.println("Bonjour")` en Java.

## Dans quel ordre sont exécutées les instructions ?

La question qu'on se pose souvent en Javascript par rapprot au Java est : dans 
quel ordre sera exécuté mon code ? C'est simple : tout code qui n'est pas 
dans une fonction sera exécuté dans l'ordre d'apparition sur la page.

Et le code situé dans une fonction sera exécuté au moment où cette fonction sera
appelée, c'est-à-dire soit durant le chargement de la page ou bien après
déclenchement d'un évènement (clic de souris ou autre).

## Les variables prédéfinies

Il existe principalement 3 variables importantes en Javascript pour débuter :

- [window](https://developer.mozilla.org/fr/docs/Web/API/Window) : représente 
  la fenêtre du navigateur (présente côté front-end uniquement)
- [document](https://developer.mozilla.org/fr/docs/Web/API/Document) :
  représente le document HTML dans lequel s'exécute le script
- [console](https://developer.mozilla.org/fr/docs/Web/API/Console) : 
  représente la sortie console du script.

Chaque variable est d'un type bien précis, référez-vous à la référence sur le
*Mozilla Developer Network* pour en apprendre plus sur ces types de données, ça
ressemble à de la javadoc.

## Différences Java / JavaScript

Il faut savoir que la syntaxe du JavaScript est très similaire au Java. À tel
point qu'on peut les considérer identiques, à quelques diférences près que 
nous allons maintenant passer en revue.

### Opérateurs `==` et `===`

Les opérateurs sont quasiment tous identiques : somme, multiplication,
modulo...Etc. La principale différence réside dans l'opérateur de
comparaison `==`. En Java on utilise `==` pour comparer des valeurs primitives (
nombres ou booléens) et on utilise la méthode `Object.equals(Object)` pour
comparer 2 objets.

En Javascript l'opérateur `==` est **trèèèèès tolérant** (TROP). Vous aurez donc
des choses comme ceci :

```javascript
let a = 5;
let b = '5';
if (a == b) {
    console.log('a et b sont égaux');
} else {
    console.log('a et b sont différents');
}
```

> Résultat (oui oui !) :
> `a et b sont égaux`

Heureusement il existe un opérateur plus fiable qui est `===` et qu'il est
préférable d'utiliser à la place du `==`.

```javascript
let a = 5;
let b = '5';
if (a === b) {
    console.log('a et b sont égaux');
} else {
    console.log('a et b sont différents');
}
```

> Résultat :
> `a et b sont différents`

### Déclarer une variable

| Java                           | Javascript                                                                  |
|--------------------------------|-----------------------------------------------------------------------------|
| `int i = 2;`                   | <pre>let i = 2;</pre>                                                       |
| `String s = "Bonjour";`        | <pre>let s = "Bonjour";<br>let s = 'Bonjour';<br>let s = \`Bonjour\`;</pre> |
| `double d = 2.3612;`           | <pre>let d = 2.3612;</pre>                                                  |
| `boolean b = true;`            | <pre>let b = true;</pre>                                                    |
| `Date today = new Date();`     | <pre>let today = new Date();</pre>                                          |
| `int[] array = new int[]{1,2}` | <pre>let array = [1,2];</pre>                                               |

> Notez l'utilisation d'un mot-clé unique pour déclarer une variable : `let`.
> On ne déclare pas le type de la variable mais rappelez-vous qu'elle a quand-même
> un type implicite qui est déterminé par la valeur qu'on lui assigne.

### Chaînes de caractères

En Javascript il y a 3 types de caractères pour encadrer une chaîne de
caractères :
Le double-quote ("), le simple quote (') et le back tick (\`) :

```javascript
let myString1 = 'Value1'; // forme 1 (simple quote)
let myString2 = "Value2"; // forme 2 (double quote)
let myString3 = `Value3`; // forme 3 (back-tick, touches ALT-GR + 7 + SPACE)
```

Intérêt de la forme n°2 : elle permet d'écrire des chaînes contenant un simple
quote sans caractère d'échappement.

Intérêt de la forme n°3 : elle permet d'intégrer des variables dans la chaine
sous la forme `${nomDeVariable}`. Par exemple :

```javascript
let age = 42;
let happybirthday = `Happy Birthday! you are ${age} years old :)`;
console.info(happybirthday);
```

### Déclarer une fonction

Le gros problème en Javascript c'est qu'on ne peut pas déclarer le type de
retour d'une fonction. C'est pour cela qu'il est difficile de se renseigner sur
le résultat qui est retourné par une fonction.

Java :

```java
int somme(int a,int b){
    return a+b;
}

// Appel de la fonction :
int c=somme(40,5);
```

Javascript :

```javascript
function somme(a, b) {
    return a + b;
}

// Appel de la fonction
let c = somme(40, 5);
```

> Pour palier à ce manque dans Javascript, je vous conseille de toujours bien
> mettre une documentation JSDoc au-dessus de vos fonctions pour 
> préciser leur type de retour et le type de leurs paramètres. Ainsi que nommer vos
> variables en utilisant une convention explicite comme par exemple un "i" 
> devant le nom d'un nombre entier :

```javascript
/**
 * Calcule la somme de 2 variables.
 *
 * @param iOperande1 : int - Premier opérande
 * @param iOperande2 : int - Second opérande
 *
 * @return int - La somme de 'iOperande1' + 'iOperande2'.
 */
function somme(iOperande1, iOperande2) {
    return iOperande1 + iOperande2;
}
```

### Déclarer des objets personnalisés en JSON

En Javascript on peut écrire n'importe quelle structure de données grâce à une
syntaxe qui a donné son nom au format JSON. Cette notation est très simple :

```javascript
let john = {
    nom: ['John', 'Lennon'], // tableau
    age: 32,
    mail: 'john@legend.com',

    bonjour: function () {
        console.log(`Bonjour, je suis ${this.nom[0]} ${this.nom[1]}, j'ai ${this.age} ans`);
    }
};

// Appel de la méthode 'bonjour' sur l'objet 'john' :
john.bonjour();
```

> **Note :** on utilise aussi `this` pour désigner les variables de l'objet
> courant quand on écrit le code de cet objet.

### Quid des classes ?

Les classes sont possibles en JavaScript depuis peu de temps donc il n'est pas
forcément conseillé d'en écrire pour le moment tant que tous les navigateurs du
marché n'ont pas encore pris en charge ce concept correctement.

## Pour aller plus loin

Je vous recommande le [site de Pierre Giraud](https://www.pierre-giraud.com/javascript-apprendre-coder-cours/)
très complet pour apprendre la théorie JavaScript.

Pour commencer en douceur, faites le tutoriel *Getting Started* du *Mozilla 
Developer Network*
[en français](https://developer.mozilla.org/fr/docs/Learn/Getting_started_with_the_web/JavaScript_basics)
ou [en anglais](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/JavaScript_basics).