# Tutorial Elixir

### Que es elixir
https://elixir-lang.org/

Programacion funcional
Definicion de cosas para solucionar un problema

### Instalar elixir

1. Install elixir

- Instalar erlang y elixir
- VM erlang, traduce al procesador la compilacion que hacemos con elixir

```sh 
docker run -it --rm elixir
```


### Ejecutar comandos por consola (Interactive Elixir)
REPL (Read, Eval, Print, Loop): Herramienta para correr interactivamente programas 
Elixir es un lenguaje basado en expresiones
Con la REPL: nos ayuda a teclear expresiones y verlas sobre la mancha

en elixir la REPL se llama iex

en la powershell usar iex.bat


### Como hacer asignaciones
https://hexdocs.pm/elixir/basic-types.html

Elixir acepta expresiones, si introduzco en la REPL un numero 5, el lo evalua e imprime ese 5 como un tipo de dato primitivo
Elixir no redondea, los numeros pueden ser tan largos como queramos

Con las asignaciones lo que hacemos es dar un nombre especial a una expresion

identificadores se almacenan en alguna parte del ordenador (tabla gigante) y podriamos usar su valor

```elixir
pi = 3.141592263
x = 2
pi * x
```

cuando hacemos una asignacion ya no puede ser cambiada, RELP nos permite hacer un cambio 


### Tipos de datos
Para saber mas sobre un tipo de dato anteponer la letra i
```elixir
pi = 3.141592263
i pi
```

### Atomos
Usar dos puntos antes de unos caracteres
```elixir
:orange
i :orange
```

la salida de iex tiene un color y es de acuerdo al tipo de dato

Atomos = Azul
Entero = Amarillo
Boolean = Purpura


atomo :nil , es un comodin para representar un dato que no existe
nil es el null de otros lenguajes de programacion

si escribo nil sin dos puntos tambien lo imprime
es uno de los tres atomos mas importantes en compañia de true y false

```elixir
nil
true
false
```

### Operadores

Asignacion =
Igualdad ==
Diferente !=
menor <
mayor


false == :false

Si en el diccionario sale mas tarde una letra en el alfabeto esa sera mayor

```elixir
iex(34)> :a == :a
true
iex(39)> :aaa > :aa
true
iex(40)> :aaa > :aaaaa
false
```

### Comparacion estricta (mismo tipo y valor) ===

```elixir
iex(41)> 3 == 3.0
true
iex(42)> 3 === 3.0
false
```

https://hexdocs.pm/elixir/operators.html#term-ordering


### Operadores logicos

Estos son los operadores en orden y precedencia de evaluacion

Comparadores estrictos

not
and
or

```elixir
iex(1)> not false
true
iex(2)> not true
false
iex(3)> x = true
true
iex(4)> not x
false
iex(5)> true and true
true
iex(6)> false and false
false
iex(7)> true and false
false
iex(8)> x and x
true
iex(9)> true or false
true
iex(10)> false or false
false
iex(11)> true or true
true
iex(12)> true and true
true
iex(13)> (true and true) or false
true
iex(14)> (true and false) or false
false
iex(15)> true and not false
true
iex(16)> true and not true
false
iex(17)> true and false or false and true
false
iex(18)> true and true or false and true
```

Comparadores flexibles

!
&&
||

los numeros son tratados como true
nil es tratado como false

```elixir
iex(1)> 5 && 3
3
iex(2)> !5
false
iex(3)> 5 && true
true
iex(4)> nil && true
nil
iex(5)> true || 5
true
iex(6)> true && 5
5
iex(7)> 5 || true
5
iex(8)> !5 && true
false
iex(9)>
```

tener en cuenta el valor de la izquierda

### Funciones
rem es el modulo de elixir
```elixir
iex(6)> round(3.54)
4
iex(7)> rem(4,2)
```

cuando la funcion tiene un solo parametro no hay necesidad de usar parentesis,
pero es bueno mantenerlos por visibilidad

```elixir
i 5
```
podemos usar el tab para mostrar las funciones de elixir

```elixir
Atom.
Integer.
```
kernel es el modulo mas importante, no es necesario poner Kernel.
es decir... son lo mismo

```elixir
Kernel..rem
rem
```
### Strings
Los atomos se usan para comunicacion interna entre fnuciones
Las cadenas son para el mundo exterior
las cadenas admiten mas caracteres
```elixir
"hola zonia 🤩📈🥸🤡🤡"
iex(56)> "Amor
...(56)> quiero comer
...(56)> ya!"
"Amor \nquiero comer\nya!"
```

### List and tuples
```elixir
iex(50)> familia = ["papa", "mama", "hijos"]
["papa", "mama", "hijos"]
iex(51)> length(familia)
```

se puede concatenar listas con ++ o sustraer con --

**Tuplas**
```elixir
tuple = {:ok, "hello"}
{:ok, "hello"}
put_elem(tuple, 1, "world")
{:ok, "world"}
tuple
{:ok, "hello"}

put_elem()
elem()
```

En pocas palabras, las listas se utilizan cuando el número de elementos devueltos puede variar. Las tuplas tienen un tamaño fijo.

### 

puts: imprimir caracteres, sirve para no mostrar caracteres extraños por la salida
```elixir
iex(1)> IO.puts("Hola amor")
Hola amor
:ok
iex(2)> x = "hola reina
...(2)> hazme
...(2)> la cena por
...(2)> favor"
"hola reina\nhazme\nla cena por\nfavor"
iex(3)> x
"hola reina\nhazme\nla cena por\nfavor"
iex(4)> IO.puts(x)
```
El return de puts es :ok
Las funciones deben ser puras


gets: 
```elixir
iex(6)> entrada = IO.gets("Escribe aqui: ")
Escribe aqui: hola mundo!
"hola mundo!\n"
iex(7)> entrada
"hola mundo!\n"
```