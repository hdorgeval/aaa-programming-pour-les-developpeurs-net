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

ou bien de la forme

```Csharp
//Arrange
var invoice = new Invoice();
invoice.Currency = new Currency() { IsoCode = "GBP", Description = "British Pound" };
```


Le code ci-dessus pose plusieurs problèmes:
* Le code de la partie Arrange du test unitaire forme un pattern qui est répété dans chaque test unitaire;

* Le code de la partie Arrange manque d'expressivité, c'est à dire qu'on ne comprend pas très bien pour quel usage sont crées ces objets;

* L'usage du mot clé ```new``` entraine un couplage fort entre la classe de test et toutes les classes qui consommeront les classes ```Invoice``` et ```Currency```. En particulier vous pouvez vous rendre compte que si les noms des propriétés ou si le contenu des propriétés de la classe ```Currency``` changent, cela va entraîner un refactoring important des classes clientes.

* Le test unitaire fait deux choses simultanément : il prend la responsabilité de créer correctement tous les objets nécessaires dans la partie ```Arrange``` et il prend la responsabilité de mener à bien le test dans la partie ```Act``` et ```Assert```. Si il s'agit d'instancier des objets non métiers , cela pose en général aucun problème, mais si il s'agit d'instancier des objets métiers il est vraisemblable que cela doit se faire en suivant des règles métiers prédéfinies qui peuvent changer à tout moment