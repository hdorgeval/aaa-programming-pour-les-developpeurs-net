# Comment coder négativement une expression booléenne

  
 Il existe des cas où le fait de penser négatif permet de faire immédiatement un ```return``` dans l'implémentation d'une méthode ou d'une propriété.
 
 Votre code doit raconter une histoire; par conséquent toute expression booléenne telle que :
 
 ```Csharp
if ( ! A )
{
  //code omitted for brevity
}
```
 
 doit être écrite sous la forme d'une phrase négative. 
 
 Pour réaliser cela, substituer l'expression ```! A``` par  une méthode d'extension définie sur le type d'objet qui vous semble le plus approprié.
  
 Cette méthode d'extension doit être nommée en utilisant l'une des trois options ci-dessous:
* avoir le préfixe :
  * *IsNot*; 
  * *HasNo*; 
  * *Cannot*.
* Être Un verbe à la troisième personne du singulier comme :
  * *DoesNotExist*;
* Être Une séquence de mots qui représente une phrase négative en langage naturel dont on a supprimé les espaces entre les mots.
 
Pour mettre en œuvre la méthodologie de création de nom d'une méthode ou d'une propriété qui renvoie un booléen reportez vous à la section correspondante : [Comment nommer une méthode ou une propriété qui renvoie un booléen](NameThingsCorrectly/HowToCreateNameForBooleanMethodOrPrperty.md).
 

Le code snippet ci-dessus peut donc être réécrit de la manière suivante:

```Csharp
var myObject = ... //code omitted for brevity
if ( myObject.IsNotXXX() )
{
  //code omitted for brevity
}
```

ou bien

```Csharp
var myObject = ... //code omitted for brevity
if ( myObject.HasNoXXX() )
{
  //code omitted for brevity
}
```

ou bien

```Csharp
var myObject = ... //code omitted for brevity
if ( myObject.CannotXXX() )
{
  //code omitted for brevity
}
```

ou bien

```Csharp
var myObject = ... //code omitted for brevity
if ( myObject.DoesNotExist() )
{
  //code omitted for brevity
}
```

La mise en œuvre de cette méthode d'extension se fait en trois étapes:
1. Implémentation de la version positive de la méthode;
2. Mise en œuvre des tests unitaires sur la version positive uniquement;
3. Définition de la version négative sous la forme montrée dans les exemples ci-dessous:

```Csharp
public static bool IsIn(this string input, string[] values)
{
    //code omitted for brevity
}

public static bool IsNotIn(this string input, string[] values)
{
    return input.IsIn(values) == false;
}
```

```Csharp
public static bool HasXXX(this MyClass input)
{
  //code omitted for brevity
}

public static bool HasNoXXX(this MyClass input)
{
    return input.HasXXX() == false;
}
```

Remarquez que la version négative est toujours codée en s'appuyant sur la forme positive :
```Csharp
return <expresion positive> == false;
```

Remarquez aussi que la version négative est codée sans utiliser l'opérateur de négation ```!```.

En résumé il est possible de ne jamais coder explicitement la forme négative d'une expression.

Mais surtout gardez à l'esprit la règle suivante:

>Ne jamais tester unitairement la version négative d'une méthode 
