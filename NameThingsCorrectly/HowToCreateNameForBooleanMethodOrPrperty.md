## Comment nommer une méthode ou une propriété qui renvoie un booléen


Une méthode ou une propriété qui renvoie un booléen doit être nommée en utilisant l'une des quatre options ci-dessous:
* le préfixe :
  * *Is*; 
  * *Has*; 
  * *Can*.
* Un verbe à la troisième personne du singulier comme :
  * *Exists*;
  * *Allows*.
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

Il convient de coder toutes les méthodes publiques d’instance en utilisant la technique des méthodes d'extension. 

En effet, les méthodes d'extension permettent d'étendre le code d'une classe sans avoir accès au code source de cette classe. Il est donc possible d'enrichir n'importe quelle classe du Framework .Net avec ses propres méthodes. Par conséquent il est possible d’enrichir également ses propres classes sans avoir à modifier leur code source.

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

A compléter