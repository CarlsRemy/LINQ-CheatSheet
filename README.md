# LINQ-CheatSheet
Language Integrated Query o Consulta Integrada en el Lenguaje es un componente de la plataforma Microsoft .NET que agrega capacidades de consulta a datos de manera nativa a los lenguajes .NET


## Operadores de Consulta
Los operadores de consulta de LINQ permiten realizar consultas sobre colecciones de datos. Algunos de los más comunes son

### Select
Proyecta cada elemento de una secuencia en un nuevo formulario.

```c#
var nombres = new List<string> { "Juan", "María", "Carlos" };
var nombresEnMayusculas = nombres.Select(nombre => nombre.ToUpper());
//Result: List<string> { "JUAN", "MARIA, "CARLOS" };

string[] fruits = { "apple", "banana", "mango", "orange", "grape" };

var query =
    fruits.Select((fruit, index) =>
                      new { index, str = fruit.Substring(0, index) });
/*Result:
[
 { index = 0, str =  },
 { index = 1, str = b },
 { index = 2, str = ma },
 { index = 3, str = ora },
 { index = 4, str = pass },
 { index = 5, str = grape }
]
 */
```

### Where
Filtra los elementos de una secuencia basándose en un predicado.

```c#
var numeros = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8};
var numerosPares = numeros.Where(num => num % 2 == 0);
// Result: {2,4,6,8}
```
### Distinct
Excluye los elementos duplicados.
```c#
var numeros = new List<int> { 1, 2, 3, 3, 4 };

var noduplicates = numeros.Distinct();
// Result: { 1, 2, 3, 4 };
```

### OrderBy / OrderByDescending
 Ordena los elementos de una secuencia.

```c#
var numeros = new List<int> { 5, 3, 8, 1, 6, 2, 7, 4 };
var numerosOrdenadosAscendente = numeros.OrderBy(num => num);
var numerosOrdenadosDescendente = numeros.OrderByDescending(num => num);
```
### GroupBy
Agrupa los elementos de una secuencia según una clave.
``` c#
var personas = new List<Persona>
{
    new Persona { Nombre = "Juan", Edad = 25 },
    new Persona { Nombre = "María", Edad = 30 },
    new Persona { Nombre = "Carlos", Edad = 25 }
};
var personasPorEdad = personas.GroupBy(persona => persona.Edad);

/*Result:
{
	25: [ // Grupo de personas con edad 25
		{ Nombre: "Juan", Edad: 25 },
		{ Nombre: "Carlos", Edad: 25 }
	],
	30: [ // Grupo de personas con edad 30
		{ Nombre: "María", Edad: 30 }
	]
}
*/
```
### Join
Realiza una unión entre dos secuencias basándose en una clave.

``` c#
Person magnus = new Person { Name = "Hedlund, Magnus" };
Person terry = new Person { Name = "Adams, Terry" };

Pet barley = new Pet { Name = "Barley", Owner = terry };
Pet daisy = new Pet { Name = "Daisy", Owner = magnus };

List<Person> people = new List<Person> { magnus, terry };
List<Pet> pets = new List<Pet> { barley, daisy };

var query = people.Join(pets, person => person, pet => pet.Owner,(person, pet) =>
	new { OwnerName = person.Name, Pet = pet.Name }
);

/*Result
 {OwnerName: "Hedlund, Magnus" , Pet: "Daisy"}
 {OwnerName: "Adams, Terry" Pet: "Barley"}
*/
```
## Operadores de Elemento
Estos operadores permiten seleccionar elementos específicos de una secuencia


### First / FirstOrDefault
Devuelve el primer elemento de una secuencia que cumple con un predicado.

```c#
var numeros = new List<int> { 1, 2, 3, 4, 5 };
var primerNumeroMayorATres = numeros.First(num => num > 3);
var primerNumeroMenorAUno = numeros.FirstOrDefault(num => num < 1);
```
### Last / LastOrDefault
Devuelve el último elemento de una secuencia que cumple con un predicado.

```c#
var numeros = new List<int> { 1, 2, 3, 4, 5 };
var ultimoNumeroPar = numeros.Last(num => num % 2 == 0);
var ultimoNumeroMayorASeis = numeros.LastOrDefault(num => num > 6);
```
### Single / SingleOrDefault
Devuelve el único elemento de una secuencia que cumple con un predicado.

```c#
var numeros = new List<int> { 1, 2, 3, 4, 5 };
var numeroTres = numeros.Single(num => num == 3);
var numeroDiez = numeros.SingleOrDefault(num => num == 10);
```
## Operadores de Conjunto
Permiten realizar operaciones de conjuntos en secuencias

### Union
Combina dos secuencias y elimina duplicados.

```c#
var secuencia1 = new List<int> { 1, 3, 2 };
var secuencia2 = new List<int> { 3, 4, 5 };
var union = secuencia1.Union(secuencia2);
// Result: {1,3,2,4,5}
```

### Intersect
Devuelve los elementos comunes entre dos secuencias.
```c#
var secuencia1 = new List<int> { 1, 2, 3 };
var secuencia2 = new List<int> { 3, 4, 5 };
var interseccion = secuencia1.Intersect(secuencia2);
// Result: {3}
```

### Except
Devuelve los elementos de la primera secuencia que no están en la segunda.
```c#
var secuencia1 = new List<int> { 1, 2, 3 };
var secuencia2 = new List<int> { 3, 4, 5 };
var diferencia = secuencia1.Except(secuencia2);
// Result: {1,2}
```

## Operadores de Agregación
Permiten realizar operaciones de agregación en secuencias numéricas

### Count
Devuelve el número de elementos en una secuencia.
```c#
var numeros = new List<int> { 1, 2, 3, 4, 5 };
var cantidad = numeros.Count();
// Result: 5
```

### Sum
Devuelve la suma de los valores en una secuencia.
```c#
var numeros = new List<int> { 1, 2, 3, 4, 5 };
var suma = numeros.Sum();
// Result: 15
```

### Average
Devuelve el promedio de los valores en una secuencia.
```c#
var numeros = new List<int> { 1, 2, 3, 4, 5 };
var promedio = numeros.Average();
```

### Min
Devuelve el valor mínimo en una secuencia.
```c#
var numeros = new List<int> { 1, 2, 3, 4, 5 };
var minimo = numeros.Min();
// Result: 1
```

### Max
Devuelve el valor máximo en una secuencia.
```c#
var numeros = new List<int> { 1, 2, 3, 4, 5 };
var maximo = numeros.Max();
// Result: 5
```

## Operadores de Conversión
Permiten convertir una secuencia en otro tipo de colección

### ToList
Convierte una secuencia en una lista.
```c#
var arreglo = new int[] { 1, 2, 3, 4, 5 };
var lista = arreglo.ToList();
```

### ToDictionary
Convierte una secuencia en un diccionario.
```c#
var nombres = new List<string> { "Juan", "María", "Carlos" };
var diccionario = nombres.ToDictionary(nombre => nombre[0]);
```

### ToArray
Convierte una secuencia en un arreglo.
```c#
var lista = new List<int> { 1, 2, 3, 4, 5 };
var arreglo = lista.ToArray();
```

## Operadores de Quantificador
Permiten verificar si una secuencia satisface ciertas condiciones

### Any
Verifica si algún elemento de una secuencia cumple con un predicado.
```c#
var numeros = new List<int> { 1, 2, 3, 4, 5 };
var hayNumerosPares = numeros.Any(num => num % 2 == 0);
//Result: True
```

### All
Verifica si todos los elementos de una secuencia cumplen con un predicado.
```c#
var numeros = new List<int> { 1, 2, 3, 4, 5 };
var todosMenoresASeis = numeros.All(num => num % 2 == 0);
//Result: False
```
### SequenceEqual
Determina si dos secuencias son iguales, es decir, si tienen los mismos elementos en el mismo orden. 

```c#
var secuencia1 = new List<int> { 1, 2, 3 };
var secuencia2 = new List<int> { 1, 2, 3 };
bool sonIguales = secuencia1.SequenceEqual(secuencia2);
// Result: true
```

## Operadores de Concatenación


### Concat
Combina dos secuencias en una sola.
```c#
var secuencia1 = new List<int> { 1, 2, 3 };
var secuencia2 = new List<int> { 4, 5, 6 };
var concatenacion = secuencia1.Concat(secuencia2);
// Result: {1,2,3,4,5,6}
```

## Operadores de Elemento de Conjunto

### ElementAt
Devuelve el elemento en una posición específica de una secuencia.
```c#
var numeros = new List<int> { 1, 2, 3, 4, 5 };
var tercerNumero = numeros.ElementAt(2);
//Result: {3}
```

### Skip
Omite un número especificado de elementos en una secuencia.
```c#
var numeros = new List<int> { 1, 2, 3, 4, 5 };
var numerosDespuesDelSegundo = numeros.Skip(2);
//Result: { 3, 4, 5 }
```
### Take
Toma un número especificado de elementos de una secuencia.
```c#
var numeros = new List<int> { 1, 2, 3, 4, 5 };
var primerosTresNumeros = numeros.Take(3);
//Result:  { 1, 2, 3 }
```