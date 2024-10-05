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



