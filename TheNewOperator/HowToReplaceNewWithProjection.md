# Comment remplacer l'opérateur new : propriété statique et chaînage de méthode



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


Le code ci-dessus pose plusieurs problèmes:
* Le code de la partie ```Arrange``` du test unitaire forme un pattern qui est répété dans chaque test;

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

>Tout duplication d'un pattern d'écriture de code doit être factorisé.

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

Grâce à cette première factorisation le code de test peut maintenir s'écrire:
```Csharp
//Arrange
var invoice = new Invoice();
invoice.Currency = Currency.Euro;

//Act
...

//Assert
...
```

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
 
 Dans cette deuxième étape de factorisation, j'ai introduit un pattern de codage dans la classe ```Invoice``` entre les propriétés ```EmptyInvoiceInEuro``` et ```EmptyInvoiceInBritishPound```. Ce pattern pourrait se nommer EmptyInvoiceInCurrencyX où X est le code ISO code de la devise.
 
 
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

Grâce à cette troisième factorisation le code du deuxième test peut maintenir s'écrire:
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
 
 
 La classe ```Currency``` contient maintenant un pattern d'écriture de code qui est le suivant:
 ```Csharp

var result = new Currency()
{
    IsoCode = "Euro",
    Description = "Euro"
};
return result;
```


 ```Csharp

var result = new Currency()
{
    IsoCode = "GBP",
    Description = "British Pound"
};
return result;
       

```
 
 Ce pattern consiste à créer un objet à partir de deux autres objets : le code ISO de la devise et sa description. 
 
 Une première solution possible est de définir un constructeur paramétré dans la classe ```Currency```. Dans ce cas la classe ```Currency``` pourrait être factorisée de la manière suivante:
 
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

Si la méthode d’instanciation d'un objet de type ```Currency``` doit être modifiée pour répondre à une évolution de l'application, il faudra alors réécrire toutes les méthodes qui font appel au constructeur paramétré.

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

Dans la classe ```Currency``` , l'usage de l'opérateur ```new``` a été centralisé dans une méthode statique dont le nom comme par le terme ```From```. 

Ce terme indique la création d'un objet de type ```Currency``` à partir d'un ou de plusieurs autres objets. 

La technique consistant à déclarer dans la méthode ```From...``` un paramètre optionnel dont le nom commence par le terme ```with``` ou bien le terme ```and``` est empruntée de la méthodologie de nommage des méthodes et paramètres préconisée par Apple. 
Cette méthodologie rend le code encore plus expressif.

 A compléter.