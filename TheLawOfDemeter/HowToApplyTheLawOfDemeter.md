# Comment appliquer la loi de Demeter



Imaginez une facture fournisseur définie de la manière suivante:
```Csharp
public class Invoice
{
    public Currency Currency { get; set; }

    //code omitted for brevity
}
```