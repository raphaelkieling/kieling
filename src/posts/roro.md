---
title: RORO Pattern
date: 26/03/2019
autor: Raphael Kieling Tondin
nc: 1379
---

# RORO Pattern

<description-post/>

![beer](https://philna.sh/assets/posts/destructured_beers-e79981058aae8ee2744370c5dc0951352039658395b46c74aaa2ba9cfe6aadd7.jpg)

Logo que comecei a trabalhar na empresa (em 2018) que estou hoje utilizando PHP, eu via um tanto de funções assim:

```php
// Anything file.php
$this->save(false);
$this->getAll(false);
Person->getName(true, false);
```

Agora vai a pergunta de um milhão de dólares. Que porra é esse `false` e `true` que tá sendo passado por parâmetro, o que elas fazem? Vamos melhorar isto logo em seguida.

## Sumário

- [O que é?](#o-que-e)
- [Parâmetros Nomeados](#parametros-nomeados)
- [Parâmetros Defaults](#parametros-defaults)
- [Valores de retorno mais ricos](#valores-mais-ricos)
- [Finalizando](#finalizando)

## O que é?

RORO ou `Receive an object, return an object` sendo traduzido para `Receba um objeto, retorne um objeto`. É um pattern que se utiliza de algo MUITO legal no javascript, o `destructuring`. Este artigo foi baseado em um artigo em inglês do Bill Sourour que achei muito foda e deixei ali nas referências caso queira dar uma olhada.

```js
    // No
    let save = (person, returnSaved) => {
        // logic to save, generated pessoaSaved
        if(returnSaved) return pessoaSaved;
    }

    save(personInstance, false);

    // Yeah!
    let save = ({ person, returnSaved=true }) => {
        // logic to save, generated pessoaSaved
        if(returnSaved) return pessoaSaved;
    }

    save({ 
        person: personInstance,
        returnSaved: true
    });
```

Caramba, muito mais claro não acha? Isso traz algumas vantagens como:

- Parâmetros nomeados
- Parâmetros default mais limpos
- Valores retornados mais ricos
- Facil pra fazer composição de funções (será abordado em outro artigo sobre composição)

### Parâmetros nomeados

```js
    // No
    function getAll(active, role, withJob){...}
    getAll(true, false, true); // Ai complica... que tal

    // Yeah!
    function getAll({ active, role, withJob }){...}
    getAll({ 
        active: true,
        withJob: false
    }); // Ai ficou show!!
```

Pera ai. Tu viu que eu esqueci de passar `withJob` na ultima função? Brincadeira, isso ai foi gancho pro outro tópico hehe

### Parâmetros Defaults

O destructuring nos da possibilidade de passar o que a gente quiser! Isto porque ele vai tentar encaixar o que ele tá mandando com o que a função está pedindo, melhor ainda ele também vai colocar valores defaults caso tu não mande alguns parâmetros necessários como:

```js
    let save = ({ person, active = true }) => {...}
    save({ person: new Person() })
```
Então já que mandamos só `person` o parâmetro `active` já vai iniciar como `true`!

### Valores mais ricos

Auto explicativo:

```js
    // No
    let save = ({ person, active }) =>{
        return true;
    }

    // Yeah!
    let save = ({ person, active }) =>{
        // logic to save in database
        return {
            operation: 'INSERT',
            saved: personSavedReturn,
            success: true 
        }
    }
```

## Finalizando

O pattern é muito útil, acho meio óbvio mas vou reforçar... ele é um pattern pra te ajudar a resolver problemas, não é preciso fazer isto em TODO lugar a TODO momento em TODO caso. Exemplo:

```js
    let isNumber = ({ value }) => ...
```

Precisa mesmo passar um `{ value: 2 }`?, acho que não.

Até a próxima

## Referências

- [Elegant patterns in modern JavaScript: RORO
](https://medium.freecodecamp.org/elegant-patterns-in-modern-javascript-roro-be01e7669cbd)
- [Reddit discutindo sobre o artigo](https://www.reddit.com/r/javascript/comments/81zygu/elegant_patterns_in_modern_javascript_roro/)