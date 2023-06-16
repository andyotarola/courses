# Typescript

## Type Aliases

Los Type Alias (alias de tipo) permiten crear nombres alternativos para tipos existentes. Esto puede ser útil para simplificar tipos complejos, mejorar la legibilidad del código o para hacer que el código sea más modular y reutilizable.

```ts
type HeroBaseInfo = {
  name: string
  age: number
}
```

## Template Unions type

Los Template Union Types (tipos de unión de plantillas) en TypeScript son una característica que combina la capacidad de trabajar con plantillas de cadenas de texto y tipos de unión. Esta característica permite crear tipos que pueden aceptar un conjunto específico de valores literales o plantillas de cadena de texto como argumentos.

```ts
type HeroId = `${string}-${string}-${string}-${string}-${string}`
```

## Union Types

Los Union Types (tipos de unión) en TypeScript permiten combinar varios tipos en uno solo, lo que significa que una variable o parámetro puede aceptar más de un tipo de valor.

Un Union Type se define utilizando el operador de tubería (|) entre los tipos que se desean combinar. Por ejemplo:

```ts
let variable: string | number = 4
```

## Intersections Types

Los Intersection Types en TypeScript permiten combinar múltiples tipos en uno solo, creando un nuevo tipo que contiene todas las propiedades y miembros de los tipos combinados.

```ts
type Hero = HeroBaseInfo & HeroProperty
```

## Type Indexing

Type Indexing (indexación de tipos) en TypeScript se refiere a la capacidad de acceder a las propiedades de un objeto utilizando un índice o clave dinámica en lugar de acceder directamente a ellas. Esto permite trabajar con objetos que tienen propiedades dinámicas cuyos nombres no se conocen de antemano.

```ts
type MiObjeto = {
  [clave: string]: number
}

const miObjeto: MiObjeto = {
  edad: 25,
  calificaciones: 90,
  horasTrabajadas: 40,
}
```

Otro ejemplo:

```ts
type HeroProperties = {
  isActive: boolean
  address: {
    planet: string
    city: string
  }
}

const addressHero: HeroProperties['address'] = {
  city: 'Lima',
  planet: 'Mars',
}
```

## Type from value

Crear un tipo a partir de una variable

```ts
const address = {
  planet: 'Tierra',
  city: 'Lima',
}
type Address = typeof address

const location: Address = {
  planet: 'Marte',
  city: 'Marte',
}
```

## Type from function return

Crear un tipo a partir del retorno de una función

```ts
function createAddress() {
  return {
    planet: 'Tierra',
    city: 'San Francisco',
  }
}

type Address = ReturnType<typeof createAddress>

const location: Address = {
  planet: 'Tierra',
  city: 'San Isidro',
}
```

## Array

```ts
const languages: (string | number)[] = []
languages.push('JavaScript')
languages.push('TypeScript')
languages.push(1)
```

## Matriz

```ts
type CellValue = 'X' | 'O' | ''

const gameBoard: CellValue[][] = [
  ['X', 'O', ''],
  ['X', 'O', 'X'],
  ['X', 'O', 'X'],
]
```

## Tupla

En un array que tiene un límite fijado de longitud

```ts
type CellValue = 'X' | 'O' | ''

type GameBoard = [
  [CellValue, CellValue, CellValue],
  [CellValue, CellValue, CellValue],
  [CellValue, CellValue, CellValue]
]

const gameBoard: GameBoard = [
  ['X', 'O', ''],
  ['X', 'O', 'X'],
  ['X', 'O', 'X'],
]
```

## Enums

En TypeScript, los enums (enumeraciones) son una forma de definir un conjunto de valores con nombres descriptivos. Los enums permiten asignar nombres simbólicos a valores numéricos o de cadena de texto, lo que facilita su uso y comprensión en el código.

```ts
enum ErrorTypes {
  NOT_FOUND,
  UNAUTHORIZED,
  FORBIDDEN,
}
```

## Type Guard

En TypeScript, un Type Guard (guardia de tipo) es una técnica que permite comprobar y restringir el tipo de una variable en tiempo de ejecución. Estas comprobaciones adicionales ayudan al compilador a inferir y verificar de manera más precisa los tipos de variables dentro de un bloque de código específico.

Los Type Guards se utilizan comúnmente con los tipos de unión (Union Types) y los tipos de intersección (Intersection Types) para realizar comprobaciones condicionales sobre los tipos de las variables y reducir el conjunto de tipos posibles. Esto permite realizar operaciones seguras en función del tipo específico de una variable en un punto determinado del programa.

```ts
interface Fish {
  name: string
  swim: () => void
}
interface Bird {
  name: string
  fly: () => void
}

type Pet = Fish | Bird

const isBird = (pet: Pet): pet is Bird => {
  return (pet as Bird).fly !== undefined
}

function jugar(pet: Pet) {
  if (isBird(pet)) {
    pet.fly()
    return
  }
  pet.swim()
}
```
