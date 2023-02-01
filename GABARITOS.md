# Gabaritos

## Fixação 1

  ### Escreva uma função chamada *mergeObjects* que deve receber dois objetos de tipos genéricos e retornar a junção deles.

  - Dica: lembre-se do [spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

  ## Solução:

  ```typescript
  function mergeObjects<T, U>(obj1: T, obj2: U): T & U {
    return { ...obj1, ...obj2 };
  }
  ```

  <br>

  ## Fixação 2

  ### Escreva uma interface chamada *IPerson* com três atributos:
  1. `name` que deve ser do tipo string
  2. `id` que deve ser de um tipo genérico que extenda os tipos string e number
  3. `compareId` que recebe um parâmetro do mesmo tipo passado ao atributo `id` e retorna um booleano

  ## Solução:

  ```typescript
  interface IPerson<T extends string | number> {
    name: string
    id: T
    compareId(id: T): boolean
  }
  ```

  <br>

  ## Fixação 3

   ### Crie uma classe chamada *Person* que implemente a interface *IPerson* criada no exercício de fixação anterior, ela deve possuir as seguintes características:
  1. um atributo `name` que deve ser do tipo string
  2. um atributo `id` que deve ser de um tipo genérico que extenda os tipos string e number
  3. um método `compareId` que recebe um parâmetro do mesmo tipo passado ao atributo `id` e retorna um booleano

  ### Além disso, crie uma instância da classe *Person* e teste o método `compareId` passando um `id` igual e um diferente do `id` definido no construtor.

  ## Solução:

  ```typescript
  class Person<T extends string | number> implements IPerson<T> {
    constructor(
      public name: string,
      public id: T,
    ) {}

    public compareId(id: T) {
      return id === this.id;
    }
  }

  const person = new Person<number>('John', 27);

  person.compareId(10);
  // retorna false

  person.compareId(27);
  // retorna true
  ```

  <br>

  ## Exercício 1

  ### Crie uma função chamada findMax que deve:
  - Receber como parâmetro um elemento que estenda dos tipos string e number
  - Retornar o maior elemento

  ## Solução:

  ```typescript
  const findMax = <T>(array: T[]): T => {
    let max = array[0];

    for (let i = 1; i < array.length; i += 1) {
      if (array[i] > max) {
        max = array[i]; 
      }
    }

    return max;
  };

  findMax([1, 2, 3, 4]);
  // retorna 4

  findMax(['a', 'b', 'c', 'd']);
  // retorna 'd'
  ```

  <br>

  ## Exercício 3

  ### Recrie a função find do JavaScript.

  #### Sua função deve:
  - Receber como primeiro parâmetro um array de qualquer tipo
  - Receber como segundo parâmetro uma função callback
  - Retornar um elemento do mesmo tipo do array recebido ou undefined
  - A função callback deve receber como primeiro parâmetro um elemento do tipo do array recebido
  - A função callback pode receber como segundo parâmetro o índice do array recebido
  - A função callback pode receber como terceiro parâmetro o próprio array recebido
  - A função callback deve retornar um valor booleano

  ## Solução:

  ```typescript
  type FindCallback<T> = (element: T, index?: number, array?: T[]) => boolean;

  function myFind<T>(array: T[], callback: FindCallback<T>): T | undefined {
    let elementFound: T | undefined = undefined;

    for(let i = 0; i < array.length; i += 1) {
      if(callback(array[i], i, array)) {
        elementFound = array[i];
        break;
      }
    }

    return elementFound;
  }

  console.log(
    myFind<number>(
      [6, 2, 3, 4],
      (element, index, array) => element % 2 !== 0,
    )
  );
  // retorna 3
  ```

  <br>

  ## Exercício 4

  ## Solução:

  ```typescript
  interface IPokemon<E, T> {
    name: string
    id: number
    evolutions: E
    type: T
  }
  ```

  <br>

  ## Exercício 5

  ## Solução:

  ```typescript
  class Pokemon<E, T> implements IPokemon<E, T> {
    constructor(
      public name: string,
      public id: number,
      public evolutions: E,
      public type: T,
    ) {}
  }

  const bulbasaur = new Pokemon('bulbasaur', 1, ['ivysaur', 'venusaur'], ['grass', 'poison']);
  const pikachu = new Pokemon('pikachu', 25, 'raichu', 'electric');

  console.log(pikachu.type); // imprime 'electric'
  console.log(bulbasaur.type); // imprime ['ivysaur', 'venusaur']
  ```

  <br>

  ## Exercício 6

  ### Recrie a função map do JavaScript.

  #### Sua função deve:
  - Receber como primeiro parâmetro um array de qualquer tipo
  - Receber como segundo parâmetro uma função callback
  - Retornar um array de qualquer tipo com o mesmo tamanho do array recebido
  - A função callback deve receber como primeiro parâmetro um elemento do tipo do array recebido
  - A função callback pode receber como segundo parâmetro o índice do array recebido
  - A função callback pode receber como terceiro parâmetro o próprio array recebido
  - A função callback deve retornar um elemento de qualquer tipo

  ## Solução:

  ```typescript
  type MapCallback<T> = (element: T, index?: number, array?: T[]) => any;

  function myMap<T>(array: T[], callback: MapCallback<T>): any[] {
    const mappedArray: any[] = [];

    for(let i = 0; i < array.length; i += 1) {
      mappedArray.push(callback(array[i], i, array));
    }

    return mappedArray;
  }

  console.log(
    myMap<number>(
      [1, 2, 3, 4],
      (element, index, array) => element % 2 === 0,
    )
  );
  // retorna [false, true, false, true]
  ```
  <br>

  ## Exercício 7

  ### Recrie a função reduce do JavaScript.

  #### Sua função deve:
  - Receber como primeiro parâmetro um array de qualquer tipo
  - Receber como segundo parâmetro uma função callback
  - Receber como treceiro parâmetro opcional um elemento de qualquer tipo
  - Retornar um elemento do mesmo tipo do primeiro elemento do array recebido, ou do mesmo tipo elemento recebido no terceiro parâmetro caso exista
  - A função callback deve receber como primeiro parâmetro o primeiro elemento do array recebido, ou o terceiro parâmetro, caso este tenha sido passado
  - A função callback deve receber como segundo parâmetro um elemento do tipo do array recebido
  - A função callback pode receber como terceiro parâmetro o índice do array recebido
  - A função callback pode receber como quarto parâmetro o próprio array recebido
  - A função callback deve retornar um elemento do mesmo tipo do seu primeiro parâmetro

  ## Solução:

  ```typescript
  type ReduceCallback<T> = (accumulator: any, element: T, index?: number, array?: T[]) => any;

  function myReduce<T>(array: T[], callback: ReduceCallback<T>, accumulator: any): any {
    for(let i = 0; i < array.length; i += 1) {
      accumulator = callback(accumulator, array[i], i, array)
    }

    return accumulator;
  }

  console.log(
    myReduce<number>(
      [1, 2, 3, 4],
      (acc, element, index, array) => acc + element,
      0
    )
  );
  // retorna 10
  ```