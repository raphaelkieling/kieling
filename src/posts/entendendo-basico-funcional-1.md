---
title: Entendendo o básico de programação funcional com Javascript - Parte 1
date: 26/03/2019
autor: Raphael Kieling Tondin
---

# Entendendo o básico de programação funcional com Javascript - Parte 1

<description-post/>

<p align="center">
    <img src="https://deployeveryday.com/img/lambda_symbol.png" width="150" height="150">
</p>

Sou apaixonado por programação funcional, é um sintaxe linda e organizada que deixa qualquer programador de outro paradigma curioso. Hoje vamos ver alguns conceitos sobre FP (para os intimos), está é a parte 1/2 sobre programação funcional.

## Sumário

- [Porque eu estudaria isto?](#porque-eu-estudaria-isto)
- [Quem usa?](#porque-eu-estudaria-isto)
- [O que é Programação Funcional?](#o-que-e-programacao-funcional)
- [Conceitos chaves](#conceitos-chaves)
    - [Funções de Primeira Classe](#funcoes-de-primeira-classe)
    - [Função Matemática ou Função Pura](#funcao-matematica-ou-funcao-pura)
    - [Recursividade](#recursividade)
    - [Ditar O QUE ser feito e não COMO](#ditar-o-que-ser-feito-e-nao-como)
    - [Efeitos Colaterais](#efeitos-colaterais)
    - [Imutabilidade](#imutabilidade)
- [Exemplo Final](#exemplo-final)
- [Finalizando](#finalizando)
- [Referências](#referencias)


## Porque eu estudaria isto?

Alguns pontos fazem dessa abordagem uma ótima escolha:
- Funções puras evitando assim efeito colaterais
- Reduz a complexidade, se `A + B` então é pra somar, não para somar, ir no banco e dar log no console.
- Facilmente testável. `(a , b) => a + b;` Da pra testar isso só de olhar hehe.
- Trabalha facilmente com concorrência

## Quem usa?

Spark, Netflix, Google, Facebook, Amazon (Amazon Lambda), sistemas de avião como da família Airbus A340, entre muitos outros.

## O que é Programação Funcional?

Programação funcional e para os mais íntimos FP, é um paradígma de programação como Orientação a Objetos (OOP). Entre elas ainda temos:

- Procedural
- Meta Programação
- Imperativa
- Declarativa
- ...

Ok, acho que tu já entendeu. Mas entenda que um paradígma dita a filosofia de uma linguagem em certo ponto, na `orientação a objetos` nós temos entidades que servem de base para nós trabalharmos pensando no sistema como objetos em si, na `procedural` definimos linha a linha o que vai ser feito como uma receita de bolo. O FP modifica a linha de raciocínio para algo mais volta a obviamente `funções` de forma mais declarativa. Que tal um exemplo?

```js
let pessoas = [
    { nome: 'Raphael', idade: 21 },
    { nome: 'Emilio', idade: 30 },
    { nome: 'Jeromel', idade: 13 }
];

// Imperativo é focado em COMO ele opera
let filtradosMenorIdade = [];

for(let i=0; i < pessoas.length; i++){
    if(pessoa.idade < 18){
        let pessoa = pessoas[i];
        pessoa.nome = pessoa.nome.toUpperCase(); 
        filtradosMenorIdade.push(pessoa);
    }
}


// Declarativo 
function colocaNomeParaMaiusculo(person){
    person.nome = person.nome.toUpperCase();
    return person;
}

function isMenorDeIdade(pessoa){
    return pessoa.idade < 18
}

let novaListagemMenoresDeIdade = pessoas
    .filter(isMenorDeIdade)
    .map(colocaNomeParaMaiusculo)
```

Estranho? Não te preocupa, isto faz sentido. Olhando com calma nós vemos uma diferença muito simples que é facil de pegar.

- Primeiro abordagem (Imperativa)
    - De forma imperativa criamos um `for` baseado no tamanho do array, passamos pela listagem verificando quem é menor de idade.
    - Sendo menor de idade colocamos o nome para maisculo e adicionamos na lista chamada `filtradosMenorIdade`
- Segunda abordagem (Declarativa)
    - Filtramos as pessoas verificando quem é menor de idade
    - Mapeamos a nova listagem vinda do `filter` de forma recursiva colocando tudo para maiúsculo e retorna para `novaListagemMenoresDeIdade`.

Vai dizer. Fácil né.

## Conceitos chaves

### Funções de primeira classe

O objetivo é evitar o `state` e abstrair para ser o mais reutilizavel possível, aceitando até mesmo outras funções como argumento. De modo geral as funções `.map()` e `.filter()` fazem exatamente isto, aqui vai um exemplo do livro **Eloquent Javascript**:

```js
function greaterThan(n) {
    return function(m) {
        return m > n;
    };
}

var greaterThan10 = greaterThan(10);
```

A função `greaterThan` devolve uma função, então quer dizer que ela pode ser reutilizada, utilizando [clojure](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Guide/Closures) que é quando utilizamos aquela variável `n` dentro da segunda função `function(m){...}`


### Função Matemática ou Função Pura
Na matemática a função é relação entre as entradas e as saídas em que cada combinação de entrada seja exatamente a mesma saída. Na programação é a mesma coisa mas além disso **NÃO** alterar nada que esteja fora da função evitando assim efeitos colaterais.

```js
    function pegaMaiorNumero(a, b){
        return a > b ? a : b
    }

    pegaMaiorNumero(5, 30); // Output: 30
    pegaMaiorNumero(5, 30); // Output: 30
```

### Recursividade

FP não é FP sem a famosa recursividade. Recursividade nada mais é que um função que chama ela mesmo, olha só:

```js
    let lista = [1,2,3];

    // Sem recursividade
    for(let i=0; i < lista.length; i++){
        console.log(lista[i]); // Output: 1,2,3
    }


    // Com recursividade
    lista
        .forEach(numero => console.log(numero)); // Output: 1,2,3
```

Ela chama ela mesma até finalizar o array.

### Ditar O QUE ser feito e não COMO

No primeiro exemplo utilizamos o `for` "normal" e na segunda abordagem utilizam uma maneira de ditar o que devia ser feito sem ter que explicitar. Temos algumas funções como:

- Filter
- Reduce
- Map
- Some
- Find
- Every

Quer filtrar quem tem poder mais de 8.000 e logo depois pegar o que tem o maior poder dentre os filtrados? Sem problemas. 

```js
    let listaParaFiltrar = [100, 6000,30000,2000, 1000, 6050];

    function temMaisQuePoderMinimo(poderMinimo){
        return poder => poder > poderMinimo;
    }

    function pegaMaisPoderoso(prev, now){
        return prev > now ? prev : now;
    }

    let osMelhores = listaParaFiltrar
        .filter(temMaisQuePoderMinimo(8000))
        .reduce(pegaMaisPoderoso)

    console.log(osMelhores); // Output: 30000
```

### Efeitos Colaterais

Talvez o mais importante conceito da programação funcional, evitar fazer o que não deveria estar fazendo!

```js
    function adicionarPessoaNoBanco(pessoa){
        pessoa.ativa = true;

        // Lógica de adicionar no banco ...
        // bla bla bla
    }

    let pessoa = { nome: 'Damião' };

    adicionarPessoaNoBanco(pessoa);
```

Olha bem pra isto. Tá vendo algo errado? `pessoa.ativa = true`. Isto não deveria estar aqui, deveria? Como é que alguem vai saber que na hora que tu adicionar ele já vai colocar como ativa? Sou vidente? Vamos fazer algumas mudanças:

```js
    function adicionarPessoaNoBanco(pessoa){
        // Lógica de adicionar no banco ...
    }

    function colocaPessoaParaAtiva(pessoa){
        pessoa = Object.assign({}, pessoa);
        pessoa.ativa = true;
        return pessoa;
    }

    let pessoa = { nome: 'Damião', ativa: false };
    pessoa = colocaPessoaParaAtiva(pessoa);
    adicionarPessoaNoBanco(pessoa);
```

### Imutabilidade

O conceito supremo. A função não deve modificar o dado original! Sempre retorne o novo estado assim evita-se de trabalhar em um objeto onde algo já o modificou.

```js
    let pessoa = {
        nome: 'Duck'
    };

    // Errado!
    function alteraNomePessoaErrado(pessoa){
        pessoa.nome = 'Damião';
        return pessoa;
    }


    // Corretão
    function alteraNomePessoaCerto(pessoa){
        pessoa = Object.assign({}, pessoa);
        pessoa.nome = 'DJ Rogerinho'
        return pessoa;
    }

    alteraNomePessoaErrado(pessoa);
    console.log(pessoa.nome); // Output: Damião

    alteraNomePessoaCerto(pessoa);
    console.log(pessoa.nome); // Output: Damião
```

Percebeu que o `alteraNomePessoaCerto` não alterou o nome? Exatamente. Utilizamos um cara chamado `Object.assing` onde criamos uma nova referência em memória evitando assim trabalhar no objeto original.

## Exemplo Final

O objetivo é ir na API de cep, perguntar por um cep válido, tratar o retorno e dar um `console.log` do resultado.

```js
/**
 * Esta função cria um sistema de composição de função onde ao passar várias funções
 * ela executa uma em sequência da outra passando o resultado da função anterior 
 * como parâmetro para próxima.
 * */
function compose(...fn){
  return (objectToJob) => fn.reduce((ant, now)=> now(ant), objectToJob)
}

/**
 * Retorna uma Promise com o resultado da requisição em json
 * */
function getCepResponseDataInJSON(cepNumber){
    return fetch(`https://viacep.com.br/ws/${cepNumber}/json/`)
        .then(response => response.json());
}

/**
 * Retorna [uf] localidade - cep
 * ao passar um cep válido
 * */
function getCepInformationString(cepNumber){
    let getLocateAndUf = ({ localidade, uf, cep }) => ({ localidade, uf, cep }) ;
    let concatNameWithCep = ({ localidade, uf, cep }) => `[${uf}] ${localidade} - ${cep}`;

    return getCepResponseDataInJSON(cepNumber).then(response => {

        /** 
         * Executa getLocateAndUf pega o resultado e passa para concatNameWithCep
         * getLocateAndUf -> concatNameWithCep
         * 
         * O response ali no final serve para alimentar a primeira função no caso
         * a getLocateAndUf
         * 
         * Olhe como fica mais organizado perto de outras abordagens como
         * ----
         * let locateWithUf = getLocateAndUf(response);
         * let concated = concatNameWithCep(locateWithUf);
         * return concated;
         * --- ou
         * return concatNameWithCep(locateWithUf(response));
         * */
        return compose(getLocateAndUf, concatNameWithCep)(response);
    });
}

getCepInformationString('95555000')
    .then(console.log);
    // Output: [RS] Capão da Canoa - 95555-000
```

## Finalizando

Deixamos de passar em alguns conceitos bem legais, mas que considero mais avançados comos:
- Memoize
- Curry
- Compose
- Pipe
- Mônadas

Mas acho que por enquanto já foi mais do que necessário pra entender os conceito básicos. Caso tu queira algumas bibliotecas para deixar o Javascript mais legal ainda de trabalhar com programação funcional de uma olhada em:

- [Pareto JS](https://github.com/concretesolutions/pareto.js/)
- [Ramda JS](https://ramdajs.com/)


## Referências

- [Programação funcional para iniciantes](https://medium.com/trainingcenter/programa%C3%A7%C3%A3o-funcional-para-iniciantes-9e2beddb5b43)
- [Functional Programming in JavaScript](https://codeburst.io/functional-programming-in-javascript-e57e7e28c0e5)
- [FUNCTIONAL VS PROCEDURAL JAVASCRIPT](https://www.scalablepath.com/blog/javascript-functional-vs-procedural/)
- [Funções Puras - Programação Funcional: Parte 1](https://www.youtube.com/watch?v=BMUiFMZr7vk)