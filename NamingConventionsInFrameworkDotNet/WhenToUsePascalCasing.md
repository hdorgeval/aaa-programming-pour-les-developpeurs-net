### Quand utiliser Pascal Casing


La convention de nom Pascal Casing doit être utilisée pour nommer les éléments suivants:
* Une classe;
* Une énumération;
* La valeur d'une énumération;
* Un événement;
* Un membre public static et read-only;
* Une méthode;
* Une propriété;
* Un namespace;
* Une interface.

>L'interface est un cas particulier dans la mesure où, par convention, le nom doit être préfixé par la lettre **I** comme c'est le cas pour les interfaces disponibles dans le Framework .Net comme par exemple:
* IEnumerable;
* IQueryable;
* IDisposable.

Je vous propose, ci-dessous, d'étudier quelques exemples d'application de la convention de nom Pascal Casing.
L'objectif de ces exemples est de vous amenez à découvrir comment déterminer si un nom est correct.  

#### Exemple 1
```Csharp
public class Class1
{
}
```
 Par défaut Visual Studio applique automatiquement la convention de nom Pascal Casing quand vous ajoutez un nouveau fichier de classe dans votre projet.
 *Class1* est conforme à la convention Pascal Casing : il s'agit d'un nom constitué d'un seul mot et la première lettre de ce mot est en majuscule.
 Il est donc parfaitement valide de conserver ce nom, mais en général vous, comme moi, changez *Class1* en un nom plus explicite. Conserver le nom par défaut donné par Visual Studio aurait pour résultat d'obfusquer votre code.
 
 >A mes yeux, le nom *Class1*, bien que conforme à la convention de nom Pascal Casing, ne véhicule rien de spécifique quant à l'usage ou l'objectif de cette classe. *Class1* est un nom qui manque d'expressivité, il contribue à rendre plus difficile l'usage et la compréhension de cette classe pour un développeur externe qui serait amené à co-développer votre projet. 
  
  A compléter