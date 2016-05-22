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

Un code snippet est un mot clé qui permet d’insérer un bloc de code prédéfini. 
Pour mettre en action un code snippet, il suffit de cliquer à l'endroit où on souhaite ajouter le bloc de code prédéfini, de taper ensuite le mot clé associé au code snippet, comme par exemple *propfull*, puis de cliquer deux fois sur la touche TAB.

L'objectif du code snippet est de favoriser l'insertion rapide de code. Il s'agit donc d'un outil de productivité.
Il existe plein de code snippets disponibles pour le language CSharp. Pour découvrir les codes snippets disponibles dans Visual Studio, allez dans le menu *Tools* de Visual Studio puis sélectionnez l'option *Code Snippets Manager...* :

![](CodeSnippetManager.PNG)

A compléter.