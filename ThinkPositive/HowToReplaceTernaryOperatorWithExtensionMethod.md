# Comment remplacer l'opérateur ternaire ? par une méthode d'extension

  
L'opérateur ternaire ```?``` permet de coder un ```if...else``` sur une seule ligne.

```Csharp
var result = (A) ? expression1 : expression2;
```

La ligne ci-dessus est équivalente au code ci-dessous:
```Csharp
if (A)
{
    result = expression1;
}
else
{
    result = expression2;
}
```

L'opérateur ternaire ```?``` est donc une manière élégante d'écrire un ```if...else```.

Cette élégance conduit inévitablement au syndrome connu qui consiste à tenter de coder un maximum de choses en une seule ligne comme le montre l'exemple ci-dessous:


```Csharp
string code = ... //product code;
string libelle = ... //product description;
string lib = (libelle != "" && !string.IsNullOrEmpty(libelle)) ? string.Concat(code, " - ", libelle) : code;
```

L’opérateur ternaire ```?``` est une manière déguisée de coder en pensée négative mais est aussi une des causes principales du fameux "pourquoi faire simple quand on peut faire compliquer".

Dans la section précédente je vous ai montré qu'il est très souvent possible de remplacer un ```if...else``` par une projection.

Cela est moins vrai concernant l'opérateur ternaire ```?```.

En effet, cet opérateur est souvent utilisé pour exprimer une exigence métier, une exigence technique (comme par exemple une règle d'affichage - qui est en réalité l'expression d'une exigence métier au niveau de l'interface graphique).

Pour factoriser ce type de code ou pour vous aider à ne plus utiliser cet opérateur, appuyez vous sur les règles suivantes:

>Substituez l'usage de l'opérateur ternaire ```?``` par une méthode d'extension.

> Sur une ligne de code ne faites qu'une seule chose à la fois.

Je vais vous montrer comment substituer l'opérateur ```?``` dans l'exemple ci-dessus.

Il faut dans un premier temps décrire sous la forme d'une phrase positive la ligne de code contenant l'opérateur ternaire. Cette phrase doit être la plus simple possible:

```
Quand le produit a une description
Le code de ce produit est concaténé avec un séparateur et la description.
```

Puis transformer cette phrase en du pseudo code, en supprimant tous les mots inutiles et en  concaténant ceux qui restent.
La phrase ci-dessus pourrait être alors transcrite de la manière suivante (pseudo-code):

```Csharp
string label = productCode;
if (Product.HasDescription)
{
  label = productCode.ConcatWithSeparatorAndValue(" - ", productDescription);
}
```

La méthode ```ConcatWithSeparatorAndValue()``` peut être développée sous la forme d'une méthode d'extension :

```Csharp
public static string ConcatWithSeparatorAndValue(this string input, string separator, string value)
{
    if (input == null)
    {
        return null;
    }

    if (value == null)
    {
        return input;
    }

    if (value == string.Empty)
    {
        return input;
    }

    if (separator == null)
    {
        return input.ConcatWithSeparatorAndValue(string.Empty, value);
    }
    
    var result = string.Format(@"{0}{1}{2}",input,separator,value);
    return result;

}
```

Grâce à cette méthode d'extension, le code initial :

```Csharp
string code = ... //product code;
string libelle = ... //product description;
string lib = (libelle != "" && !string.IsNullOrEmpty(libelle)) ? string.Concat(code, " - ", libelle) : code;
```

devient:

```Csharp
string code = ... //product code;
string libelle = ... //product description;
string lib = code.ConcatWithSeparatorAndValue(" - ",libelle);
```

La méthodologie exposée ci-dessus est itérative. Cette première itération a permis d'externaliser une exigence métier et a permis de rendre le code plus lisible.

A compléter