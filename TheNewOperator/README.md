# L'opérateur new

Pour créer un objet il suffit de créer une instance de la classe voulue en utilisant l'opérateur ```new``` comme dans l'exemple ci-dessous:

```Csharp
var myObject = new MyClass();
```

L'usage de cet opérateur paraît anodin tant il est la base de la programmation orientée objet.

Cependant chaque fois que vous faîtes un ```new```, vous rendez votre code moins maintenable, moins évolutif et moins testable.

Chaque fois que vous vous apprêtez à écrire un ```new``` dans votre code, posez vous la question : comment pourrais-je faire pour ne pas faire de ```new``` à cet endroit?

L'objet de ce chapitre est de vous montrer comment faire pour utiliser le moins possible, l'opérateur ```new```.

