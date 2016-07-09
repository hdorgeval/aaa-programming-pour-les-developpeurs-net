# Toujours penser positif

  Si un des facteurs clés pour délivrer rapidement une application est de coder en ayant à l'esprit de raconter une histoire et le chapitre précédent vous a donné les éléments de base pour créer des noms suffisamment expressifs pour rendre la lecture du code source similaire à la lecture d'une histoire, l'autre élément clé du succès est la pensée positive.
  
  En terme de programmation, la pensée négative se résume principalement sous la forme du pattern ci-dessous :
  
  ```Csharp
if ( une certaine condition n'est pas remplie )
{
  // la plupart du temps beaucoup de lignes de code
}
else {
  // la plupart du temps très peu de lignes de code
}
```

Ce pattern est tellement commun que la plupart des développeurs que j'ai pu rencontrer pensent qu'il s'agit d'un standard de programmation.

La pensée négative pose cependant deux problèmes:

>Le premier problème est que l'usage de ce pattern de la pensée négative est en contradiction avec une approche TDD (Test Driven Development) et/ou BDD (Behavior Driven Development) et de manière générale est en contradiction avec la façon de coder un test unitaire.

En effet pour tester le code suivant:

```Csharp
// A est une expression booléenne
if ( ! A )
{
  // la plupart du temps beaucoup de lignes de code
}

```

Il va falloir mettre en place autant de tests unitaires que de cas où l'expression A est fausse. Il est vraisemblable que ces cas forment un ensemble ouvert, c'est à dire un ensemble non exhaustif des cas possibles.

Le risque de tomber sur un cas imprévu quand l'application sera déployée en production devient alors extrêmement élevé.

Dans un contexte TDD ou BDD, la spécification associée à un test est exprimée grossièrement de la manière suivante : 

>Quand je suis dans la situation ```A```, je m'attends à avoir le résultat ```R```. 

C'est le principe de la spécification par l'exemple. 

L'écriture de la méthode ou de la propriété à tester d'après cette spécification se ferait ainsi en deux temps. Dans un premier temps la méthode ou la propriété contient une seule ligne de code:

```Csharp
throw new NotImplementedException();
```

Cette ligne de code garanti que le test unitaire va à l'échec lors de sa première exécution.

Dans un deuxième temps le contenu de la méthode ou de la propriété devient:

```Csharp
if ( A )
{
  // la plupart du temps peu de lignes de code
  return R
}

throw new NotImplementedException();
```

Vous pouvez ainsi constater que le code obtenu est la version positive du pattern évoqué en début de chapitre.

La pensée négative est donc en contradiction avec une approche TDD et/ou BDD, et de manière générale est en contradiction avec la façon de coder un test unitaire. 

>Le deuxième problème posé par la pensée négative est qu'elle réduit considérablement la productivité du développeur ainsi que la lisibilité et la compréhension du code ce qui affectera les délais de correction ou de mise à disposition de nouvelles fonctionnalités.

Je vous invite à analyser la méthode ci-dessous et à déterminer quel devrait être le nom réel de cette méthode:

```Csharp
public static bool F(this string path)
{
    if (path != null)
    {
        int num = path.Length;
        while (--num >= 0)
        {
            char c = path[num];
            if (c == '.')
            {
            return num != path.Length - 1;
            }
        }
    }
    return false;
}
```

Notez combien de temps il vous a fallu pour déterminer le nom exact de cette méthode.
Demandez aux développeurs de votre équipe d'analyser ce code et de trouver le meilleur nom pour cette méthode.
Notez le temps qu'ils ont mis pour accomplir cette tâche.

Déterminez ainsi le temps moyen mis pour analyser une seule ligne de code (en divisant la durée d'analyse par le nombre effectif de lignes de code - soit 7 dans l'exemple ci-dessus).

Voici un autre exemple de code qui est une variante de la pensée négative basée sur l'usage de l'opérateur ternaire ```?```:
```Csharp
public void ExportToCsv(bool isDetailedExport, bool isAnnualReport)
{
    var connection = new SqlConnection("...");
    var command = connection.CreateCommand();
    command.CommandType = System.Data.CommandType.StoredProcedure;
    command.CommandText = !isDetailedExport ? (!isAnnualReport ? "ps4" : "ps2"):(isAnnualReport?"ps3":"ps1");
    // code omitted for brevity
}
```

Pour ce type de code la démarche est la suivante: déterminez quelles sont les conditions pour que la procédure stockée appelée soit ```ps1```, mais surtout déterminez combien de temps il vous faut pour répondre de façon certaine à la question.

Demandez aux développeurs de votre équipe d'analyser ce code et de trouver la réponse à la question.
Notez le temps qu'ils ont mis pour accomplir cette tâche.

Déterminez ainsi le temps moyen mis pour analyser une seule ligne de code (en divisant la durée d'analyse par le nombre effectif de lignes de code - soit une seule ligne de code dans l'exemple ci-dessus).

Déterminez ensuite le nombre de lignes de code, dans l'application que vous développez, qui suivent le pattern de la pensée négative.
Imaginons par exemple que vous avez déterminé que le temps moyen pour analyser une ligne de code ( à partir des deux exemples ci-dessus) est de 4 secondes et qu'il y a 1000 lignes de code dans votre application qui suivent le pattern de la pensée négative:
chaque correction ou chaque évolution de l'application prendra vraisemblablement au moins une heure de plus (pour chaque développeur affecté à cette correction ou évolution) qu’initialement prévu au planning.

La pensée négative a donc un coût qu'il est possible de quantifier en utilisant la méthodologie exposée à partir des exemples ci-dessus.
La pensée négative, en fonction de la taille de l'application, en fonction du pourcentage de lignes de code écrites en pensée négative, en fonction du nombre de développeurs dans l’équipe, peut entraîner un surcoût pouvant aller de 10% à 100% du budget initialement prévu.

L'objectif de ce chapitre est de vous montrer les techniques de base qui vont vous permettre de toujours penser positif. 