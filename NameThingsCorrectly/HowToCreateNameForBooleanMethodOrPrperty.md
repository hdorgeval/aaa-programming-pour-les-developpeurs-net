## Comment nommer une méthode ou une propriété qui renvoie un booléen


Une méthode ou une propriété qui renvoie un boolean doit être nommée en utilisant l'une des trois options ci-dessous:
* le préfixe :
  * Is; 
  * Has; 
  * Can;
  * Should.
* Un verbe à la troisième personne du singulier comme :
  * Exists;
  * Allows.
* Une séquence de mots qui représente une phrase en langage naturel.

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
        /// 
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

