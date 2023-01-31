# Aplicações na prática de tipos genéricos em TypeScript

Esse conteúdo foi criado para a segunda etapa do processo seletivo de Summer Job de Currículo na [Trybe](https://www.betrybe.com/).

<br>

## O que vamos aprender? 

Hoje iremos aprender sobre **Generics**, uma funcionalidade fundamental do **TypeScript** e também de outras linguagens fortemente tipadas como **C#** e **Java**. Você verá como ele funciona na prática, e esse conhecimento será essencial para tornar seu código mais *flexível* e *reutilizável*. Vamos lá? 🚀

<br>

---

<br>


## Você será capaz de:

* Compreender o que são **Generics**
* Utilizar Generics em funções
* Utilizar Generics em interfaces
* Utilizar Generics em classes
* Criar funções que recebam múltiplos parâmetros genéricos

<br>

---

<br>

## Por que isso é importante?

<br>


Sabemos que o **TypeScript** veio para solucionar problemas que o **JavaScript** por si só não consegue, sendo o principal deles, a tipagem de elementos. Saber os tipos das variáveis com que estamos trabalhando é um passo essencial para tornarmos nosso código mais robusto, confiável e menos propenso a erros.

Porém, em alguns casos, a tipagem pode ser trabalhosa. Não seria legal ter que criar uma função para trabalhar com cada tipo primitivo, concorda? Por isso devemos buscar práticas que deixem nosso código mais dinâmico e reutilizável.

Os **Generics** são uma funcionalidade que nos permite unir esses conceitos, de forma a criar funções, classes e interfaces que possam receber um ou mais parâmetros de tipos distintos.

Quer ver como funciona? Então bora pro código! 🤓 💻

<br>

# Conteúdos

## O que são Generics?

<br>

Para começar, vamos a um exemplo prático. Suponha que você quer criar uma função que verifique se dois números são iguais. Uma das soluções possíveis seria mais ou menos assim:

<br>

![equalNumbers](./assets/equalNumbers.png)

<br>

Agora, imagine que você precise criar uma função que verifique se duas strings são iguais. Isso poderia ser feito assim:

<br>

![equalStrings](./assets/equalStrings.png)

<br>

Você já deve ter reparado que estamos repetindo código, não é mesmo? Então, como faríamos para construir uma função que aceite receber parâmetros de diferentes tipos e verificar se eles são iguais?

É aqui que entram os `Generics`, veja como ficaria a nossa função de verificação genérica:

<br>

![checkEquality](./assets/checkEquality.png)

Dessa forma podemos receber parâmetros de diversos tipos sem que a função apresente nenhum erro e continue nos trazendo o retorno esperado. Legal, não é mesmo?

<br>

> 💡 Definição: `Generics` é uma das principais funcionalidades do TypeScript para criar componentes que não precisem declarar explicitamente o tipo de variável que será recebida por parâmetro, e que possam trabalhar com uma variedade de tipos ao invés de somente um. Sem eles, teríamos que desenvolver versões separadas de funções, classes ou interfaces para cada tipo de dado que quiséssemos trabalhar. Eles nos ajudam a tornar nosso código mais reutilizável e escalável!

<br>

## Utilizando Generics em funções

<br>

A sintaxe dos `Generics` pode parecer confusa no começo, mas com o tempo você irá se acostumar, veja um exemplo de uma função que remove o segundo elemento de um array:

```typescript
function removeSecondElement<T>(array: T[]) {
  return array.filter((_element, index) => index !== 1);
}

console.log(removeSecondElement<number>([1, 2, 2, 3]));
// imprime [1, 2, 3]

console.log(removeSecondElement<string>(['a', 'b', 'b', 'c']));
// imprime ['a', 'b', 'c']

console.log(removeSecondElement<boolean>([true, false]));
// imprime [true]
```

<br>

Aqui estamos definindo que a função *removeSecondElement* recebe por parâmetro um array de tipos genéricos com a sintaxe `<T>(array: T[])`, onde `T` pode ser qualquer tipo passado na hora que a função é chamada. Antes que você pergunte, a escolha da letra `T` é apenas uma convenção, afinal, estamos declarando um `Tipo` 😅. Sinta-se livre para utilizar a letra que quiser!

<br>

Podemos criar funções que recebem múltiplos *Generics*. Vejamos agora uma função que recebe mais de um parâmetro genérico e verifica se eles pertencem ao mesmo tipo primitivo:

```typescript
function compareTypes<T, U>(param1: T, param2: U): boolean {
  return typeof param1 === typeof param2
}

console.log(compareTypes<boolean, string>(false, 'a'));
// imprime false

console.log(compareTypes<number, number>(1, 2));
// imprime true
```

<br>

Também é possível dar um valor padrão para os tipos genéricos ou limitá-los fazendo com que eles estendam de outros tipos:

```typescript
function sayHello<T extends string | number, U = boolean>(
  name: T,
  isAdmin: U,
) {
  if (isAdmin) {
    console.log(`Wellcome back, ${name}`);
  } else {
    console.log(`Hello, ${name}`)
  }
}

sayHello('John', true);
// imprime 'Wellcome back, John'

sayHello(30, false);
// imprime 'Hello, 30'
```

<details>
  <summary>📌 Fixação 1</summary>

  <br>

  ### Escreva uma função chamada *mergeObjects* que deve receber dois objetos de tipos genéricos e retornar a junção deles.

  - Dica: lembre-se do [spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

  [Ver gabarito](./GABARITOS.md#fixação-1)
</details>

<br>

## Utilizando Generics em interfaces

<br>

Vimos que `interfaces` são moldes criados para que nossas classes se encaixem, elas definem o formato, os nomes e os tipos dos atributos que queremos utilizar.

Como nem sempre sabemos o tipo exato do atributo que será passado, utilizar os `Generics` é a forma mais fácil de declarar um atributo que terá seu tipo definido somente durante a construção de um objeto, vejamos um exemplo:

```typescript
interface IProfile<T> {
  name: string
  age: number
  data: T[]
}
```
<br>

Dessa forma, o atributo `data` receberá um array de qualquer tipo que seja passado quando um objeto que implemente essa interface for criado.

<br>

<details>
  <summary>📌 Fixação 2</summary>

  <br>

  ### Escreva uma interface chamada *IPerson* com três atributos:
  1. `name` que deve ser do tipo string
  2. `id` que deve ser de um tipo genérico que extenda os tipos string e number
  3. `compareId` que recebe um parâmetro do mesmo tipo passado ao atributo `id` e retorna um booleano

  ⚠️ Essa interface será usada no próximo exercício de fixação. Certifique-se de realizar esse exercício antes de prosseguir.

  [Ver gabarito](./GABARITOS.md#fixação-2)
</details>

<br>

## Utilizando Generics em classes

<br>

`Classes` são abstrações de características e ações comuns a objetos, mas como essas características podem existir e se expressar de formas diferentes, usar `Generics` com `classes` pode ser uma vantagem. A sintaxe para criar `classes` genéricas é bem parecida com a de `interfaces`, veja:

```typescript
class KeyValuePair<K = string, V = number> {
  private key: K;
  private value: V;

  constructor(
    key: K,
    value: V,
  ) {
    this.key = key;
    this.value = value;
  }

  public setKeyValue(key: K, value: V) {
    this.key = key;
    this.value = value;
  }

  public getKey() { return this.key; }

  public getValue() { return this.value; }
}

const instance1 = new KeyValuePair<string, number>('id', 2);
instance1.setKeyValue('ID', 22);

console.log(instance1.getKey());
/** imprime 'ID' */

const instance2 = new KeyValuePair<number, string>(2, 'value');
instance2.setKeyValue('value', 2);
/** Error: Argument of type 'string' is not assignable to parameter of type 'number'. */
```
<br>

Aqui estamos criando uma classe chamada `KeyValuePair` que recebe em seu construtor os parâmetros `key` e `value`, de tipos genéricos. Além disso possui os métodos *getKey* e *getValue* para recuperar os valores privados, e o método *setKeyValue*, que altera ambos os valores de uma vez.

Nesse exemplo, podemos ver que ao tentar chamar o método *setKeyValue* da instância `instance2`, o *TypeScript* gera um erro dizendo que o tipo `string` não pode ser assinalado ao tipo `number`.

Isso acontece porque quando criamos a instância `instance2`, definimos que o tipo do primeiro parâmetro é `number` e o tipo do segundo parâmetro é `string`. Uma vez definidos os tipos, não podemos mais alterá-los.

Esse comportamento do *TypeScript* nos ajuda a manter a coesão no nosso código e evita diversos outros erros.

<br>

<details>
  <summary>📌 Fixação 3</summary>

  <br>

 ### Crie uma classe chamada *Person* que implemente a interface *IPerson* criada no exercício de fixação anterior, ela deve possuir as seguintes características:
  1. um atributo `name` que deve ser do tipo string
  2. um atributo `id` que deve ser de um tipo genérico que extenda os tipos string e number
  3. um método `compareId` que recebe um parâmetro do mesmo tipo passado ao atributo `id` e retorna um booleano

  ### Além disso, crie uma instância da classe *Person* e teste o método `compareId` passando um `id` igual e um diferente do `id` definido no construtor.

  [Ver gabarito](./GABARITOS.md#fixação-3)
</details>

<br>

# Vamos praticar!

<details>
  <summary>Exercício 1</summary>

  ### Crie uma função chamada findMax que deve:
  - Receber como parâmetro um elemento que estenda dos tipos string e number
  - Retornar o maior elemento

  [Ver gabarito](./GABARITOS.md#exercício-1)
</details>

<details>
  <summary>Exercício 2</summary>

  ### Recrie a função find do JavaScript.

  #### Sua função deve:
  - Receber como primeiro parâmetro um array de qualquer tipo
  - Receber como segundo parâmetro uma função callback
  - Retornar um elemento do mesmo tipo do array recebido ou undefined
  - A função callback deve receber como primeiro parâmetro um elemento do tipo do array recebido
  - A função callback pode receber como segundo parâmetro o índice do array recebido
  - A função callback pode receber como terceiro parâmetro o próprio array recebido
  - A função callback deve retornar um valor booleano

  [Ver gabarito](./GABARITOS.md#exercício-3)
</details>

<details>
  <summary>Exercício 3</summary>

  ### Crie uma interface IPokemon com as seguintes características:
  - um atributo `name` que deve ser do tipo string
  - um atributo `id` que deve ser do tipo number
  - um atributo `evolutions` que deve ser de um tipo genérico
  - um atributo `type` que deve ser de um tipo genérico

  [Ver gabarito](./GABARITOS.md#exercício-4)
</details>

<details>
  <summary>Exercício 4</summary>

  ### Crie uma classe Pokemon que implemente a interface IPokemon. Além disso, crie duas instâncias da classe pokemon com as seguintes características:
  - primeira instância:
    - o atributo `name` deve ser `bulbasaur`
    - o atributo `id` deve ser `1`
    - o atributo `evolutions` deve ser o array `['ivysaur', 'venusaur']`
    - o atributo `type` deve ser o array `['grass', 'poison']`
  
  - segunda instância:
    - o atributo `name` deve ser `pikachu`
    - o atributo `id` deve ser `25`
    - o atributo `evolutions` deve ser a string `raichu`
    - o atributo `type` deve ser a string `electric`

  [Ver gabarito](./GABARITOS.md#exercício-5)
</details>

<br>

# Exercícios bônus

<details>
  <summary>Exercício 5</summary>

  ### Recrie a função map do JavaScript.

  #### Sua função deve:
  - Receber como primeiro parâmetro um array de qualquer tipo
  - Receber como segundo parâmetro uma função callback
  - Retornar um array de qualquer tipo com o mesmo tamanho do array recebido
  - A função callback deve receber como primeiro parâmetro um elemento do tipo do array recebido
  - A função callback pode receber como segundo parâmetro o índice do array recebido
  - A função callback pode receber como terceiro parâmetro o próprio array recebido
  - A função callback deve retornar um elemento de qualquer tipo

  [Ver gabarito](./GABARITOS.md#exercício-6)
</details>

<details>
  <summary>Exercício 6</summary>

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

  [Ver gabarito](./GABARITOS.md#exercício-7)
</details>

<br>

# Recursos adicionais

- [Generics - Documentação do TypeScript](https://www.typescriptlang.org/docs/handbook/2/generics.html)
- [TypeScript Basic Generics - W3Schools](https://www.w3schools.com/typescript/typescript_basic_generics.php)
- [Typescript Generics - O que é, porque existe e como utilizar](https://dev.to/magoacademico/typescript-generics-59h6)
- [Introdução aos Genéricos - Microsoft](https://learn.microsoft.com/pt-br/training/modules/typescript-generics/2-what-are-generics)
- [Why you should consider using TypeScript Generics instead of Any](https://ndcunningham.medium.com/why-you-should-consider-using-typescript-generics-instead-of-any-4c6543ba88ec)
