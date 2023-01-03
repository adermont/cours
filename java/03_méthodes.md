# Java : les méthodes

## Préambule

- Pour éviter de devoir réécrire du code qu'on utilise souvent, on le factorise dans 
des fonctions. Et en Java, on parle plutôt de **méthodes** que de fonctions. 

- Une méthode doit toujours être déclarée à l'intérieur d'une classe. 

- Pour nommer une méthode, il existe une convention appelée **notation hongroise** :
première lettre en minuscules et ensuite on débute chaque mot par une majuscule.

```java
class <NomDeVotreClasse> {

	// Le code entre crochets est optionnel (dépend du type de la méthode)

	<visibilité> <type de retour> <nomDeLaMéthode>(<arguments>) {
	
		[return <résultat>;]
		
	} // <--------------------------------------- Fin de la méthode
	
} // <------------------------------------------- Fin de la classe
```

Exemples :

	int calculerLaSommeDeDeuxNombres(int nompbre1, int nombre2) {
		return nombre1 + nombre2;
	}
	
	void methodeSansRetour(){
		// Cette méthode ne retourne pas de valeur
	}

## Visibilité d'une méthode

La **visibilité** d'une méthode détermine les endroits à partir desquels vous pourrez l'appeler.

Il existe 4 types de visibilité : 

|Visibilité                   | Effet                                          |
|-----------------------------|------------------------------------------------|
|private                      | Visible seulement à l'intérieur de la classe.|
|protected                    | Visible dans la classe, ses sous-classes et le package.
|public                       | Visible depuis n'importe quelle classe.
|*default* (pas de mot-clé)   | Visible seulement par les classes du package mais pas les classes qui héritent.



### La méthode main()

En Java, pour exécuter un programme il faut ce qu'on nomme un **point d'entrée**.
La machine virtuelle va toujours chercher à exécuter le code qui se trouve dans 
la méthode "main()".

La méthode main() se déclare comme suit :

	public static void main(String[] args){
		// Votre programme ici
	}

Quelques éléments importants de cette méthode :

- Elle doit être déclarée avec le mot-clé "static"
- Son type de retour est obligatoirement "void"
- Elle prend 1 seul argument : un tableau de chaines de caractères `String[]`
