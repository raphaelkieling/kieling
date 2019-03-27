---
title: v-cloak VueJS
description: v-cloak VueJS
date: 26/03/2019
autor: Raphael Kieling Tondin
---

# v-cloak VueJS

<description-post/>

`v-cloak` é um diretiva que ficará atrelada em todos os componentes enquanto eles não estiverem finalizados. Infelizmente ele não vem por default e precisamos colocar na mão. Os exemplos foram retirados [daqui](https://medium.com/vuejs-tips/v-cloak-45a05da28dc4).

### O problema

Quando o `VueJS` não é instanciado não carrega ele vai acabar mostrando o conteúdo `html` sem lógica mesmo. Isso pode acontecer em outros caras como o `Twig` do symfony onde existe um problema de renderização bem visível, onde o componente inicia com html e espera o `VueJS` vir trabalhar nele. 

Vamos simular um problema, forçando um renderização atrasada.

<iframe width="100%" height="300" src="//jsfiddle.net/neves/ykepd525/embedded/html,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

### Resolvendo

Vamos adicionar um css para esconder ele enquanto estiver em processo de renderização:

```css
[v-cloak] > * { display:none }
[v-cloak]::before { content: "loading…" }
```

<iframe width="100%" height="300" src="//jsfiddle.net/4f7ae11y/embedded/html,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>


## Finalizando

- O `v-cloak` é apenas um classe no final de contas, utiliza seletores css a vontade.
- Não utilize ele para aguardar requisições ou estado de objetos, o `v-if` cumpre bem o seu papel.
- Não adicione em atributos como `img` provavelmente a imagem irá carregar bem depois.


## Referências

- [How do I hide the VueJS syntax while the page is loading?](https://stackoverflow.com/questions/36186831/how-do-i-hide-the-vuejs-syntax-while-the-page-is-loading)
- [Hide elements during loading using "v-cloak"](http://vuetips.com/v-cloak-directive-hides-html-on-startup)
- [v-cloak](https://medium.com/vuejs-tips/v-cloak-45a05da28dc4)
- [v-cloak vue api](https://vuejs.org/v2/api/#v-cloak)