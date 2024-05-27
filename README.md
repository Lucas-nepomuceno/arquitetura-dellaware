# MVC - LedTech/Dell
- <b> Nome do Projeto: </b> DellAware
- <b> Descrição: </b> Trata-se de uma aplicação web que será desenvolvida para a empresa Dell Technologies voltada a resolver o problema das pausas na linha de produção. Para tanto, disponibilizar-se-á, por meio da ação dos administradores, os manuais necessários para a linha de produção individualmente a cada montador da fábrica. Além disso, os montadores terão a chance de checar os manuais que já leram e os administradores verão o desempenho dos montadores em relação a leitura dos manuais.
- <b> Arquitetura: </b> MVC (Model-View-Controller)
- <b> Ferramenta de Diagramação: </b> draw.io

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

&nbsp;&nbsp;&nbsp;&nbsp; Nesta aplicação, os usuários serão divididos em <i> engineer </i>, <i> worker </i>, e <i> administrators </i>. Os administradores têm acesso aos seguintes controladores:
- create: adiciona um funcionário à lista de <code> worker </code> ou <code>engineer</code>:
  - Parâmetros de entrada: registrations, names, emails, birthdays, (lines), actives
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para adicionar um registro à tabela <code> worker </code>
  - View: cria um <i> worker's interface </i> para o novo montador

- getById: possibilita a visualização dos dados de um funcionário
  - Parâmetros de entrada: id (<code> worker </code> ou <code>engineer</code>)
  - Parâmetros de saída:  names, emails, birthdays, (lines), actives
  - Ações: Pedir ao model para consultar os dados de um funcionário sob o id da tabela <code> worker </code> ou <code>engineer</code>
  - View: Abre uma aba com os dados do funcionário

- getAll: possibilita a visualização dos dados de todos os funcionários de <code>worker</code> ou <code>engineer</code>
  - Parâmetros de entrada: N/A
  - Parâmetros de saída:  names, emails, birthdays, (lines), actives
  - Ações: Pedir ao model para consultar todos os dados de <code>worker</code> ou <code>engineer</code>
  - View: Atualiza a team

- update: atualiza um funcionário na lista de <code> worker </code> ou <code>engineer</code>
  - Parâmetros de entrada: id, registrations, names, emails, birthdays, (lines), actives
  - Ações: Pedir ao model para alterar um registro da tabela <code> worker </code> ou <code>engineer</code>
  - View: atualiza a team

- delete: exclui um funcionário da lista <code> worker </code> ou <code>engineer</code>
  - Parâmetros de entrada: id
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para deletar um registro da tabela <code> worker </code> ou <code>engineer</code>
  - View: exclui o<i> worker's interface </i> ou <i>engineer's dashboard</i> do montador ou engenheiro excluído, respectivamente

&nbsp;&nbsp;&nbsp;&nbsp; Já os engenheiros têm acesso aos seguintes controllers:

- create_manual: adiciona um manual à lista de manuais
  - Parâmetros de entrada: names, categories, sub_categories1, sub_categories2, sub_categories3, sub_categories4, sub_categories5, actives
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para adicionar um registro a tabela <code> manual </code>
  - View: altera o repositório de manuais, adicionando um manual

- update_manual: atualiza um manual já criado
  - Parâmetros de entrada: id (<code> manual </code>), date, update_descriptions, actives
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para alterar um registro da tabela <code> manual </code>
  - View: altera o repositório de manuais, atualizando-o; adiciona uma descrição da atualização aos funcionários que tinham o manual na sua lista de leitura e altera o interface do funcionário atualizando a leitura

- delete_manual: exclui um manual da tabela <code>manual</code>
  - Parâmetros de entrada: id
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para deletar um registro da tabela <code> manual </code>
  - View: exclui o manual do repositório

- getAll_manual: possibilita a visualização dos dados de todos os manuais
  - Parâmetros de entrada: N/A
  - Parâmetros de saída: id (<code> manual </code>), date, update_descriptions, actives 
  - Ações: Pedir ao model para consultar todos os dados de <code>manual</code>
  - View: Atualiza o repositorio

- getById_manual: possibilita a visualização dos dados de um manual 
  - Parâmetros de entrada: id
  - Parâmetros de saída: id (<code> manual </code>), date, update_descriptions, actives 
  - Ações: Pedir ao model para consultar todos os dados de <code>manual</code> sob o id requisitado
  - View: Abre uma aba com os dados
  
- create_file: adiciona um arquivo à lista de <code> file </code>
  - Parâmetros de entrada: id (<code> manual </code>), types, url
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para adicionar um registro a tabela <code> file </code>
  - View: altera o repositório de manuais, adicionando um arquivo dentro do respectivo manual

- delete_file: deleta um file já criado
  - Parâmetros de entrada: id (<code> file </code>)
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para deletar um registro da tabela <code> file </code>
  - View: altera o repositório de manuais, deletando um arquivo de dentro do respectivo manual

- delete_file: exclui um file da tabela <code>file</code>
  - Parâmetros de entrada: id
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para deletar um registro da tabela <code> file </code>
  - View: exclui o file dos manuais

- getById_file: possibilita a visualização dos dados de um manual 
  - Parâmetros de entrada: id
  - Parâmetros de saída: id (<code> manual </code>), types, url 
  - Ações: Pedir ao model para consultar todos os dados de <code>file</code> sob o id requisitado
  - View: Abre uma aba com os dados

- create_delegation: delega uma leitura a um montador
  - Parâmetros de entrada: registrations (<code> engineer </code>), registrations (<code> worker </code>), id (<code> manual </code>)
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para adicionar um registro a tabela <code> delegation </code>
  - View: altera o interface do montador, adicionando a leitura; altera a dashboard do administrador com novas informações

- delete_delegation: deleta uma delegation já criada
  - Parâmetros de entrada: id
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para deletar um registro da tabela <code> delegation </code>
  - View: altera o dashboard dos engenheiros


&nbsp;&nbsp;&nbsp;&nbsp; Já os montadores têm acesso aos seguintes controllers:
- already_read: dá um "check" no manual
  - Parâmetros de entrada: id (<code> delegation </code>)
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para atualizar o registro sob id (<code> delegation </code>), setando o atributo <i> done </i> como verdadeiro.
  - View: altera a interface do montador, "riscando" a tarefa da lista; altera o dashboard do administrador com novas informações
  
- acess: possibilita a leitura do manual
  - Parâmetros de entrada: id (<code> delegation </code>), id (<code> manual </code>)
  - Parâmetros de saída: names, types, url (<code> file </code>)
  - Ações: Pedir ao model para consultar os arquivos sob o registro id (<code> manual </code>)
  - View: Abre uma aba com os arquivos do manual

&nbsp;&nbsp;&nbsp;&nbsp; Além disso, engenheiros e montadores terão acesso ao seguinte controller:
- Auth: permite logar na aplicação
  - Parâmetros de entrada: emails e passwords
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para consultar o registro e <i>emails </i> e checar a senha nas tabelas <code> worker </code> e <code> engineer </code>
  - View: atualiza a view, redirecionando o usuário a seu respectivo interface

## Views (Views):

&nbsp;&nbsp;&nbsp;&nbsp; As views, ou seja, as interfaces as quais os usuários irão interagir são:
- Login: permitirá o usuário logar na aplicação;
- engineer_dashboard: permitirá o administrador delegar manuais da lista de leitura de seus funcionários e ver o desempenho deles;
- worker_interface: permitirá o montador ver sua lista de leitura, checar as leituras já feitas e acessar os manuais;
- repository: permitirá ao engenheiro adicionar, atualizar, ver e deletar manuais e arquivos desses respectivos manuais
- administrator_interface: permitirá ao administrador ver, adicionar, deletar e ver seus funcionários

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
