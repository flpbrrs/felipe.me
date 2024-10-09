---
tags:
  - Arquitetura
  - DDD
data de criação: 2024-10-03
---
> É um modelo de software do domínio do negócio muito ==especifico== em que você está trabalhando. Costuma ser implementado como ==um modelo de objeto==, quando esses objetos têm ==dado== e ==comportamentos== com um significado literal e preciso de negócio.

# Modelos anêmicos

O sintoma básico de um modelo anêmico é que ele ==se parece com um modelo real==. Existem objetos que até usam substantivos do espaço do domínio, o problema surge quando se olha para a ==ausência de comportamentos==, tornando-os nada mais do que ==sacos de getters e setters==

# Entidades

> Projetamos um conceito de domínio como um **Entidade** quando nos preocupamos com sua individualidade, e diferenciá-la de todos os outros objetos em um sistema é uma restrição obrigatória.

Ex.: Paciente, Consulta, Exame, Medicação

Uma entidade é definida por sua **identidade** (atributo especifico, como id) e não por seus **atributos**.

Exemplo:
```typescript
export default class Pessoa {
    constructor(
        public nome: string,
        public id?: string
    ) { }
}
```
# Objetos de valor

Um objeto de valor que sua identidade está no conjunto de todos os seus valores.

O ideal é que dentro de nossas entidades estejam os objetos de valores ao invés de outras entidades.

>[!tip] Não pensar de forma muito genérica. É mais proveitoso lidar diretamente com o caso que se está trabalhando, evitando muitas generalizações.

# Serviços de domínio

Devemos dar preferência a colocar nossas regras de negócios nos objetos de valor e nas entidades, contudo algumas regras extrapolam esse escopo, as vezes por envolver mais de uma entidade ou uma lista de entidades, e precisamos de um novo conceito para esses casos.

É ai que surgem os serviços de domínio, que são:

> Operações sem estado que realizam uma tarefa especifica de domínio. Frequentemente a melhor indicação de que você deve criar um **Serviço** no modelo de domínio é quando a operação que você precisa executar parece despropositada como um método em um **Agregado** ou um **Objeto de valor.**

Não confundir ==Serviços de domínio== com ==Serviços de aplicação== (Casos de uso). Não queremos hospedar regras de negócios em um serviço de aplicação. Além disso, um serviço de domínio não deve ser associado a lógicas pesadas, rudimentar e com capacidades remotas.