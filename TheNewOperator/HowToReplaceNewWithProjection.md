# Comment remplacer l'opérateur new par une propriété statique



Imaginez une facture fournisseur définie de la manière suivante:

```Csharp
public class Currency
{
    public string IsoCode { get; set; }
    public string Description { get; set; }
    
    //code omitted for brevity
}

public class Invoice
{
    public Currency Currency { get; set; }

    //code omitted for brevity
}
```


Si vous êtes dans une approche TDD, chaque test unitaire que vous allez écrire sera de la forme:

```Csharp
//Arrange
var invoice = new Invoice();
invoice.Currency = new Currency() { IsoCode = "EUR", Description = "Euro" };
```

ou bien de la forme:

```Csharp
//Arrange
var invoice = new Invoice();
invoice.Currency = new Currency() { IsoCode = "GBP", Description = "British Pound" };
```


Le code ci-dessus pose plusieurs problèmes:
* Le code de la partie Arrange du test unitaire forme un pattern qui est répété dans chaque test unitaire;

* Le code de la partie ```Arrange``` manque d'expressivité, c'est à dire qu'on ne comprend pas très bien pour quel usage sont crées ces objets;

* L'usage du mot clé ```new``` entraîne un couplage fort entre la classe de test et et les classes ```Invoice``` et ```Currency```. En particulier vous pouvez vous rendre compte que si les noms des propriétés ou si le contenu des propriétés de la classe ```Currency``` changent, cela va entraîner un refactoring important des classes clientes;

* Le test unitaire fait deux choses simultanément : 
  * il prend la responsabilité de créer correctement tous les objets nécessaires dans la partie ```Arrange``` ;
  * et il prend la responsabilité de mener à bien le test dans la partie ```Act``` et ```Assert```. 
  
  S'il s'agit d'instancier des objets non métiers , cela pose en général aucun problème, mais s'il s'agit d'instancier des objets métiers il est vraisemblable que cela doive se faire en suivant des règles métiers prédéfinies mais susceptibles de changer à tout moment.
  
  
  L'usage de l'opérateur ```new``` entraîne donc les effets suivants:
  * Duplication de code;
  * Manque d'expressivité du code;
  * Fragilisation du code parce qu'il prend des responsabilités (celles de créer correctement des objets qui sont le plus souvent des objets métiers) qui ne sont pas de son ressort.


Pour vous aider à utiliser le moins souvent possible l'opérateur ```new```, vous pouvez vous appuyer sur les règles suivantes:

>Tout duplication d'un pattern d'écriture de code doit être factorisé

>Ne prenez jamais la responsabilité de construire par vous même un objet métier

>Ne faites qu'une seule chose à la fois dans votre code mais faites le bien





  