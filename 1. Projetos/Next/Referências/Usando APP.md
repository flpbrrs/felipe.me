---
tags:
  - Next
data de criação: 2024-09-23
---
Nem tudo que está dentro da pasta `app` será uma página (rota), assim como era na pasta `pages`. Agora as rotas seguem uma convenção de nomes:

```
🗀 pag_name
	∟ 🗋 page.tsx /* Será gerado a rota pag_name */
```
## Páginas e layouts

O `layout` presente na pasta `app`, ou o `root_layout` é um arquivo obrigatório. Ele é um englobador da aplicação, tudo aplicado a ele será aplicado em todas as rotas da aplicação.

Os `latouts` são hierarquizáveis, ou seja, a aplicação é compostas por `layouts` um dentro de outro, onde dentro desses layouts estarão presentes os elementos das nossas páginas.

## Grupos de rotas

 Sabemos que o Next trabalha com uma hierarquia de pastas que refletem nas rotas de nossa aplicação.

```
🗀 (interno)
	∟ 🗀 landing
		∟ 🗋 page.tsx
```
 	
 Resulta na rota: `host/interno/landing`
 
 Mas, caso quisermos criar uma separação física das nossas pastas sem que reflitam nas nossas rotas, podemos usar a convenção `( )` ao redor da página.
 
 Sendo assim, o nome da pasta não aparece mais na URL.

Além disso, o arquivo `page` no raiz representa a raiz da aplicação, contudo ela não é obrigatória estar ali. Podemos mover esse arquivo para dentro de um parte da nossa hierarquia de pastas, onde assumirá o papel de root, basta que não esteja dentro de um pasta que represente uma nova parte da rota.

## Reconhecendo a rota onde estou

