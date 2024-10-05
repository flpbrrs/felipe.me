---
tags:
  - Testes
data de criação: 2024-10-05
---
# O que é um teste?

É a validação de uma funcionalidade do código, seja feito via manual ou com o uso de ferramentas.

# Fluxos de testes

Em geral, as funcionalidades de software seguem um fluxo de uso, devemos então conhecer esse fluxo para desenvolver testes apropriados para todos os cenários da funcionalidade. Essa tarefa fica mais fácil se temos o conhecimento dos requisitos do nosso sistema.

Na criação do nosso fluxo, criaremos uma arvore de cenários de testes, onde um acontece dependendo de certas ações do usuário.

**Um exemplo de fluxo:**
![[Pasted image 20241005090338.png]]

Uma forma análoga ao fluxo é a tabela de decisão:
![[Pasted image 20241005090518.png]]

# Casos de teste

Podemos estruturar nossos testes em uma estrutura lógica que indica tudo que é necessário para a realização do teste, bem como tudo que se espera após a realização do teste.

Segue um exemplo de caso de teste:
![[Pasted image 20241005090713.png]]
![[Pasted image 20241005090802.png]]

Uma forma mais semântica de obter o mesmo resultado seria usar técnicas como o BDD - Desenvolvimento Guiado por Comportamento, que usa a seguinte estrutura:

**DADO - QUANDO/E - ENTÃO**:
**Dado**: Quais pré-condições devem ser verdadeiras para que eu execute o teste?
**Quando/E**: Quais ações serão executadas no sistema que fornecerá o resultado valido?
**Então**: De acordo com a ação disparada qual o resultado esperado?

Os casos e planos de teste devem ser explicitados no [[Plano de testes (Modelo)]].

