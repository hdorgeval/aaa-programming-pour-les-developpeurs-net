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