# Comment remplacer l'opérateur new : propriété statique, méthode statique et chaînage de méthode



Imaginez une facture fournisseur définie de la manière suivante:
```Csharp
public class Invoice
{
    public Currency Currency { get; set; }

    //code omitted for brevity
}
```
La classe ```Invoice``` contient une propriété ```Currency``` dont le type est défini ci-dessous:

```Csharp
public class Currency
{
    public string IsoCode { get; set; }
    public string Description { get; set; }
    
    //code omitted for brevity
}
```

Si vous êtes dans une approche TDD, chaque test unitaire que vous allez écrire pour tester la classe ```Invoice``` sera de la forme:

```Csharp
//Arrange
var invoice = new Invoice();
invoice.Currency = new Currency() { IsoCode = "EUR", Description = "Euro" };

//Act
...

//Assert
...
```

ou bien de la forme:

```Csharp
//Arrange
var invoice = new Invoice();
invoice.Currency = new Currency() { IsoCode = "GBP", Description = "British Pound" };

//Act
...

//Assert
...
```
Ce code de test pose plusieurs problèmes:
* Le code de la partie ```Arrange``` forme un pattern qui est répété dans chaque test;

* Le code de la partie ```Arrange``` manque d'expressivité, c'est à dire qu'on ne comprend pas très bien pour quel usage sont crées ces objets;

* L'usage du mot clé ```new``` entraîne un couplage fort entre la classe de test et les classes ```Invoice``` et ```Currency```. En particulier vous pouvez vous rendre compte que si les noms des propriétés ou si le contenu des propriétés de la classe ```Currency``` changent, cela va entraîner un refactoring des classes clientes et notamment des classes de test;

* Le test unitaire fait deux choses simultanément : 
  * il prend la responsabilité de créer correctement tous les objets nécessaires dans la partie ```Arrange```;
  * et il prend la responsabilité de mener à bien le test dans la partie ```Act``` et ```Assert```. 
  
  S'il s'agit d'instancier des objets non métiers , cela pose en général aucun problème, mais s'il s'agit d'instancier des objets métiers il est vraisemblable que cela doive se faire en suivant des règles métiers prédéfinies mais susceptibles de changer à tout moment.
  
  L'usage de l'opérateur ```new``` entraîne donc les effets suivants:
  * Duplication de code;
  * Manque d'expressivité du code;
  * Fragilisation du code parce qu'il prend des responsabilités (celles de créer correctement des objets qui sont le plus souvent des objets métiers) qui ne sont pas de son ressort.


Pour vous aider à utiliser le moins souvent possible l'opérateur ```new```, vous pouvez vous appuyer sur les règles suivantes:

>Toute duplication d'un pattern d'écriture de code doit être factorisé.

>Ne prenez jamais la responsabilité de construire par vous même un objet métier.

>Ne faites qu'une seule chose à la fois dans votre code mais faites le bien.

Je vais vous montrer comment utiliser ces principes pour factoriser le code de test ci-dessus.

La classe ```Currency``` peut être modifiée de la façon suivante:
```Csharp
public class Currency
{
    public string IsoCode { get; set; }
    public string Description { get; set; }

    public static Currency Euro
    {
        get
        {
            var result = new Currency()
            {
                IsoCode = "Euro",
                Description = "Euro"
            };
            return result;
        }
    }

    public static Currency BritishPound
    {
        get
        {
            var result = new Currency()
            {
                IsoCode = "GBP",
                Description = "British Pound"
            };
            return result;
        }
    }
    //code omitted for brevity
}

```

Grâce à cette première factorisation le premier test unitaire peut maintenir s'écrire:
```Csharp
//Arrange
var invoice = new Invoice();
invoice.Currency = Currency.Euro;

//Act
...

//Assert
...
```

Et le deuxième test unitaire peut s'écrire:
```Csharp
//Arrange
var invoice = new Invoice();
invoice.Currency = Currency.BritishPound;

//Act
...

//Assert
...
```
Vous voyez que cette première factorisation a permis : 
* de passer de 2 ```new``` à un seul ```new``` pour chaque test unitaire;
* de déléguer la responsabilité de remplir correctement les propriétés ```IsoCode``` et ```Description``` à la classe même où sont définies ces propriétés.


Dans une deuxième étape de factorisation la classe ```Invoice``` peut être modifiée de la façon suivante:
```Csharp
public class Invoice
{
    public Currency Currency { get; set; }

    public static Invoice EmptyInvoiceInEuro
    {
        get
        {
            var result = new Invoice()
            {
                Currency = Currency.Euro
            };
            return result;
        }
    }
    
    public static Invoice EmptyInvoiceInBritishPound
    {
        get
        {
            var result = new Invoice()
            {
                Currency = Currency.BritishPound
            };
            return result;
        }
    }

    //code omitted for brevity
}

```

Grâce à cette deuxième factorisation le code du premier test peut maintenir s'écrire:
```Csharp
//Arrange
var invoice = Invoice.EmptyInvoiceInEuro;

//Act
...

//Assert
...
```

Grâce à cette deuxième factorisation le code du deuxième test peut maintenir s'écrire:
```Csharp
//Arrange
var invoice = Invoice.EmptyInvoiceInBritishPound;

//Act
...

//Assert
...
```
 
 Cette deuxième étape de factorisation a permis:
 * d'éliminer l'usage de l'opérateur ```new``` : l'action de créer correctement un objet est maintenant totalement déléguée à la classe où est défini cet objet.
 
Cependant cette deuxième factorisation a introduit un pattern de codage dans la classe ```Invoice``` entre les propriétés ```EmptyInvoiceInEuro``` et ```EmptyInvoiceInBritishPound```. Ce pattern pourrait se nommer ```EmptyInvoiceInCurrencyX``` où X est le code ISO code de la devise. 

Si l'application qui gère les factures ne gère que deux devises, cela ne pose aucun problème. Par contre si l'application est réellement multi-devises, l'implémentation des différentes devises, au sein de la classe ```Invoice``` se fera par copier/coller d'une propriété existante. 
 
Il est donc nécessaire de réaliser une troisième étape de factorisation pour éliminer ce pattern.
Pour cela il existe une méthode de codage qui est très courante en JavaScript et qui s'appelle le chaînage de méthode (Fluent API en anglais).
 
 En appliquant cette méthode dite de chaînage, la classe ```Invoice``` peut être modifiée de la façon suivante:
```Csharp
public class Invoice
{
    public Currency Currency { get; set; }

    public static Invoice Empty
    {
        get
        {
            var result = new Invoice();
            //application des règles métiers 
            //pour l'initialisation d'une nouvelle facture
            return result;
        }
    }

    //code omitted for brevity
}

public static class InvoiceExtensions
{
    public static Invoice SetCurrencyTo(this Invoice input, Currency  value)
    {
        if (input == null)
        {
            return input;
        }

        var oldValue = input.Currency;
        input.Currency = value;

        //application des règles métiers quand la devise change
        
        return input;
    }
}

``` 
 
Grâce à cette troisième factorisation le code du premier test peut maintenir s'écrire:
```Csharp
//Arrange
var invoice = Invoice.Empty
                     .SetCurrencyTo(Currency.Euro);

//Act
...

//Assert
...
```

Et le code du deuxième test peut maintenir s'écrire:
```Csharp
//Arrange
var invoice = Invoice.Empty
                     .SetCurrencyTo(Currency.BritishPound);

//Act
...

//Assert
...
```
 
 Grâce à cette technique de chaînage de méthode, le code de la classe ```Invoice``` a été allégé et toutes les méthodes de chaînage sont externalisées sous la forme de méthodes d'extension.
 
 Notez également qu'une méthode de chaînage renvoie toujours le même objet (et doit toujours renvoyer le même objet) si bien que le chaînage des appels se passe correctement y compris quand l'objet de départ est nul.
 
 Cette technique de chaînage des méthodes a aussi renforcé l'expressivité du code.
 En effet, si on extrait de son contexte la ligne de code suivante:
 
 ```Csharp
var invoice = Invoice.Empty
                     .SetCurrencyTo(Currency.BritishPound);

```
 On comprend parfaitement que le code réalise en séquence les étapes suivantes:
 * création d'une nouvelle facture;
 * affection de la devise GBP à cette facture.
 
 
 La classe ```Currency``` contient maintenant un pattern d'écriture de code, situé à l'intérieur de chacune des propriétés statiques ```Euro``` et ```BritishPound```. Ce pattern est le suivant:
 ```Csharp
var result = new Currency()
{
    IsoCode = "X",
    Description = "Y"
};
return result;
```
 
 Ce pattern consiste à créer un objet à partir de deux autres objets : le code ISO de la devise et sa description. 
 
 Ce pattern d'écriture sera dupliqué à chaque définition d'une nouvelle devise. Il faut donc factoriser cette répétition qui n'est pas la répétition d'un ensemble de lignes de code mais qui est la répétition d'un pattern d'écriture de code.
 
 Une première solution possible est de définir un constructeur paramétré dans la classe ```Currency```. Dans ce cas, la classe ```Currency``` pourrait être factorisée de la manière suivante:
 
 ```Csharp
public class Currency
{
    public string IsoCode { get; set; }
    public string Description { get; set; }

    public Currency(string isocCode, string description)
    {
        this.IsoCode = IsoCode;
        this.Description = description;
    }

    public static Currency Euro
    {
        get
        {
            var result = new Currency("Euro", "Euro");
            return result;
        }
    }

    public static Currency BritishPound
    {
        get
        {
            var result = new Currency("GBP", "British Pound");
            return result;
        }
    }

}
```
 
 Dans le code ci-dessus, il reste toujours un pattern d'écriture de code qui est le suivant:
 ```Csharp
var result = new Currency("XXX", "YYY");
return result;
```

Si la méthode d'instanciation d'un objet de type ```Currency``` doit être modifiée pour répondre à une évolution de l'application, il faudra alors réécrire toutes les méthodes qui font appel au constructeur paramétré.

L'utilisation de l'opérateur ```new``` doit être centralisée au sein d'une seule et unique méthode dans la classe correspondante. Cette méthode peut être codée de la manière suivante:

 ```Csharp
public class Currency
{
    public string IsoCode { get; set; }
    public string Description { get; set; }

    public static Currency FromIsoCode(string isoCode, string withDescription = null)
    {
        var result = new Currency();
        result.IsoCode = isoCode;
        result.Description = isoCode;
        
        if (withDescription == null)
        {
            return result;
        }

        result.Description = withDescription;
        return result;

    }

    public static Currency Euro
    {
        get
        {
            var result = Currency.FromIsoCode("Euro");
            return result;
        }
    }

    public static Currency BritishPound
    {
        get
        {
            var result = Currency.FromIsoCode("GBP", withDescription: "British Pound");
            return result;
        }
    }

}
```

Dans la classe ```Currency``` , l'usage de l'opérateur ```new``` est maintenant centralisé dans une méthode statique dont le nom commence par le terme ```From```. 

Ce terme indique la création d'un objet de type ```Currency``` à partir d'un ou de plusieurs autres objets. 

La technique consistant à déclarer dans la méthode ```FromXXX``` un paramètre optionnel dont le nom commence par le terme ```with``` ou bien le terme ```and``` est empruntée à la méthodologie de nommage des méthodes et paramètres préconisée par Apple. 
Cette méthodologie rend le code encore plus expressif.

 Si un test unitaire souhaite créer une devise "bidon" pour vérifier son impact dans d'autres parties de l'application, il pourra s'écrire de la façon suivante:
 
 ```Csharp
//Arrange
var deviseBidon = Currency.FromIsoCode("IGA", withDescription: "Inter Galactique");

//Act
...

//Assert
...
```

Toutes les factorisations effectuées ci-dessus ont permis de centraliser la création des instances en un seul endroit pour chacune des classes ```Currency``` et ```Invoice```. Les clients de ces classes et notamment l'ensemble des tests unitaires associés n'ont plus besoin de prendre la responsabilité de créer par eux-même des instances valides du point de vue métier. 

Vous pouvez constater que l'usage de l'opérateur ```new``` a également disparu dans toutes les classes clientes. 

Vous pouvez aussi constater que la factorisation progressive du mot clé ```new``` a rendu le code plus expressif en utilisant les techniques suivantes:
* Propriété statique typiquement nommée ```Empty```;
* Chaînage de méthode (la base des APIs dites Fluent - technique principalement empruntée à JavaScript);
* Méthode statique typiquement nommée ```FromXXX``` ;
* Paramètres optionnels dont le nom est typiquement préfixé par ```with``` ou ```and``` (technique empruntée à Apple).

