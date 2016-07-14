# Synthèse des règles spécifiques au AAAProgramming



Ce chapitre regroupe l'ensemble des règles qui ont été expliquées et démontrées dans cet ouvrage.

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
|Ne jamais utiliser l’opérateur de négation ```!``` = pensez toujours positif. |
| |

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


A compléter