# Comment coder une expression booléenne

  
 Votre code doit raconter une histoire; par conséquent toute expression booléenne telle que :
 
 ```Csharp
if ( A )
{
  //code omitted for brevity
}
```
 
 doit être écrite sous la forme d'une phrase positive.
 
 Par défaut, et dans la mesure du possible, vous devez toujours formuler de manière positive l'expression booléenne que vous êtes sur le point de coder. 
 
 Pour réaliser cela, substituer l'expression ```A``` par  une méthode d'extension définie sur le type d'objet qui vous semble le plus approprié.
  
 Cette méthode d'extension doit être nommée en utilisant l'une des trois options ci-dessous:
* le préfixe :
  * *Is*; 
  * *Has*; 
  * *Can*.
* Un verbe à la troisième personne du singulier comme :
  * *Exists*;
* Une séquence de mots qui représente une phrase en langage naturel dont on a supprimé les espaces entre les mots.
 
 Pour mettre en œuvre la méthodologie de création de nom d'une méthode ou d'une propriété qui renvoie un booléen reportez vous à la section correspondante : 
 
[Comment nommer une méthode ou une propriété qui renvoie un booléen](NameThingsCorrectly/HowToCreateNameForBooleanMethodOrPrperty.md)
 

Le code snippet ci-dessus peut donc être réécrit de la manière suivante:

```Csharp
var myObject = ... //code omitted for brevity
if ( myObject.IsXXX() )
{
  //code omitted for brevity
}
```

ou bien

```Csharp
var myObject = ... //code omitted for brevity
if ( myObject.HasXXX() )
{
  //code omitted for brevity
}
```

ou bien

```Csharp
var myObject = ... //code omitted for brevity
if ( myObject.CanXXX() )
{
  //code omitted for brevity
}
```

Notez que je commence toujours par coder l'usage de la méthode d'extension avant même de coder son implémentation.


Je laisse de côté pour l'instant le cas où l'expression booléenne est décrite sous la forme d'une phrase négative : ce cas sera étudié en détail dans la prochaine section.

A compléter