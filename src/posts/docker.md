---
title: Iniciando com Docker e Node
date: 26/03/2019
autor: Raphael Kieling Tondin
private: true
---

# Iniciando com Docker e Node

<description-post/>

Docker além de ser uma empresa é também um ferramenta muito utiliza hoje em dia. Ela trabalha com um sistema de containers que nôs faz lembrar muito as famosas VMs.

Antes de qualquer linha de código vamos entender com calma o que são esses bichos.

## Sumário

...

## Pré-requisitos
- Windows 10 PRO / Ubuntu

## Por que eu gastaria meu tempo estudando isto?
A utilização dos containers é muito ampla mas as principais vantagens dela são:
- Produtividade elevada para colocar sistemas em produção
- Menos uso de memória que as VMs
- Maior poder de orquestração, podendo parar ou iniciar um container de forma muito rápida.
- Clusterização automática, onde ela sobe um clone da tua aplicação pra receber requisições. Evitando assim sobrecarregar um única aplicação.
- Sistema de cache tornando os deploys ainda mais rápidos
- Compatibilidade e manutenabilidade
- Deploy Contínuo e testes
- Portabilidade, tendo muitas `multi-clound platforms` disponíveis

## Qual a diferença entre VM e Container?

São muito similares até certo porto, elas tem isolamento e são auto contidas podendo ser executadas em qualquer lugar. Além disso elas removem a necessidade de mais hardware. Imagina ter mais de um servidor

![Docker Vs VM](https://blog.apiki.com/wp-content/uploads/sites/2/2017/01/docker-vs-vm.png)

> lado direito (VM) e lado esquerdo (Container)

## Referências
- [Top 10 Benefits of Docker](https://dzone.com/articles/top-10-benefits-of-using-docker)
- [A Beginner-Friendly Introduction to Containers, VMs and Docker](https://medium.freecodecamp.org/a-beginner-friendly-introduction-to-containers-vms-and-docker-79a9e3e119b)