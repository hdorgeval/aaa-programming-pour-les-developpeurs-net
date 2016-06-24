# Règle 2 : Toujours penser positif

  Si un des facteurs clés pour délivrer rapidement une application est de coder en ayant à l'esprit de raconter une histoire et le chapitre précédent vous a donné les éléments de base pour créer des noms suffisamment expressifs pour rendre la lecture du code source similaire à la lecture d'une histoire, l'autre élément clé du succès est la pensée positive.
  
  Le pattern de la pensée négative se résume principalement sous la forme du pseudo code ci-dessous :
  
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

Le premier problème est que l'usage de ce pattern de la pensée négative est en contradiction avec une approche TDD (Test Driven Development) et/ou BDD (Behavior Driven Development) et de manière générale est en contradiction avec la façon de coder un test unitaire.

En effet la structure d'un code unitaire est en principe la suivante:



A Compléter