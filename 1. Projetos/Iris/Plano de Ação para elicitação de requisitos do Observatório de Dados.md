#### **Contexto**

Atualmente no projeto do Observatório de Dados, visualizamos uma divisão macro em três grandes frentes de trabalho: Requisitos, Backend e Frontend.

No momento, enfrentamos um desbalanceamento considerável entre essas frentes. A área de **Requisitos** está atrasada, o **Backend** está iniciando (devido a problemas de integração com o Acesso Cidadão), enquanto o **Frontend** já está bastante avançado. Esse cenário não é ideal, pois o Backend vai acabar sendo projetado com base em telas do Frontend, sem uma clara definição dos requisitos, o que pode comprometer a saúde e a evolução do sistema no longo prazo.

Adicionalmente, a pessoa responsável por definir a visão macro do projeto e validar as entregas com base nessa visão ainda não foi identificada, o que adiciona complexidade ao processo de elicitação dos requisitos.
#### **Motivações**

Para contornar os problemas indicados, proponho uma estratégia de elicitação alternativa, considerando dois caminhos principais:

1. **Seguir com a elicitação Tradicional**: Obter a visão macro do projeto diretamente com as pessoas de referência disponíveis (Se disponíveis), focando nas funcionalidades e expectativas mais conceituais do sistema.
   
2. **Aproveitamento do Conhecimento Técnico da Equipe**: Unificar as visões dos membros da equipe de desenvolvimento, que já possuem um entendimento técnico do produto. Assim, os requisitos mais técnicos serão extraídos em colaboração com a equipe, composta por especialistas em Desenvolvimento (Frontend e Backend), DevOps, Análise de Dados e gestão do projeto.

O objetivo geral é alinhar as expectativas do cliente com a capacidade técnica do time, criando uma base sólida para o desenvolvimento sustentável e eficiente do sistema, definindo um escopo e controlando as exceptivas referentes ao projeto.

---

### **Plano de Ação**

#### **Reunião de Quickoff**

- **Objetivo**: Identificar as partes interessadas e iniciar a coleta de visão e requisitos.
- **Participantes**: Todos os stakeholders, incluindo usuários finais, analistas de dados, gerentes do projeto, desenvolvedores, etc.
  
**Ações**:
1. **Solicitação de Documento de Página Única**:
   - Solicitar às partes interessadas um documento (Narrativa) que descreva, de forma concisa, as funcionalidades e expectativas de cada área ou persona que interagirá com o sistema.

2. **Entrega das Perguntas de Entendimento Geral do Projeto (Versão Cliente)**:
   - Entregar um conjunto de perguntas focadas em entender o projeto de maneira estratégica e macro, sem tecnicismos.

---

#### **Reuniões Focadas nas Equipes Técnicas**

- **Objetivo**: Coletar informações mais técnicas e detalhadas sobre as expectativas e decisões relacionadas à infraestrutura e arquitetura do sistema.
- **Participantes**: Equipes técnicas (Backend, DevOps, Análise de Dados, Frontend) e professores.

**Ações**:
1. **Apresentação das Perguntas Técnicas (Versão Servidor)**:
   - Apresentar perguntas específicas sobre integrações, segurança, escalabilidade, performance e análise de dados, com foco nos detalhes técnicos.
   
2. **Discussão e Validação Técnica**:
   - Discutir as estratégias tecnológicas, identificar gargalos e mapear expectativas e limitações técnicas baseadas na visão do cliente sobre o projeto.

---

#### **Análise de Personas e Refinamento dos Requisitos**

- **Objetivo**: Definir quem são os usuários do sistema, suas necessidades e o que esperam em termos de funcionalidades e interatividade.
- **Participantes**: Equipe de desenvolvimento + pessoas de referência do cliente.

**Ações**:
1. **Definição de Personas**:
   - Identificar e validar as personas que utilizarão o sistema, descrevendo suas necessidades e expectativas.
   
2. **Mapeamento de Funcionalidades**:
   - Relacionar as funcionalidades críticas a cada persona, considerando os diferentes perfis de usuários.

---

#### **Estabelecimento de Ciclos de Feedback

- **Objetivo**: Alinhar o desenvolvimento técnico com os requisitos levantados, garantindo que o que está sendo desenvolvido é aprovado pelas partes interessadas.
- **Participantes**: Equipe técnica, gerentes de projeto e partes interessadas.

**Ações**:
1. **Estabelecimento de Ciclos de Feedback**:
   - Garantir que as entregas sejam validadas continuamente pelas partes interessadas.
   
2. **Testes e Homologação**:
   - Validar as funcionalidades entregues com base nos critérios definidos anteriormente.
   
3. **Ajustes:
   - Realizar correções e ajustes com base no feedback e viabilidade.

---

### **Conclusão**

O plano de ação foi desenvolvido para garantir que o projeto avance de maneira equilibrada, abordando o descompasso atual entre as frentes de desenvolvimento. Com base na elicitação de requisitos, organização da equipe e validação contínua, esperamos alinhar o escopo e construir uma plataforma eficiente para o gerenciamento de dados de programas sociais.

---
# Anexos:
---
### **Versões das Perguntas de Elicitação**

#### **[1] Versão 1 - Perguntas para o Cliente (Foco no Macro)**

1. **Objetivo do Projeto**
   - Qual é o impacto social esperado com a criação da plataforma?
   - Como o sistema ajudará a melhorar a execução dos programas sociais?

2. **Usuários**
   - Quem utilizará essa plataforma no dia a dia?
   - Quais necessidades esses usuários têm que a plataforma deve resolver?

3. **Integração de Dados**
   - Quais tipos de dados você espera ver integrados na plataforma?
   - Quem fornecerá os dados? Serão de fontes públicas ou privadas?

4. **Geração de Informações**
   - Que tipo de informações e relatórios você espera visualizar nos painéis da plataforma?
   - Como esses dados serão úteis para gestores e cidadãos?

5. **Interatividade e Personalização**
   - Como os usuários poderão customizar os relatórios e visualizações?
   - Que tipos de filtros e opções de segmentação serão importantes?

6. **Segurança**
   - Que tipo de acesso os diferentes usuários terão na plataforma?
   - Quais dados precisam de maior proteção?

7. **Escalabilidade e Futuro**
   - Qual a expectativa de crescimento para o volume de dados nos próximos anos?
   - A plataforma precisará se integrar com outras ferramentas no futuro?

---

#### **[2] Versão 2 - Perguntas para a Equipe Técnica (Foco no Detalhe)**

1. **Objetivo do Projeto**
   - Qual é a arquitetura ideal para garantir que a plataforma suporte os requisitos de performance e segurança?
   - Como garantir a integridade e a escalabilidade do sistema ao longo do tempo?

2. **Integração de APIs**
   - Quais serão as origens das APIs a serem integradas? Haverá fontes públicas, privadas ou mistas?
   - Quais são os requisitos de segurança e conformidade que as APIs deverão seguir?

3. **Tecnologia de Dashboards**
   - Quais tipos de componentes de visualização (gráficos, mapas, tabelas) o dashboard deve suportar?
   - Como garantir a personalização de layout, cores e organização dos componentes no dashboard?

4. **Personalização e Interatividade**
   - Quais perfis de usuário poderão modificar os dashboards? Como gerenciar as permissões?
   - Como implementar filtros dinâmicos e segmentação de dados eficiente para grandes volumes?

5. **Segurança e Controle de Acesso**
   - Quais níveis de permissão precisarão ser implementados? Como proteger os dados mais sensíveis?
   - Quais padrões de segurança devem ser seguidos para o cadastro e o uso de APIs?

6. **Escalabilidade**
   - Qual o volume de dados esperado e como o sistema deve ser dimensionado para suportar o aumento de dados e usuários?
   - Quais estratégias serão usadas para manter a performance conforme a plataforma cresce?