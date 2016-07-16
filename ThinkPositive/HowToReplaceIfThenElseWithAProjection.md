# Comment remplacer un IF...ELSE par une projection

  
Beaucoup de constructions ```if...else``` sont en réalité des projections et peuvent être substituées en développant une méthode d'extension nommée ```ToXXX()``` sur l'objet concerné par cette projection.

Voici un premier exemple tiré d'une couche d'accès au données:

 ```Csharp
var input = "test";
if (input != null)
{
    command.Parameters.Add(new SqlParameter("@UserLogin", input));
}
else
{
    command.Parameters.Add(new SqlParameter("@UserLogin", System.DBNull.Value));
}
```

L'exemple ci-dessus consiste en réalité à projeter un objet de type ```string``` soit vers lui-même soit vers la constante ```System.DBNull.Value```.

Si vous êtes amené à développer une couche d'accès aux données en vous appuyant sur ADO.NET, vous serez amené  à répéter très souvent ce pattern.

L'exemple ci-dessus peut être factorisé de la façon suivante:

```Csharp
var input = "test";
command.Parameters.Add(new SqlParameter("@UserLogin", input.ToStringOrDBNull() ));
```

```ToStringOrDBNull()``` est une méthode d'extension qui pourrait être définie de la manière suivante:

```Csharp
public static object ToStringOrDBNull(this string input)
{
    if (input == null)
    {
        return System.DBNull.Value;
    }
    return input;
}
```

Voici un autre exemple similaire au précédent:


 ```Csharp
int? input = 10;
if (input != null && input.HasValue)
{
    command.Parameters.Add(new SqlParameter("@Quantity", input.Value));
}
else
{
    command.Parameters.Add(new SqlParameter("@Quantity", System.DBNull.Value));
}
```

cet exemple peut être refactorisé de la manière suivante:
```Csharp
int? input = 10;
command.Parameters.Add(new SqlParameter("@Quantity", input.ToValueOrDBNull() ));
```

```ToValueOrDBNull()``` est une méthode d'extension qui pourrait être définie de la manière suivante:

```Csharp
public static object ToValueOrDBNull<T>(this T? input) where T : struct
{
    if (input == null)
    {
        return System.DBNull.Value;
    }

    if (input.HasValue)
    {
        return input.Value;
    }

    return System.DBNull.Value;
}
```

Cette méthode d'extension peut ainsi être réutilisée pour être appliquée sur n'importe quelle structure : ```int```, ```long```, ```decimal```, ```float```, etc...
