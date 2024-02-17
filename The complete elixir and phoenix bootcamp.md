# The complete elixir and phoenix bootcamp
### Install elixir

- Instalar erlang y elixir
- VM erlang, traduce al procesador la compilacion que hacemos con elixir

```sh 
docker run -it --rm elixir
```
elixir
elixirc
mix
iex

```sh
# create project
mix new cards

# Elixir modules and methods
cd cards/
iex -S mix

```


Un modulo es un acoleccion de metodos o funciones

The iex doesn't recompile automatically, use

```elixir
recompile
Cards.create_deck
```

### Desing patterns elixir
Make a difference between object oriented and functional programming

def shuffle(deck) do

end

Cards.shuffle([])

### Enum module

[Elixir documentacion](https://elixir-lang.org/docs.html)

Arity(aridad), es el numero de argumentos que recibe una funcion


```elixir
iex(5)> deck = Cards.create_deck
["Ace", "Two", "Three"]
iex(6)> Cards.shuffle(deck)
["Three", "Two", "Ace"]
```


### Inmutability
En elixir nunca modificamos una variable o estructura de datos, solo creamos una copia, hacemos un procesamiento sobre la copia y retornamos la nueva estructura con datos


### Comprehension <-
```elixir
def create_deck do
    values = ["Ace", "Two", "Three", "Four", "Five"]
    suits = ["Spades", "Clubs", "Hearts", "Diamonds"]
    # Comprehension <-
    cards = for suit <- suits do
      for value <- values do
        "#{value} of #{suit}"
      end
    end
    ## Aplana las listas en una sola
    List.flatten(cards)
end
```

### Nested list
```elixir
    for suit <- suits, value <- values do
        "#{value} of #{suit}"
    end
```

### Tuples

```sh
deck = Cards.create_deck
```

```sh
iex(3)> deck = Cards.create_deck
["Ace of Spades", "Two of Spades", "Three of Spades", "Four of Spades",
 "Five of Spades", "Ace of Clubs", "Two of Clubs", "Three of Clubs",
 "Four of Clubs", "Five of Clubs", "Ace of Hearts", "Two of Hearts",
 "Three of Hearts", "Four of Hearts", "Five of Hearts", "Ace of Diamonds",
 "Two of Diamonds", "Three of Diamonds", "Four of Diamonds", "Five of Diamonds"]

iex(4)> Cards.deal(deck, 5)
{["Ace of Spades", "Two of Spades", "Three of Spades", "Four of Spades",
  "Five of Spades"],
 ["Ace of Clubs", "Two of Clubs", "Three of Clubs", "Four of Clubs",
  "Five of Clubs", "Ace of Hearts", "Two of Hearts", "Three of Hearts",
  "Four of Hearts", "Five of Hearts", "Ace of Diamonds", "Two of Diamonds",
  "Three of Diamonds", "Four of Diamonds", "Five of Diamonds"]}
```

### Pattern matching

El pattern matching o concordancia de patrones es el sustituto de elixir para la asignacion de variables.

El pattern matching siempre se usa cuando usamos el signo igual.

```sh
iex(10)> {hand, rest_of_deck} = Cards.deal(deck,5)
{["Ace of Spades", "Two of Spades", "Three of Spades", "Four of Spades",
  "Five of Spades"],
 ["Ace of Clubs", "Two of Clubs", "Three of Clubs", "Four of Clubs",
  "Five of Clubs", "Ace of Hearts", "Two of Hearts", "Three of Hearts",
  "Four of Hearts", "Five of Hearts", "Ace of Diamonds", "Two of Diamonds",
  "Three of Diamonds", "Four of Diamonds", "Five of Diamonds"]}
iex(11)> hand
["Ace of Spades", "Two of Spades", "Three of Spades", "Four of Spades",
 "Five of Spades"]
iex(12)> rest_of_deck
["Ace of Clubs", "Two of Clubs", "Three of Clubs", "Four of Clubs",
 "Five of Clubs", "Ace of Hearts", "Two of Hearts", "Three of Hearts",
 "Four of Hearts", "Five of Hearts", "Ace of Diamonds", "Two of Diamonds",
 "Three of Diamonds", "Four of Diamonds", "Five of Diamonds"]
```

```sh
iex(2)> [papa, mama, hija, cunis] = ["cristhian","zonia","isabela", "luchita"]
["cristhian", "zonia", "isabela", "luchita"]
iex(3)> papa
"cristhian"
iex(4)> mama
"zonia"
iex(5)> hija
"isabela"
iex(6)> cunis
"luchita"
iex(7)> {color1, color2}= {"azul", "amarillo"}
{"azul", "amarillo"}
iex(8)> color1
"azul"
iex(9)> color2
"amarillo"
iex(7)> {[color1], color2, {color3}}= {["azul"], "amarillo", {"rojo"}}
{["azul"], "amarillo", {"rojo"}}
iex(8)> color1
"azul"
iex(9)> color2
"amarillo"
iex(10)> color3
```

### Elixir relationship with Erlang

Escribimos codigo en elixir
elixir se transpila a Erlang
erlang compila y ejecuta BEAM (Virtual machine at the core erlang)

Escribimos en elixir para no tener que lidiar con Erlang
BEAM: Bodgan Erlang Abstract Machine


### Save and read files


```sh
iex(16)> deck = Cards.create_deck
["Ace of Spades", "Two of Spades", "Three of Spades", "Four of Spades",
 "Five of Spades", "Ace of Clubs", "Two of Clubs", "Three of Clubs",
 "Four of Clubs", "Five of Clubs", "Ace of Hearts", "Two of Hearts",
 "Three of Hearts", "Four of Hearts", "Five of Hearts", "Ace of Diamonds",
 "Two of Diamonds", "Three of Diamonds", "Four of Diamonds", "Five of Diamonds"]
iex(17)> Cards.save(deck,"file1")
:ok
iex(18)> File.read("file1")
{:ok,
 <<131, 108, 0, 0, 0, 20, 109, 0, 0, 0, 13, 65, 99, 101, 32, 111, 102, 32, 83,
   112, 97, 100, 101, 115, 109, 0, 0, 0, 13, 84, 119, 111, 32, 111, 102, 32, 83,
   112, 97, 100, 101, 115, 109, 0, 0, 0, 15, 84, ...>>}
iex(19)> {status, binary} = File.read("file1")
{:ok,
 <<131, 108, 0, 0, 0, 20, 109, 0, 0, 0, 13, 65, 99, 101, 32, 111, 102, 32, 83,
   112, 97, 100, 101, 115, 109, 0, 0, 0, 13, 84, 119, 111, 32, 111, 102, 32, 83,
   112, 97, 100, 101, 115, 109, 0, 0, 0, 15, 84, ...>>}
iex(20)> binary
<<131, 108, 0, 0, 0, 20, 109, 0, 0, 0, 13, 65, 99, 101, 32, 111, 102, 32, 83,
  112, 97, 100, 101, 115, 109, 0, 0, 0, 13, 84, 119, 111, 32, 111, 102, 32, 83,
  112, 97, 100, 101, 115, 109, 0, 0, 0, 15, 84, 104, 114, ...>>
iex(21)> :erlang.binary_to_term(binary)
["Ace of Spades", "Two of Spades", "Three of Spades", "Four of Spades",
 "Five of Spades", "Ace of Clubs", "Two of Clubs", "Three of Clubs",
 "Four of Clubs", "Five of Clubs", "Ace of Hearts", "Two of Hearts",
 "Three of Hearts", "Four of Hearts", "Five of Hearts", "Ace of Diamonds",
 "Two of Diamonds", "Three of Diamonds", "Four of Diamonds", "Five of Diamonds"]
iex(22)>
```
### case

**cuando necesitemos chequear un valorAlejar nuestra mente de solucionar problemas con condicional if**

```elixir
  def load(filename) do
    {status, binary} = File.read(filename)

    case status do
      :ok -> :erlang.binary_to_term binary
      :error -> "That file doesn't exist"
    end
  end
```

### Pipe operator

|> sirve para hacer una ejecucion de varios metodos de manera encadenada (como una tuberia)
este operador pasa como primer argumento al siguiente metodo su resultado:

```elixir
  def create_hand(hand_size) do
    Cards.create_deck
    |> Cards.shuffle
    |> Cards.deal(hand_size)
  end
```

### documentacion

https://hexdocs.pm/ex_doc/0.25.0/readme.html

al crear el projecto con el comando
> mix new cards

creamos un archivo llamado 
> mix.exs

hay una linea que dice "**deps**" (abreviatura de dependencies) alli es donde van nuestras dependencias


```sh
# Actualizar dependencias
mix deps.get

# Generar documentacion
mix docs
```

### Testing

Hay dos tipos de pruebas que podemos hacer en elixir.

1. test cases: (casos de prueba) son las pruebas en nuestro archivo de pruebas, con assertions a nuestros modulos.

2. doctesting: Cuando escribimos documentacion en nuestras funicones y hacemos la seccion de examples esto tambien se prueba cuando ejecutamos nuestros tests haciendo un assertion. equal

```sh
mix test
```


### Mapas y 

Mapas: Colecciones clave valor

```sh
iex(1)> colors = %{primary: "red"}
%{primary: "red"}
iex(2)> colors.primary
"red"
iex(3)> colors = %{primary: "red", secondary: "blue"}
%{primary: "red", secondary: "blue"}
iex(4)> colors.secondary
"blue"
iex(5)> %{secondary: secondary_color} = colors
%{primary: "red", secondary: "blue"}
iex(6)> secondary_color
"blue"
```

Las estructuras de datos que creemos no se pueden manipular, debemos crear una nueva a partir de una existente con alguna diferencia.

En otras palabras debemos crear un nuevo mapa

Revisar la documentacion de Elixir puesto que hay muchos metodos para trabajar con los Mapas.

```sh
# primero pasamos el Mapa, segundo es la clave que queremos actualziar como atomo, tercero el valor
iex(7)> Map.put(colors, :primary, "purple")
%{primary: "purple", secondary: "blue"}
iex(8)> colors.primary
"red"
iex(9)> colors
%{primary: "red", secondary: "blue"}
```

Otra forma para editar los mapas es con el pipe |
```sh
iex(10)> %{ colors | primary: "brown" }
%{primary: "brown", secondary: "blue"}
iex(11)> colors
%{primary: "red", secondary: "blue"}
```
Es importante observar que luego de hacer la modificación, nada cambia en el mapa original y si debemos conservar ese cambio, debemos asignarlo a una variable "pattern matching".
Esta forma de modificar solo aplica si el key esta dentro del mapa.

```sh
iex(14)> Map.put(colors, :secondary_color, "green" )
%{primary: "red", secondary: "blue", secondary_color: "green"}
iex(15)> %{ colors | secondary_color: "yellow" }
```
 
### Keyword List
Es una mexcla de una tupla, una lista y un mapa.

```sh
#Se usa los corchetes y dentro las llaves [{}]
iex(18)> colors = [{:primary, "red"}, {:secondary, "green"}]
# Nuestro resultado es como una clave-valor
[primary: "red", secondary: "green"]
iex(19)> colors[:primary]
"red"
```
Elixir internamente sigue tratando esto como una tupla

```sh
iex(1)> colors = [primary: "red", secondary: "blue"]
[primary: "red", secondary: "blue"]

#El Map no permite tener dos llaves con el mismo nombre, sobreescribe
iex(2)> colors = %{ primary: "red", primary: "blue" }
warning: key :primary will be overridden in map
└─ iex:2

%{primary: "blue"}
# La Keyword list si lo permite
iex(3)> colors = [primary: "red", primary: "red"]
[primary: "red", primary: "red"]
```