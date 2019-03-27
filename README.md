# Kieling

[![Netlify Status](https://api.netlify.com/api/v1/badges/6244d5e8-4935-4aad-aaf8-e40a07d2906d/deploy-status)](https://app.netlify.com/sites/kieling/deploys)

<p align="center">
    <a href="">Ainda não tem um link, irei colocar no ar em breve</a>
</p>

O intuito deste repositório é guardar o um blog sobre desenvolvimento, com estudos/pesquisas sobre coisas que eu gosto mas ao mesmo tempo passando conhecimento pra frente.

Utilizei apenas Vuepress para criar o blog, **não** tem utilização de banco de dados.

## Pegando a quantidade de caracteres de leitura

Utilizado para calcular o tempo de leitura. Gambiarra das mais top's

```js
Array.from(document.querySelectorAll('p')).reduce((a,n)=>{
	return a + n.textContent.length
},0)
```

## Contribuindo

Caso queira, fique a vontade para adicionar um `.md` dentro da pasta `src/.vuepress/posts/meuTitulo.md` e mandar um pull request.