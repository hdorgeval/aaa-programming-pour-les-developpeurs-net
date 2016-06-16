## Comment nommer une méthode ou une propriété qui renvoie un booléen


Une méthode ou une propriété qui renvoie un booléen doit être nommée en utilisant l'une des quatre options ci-dessous:
* le préfixe :
  * *Is*; 
  * *Has*; 
  * *Can*.
* Un verbe à la troisième personne du singulier comme :
  * *Exists*;
* Une séquence de mots qui représente une phrase en langage naturel dont on a supprimé les espaces entre les mots.
* *ToBooleanOrDefault()* dans le cas d'une méthode qui projette un objet vers un booléen.

Voici ci-après quelques exemples d'application.

#### Propriété automatique
```Csharp
public class Myclass
{
    ...
    public bool IsValid { get; set; }
    ...
}
```

#### Propriété avec membre privé associé
```Csharp
#region IsReadOnly

        private bool _isReadOnly = false;
        /// <summary>
        /// ...
        /// </summary>
        public bool IsReadOnly
        {
            get
            {
                return this._isReadOnly;
            }
            set
            {
                this._isReadOnly = value;
            }
        }

#endregion
```


#### Méthode d'instance développée sous la forme d'une méthode d'extension
```Csharp
public static class MyclassExtenions
{
    public static bool IsEqualTo(this Myclass input, Myclass value)
    {
        //code omitted for brevity
    }   
}

public class Myclass
{
  //code omitted for brevity
}


```
Plutôt que de développer les méthodes publiques d'instance sous la forme:
```Csharp
public class Myclass
{
  public bool IsEqualTo(Myclass value)
  {
      //code omitted for brevity
  }
}
```

Il est plus intéressant de coder toutes les méthodes publiques d’instance en utilisant la technique des méthodes d'extension. 

En effet, les méthodes d'extension permettent d'étendre le code d'une classe sans avoir accès au code source de cette classe. Il est donc possible d'enrichir n'importe quelle classe du Framework .Net avec ses propres méthodes. Par conséquent il est également possible d’enrichir ses propres classes sans avoir à modifier leur code source.

La méthode *ToBooleanOrDefault()* décrite ci-dessous permet par exemple d'étendre la classe System.String en lui ajoutant la méthode *ToBooleanOrDefault()*, d'où le terme méthode d’extension. L'extension se fait en effet sous la forme d'une méthode et non d'une propriété.

L'avantage apporté par la méthode d’extension vient du fait que : 
* il est parfaitement valide d'invoquer cette méthode sur un objet nul : le traitement du cas nul peut ainsi être complètement encapsulé à l'intérieur de la méthode d'extension;
* La classe qui est étendue contient principalement des propriétés qui décrivent l'état de l’objet; Ce type de classe peut ainsi être utilisée pour transférer un objet d'une couche à une autre de l'application (de la couche business à la couche de présentation, ou bien de la couche data à la couche business). Ce type d'objet est appelé un DTO object (Data Transfer Object);
* Les méthodes d'extension décrivent séparément toutes les actions qu'il est possible de réaliser sur un objet issu de cette classe;
* Une méthode d'extension est testable unitairement.


#### Projection développée sous la forme d'une méthode d'extension
```Csharp
public static class StringExtensions
{
    /// <summary>
    /// Try to convert input string into a boolean.
    /// </summary>
    /// <param name="input">String to be converted.</param>
    /// <returns>
    /// Returns true when input string has one of the value "1", "ok", "OK", "Ok", "True";
    /// Returns false for all other cases (like null, string.empty,"0", "Ko", etc ...).
    /// </returns>
    public static bool ToBooleanOrDefault(this string input)
    {
        //code omitted for brevity
    }
}


```

#### Séquence de mots qui représente une phrase

Pour déterminer le nom d’une méthode sous la forme d’une séquence de mots qui représente une phrase, commencez par créer un projet de test.

Ce projet de test va vous permettre d'utiliser en situation réelle le nom que vous allez choisir. Il va vous permettre de vérifier que le nom choisi est suffisamment intuitif et que le code induit est suffisamment expressif.

Le projet de test que vous avez crée contient une méthode de test par défaut :

```Csharp
using System;
using Microsoft.VisualStudio.TestTools.UnitTesting;

namespace UnitTestProject1
{
    [TestClass]
    public class UnitTest1
    {
        [TestMethod]
        public void TestMethod1()
        {
        }
    }
}
```

L'écriture du code dans une méthode de test se fait en trois phases nommées *Arrange*, *Act*, *Assert*. 

Mettez en évidence ces trois phases de la façon suivante à l'intérieure de la méthode de test:

```Csharp
[TestMethod]
public void TestMethod1()
{
    //Arrange

    //Act

    //Assert
}
```

La phase *Arrange* est la phase dans laquelle vous allez préparer tous les objets nécessaires pour exécuter votre future méthode.

La phase *Act* est la phase pendant laquelle vous allez exécuter votre méthode et en récupérer le résultat.

La phase *Assert* est la phase pendant laquelle vous allez comparer le résultat obtenu dans la phase *Act* avec le résultat attendu; en cas de différence vous signalez l'échec du test.

En appliquant ces principes pour créer un test de la méthode d'extension *ToBooleanOrDefault()* décrite ci-dessus, vous devriez obtenir un code de test semblable au code ci-dessous:

```Csharp
[TestMethod]
public void TestMethod1()
{
    //Arrange
    var input = "1";

    //Act
    var result = input.ToBooleanOrDefault();

    //Assert
    var expected = true;
    if (result != expected)
    {
        Assert.Fail();
    }
}
```

Pour créer le premier test unitaire de votre future méthode, il faut mettre en œuvre les étapes ci-dessous dans l'ordre indiqué: 
1. Décrire brièvement ce que doit faire cette méthode sous la forme d'une seule phrase la plus synthétique possible; cette phrase doit être si possible en anglais;
2. Transformer cette phrase en une ligne de code (typiquement la ligne de code que vous seriez amené à écrire dans la partie *ACT* du test unitaire) en supprimant les mots inutiles et en concaténant les mots restants pour former un nom conforme à la convention Pascal Casing;
3. Définir le nom obtenu sous la forme d'une méthode d'extension à l'extérieur du projet de test (c'est à dire dans le projet de votre application);
4. Commenter la méthode sous la forme de [commentaires XML](https://msdn.microsoft.com/en-us/library/b2s063f7.aspx);
5. Écrire les spécifications de cette nouvelle méthode sous la forme d'exemples en commençant par les cas les plus simples;
6. Prendre le premier exemple de la spécification pour écrire la partie *Arrange* du premier test unitaire;
7. Mettre en place le code d'exécution de la nouvelle méthode dans la partie *Act* de la méthode de test en vérifiant que :
  * l'IntelliSense ramène bien le commentaire XML
  * Le commentaire affiché est cohérent avec le nom choisi
  * L'IntelliSense permet de découvrir et de manipuler rapidement cette nouvelle méthode
8. Valider le résultat dans la partie *Assert* de la méthode de test;
9. Vérifier que le test échoue;
10. Montrer l'intégralité de ce premier test unitaire aux autres membres de l' équipe pour vérifier qu'ils comprennent le code;
11. Vérifier que le nom choisi fait l'unanimité au sein de l'équipe.


Je vous propose d'appliquer ces 11 étapes pour développer une méthode qui consiste à déterminer si une chaîne de caractères est présente dans un tableau de chaînes de caractères.

#### Etape 1 : Décrire brièvement ce que doit faire la méthode

Vous pouvez construire cette phrase en la structurant de la manière suivante:

>L'objectif est de ... (verbe à l'infinitif) ... (sur ce quoi porte l'action définie par le verbe précédent) est dans une situation donnée (description de la situation) ou possède un attribut spécifique (description de l'attribut); 

Dans le cas d'une projection d'un objet vers un booléen, la phrase est structurée de la manière suivante:
>L'objectif est de ... (verbe à l'infinitif) ... (sur ce quoi porte l'action définie par le verbe précédent) en (résultat de la projection) ou bien de récupérer ... (valeur par défaut) en cas d'impossibilité.

Par exemple:
* L'objectif est de déterminer que le mot saisi par l'utilisateur est présent dans un tableau de valeurs prédéfinies.

* L'objectif est de convertir le texte présent dans une cellule d'un tableau en un booléen ou bien de récupérer la valeur *false* en cas d'échec de la conversion. 

Écrivez ensuite la phrase en anglais. Les deux exemples ci-dessus pourraient ainsi être traduits de la manière suivante:

* Checks if input string is present in a given array of values.

* Convert input string into a boolean or get false value when conversion fails.


#### Etape 2 : Transformer cette description en une ligne de code

Cette transformation peut se faire en plusieurs étapes.

Partez d'abord de l'étape précédente comme par exemple:
>Checks if input string is present in a given array of values.

Supprimez ensuite les espaces inutiles, concaténez les mots entre eux en respectant la convention PasCal Casing pour le nom de la méthode et la convention Camel Casing pour le nom des paramètres, séparez le sujet et le verbe par un point:
>Checks if inputString.IsPresentIn(givenArrayOfValues)

Supprimez tous les mots qui vous semblent inutiles pour obtenir une écriture la plus ramassée possible:
>input.IsIn(values)

Vérifiez qu'en préfixant le résultat obtenu par *var result =*, vous pouvez former une ligne de code valide pour la partie *ACT* de votre premier test unitaire:

```Csharp
//ACT
var result = input.IsIn(values);
```

Vérifiez ensuite qu'en situation réelle d'usage de la méthode, vous êtes capable de reformuler à l'identique la description de départ:

```Csharp
if (input.IsIn(values) )
{
    //Ce code est exécuté si le texte saisi par l'utilisateur est présent dans une liste de valeurs prédéfinies.
}
```

Vous allez certainement constater un écart entre la description de départ et la description reconstruite d'après la simple lecture du code.

Dans l'exemple ci-dessus la phrase reconstruite laisse penser que le paramètre *values* représente une liste de valeurs (```List<string>```) et non pas un tableau de valeurs (```string[]```).

Constater un écart signifie que l'usage de cette future méthode va poser un problème tôt ou tard soit pour vous même soit pour les autres développeurs de votre équipe, soit pour les personnes qui seront en charge de la maintenance future de l'application.

Même si cet écart vous paraît insignifiant ou négligeable, il est nécessaire de le réduire au maximum, car il introduit un risque majeur en terme de coûts quand il s'agira de faire évoluer l'application conformément aux attentes du marché ou du métier.

Pour réduire cet écart, demandez aux membres de l'équipe d'écrire ce qu'ils comprennent de votre code :

```Csharp
if (input.IsIn(values) )
{
    //Ce code est exécuté si <merci de compléter>
}
```

De cette demande d'avis va naître un échange qui vous permettra de trouver le nom de la méthode et en définir un usage qui fera l'unanimité.

A compléter