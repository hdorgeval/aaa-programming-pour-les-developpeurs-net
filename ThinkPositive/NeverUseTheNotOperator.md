# Ne jamais utiliser l’opérateur de négation ```!```

  
 L'opérateur de négation utilisé dans le langage .Net mais aussi dans le langage C et JavaScript est un point d'exclamation qui peut être utilisé de trois façons:
  
  ```Csharp
// A est une expression booléenne
if ( ! A )
{
  // la plupart du temps beaucoup de lignes de code
}

```

```Csharp
// A est un objet
if ( A != null )
{
  // la plupart du temps beaucoup de lignes de code
}

```

```Csharp
// A et B sont des objets du même type
if ( A != B )
{
  // la plupart du temps beaucoup de lignes de code
}

```

L'usage de la négation à l'aide d'un point d'exclamation provoque un ralentissement du cerveau parce qu'il rentre en conflit avec d'autres usages dans la vie de tous les jours.

En effet le point d'exclamation peut indiquer un danger comme le montre l'illustration ci-dessous:

![](Not2.jpg)

Le point d'exclamation peut indiquer un impératif quand il est utilisé en fin de phrase comme par exemple : 
> merci de respecter les délais!!!

Dans un cas comme dans l'autre, le cerveau cesse toutes ses activités pour analyser la situation actuelle et déterminer quelles seraient les conséquences de ne pas tenir compte du danger ou de l'ordre.

L'usage de la négation à l'aide d'un mot placé devant une affirmation n'existe pas dans le langage naturel. Par conséquent pour analyser le code:
 ```Csharp
if ( ! A )
{
  // la plupart du temps beaucoup de lignes de code
}

```

il faut réaliser les opérations suivantes:

* Ignorer dans un premier temps la présence du signe !
* Transformer l'expression A en une phrase
* Tourner cette phrase sous une forme négative
* Déterminer dans quelles circonstances cette forme négative est vrai

A compléter

