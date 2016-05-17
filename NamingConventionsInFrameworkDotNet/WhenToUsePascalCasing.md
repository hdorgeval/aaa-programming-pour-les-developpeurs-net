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
  
  #### Exemple 2
```Csharp
public class BasePage : System.Web.UI.Page
{
  ...
}
```
  La classe BasePage a été définie dans un projet Web ASP.NET WebForm.
  
  Ce nom est conforme à la convention de nom Pascal Casing.
  Il est aussi suffisamment évocateur pour qu'on comprenne que la classe BasePage sera utilisée comme classe de base pour toutes les nouvelles pages qui seront définies dans le projet Web.
  
  Cependant, ce nom pose problème pour deux raisons :
  * la classe System.Web.UI.Page est elle même la classe de base par défaut pour toutes les pages Web d'un projet Web ASP.NET web form.
  Le nom choisi, BasePage, semble plus générique que Page, ce qui est contradictoire avec la notion d'héritage.
  
  En effet, l'héritage permet de spécialiser de plus en plus une classe, par conséquent d'un point de vue sémantique on s'attend plutôt à avoir ce type de déclaration:
  
  ```Csharp
public class Page : BasePage
{
  ...
}
```
  
  Voici quelques exemples de classes du Framework .Net qui illustrent la relation qui existe entre une classe nommée Xyz et la classe nommée XyzBase:
  
 ```Csharp
public class Attachment : AttachmentBase
{
  ...
}
```
```Csharp
public class ColorAnimation : ColorAnimationBase
{
  ...
}
```
```Csharp
public class Setter : SetterBase, ISupportInitialize
{
  ...
}
```
```Csharp
public class Button : ButtonBase
{
  ...
}
```
  
  * Le nom BasePage diffère de la convention communément établie au sein du Framework .Net, à savoir que le mot Base doit être le dernier mot à être concaténé, comme l'illustre les quelques classes ci-dessous du Framework .Net:
    * System.Collections.DictionaryBase
    * System.Configuration.Settingsbase
    * System.Web.HttpContextBase
    * System.Web.HttpResponseBase
    * System.Windows.Controls.Primitives.ButtonBase
  
  
 > A mes yeux, le nom BasePage est un nom de classe suffisamment évocateur. Cependant ce nom aurait pu être parfaitement correct si :
   > * sa sémantique avait été conforme à son usage (car si vous demandez à un développeur du Framework .Net de classer BasePage par rapport à Page, il vous dira tout de suite: Page hérite de BasePage) 
   > * La façon de concaténer les mots avait été conforme à une concaténation similaire au sein du Framework .Net



 
 A compléter