# La Loi de Déméter

Lorsqu'un objet contient une hiérarchie d'autres objets accessibles sous la forme de propriétés ou de méthodes, il arrive souvent que l'information dont on a besoin soit portée par un objet imbriqué dans cette hiérarchie comme le montre l'exemple ci-dessous:


```Csharp
var myObject = new MyClass();
var result = myObject.PropertyA.PropertyB.GiveMeTheObjectINeed(); 
```

La propriété ```PropertyA``` est définie de la manière suivante:

```Csharp
public class MyClass
{
    public A PropertyA { get; set; }
    // code omitted for brevity
}
```

La propriété ```PropertyB``` est définie de la manière suivante:

```Csharp
public class A
{
    public B PropertyB { get; set; }
    // code omitted for brevity
}
```

La méthode ```GiveMeTheObjectINeed``` est définie de la manière suivante:

```Csharp
 public class C
{
  // code omitted for brevity
}
public class B
{
    public C GiveMeTheObjectINeed()
    {
        return new C();
    }
    // code omitted for brevity
}
```

Dans l'exemple ci-dessus, la hiérarchie d'objet est définie par l'ensemble des classes suivantes:

* MyClass
  * A
    * B


Le code ci-dessus ne compile pas parce que cette méthode n'existe pas directement sur la classe ```MyClass```


Par contre le code code ci-dessous compile
L'usage de cet opérateur paraît anodin tant il est la base de la programmation orientée objet.