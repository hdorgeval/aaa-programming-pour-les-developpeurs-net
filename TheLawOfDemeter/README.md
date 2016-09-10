# La Loi de Déméter

Lorsqu'un objet contient une hiérarchie d'autres objets accessibles sous la forme de propriétés ou de méthodes, il arrive souvent que l'information dont on a besoin soit portée par un objet imbriqué dans cette hiérarchie comme le montre l'exemple ci-dessous:


```Csharp
var myObject = new MyClass();
var result = myObject.PropertyA.PropertyB.GiveMeTheObjectINeed(); 
```

Dans la classe ```MyClass```, la propriété ```PropertyA``` est définie de la manière suivante:

```Csharp
public class MyClass
{
    public A PropertyA { get; set; }
    // code omitted for brevity
}
```

Dans la classe ```A```, la propriété ```PropertyB``` est définie de la manière suivante:

```Csharp
public class A
{
    public B PropertyB { get; set; }
    // code omitted for brevity
}
```

Dans la classe ```B```, La méthode ```GiveMeTheObjectINeed``` est définie de la manière suivante:

```Csharp
public class B
{
    public C GiveMeTheObjectINeed()
    {
        return new C();
    }
    // code omitted for brevity
}
public class C
{
  // code omitted for brevity
}
```

Dans l'exemple ci-dessus, la hiérarchie d'objet est définie par l'ensemble des classes suivantes:

* MyClass
  * A
    * B

Obtenir un objet par une succession d'appels en utilisant la notation ```.```, comme dans l'exemple montré initialement:

```Csharp
var myObject = new MyClass();
var result = myObject.PropertyA.PropertyB.GiveMeTheObjectINeed(); 
```

est une technique courante chez la plupart des développeurs : pourquoi écrire plusieurs lignes de code quand on peut tout faire en une seule ligne?
Pour certains développeurs le but ultime serait de pouvoir écrire l'application entière en une seule ligne de code.

Le syndrome typique de cette approche (faire un maximum de choses en une seule ligne de code) se manifeste souvent au niveau de l'instruction ```return``` d'une méthode comme dans l'exemple suivant:

```Csharp
public C MyMethod()
{
    var myObject = new MyClass();
    return myObject.PropertyA.PropertyB.GiveMeTheObjectINeed();
} 
```

Ce type de code pose plusieurs problèmes:
* Vous introduisez un couplage fort entre votre classe et toutes les classes qui sont utilisées dans les appels successifs. Par exemple la méthode ci-dessus ```MyMethod``` introduit outre un couplage avec la classe MyClass, un couplage avec les classes ```A``` et ```B```;
* Vous supposez que tous les objets obtenus ainsi au fil des appels sont valides et non null;
* Vous pouvez faire, sans le savoir, de la fuite de mémoire ou de la fuite de handle si les objets intermédiaires ouvrent des ressources sur le système d'exploitation, ou si les objets intermédiaires instancient en interne un objet COM;
* Quand un problème survient à l'exécution et que vous mettez un point d'arrêt sur la ligne pour analyser l'origine du problème, il est souvent difficile de démêler la séquence des appels, obligeant ainsi a ré-écrire temporairement le code comme ci-dessous:
```Csharp
public C MyMethod()
{
    var myObject = new MyClass();
    var val1 = myObject.PropertyA;
    var val2 = val1.PropertyB;
    var result = val2.GiveMeTheObjectINeed();
    return result;
}
```

Pour éviter tous ces problèmes, vous devez appliquer la loi de Déméter.
L'objet de ce chapitre est de vous montrez comment appliquer la loi de Déméter.

