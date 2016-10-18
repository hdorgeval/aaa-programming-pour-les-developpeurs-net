# Comment appliquer la loi de Déméter

Ce que dit la loi de Déméter est très simple : soyez toujours courtois avec vos interlocuteurs. Si vous avez besoin d'une information ou d'une action qui ne peut être fournie que par une connaissance directe ou indirecte de votre interlocuteur, demander à ce dernier de jouer les intermédiaires; ne court-circuitez jamais votre interlocuteur en communiquant directement avec ses relations.

Autrement dit, la loi de Déméter consiste à ne parler qu'avec ses voisins directs.

Chaque fois que vous écrivez du code qui consiste à chaîner des appels sur des objets différents via leurs propriétés ou leur méthodes en formant une séquence similaire à l'exemple ci-dessous:

```Csharp
var myObject = new MyClass();
var result = myObject.PropertyA.PropertyB.GiveMeTheObjectINeed(); 
```
cherchez à appliquer la loi de Déméter.

En choisissant de ne pas appliquer la loi de Déméter, vous diminuez la maintenabilité de votre application car toute modification d'un objet intermédiaire aura un impact sur votre code. De plus vous introduisez un couplage entre votre application et les classes sous-jacentes appelées au travers du chaînage des appels. Il est fort probable que ce couplage n'est jamais été prévu au départ de la conception de ces classes.

Pour appliquer la loi de Déméter, vous devez "remonter" le dernier appel directement sur le premier objet utilisé dans la chaîne des appels.
Ainsi l’exemple de code ci-dessus doit être écrit de la manière suivante:

```Csharp
var myObject = new MyClass();
var result = myObject.GiveMeTheObjectINeed(); 
```

Bien évidemment cette méthode ou cette propriété n'est pas disponible car sinon vous l'auriez utilisée.
En utilisant le principe des méthodes d'extension, vous pouvez créer cette méthode directement dans votre code:
