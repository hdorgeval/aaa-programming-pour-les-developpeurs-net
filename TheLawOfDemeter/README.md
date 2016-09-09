# La Loi de Déméter

Lorsqu'un objet contient une hiérarchie d'autres objets accessibles sous la forme de propriétés, il arrive souvent que l'information dont on a besoin soit portée par un objet imbriqué dans cette hiérarchie comme le montre l'exemple ci-dessous:




```Csharp
var myObject = new MyClass();
var value = myObject.GiveMeTheValueINeed(); 
```
Le code ci-dessus ne compile pas parce que cette méthode n'existe pas directement sur la classe ```MyClass```


Par contre le code code ci-dessous compile
L'usage de cet opérateur paraît anodin tant il est la base de la programmation orientée objet.