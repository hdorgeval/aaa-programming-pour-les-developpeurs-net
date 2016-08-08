# Synthèse des règles spécifiques au AAA Programming



Ce chapitre regroupe l'ensemble des règles spécifiques au AAA Programming. 

Je vous invite à les mettre en pratique. Commencez par la règle qui vous semble la plus facile à appliquer, ou bien la plus appropriée dans votre contexte. Dans tous les cas de figure vous allez vous rendre compte qu'appliquer ces règles va automatiquement enclencher une série de questions et d'échanges avec les autres développeurs. De ces questions et de ces échanges sortira une meilleure architecture, une meilleure implémentation, une meilleure cohésion d'équipe.

|Règle n° 1 |
| -- |
|La convention de nom Camel Casing doit être utilisée pour nommer les éléments suivants:<ul><li>Variable locale;</li> <li>Paramètre de méthode.</li></ul>|
| |

|Règle n° 2 |
| -- |
|La convention de nom Pascal Casing doit être utilisée pour nommer les éléments suivants:<ul><li>Classe;</li><li>Énumération;</li><li>Valeur d'une énumération;</li><li>Événement;</li><li>Membre public static et read-only;</li><li>Méthode;</li><li>Propriété;</li><li>Namespace;</li><li>Interface.</li></ul>|
| |


|Règle n° 3 |
| -- |
|Le nom d'une variable locale associée à une propriété est constitué d'un préfixe, le caractère _, suivi d'un nom conforme à la convention Camel Casing. |
| |

|Règle n° 4 |
| -- |
|Toute variable doit être déclarée au plus près de son utilisation. |
| |


|Règle n° 5 |
| -- |
|Toute variable associée à une propriété doit être utilisée exclusivement au sein du getter ou du setter de cette propriété.|
| |

|Règle n° 6 |
| -- |
|Ne jamais utiliser l’opérateur de négation ```!```  |
|= pensez toujours positif. |

|Règle n° 7 |
| -- |
|Un ```if``` ne contient jamais de ```if``` imbriqué. |
| |

|Règle n° 8 |
| -- |
|Toute ligne de code (ou ensemble de lignes) dupliquée doit être factorisée. |
| |

|Règle n° 9 |
| -- |
|La dernière instruction d'un bloc de code ```If``` est toujours  ```return``` ou ```continue``` |
| |

|Règle n° 10 |
| -- |
|Un ```If``` n'a jamais de ```else``` |
| |

|Règle n° 11 |
| -- |
|Quand vous commencer à coder un ```If```, utilisez toujours le code snippet associé en tapant ```if``` puis ```TAB``` deux fois. |
|Remarque : cette astuce vous rappelle qu'il faut toujours penser positif. |

|Règle n° 12 |
| -- |
|Dans un commentaire XML, la balise ```<returns>...</returns>``` commence toujours par ```Returns true if ...``` ou ```Returns true when ...``` |
| |

|Règle n° 13 |
| -- |
|Quand vous développez une méthode, vous devez en sortir le plus vite possible. Autrement dit si vous pouvez déterminer un cas de figure qui permet de faire immédiatement un ```return``` écrivez d'abord ce cas. |
| |

|Règle n° 14 |
| -- |
|La dernière instruction d'une méthode booléenne est toujours: ```return false;``` |
| |

|Règle n° 15 |
| -- |
|Le bloc de code qui précède la dernière ligne de code d'une méthode booléenne est toujours de la forme: <div><span class="hljs-keyword">if</span> ( A )<div>{</div><div><span class="hljs-comment" style="padding-left:15px;">//code omitted for brevity</span></div><div><span class="hljs-keyword" style="padding-left:15px;">return</span> <span class="hljs-keyword">true</span>;</div><div>}</div>|
| |


|Règle n° 16 |
| -- |
|Si vous êtes amené à documenter du code à l'intérieur d'une méthode ou d'une propriété, considérez le fait de remplacer ce code par une méthode d'extension ayant un nom suffisamment évocateur et de déplacer votre commentaire dans la [documentation XML](https://msdn.microsoft.com/en-us/library/b2s063f7.aspx) associée à la méthode d'extension.|
| |

|Règle n° 17 |
| -- |
|Quand vous développez une boucle ```for``` ou ```foreach```, vous devez en sortir le plus vite possible. Autrement dit si vous pouvez déterminer un cas de figure qui permet de passer immédiatement à l'itération suivante ,écrivez d'abord ce cas. Si vous pouvez déterminer un cas de figure qui permet de sortir de la boucle, écrivez d'abord ce cas.|
| |

|Règle n° 18 |
| -- |
|Une boucle while est toujours de la forme: <div><span class="hljs-keyword">while</span> ( true )<div>{</div><div><span class="hljs-comment" style="padding-left:15px;">//code omitted for brevity</span></div><div>}</div>|
| |

|Règle n° 19 |
| -- |
|Chaque fois que vous vous apprêtez à écrire un ```new``` dans votre code, posez vous la question : comment pourrais-je faire pour ne pas faire de ```new``` à cet endroit?|
| |



A compléter