# Introdução

O =={ sistema }== é um sistema de =={ descrição breve do sistema }==. Conta com funcionalidades =={ apresentação das funcionalidades }==. 
# Arquitetura

A =={ tecnologia }== utilizada para a implementação do sistema é o =={ descrever a tecnologia e suas principais características }==. 

Para o armazenamento, =={ Descrever }==

=={ Qualquer outra informação relevante de arquitetura  }==
# Funcionalidades

| Funcionalidades     | Comportamento Esperado                                                                                                                                                                                                                                                                                                                                                                                                                               | Verificações                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Critérios de Aceite                                                             |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| Ex. Cadastro        | Ao digitar email, nome completo, usuário e senha irá efetuar um cadastro na plataforma e o usuário deverá ser redirecionado para a tela de login.<br><br>  <br><br>Deve indicar o campo obrigatório a ser corrigido pelo usuário.                                                                                                                                                                                                                    | - Senha min 8 caracteres e no máximo 18<br>    <br>- Todos os campos devem ser obrigatórios.<br>    <br>- Exibir uma mensagem de confirmação em caso positivo.<br>    <br>- Redirecionar o usuario para tela de login.<br>    <br>- Exibir a mensagem de falha em caso de usuário existente. <br>    <br>- Exibir mensagem de falha em caso de confirmação de senha não ser igual<br>    <br>- Exibir mensagem de falha no caso de campo obrigatório incompleto. |                                                                                 |

# Estratégia de Teste

## Escopo de Testes

O plano de testes abrange todas as  funcionalidades descritas na tabela acima. Esse plano de testes exclui =={ especificar funcionalidades que não serão cobertas }==.

Serão executados testes nos níveis conforme a descrição abaixo: =={ Descrever o níveis do teste, abaixo seguem exemplos }==

**Testes Unitários:** o código terá uma cobertura de 60% de testes unitários, que são de responsabilidade dos desenvolvedores.

**Testes de Integração:** Serão executados testes de integração em todos os endpoints, e esses testes serão de responsabilidade do time de qualidade.

**Testes Automatizados:** Serão realizados testes end-to-end na funcionalidade de Login.

**Testes Manuais:** Todas as funcionalidades serão testadas manualmente pelo time de qualidade seguindo a documentação de Cenários de teste e destes plano de teste. 

**Versão Beta:** Será lançada uma versão beta para 20 usuários pré-cadastrados antes do release. 

## Ambiente e Ferramentas

Os testes serão feitos do ambiente de homologação, e contém as mesmas configurações do ambiente de produção com uma massa de dados gerada previamente pelo time de qualidade.

As seguintes ferramentas serão utilizadas no teste:

=={Exemplo de tabela de ferramentas}==

| Ferramenta | Time            | Descrição                                   |
| ---------- | --------------- | ------------------------------------------- |
| POSTMAN    | Qualidade       | Ferramenta para realização de testes de API |
| Jasmine    | Desenvolvimento | Framework utilizada para testes unitários   |
| Selenium   | Qualidade       | Ferramenta para testes end-to-end           |

# Classificação de Bugs

Os Bugs serão classificados com as seguintes severidades:

| ID  | Nivel de Severidade | Descrição                                                                                                                                                                                  |
| --- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | Blocker             | - Bug que bloqueia o teste de uma função ou feature causa crash na aplicação.<br>    <br>- Botão não funciona impedindo o uso completo da funcionalidade.<br>    <br>- Bloqueia a entrega. |
| 2   | Grave               | - Funcionalidade não funciona como o esperado<br>    <br><br>- Input incomum causa efeitos irreversíveis                                                                                   |
| 3   | Moderada            | - Funcionalidade não atinge certos critérios de aceitação, mas sua funcionalidade em geral não é afetada<br>    <br><br>- Mensagem de erro ou sucesso não é exibida                        |
| 4   | Pequena             | - Quase nenhum impacto na funcionalidade porém atrapalha a experiência <br>    <br><br>- Erro ortográfico<br>    <br>- Pequenos erros de UI                                                |
# Definição de Pronto 

=={ Definir critérios de aceite da aplicação }==
Será considerada pronta as funcionalidades que passarem pelas verificações e testes descritas nestes plano de testes, não apresentarem bugs com a severidade acima de Minor, e passarem por uma validação de negócio de responsabilidade do time de produto.