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

En effet, cet opérateur est souvent utilisé pour exprimer une règle métier, une règle technique (comme par exemple une règle d'affichage - qui est en réalité l'expression d'une règle métier au niveau de l'interface graphique).



