### Cas particulier des variables qui sont associées à une propriété

Les membres privés d'une classe sont par définition des variables locales à la classe où ils sont définis.

Le nom d'un membre privé doit par conséquent être conforme à la convention de nom Camel Casing.

Quand vous insérez une propriété dans une classe en utilisant le code snippet nommé *propfull*, vous obtenez le résultat suivant:

```Csharp
private int myVar;
public int MyProperty
{
    get { return myVar; }
    set { myVar = value; }
}
```


A compléter.