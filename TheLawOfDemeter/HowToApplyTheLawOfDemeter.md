# Comment appliquer la loi de Déméter

Ce que dit la loi de Déméter est très simple : soyez toujours courtois avec vos interlocuteurs. Si vous avez besoin d'une information ou d'une action qui ne peut être fournie que par une connaissance directe ou indirecte de votre interlocuteur, demander à ce dernier de le faire pour vous; ne le court-circuiter pas en communiquant directement


```Csharp
var myObject = new MyClass();
var result = myObject.PropertyA.PropertyB.GiveMeTheObjectINeed(); 
```



Imaginez une facture fournisseur définie de la manière suivante:
```Csharp
public class Invoice
{
    public Currency Currency { get; set; }

    //code omitted for brevity
}
```