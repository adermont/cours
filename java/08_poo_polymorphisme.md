## Le polymorphisme

En POO, le polymorphisme est sans doute le principe le plus complexe à
appréhender parce qu'il fait appel à toutes les notions précédentes...
Nous ne verrons ce principe que de manière superficielle pour le moment.

- La plupart du temps, quand un objet de type `A` est attendu quelque part
(dans les paramètres d'une méthode ou comme type de variable locale),
alors tout objet de type `B` tel que `B` hérite de `A` sera autorisé.  
  
- Si une variable est déclarée avec une classe `A` mais qu'on instancie 
un objet de type `B` qui hérite de `A`, alors on pourra transtyper 
explicitement la variable en un type `B`.  
  
- Enfin, la méthode appelée sur un objet est choisie en fonction du type 
réel de l'objet et non pas de son type déclaré.  

Voici un exemple sur une hiérarchie simple : 

[![](https://mermaid.ink/img/pako:eNqlkT1PwzAQhv9KdBOFNIodN02sjl0YYEFiQFnc-FoiJXbl2BIl5L_jfICCUFm4wXd-39Mj-66DUksEDmUt2nZfiZMRTaECH4-uOaAJdh_rdXCvLJ7Q_Db22h1qnPTpHEFfPd2kDXFXKfssaoc3q9vA1wtHjpBvUy6Y_RI6v-IK9S_odeb0gX8jIYQGTSMq6Wc5wgqwr9hgAdyXEo_C1baAQg2twln9dFElcGschuDOUlicpw_8KOrWq2ehXrT-cQfewRvwLYlyShMa04zkMWGbEC7AKaFRyjK6TWOSJZuEsT6E95FAIpImJGWM5AkjzNshoKysNg_z-ofUfwIZzZzn?type=png)](https://mermaid.live/edit#pako:eNqlkT1PwzAQhv9KdBOFNIodN02sjl0YYEFiQFnc-FoiJXbl2BIl5L_jfICCUFm4wXd-39Mj-66DUksEDmUt2nZfiZMRTaECH4-uOaAJdh_rdXCvLJ7Q_Db22h1qnPTpHEFfPd2kDXFXKfssaoc3q9vA1wtHjpBvUy6Y_RI6v-IK9S_odeb0gX8jIYQGTSMq6Wc5wgqwr9hgAdyXEo_C1baAQg2twln9dFElcGschuDOUlicpw_8KOrWq2ehXrT-cQfewRvwLYlyShMa04zkMWGbEC7AKaFRyjK6TWOSJZuEsT6E95FAIpImJGWM5AkjzNshoKysNg_z-ofUfwIZzZzn)

```java
public static void main(String[] args)
{
    Number numInteger = Integer.MAX_VALUE;
    Number numDouble = Double.MAX_VALUE;

    // Le code exécuté ici sera celui de la classe Integer
    System.out.println(numInteger.intValue());
    System.out.println(numInteger.doubleValue());

    // Ici on exécute le code de la classe Double
    System.out.println(numDouble.intValue());
    System.out.println(numDouble.doubleValue());
}
```
