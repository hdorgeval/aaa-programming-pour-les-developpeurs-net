# Ne jamais utiliser l’opérateur de négation ```!```

  
 L'opérateur de négation utilisé dans le langage .Net mais aussi dans le langage C et JavaScript est un point d'exclamation qui peut être utilisé de trois façons différentes:
  
  ```Csharp
// A est une expression booléenne
if ( ! A )
{
  //la plupart du temps beaucoup de lignes de code
}

```

```Csharp
// A est un objet
if ( A != null )
{
  //la plupart du temps beaucoup de lignes de code
}

```

```Csharp
// A et B sont des objets du même type
if ( A != B )
{
  //la plupart du temps beaucoup de lignes de code
}

```

L'usage de la négation à l'aide d'un point d'exclamation provoque un ralentissement du cerveau pour deux raisons: 

>L'usage de la négation rentre en conflit avec d'autres usages dans la vie de tous les jours.

En effet le point d'exclamation peut indiquer un danger comme le montre l'illustration ci-dessous:

![](Not.jpg)

Le point d'exclamation peut indiquer un impératif quand il est utilisé en fin de phrase comme par exemple : 

> merci de respecter les délais!!!

Dans un cas comme dans l'autre, le cerveau cesse toutes ses activités pour analyser la situation actuelle et déterminer quelles seraient les conséquences de ne pas tenir compte du danger ou de l'ordre.


>L'usage de la négation à l'aide d'un signe placé devant une affirmation est sans équivalent dans le langage naturel. 

Par conséquent pour analyser le code:
 ```Csharp
if ( ! A )
{
  //la plupart du temps beaucoup de lignes de code
}

```

il faut réaliser les opérations suivantes:

* Ignorer dans un premier temps la présence du signe ```!```;
* Transformer l'expression A en une phrase (plus l'expression A est compliquée - présence multiple de  ```&& ``` et de  ```|| ``` - plus cette transformation est longue);
* Tourner cette phrase sous une forme négative;
* Déterminer dans quelles circonstances cette forme négative est vrai;
* Refaire au moins une fois toutes ces opérations pour vérifier qu'on ne s'est pas trompé.

L'usage de l’opérateur de négation ```!``` entraîne donc un arrêt brutal de la lecture du code environnant mais aussi un ralentissement significatif au moment de l'écriture du code.

Pour toutes ces raisons, il faut toujours éviter d'utiliser l'opérateur de négation ```!```

Je vais vous montrer qu'il est parfaitement possible de se passer totalement de cet opérateur.

Partons dans un premier temps du pattern de la pensée négative exposé en introduction de ce chapitre:

 ```Csharp
if ( ! A )
{
  B //la plupart du temps beaucoup de lignes de code
}
else {
  C //la plupart du temps très peu de lignes de code
}
```

Dans l'exemple ci-dessus ```A``` représente une expression booléenne, ```B``` le bloc de code à l'intérieur du ```If```, et ```C``` le bloc de code à l'intérieur du ```else```.
Supposons dans un premier temps qu'il n'y a pas de code ni avant le ```if``` ni après le ```else``` c'est à dire que le code ci-dessus est entièrement encapsulé dans une méthode ou une propriété.


Il est possible de réécrire ce code de la manière suivante:
 ```Csharp
if ( ! A )
{
  B //la plupart du temps beaucoup de lignes de code
}
if ( A ) 
{
  C //la plupart du temps très peu de lignes de code
}
```
Notez la disparation du ```else``` et notez qu'il y a maintenant deux if qui sont indépendants l'un de l'autre: il est donc possible d'inverser les deux ```if```.

 ```Csharp
if ( A ) 
{
  C //la plupart du temps très peu de lignes de code
}
if ( ! A )
{
  B //la plupart du temps beaucoup de lignes de code
}

```

Il est possible d'ajouter un ```return``` ( ou un ```return R``` si la méthode renvoie un résultat ou s'il s'agit d'une propriété) à la fin du bloc de code ```C```  sans que cela change quoi que ce soit à l'exécution:


 ```Csharp
if ( A ) 
{
  C //la plupart du temps très peu de lignes de code
  return;
}
if ( ! A )
{
  B //la plupart du temps beaucoup de lignes de code
}

```

Il est maintenant possible de se débarrasser de l'opérateur de négation:

 ```Csharp
if ( A ) 
{
  C //la plupart du temps très peu de lignes de code
  return;
}

B //la plupart du temps beaucoup de lignes de code

```

Pour transformer en version positive un code négatif, il suffit donc d'appliquer les deux règles suivantes:

>La dernière instruction d'un bloc de code ```If``` est toujours  ```return``` ou ```continue```

>Un ```If``` n'a jamais de ```else```

Si ces deux règles sont nécessaires elles ne sont pas suffisantes.

En effet, il reste à étudier le cas suivant:

 ```Csharp
A1
if ( ! A )
{
  B //la plupart du temps beaucoup de lignes de code
}
else {
  C //la plupart du temps très peu de lignes de code
}
A2
```

Dans l'exemple ci-dessus ```A``` représente une expression booléenne, ```B``` le bloc de code à l'intérieur du ```If```, ```C``` le bloc de code à l'intérieur du ```else```. ```A1``` représente toutes les lignes de code situées avant le ```if``` et ```A2``` toutes les lignes de code situées après le ```else```.

Le cas ci-dessus est équivalent à l'écriture suivante:

 ```Csharp
A1
if ( ! A )
{
  B //la plupart du temps beaucoup de lignes de code
  A2
}
else {
  C //la plupart du temps très peu de lignes de code
  A2
}
```

Il est maintenant possible d'appliquer la transformation que vous avez apprise:
 ```Csharp
A1
if ( ! A )
{
  B //la plupart du temps beaucoup de lignes de code
  A2
}
if ( A ) 
{
  C //la plupart du temps très peu de lignes de code
  A2
}
```

puis:

```Csharp
A1
if ( A ) 
{
  C //la plupart du temps très peu de lignes de code
  A2
}
if ( ! A )
{
  B //la plupart du temps beaucoup de lignes de code
  A2
}

```

puis:
```Csharp
A1
if ( A ) 
{
  C //la plupart du temps très peu de lignes de code
  A2
  return;
}
B //la plupart du temps beaucoup de lignes de code
A2
```

Vous pouvez remarquer que les lignes représentées par ```A2``` sont dupliquées à l'issue de la transformation positive.

Ainsi l'insertion d'un bloc ```if...else``` à l'intérieur d'un bloc de code est une façon déguisée de dupliquer tout le code situé après le ```else```. 

Le codage en pensée positive a donc l'avantage de mettre en évidence la duplication de code et permet donc de découvrir très rapidement quelle partie de code doit être factorisée sous la forme d'une méthode.

Cette fois-ci pour terminer cette transformation en pensée positive il a fallu ajouter la règle suivante:

>Toute ligne de code (ou ensemble de lignes) dupliquée doit être factorisée.

Le code ci-dessous est parfaitement conforme avec la pensée positive. Par contre il pose un problème dans la mesure où le deuxième if imbriqué ne se termine pas par un ```return```:

```Csharp
if ( A ) 
{
  if ( B )
  {
    C 
  }
  D 
  return;
}
```

Le code ci-dessous est équivalent au code suivant:

```Csharp
if ( A ) 
{
  if ( B )
  {
    C
    D
    return;
  }
  if ( ! B )
  {
    D 
    return;
  }
  return;
}
```

Vous pouvez remarquer qu'un ```if``` imbriqué est une façon déguisé de penser négatif et est aussi une façon déguisée de dupliquer du code (en effet toutes les lignes représentée par ```D``` sont dupliquées). 
Cependant il est possible de transformer le code ci-dessous en une version semi-positive:

```Csharp
if ( A && B )
{
  C
  D
  return;
}
if ( A && !B )
{
  D 
  return;
}
```

Pour effectuer cette transformation semi-positive il a fallu ajouter la règle suivante :

>Un ```if``` ne contient jamais de ```if``` imbriqué.

L'application de cette règle induit cependant une complexification des expressions : d'un ```if (A) {}``` et ```if (B) {}```, on est passé à un ```if (A && B) {}``` et ```if (A && !B) {}```.

En réalité, l'application des règles ci-dessus permet de mettre rapidement en évidence l'ensemble des contextes possibles lors de l'exécution du code. Le code ci-dessus pourrait être décrit par le pseudo-code suivant:


```Csharp
if ( contexte 1)
{
  C
  D
  return;
}

if (contexte 2 )
{
  D 
  return;
}
```

La façon de coder ce contexte peut être multiple.
je vais vous donner les clés pour réaliser au mieux cette opération.

A compléter

