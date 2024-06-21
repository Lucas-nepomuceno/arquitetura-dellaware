# MVC - LedTech/Dell
- <b> Nome do Projeto: </b> DellAware
- <b> Descrição: </b> Trata-se de uma aplicação web que será desenvolvida para a empresa Dell Technologies voltada a resolver o problema das pausas na linha de produção. Para tanto, disponibilizar-se-á, por meio da ação dos engenheiros, os manuais necessários para a linha de produção individualmente a cada montador da fábrica. Além disso, os montadores terão a chance de checar os manuais que já leram e os engenheiros verão o desempenho dos montadores em relação a leitura dos manuais.
- <b> Arquitetura: </b> MVC (Model-View-Controller)
- <b> Ferramenta de Diagramação: </b> draw.io

<div align="center">
<sub>Figura 1 - Arquitetura MVC</sub> <br>
  
<img width="720" alt="Imagem da arquitetura feita no draw.io" src="/assets/arquitetura-mvc.png">

<sup>Material produzido pelos autores (2024)</sup>
</div>

## Modelos (Models):

&nbsp;&nbsp;&nbsp;&nbsp; Os modelos desse projeto apresentam 3 tabelas independentes: <code> engineer </code>, <code> worker </code> e <code> manual </code>. Uma tabela dependente <code> file </code> e uma tabela por associação <code> delegation </code>. Respectivamente, seus atributos são:
- <code> engineer </code>: id, registrations, names, emails, passwords, birthdays, actives;
- <code> worker </code>: id, registrations, names, emails, passwords birthdays, lines, actives;
- <code> manual </code>: id, names, categories, sub_categories1, sub_categories2, sub_categories3, sub_categories4, sub_categories5, update_descriptions, actives;
- <code> file </code>: id, manuals_id, names, types, url;
- <code> delegation </code>: id, engineers_id, workers_id, manuals_id, doing, done
&nbsp;&nbsp;&nbsp;&nbsp; Em relação às tabelas com chaves estrangeiras, espera-se que <code> enginners </code> tenha o relacionamento de delegar com <code> delegation </code> e <code>worker</code> e <code>manual</code> tenham a relação de delegação com a mesma. Além disso, espera-se que <code> manual </code> contenham <code> file </code>, ou seja, cada file tenha uma correspondência em um manual. Estes relacionamentos estão expostos no seguinte modelo conceitual:

<div align="center">
<sub>Figura 2 - Modelo conceitual</sub> <br>
  
<img width="720" alt="modelo-conceitural-bd" src="/assets/modelo-conceitual.png">

<sup>Material produzido pelos autores (2024)</sup>
</div>

## Controladores (Controllers):

&nbsp;&nbsp;&nbsp;&nbsp; Para essa aplicação, criou-se seis controllers que possuem os seguintes métodos.

### Auth

Login: permite logar na aplicação
  - Parâmetros de entrada: emails e passwords
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para consultar o registro e <i>emails </i> e checar a senha nas tabelas <code> worker </code> e <code> engineer </code>
  - View: atualiza a view, redirecionando o usuário a seu respectivo interface


### Enginner

- create: adiciona um engenheiro à tabela de <code>engineer</code>:
  - Parâmetros de entrada: registrations, names, emails, birthdays, actives
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para adicionar um registro à tabela <code> engineer</code>
  - View: permite acesso ao fluxo de engenheiro ao novo engenheiro

- getById: possibilita a visualização dos dados de um engenheiro
  - Parâmetros de entrada: id (<code>engineer</code>)
  - Parâmetros de saída:  registrations, names, emails, birthdays, actives
  - Ações: Pedir ao model para consultar os dados de um funcionário sob o id da tabela <code>engineer</code>
  - View: N/A

- getAll: possibilita a visualização dos dados de todos os funcionários de <code>engineer</code>
  - Parâmetros de entrada: N/A
  - Parâmetros de saída:  registrations, names, emails, birthdays, actives
  - Ações: Pedir ao model para consultar todos os dados de <code>engineer</code>
  - View: N/A

- update: atualiza um funcionário na tabela de <code>engineer</code>
  - Parâmetros de entrada: id, registrations, names, emails, birthdays, actives
  - Ações: Pedir ao model para alterar um registro da tabela <code>engineer</code>
  - View: N/A

- delete: exclui um funcionário da tabela de <code>engineer</code>
  - Parâmetros de entrada: id
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para deletar um registro da tabela <code>engineer</code>
  - View: exclui a rota privada do engenheiro deletado

### Worker

- create: adiciona um montador à tabela de <code>worker</code>:
  - Parâmetros de entrada: registrations, names, emails, birthdays, lines, actives
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para adicionar um registro à tabela <code>workers</code>
  - View: permite acesso ao fluxo de montador ao novo montador/altera os funcionários da view de delegação e funcionários

- getById: possibilita a visualização dos dados de um montador
  - Parâmetros de entrada: id (<code>montador</code>)
  - Parâmetros de saída:  registrations, names, emails, birthdays, lines, actives
  - Ações: Pedir ao model para consultar os dados de um funcionário sob o id da tabela <code>workers</code>
  - View: N/A

- getAll: possibilita a visualização dos dados de todos os funcionários de <code>montador</code>
  - Parâmetros de entrada: N/A
  - Parâmetros de saída:  registrations, names, emails, birthdays, lines, actives
  - Ações: Pedir ao model para consultar todos os dados de <code>workers</code>
  - View: N/A

- update: atualiza um funcionário na tabela de <code>montador</code>
  - Parâmetros de entrada: id, registrations, names, emails, birthdays, actives
  - Ações: Pedir ao model para alterar um registro da tabela <code>workers</code>
  - View: altera os funcionários da view de delegação e funcionários

- delete: exclui um funcionário da tabela de <code>montador</code>
  - Parâmetros de entrada: id
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para deletar um registro da tabela <code>montador</code>
  - View: exclui a rota privada do montador deletado/ altera os funcionários da view de delegação e funcionários


### Manual

- create: adiciona um manual à tabela de <code>manuals</code>:
  - Parâmetros de entrada: names, categories, sub_categories1, sub_categories2, sub_categories3, sub_categories4, sub_categories5, update_descriptions, active
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para adicionar um registro à tabela <code>manual</code>
  - View: Altera a view de select manual/repository

- getById: possibilita a visualização dos dados de um montador
  - Parâmetros de entrada: id (<code>montador</code>)
  - Parâmetros de saída:  registrations, names, emails, birthdays, lines, actives
  - Ações: Pedir ao model para consultar os dados de um funcionário sob o id da tabela <code>montador</code>
  - View: N/A

- getAll: possibilita a visualização dos dados de todos os manuais de <code>manuals </code>
  - Parâmetros de entrada: N/A
  - Parâmetros de saída:  names, categories, sub_categories1, sub_categories2, sub_categories3, sub_categories4, sub_categories5, update_descriptions, active
  - Ações: Pedir ao model para consultar todos os dados de <code>montador</code>
  - View: N/A

- update: atualiza um funcionário na tabela de <code>montador</code>
  - Parâmetros de entrada: names, categories, sub_categories1, sub_categories2, sub_categories3, sub_categories4, sub_categories5, update_descriptions, active
  - Parâmetros de saída:  N/A
  - Ações: Pedir ao model para alterar um registro da tabela <code>manuals</code>
  - View: Altera a view de select manual/repository

- delete: exclui um manual da tabela de <code>manuals</code>
  - Parâmetros de entrada: id
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para deletar um registro da tabela <code>manuals</code>
  - View: Altera a view de select manual/repository

### Delegation

- getById: possibilita a visualização dos dados de uma delegação
  - Parâmetros de entrada: id (<code>delegation</code>)
  - Parâmetros de saída:  doing, done, engineers_id, workers_id, manuals_id
  - Ações: Pedir ao model para consultar os dados de um funcionário sob o id da tabela <code>delegations</code>
  - View: N/A

- getAll: possibilita a visualização dos dados de todos os manuais de <code>manuals </code>
  - Parâmetros de entrada: N/A
  - Parâmetros de saída: doing, done, engineers_id, workers_id, manuals_id
  - Ações: Pedir ao model para consultar todos os dados de <code>manuals</code>
  - View: N/A

- create: delega uma leitura a um montador
  - Parâmetros de entrada: registrations (<code> engineer </code>), registrations (<code> worker </code>), id (<code> manual </code>)
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para adicionar um registro a tabela <code> delegation </code>
  - View: altera o interface do montador, adicionando a leitura; altera a dashboard do engenheiro com novas informações

- update: atualiza uma delegation já criada
  - Parâmetros de entrada: doing, done
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para atualizar um registro da tabela <code> delegations </code> a depender do progresso do montador na sua leitura
  - View: altera o dashboard dos engenheiros e move o card no kanban do montador
 
- search: pesquisa delegações com base no id do montador e faz um join com manuals_id 
 - Parâmetros de entrada: workers_id
 - Parâmetros de saída:  doing, done, engineers_id, workers_id, names, categories, sub_categories1, sub_categories2, sub_categories3, sub_categories4, sub_categories5, update_descriptions, active
 - Ações: Pedir ao model para consultar todos os registros da tabela <code>delegations</code> sob o id (<code>workers</code>) e fazer um join com a tabela <code>manuals</code> onde manuals_id = id (<code>manuals</code>)
 - View: aparecem delegações personalizadas no kanban dos funcionários

- getDoing: consulta a quantidade de delegações em que doing = true.
 - Parâmetros de entrada: N/A
 - Parâmetros de saída: número
 - Ações: Pedir ao model para retornar a quantidade de delegações com a linha na coluna doing igual a verdadeiro.
 - Views: Muda o dashboard do engenheiro

- getDone: consulta a quantidade de delegações em que done = true.
 - Parâmetros de entrada: N/A
 - Parâmetros de saída: número
 - Ações: Pedir ao model para retornar a quantidade de delegações com a linha na coluna done igual a verdadeiro.
 - Views: Muda o dashboard do engenheiro

- getByManual: consulta as delegações que possuem um manual específico.
 - Parâmetros de entrada: id (<code>manual</code>)
 - Parâmetros de saída: id, doing, done, engineers_id, workers_id, names, manuals_id
 - Ações: Pedir ao model para retornar as delegações que possuem um manual específico
 - Views: N/A

## Views (Views):

&nbsp;&nbsp;&nbsp;&nbsp; As views, ou seja, as interfaces as quais os usuários irão interagir são:
- Login: permitirá o usuário logar na aplicação;
- engineer_dashboard: permitirá o engenheiro ver o desempenho de seus funcionários;
- Delegations: permitirá delegar manuais da lista de leitura aos seus funcionários.
- worker_interface: permitirá o montador ver sua lista de leitura, checar as leituras já feitas e acessar os manuais;
- repository: permitirá ao engenheiro adicionar, atualizar, ver e deletar manuais e arquivos desses respectivos manuais

## Infraestrutura:

&nbsp;&nbsp;&nbsp;&nbsp; Neste projeto, utilizamos o software Render para hospedar nosso banco de dados criado em PostgreSQL, o Dbeaver como Sistema de Gerenciamento de Banco de Dados (SGBD), o Sails.js como framework, o Node.js como <i>runtime environment</i> e o HTML5 e CSS3 para a construção da UI. Essas tecnologias se relacionam à arquitetura MVC da seguinte forma:
- HTML5 e CSS3: View
- Sails.js: Controller/model
- Dbeaver: Model
- Render: Server
- Node.js: runtime environment

&nbsp;&nbsp;&nbsp;&nbsp; Isso foi feito levando em consideração as tecnologias disponibilizadas pela instituição e a trilha de aprendizagem do módulo. Preferiu-se, também, o uso de tecnologias "open source", como o Sails.js e o Node Js. Com relação ao impacto no projeto, a integração das tecnologias escolhidas à arquitetura MVC proporciona uma estrutura robusta para o projeto. O uso do framework Sails.js agiliza o desenvolvimento ao oferecer funcionalidades predefinidas para lidar com a lógica de negócios e interação com o banco de dados. Além disso, a adoção de tecnologias de código aberto reduz os custos e aumenta a flexibilidade do projeto, permitindo adaptações conforme necessário. Essas decisões combinadas promovem uma implementação eficiente e adaptável, alinhada às exigências do projeto e as habilidades da equipe.

## Implicações da Arquitetura:

&nbsp;&nbsp;&nbsp;&nbsp; A arquitetura Model-View-Controller (MVC) traz implicações importantes para o projeto "DellAware" da LedTech/Dell em termos de escalabilidade, manutenção, testabilidade e colaboração entre equipes de desenvolvimento. Com a separação clara de responsabilidades entre Model, View e Controller, o projeto se torna mais escalável. É possível escalar diferentes partes do sistema independentemente umas das outras, respondendo de forma eficiente a mudanças na demanda ou no volume de dados. De forma semelhante, em relação à manutenção, a divisão em três componentes distintos simplifica as atualizações e correções de bugs. As alterações podem ser feitas em cada componente de forma independente, sem afetar diretamente as outras partes do sistema. Isso torna o processo de desenvolvimento mais ágil e menos propenso a introduzir novos problemas. <br>
&nbsp;&nbsp;&nbsp;&nbsp; A testabilidade também é beneficiada pela arquitetura MVC. Cada componente pode ser testado de forma isolada, garantindo que eles estejam funcionando corretamente e interagindo entre si da maneira esperada. Isso facilita a detecção e correção de erros durante o processo de desenvolvimento, garantindo a qualidade do software final. Além disso, a adoção do padrão MVC facilita a colaboração entre equipes de desenvolvimento. Com responsabilidades claramente definidas para cada componente, as equipes podem trabalhar de forma mais eficiente e coordenada, focando em suas áreas de especialização e contribuindo para o projeto de maneira mais eficaz. <br>
&nbsp;&nbsp;&nbsp;&nbsp; Em resumo, a arquitetura MVC proporciona uma estrutura sólida para o desenvolvimento do projeto "DellAware", oferecendo benefícios significativos em termos de escalabilidade, manutenção, testabilidade e colaboração entre equipes de desenvolvimento. Isso contribui para a criação de um software robusto, flexível e de alta qualidade.

