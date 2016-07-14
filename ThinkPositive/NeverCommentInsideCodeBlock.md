# Ne jamais commenter à l'intérieur d'un bloc de code

  
 Très souvent il m'arrive de vouloir commenter le bloc de code que je suis en train de mettre en place.
 Très souvent le commentaire est là pour permettre à soi même ou aux autres développeur de l'équipe de bien comprendre ce qui se passe.
 
 Documenter unitairement une ou plusieurs lignes de code à l'intérieur d'une méthode ou d'une propriété revient à décrire ce que fait le code de façon à masquer la complexité de l'écriture du code ou de l'algorithmique.
 
 Ce type de commentaire est une autre façon de penser négatif non pas vis à vis de son propre code mais vis à vis des autres développeurs qui seront amenés à le modifier dans l'avenir.
 
 Le message implicite est le suivant : comme il y a de forte chance que vous ne compreniez pas le code que j'ai écris je vais vous faire gagner du temps en vous expliquant ce qu'il fait.
 
 Le commentaire masque la complexité du code associé mais surtout masque très souvent le fait que ce code implémente une règle métier ou une algorithmique spécifique empêchant ainsi d'externaliser cette règle ou cet algorithme dans une autre partie du code ou dans une autre couche, empêchant ainsi toute forme de maintenance, de factorisation ou d'évolution du code associé.
 
 Autrement dit, un commentaire est le révélateur d'un morceau de code qui n'est pas à sa place et qui sera difficilement maintenable.
 
 L'usage des commentaires à l'intérieur d'un bloc de code pose aussi les problèmes suivants:
 
 * Ces commentaires sont perdus à la compilation;
 * Ces commentaires sont souvent assez courts pour ne pas gêner la lecture du code environnant;
 * Ces commentaires échappent à tout système de génération automatique de la documentation du logiciel tel que SandCastle.
 
 Si vous êtes amené à documenter du code à l'intérieur d'une méthode ou d'une propriété, considérez le fait de remplacer ce code par une méthode d'extension ayant un nom suffisamment évocateur et de déplacer votre commentaire dans la documentation XML associée à la méthode d'extension.

 
 En procédant de la sorte, vous rendez votre code plus lisible, plus maintenable mais surtout vos commentaires sont conservés à la compilation et seront affichés dynamiquement par l'IntelliSense quand un développeur utilisateur votre méthode d'extension. 
 
 
 
 ```Csharp
if ( A )
{
  //code omitted for brevity
}
```