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

Naviguez dans les dossiers proposés et découvrez les code snippets fournis par Microsoft.

La propriété fournie par le code snippet *propfull* déclare une variable locale à la classe et une propriété dont le getter et le setter s’appuient sur cette variable locale.

Le nom de la variable locale, *myVar*, est conforme à la convention de nom Camel Casing.
Le nom de la propriété, *MyProperty*, est conforme à la convention de nom Pascal Casing.

Le nom myVar pose cependant un problème. En effet le nom myVar est très éloigné sémantiquement du nom MyProperty laissant ainsi penser que l'un peut être modifié indépendamment de l'autre. 
Un autre développeur, qui serait amené à modifier ou à faire évoluer votre code, pourrait parfaitement modifier la variable myVar au lieu de la propriété MyProperty (et vice versa) entraînant ainsi un comportement erroné de l'objet modifié. Cela peut avoir pour conséquence un dysfonctionnement de l'interface graphique de l'application notamment quand les objets doivent être observables comme par exemple dans une application WPF.

Pour résoudre ce problème une première approche consiste à réécrire la propriété ci-dessus de la façon suivante:

```Csharp
private int myProperty;
public int MyProperty
{
    get { return myProperty; }
    set { myProperty = value; }
}
```

Le nom de la variable et le nom de la propriété sont identiques d'un point de vues sémantique puisqu'ils ne diffèrent que la par la casse de la première lettre.

Cependant cela accroît le risque d'utiliser dans d'autre partie du code la variable au lieu de la propriété (et vice versa). En effet l'IntelliSense propose maintenant les choix suivants quand vous commencez à taper le nom de la propriété:
![](MyProperty.PNG)

L'intelliSense étant un outil de productivité, il est vraisemblable que vous choisissiez, sans même vous en apercevoir, la variable locale en lieu et place de la propriété.
C'est ce que j'appelle le bug de productivité : vous introduisez un bug dans votre application parce que vous avez choisi trop rapidement l'option proposée par l'IntelliSense.

Comment résoudre ce problème posé par l'usage intensif de l'IntelliSense?

Il suffit de réécrire la propriété ci-dessus de la façon suivante:

```Csharp
private int _myProperty;
public int MyProperty
{
    get { return _myProperty; }
    set { _myProperty = value; }
}
```
En ajoutant simplement le caractère _ devant le nom de la variable locale, l'Intellisense apporte les deux avantages suivants:
* Quand vous commencez à taper le nom de la propriété, l'Intellisense masque l'accès à la variable locale:

  ![](MyProperty2.PNG)

* Quand vous commencez à taper le caractère _, l'Intellisense vous donne accès uniquement aux variables locales qui sont associées à des propriétés:

  ![](MyProperty3.PNG)