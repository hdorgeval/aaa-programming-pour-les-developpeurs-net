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
  La classe *BasePage* a été définie dans un projet Web ASP.NET WebForm.
  
  Ce nom est conforme à la convention de nom Pascal Casing.
  Il est aussi suffisamment évocateur pour qu'on comprenne que la classe *BasePage* sera utilisée comme classe de base pour toutes les nouvelles pages qui seront définies dans le projet Web.
  
  Cependant, ce nom pose problème pour deux raisons :
  * la classe *System.Web.UI.Page* est elle même la classe de base par défaut pour toutes les pages Web d'un projet Web ASP.NET Web Form.
  Le nom choisi, *BasePage*, semble plus générique que *Page*, ce qui est contradictoire avec la notion d'héritage.
  
  En effet, l'héritage permet de spécialiser de plus en plus une classe, par conséquent d'un point de vue sémantique on s'attend plutôt à avoir ce type de déclaration:
  
  ```Csharp
public class Page : BasePage
{
  ...
}
```
  
  Voici quelques exemples de classes du Framework .Net qui illustrent la relation qui existe entre une classe nommée *Xyz* et la classe nommée *XyzBase*:
  
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
  
  * Le nom *BasePage* diffère de la convention communément établie au sein du Framework .Net, à savoir que le mot *Base* doit être le dernier mot à être concaténé, comme l'illustre les quelques classes ci-dessous du Framework .Net:
    * System.Collections.DictionaryBase
    * System.Configuration.Settingsbase
    * System.Web.HttpContextBase
    * System.Web.HttpResponseBase
    * System.Windows.Controls.Primitives.ButtonBase
  
  
 > A mes yeux, le nom *BasePage* est un nom de classe suffisamment évocateur. Cependant ce nom aurait pu être parfaitement correct si :
   > * Sa sémantique avait été conforme à son usage (car si vous demandez à un développeur du Framework .Net de classer *BasePage* par rapport à Page, il vous dira tout de suite: *Page* hérite de *BasePage*); 
   > * La façon de concaténer les mots avait été conforme à une concaténation similaire au sein du Framework .Net.
   > 
   > Pour que le nom soit correct il faudrait le remplacer par un nom comme *MyAppPageBase* où *MyApp* serait le nom interne de votre application.

Autrement dit quand vous donnez un nom à une classe, une propriété ou une méthode, cherchez à savoir si il existe des noms similaires dans le Framework .Net et comparez toujours avec ce qui existe dans le Framework .Net pour déterminer la pertinence de votre choix. 

[IlSpy](https://github.com/icsharpcode/ILSpy) est un outil qui peut vous aider dans cette démarche d'analyse.
 
 Quand vous estimez que le nom choisi rempli tous les critères à savoir:
 * Le nom est expressif
 * Le nom est conforme à ce qui existe déjà dans le Framework .Net

validez toujours votre choix de la façon suivante:
 * Obtenez le consensus au sein de l'équipe;
 * Appliquer la méthode TDD (Test Development Driven) à votre nouvelle classe, méthode ou propriété pour vérifier que le code est facile à écrire, facile à comprendre, facile à modifier avec le nom que vous avez choisi.
 
 Si vous rencontrez la moindre difficulté pour obtenir le consensus ou pour écrire simplement des test unitaires, je vous recommande fortement de changer de nom.
 
   Si a la troisième itération, le nom choisi cause toujours des difficultés, il convient de s'arrêter et de réfléchir, avec l'ensemble de l'équipe, à la pertinence du ou des choix techniques qui ont amené à la création de la classe, de la méthode ou de la propriété en question.
 
 