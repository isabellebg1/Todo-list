# Projeto API REST para o BootCamp Decola Tech da Avanade 

# Introdução 
Projeto feito para demonstrar o uso de ferramentas Java, incluindo Spring Data JPA, OpenAPI e Postgre SQL. É implantado no Railway. Permite ao usuário fazer listas to-do (lista de tarefas), usando operações CRUD (Create, Read, Update, Delete).
Objetivo 
# Tecnologias utilizadas 
- Spring Boot: framework para aplicações Java
- Spring Data JPA: biblioteca
- H2 Database
- PostgreSQL
- Open API (Swagger)
- Railway
# Fluxogramas 
- Fluxograma de componentes
![Componente](https://github.com/user-attachments/assets/35e70dcd-9391-4c0a-8e42-7afa13444051)

  - TodoController: Lida com solicitações HTTP recebidas e retorna respostas; coloca endpoints REST para gerenciar itens de tarefas; 
  - TodoService: Contém a lógica para gerenciar os itens da lista; interage com a layer de repositório para realizar operações de banco de dados;
  - TodoRepository: Prover uma interface para interagir com o banco de dados usando Spring Data JPA;
  - Base de dados: Guarda itens e dados;
  - Todo: Representa a estrutura de dados e mapas para o banco de dados;
  - SwaggerUI: Documentação API e interface para usuário.

- Fluxograma de flow
  ![Flow](https://github.com/user-attachments/assets/cab4fae7-42e4-45ff-b2a4-1a3f5735a1d8)
  - Usuário: Envia uma solicitação POST para /apo/todos;
  - TodoController: Recebe a solicitação e envia para TodoService;
  - TodoService: Valida o input e pede ao TodoRepository para salvar o item na base de dados;
  - TodoRepository: Salva o item e retorna a entidade salva ao TodoService;
  - TodoService: Retorna o item para o TodoControler;
  - TodoController: Envia a resposta de volta ao usuário.
# Passo a passo do projeto 
- 1° Passo: Baixar o arquivo no Spring Initializr, com as seguintes dependências: Spring Web, Spring Data JPA, H2 Database e PostgreSQL; E seguintes configurações: gradle - groovy, linguagem java, Spring Boot 3.4.4 e versão java 17;
- 2° Passo: Inicializar o projeto no IDE IntelliJ;
- 3° Passo: Configurar o IntelliJ com o SDK para Java 17;
- 4° Passo: Organizar o arquivo, criando as classes; 
- 5° Passo: Códigos; 
- 6° Passo: Construir o projeto e rodar a aplicação;
- 7° Passo: Configurar o projeto para o Deploy no Railway no application properties e arquivo Procfile;
- 8° Passo: Mandar o projeto para o GitHub;
- 9° Passo: Configurar o Railway: Adicionando a base de dados PostgreSQL e variáveis: DATABASE_URL; SPRING_DATASOURCE_DRIVER_CLASS_NAME; SPRING_DATASOURCE_PASSWORD; SPRING_DATASOURCE_URL; SPRING_DATASOURCE_USERNAME;
- 10° Passo: Configurar um domain no Railway e assegurar que no applicaton properties e Procfile esteja definida uma porta de acesso;
- 11° Passo: Dar deploy na aplicação e abrir o seu domain com /swagger-ui/index.html.
  # Funcionamento/ funções
- Modelo (todo.java): id, title, description e completed - passos do uso da lista; anotado com @Entity para mapear a classe para uma tabela de dados
- Repositório (todorepository.java): estende JPA Repository para operações CRUD para entidade todo; Spring Data JPA fornece implementações padrão
- Serviço (todoservice.java): contém métodos para gerenciar os itens da lista:
  - getAllTodos(): recupera todos os itens
  - getTodoById(Long id): recuperar um item pelo id
  - CreateTodo(Todo todo): cria um novo item
  - updateTodo(Long id, Todo todoDetails): atualiza um item existente
  - deleteTodo(Long id): deleta um item pelo seu id
- Controller (todoController.java): coloca REST endpoints para gerenciar items to-do:
  - GET /api/todos: repara todos os itens
  - GET /api/todos/{id}: recuperar um item pelo id
  - POST /api/todos: cria um novo item
  - PUT /api/todos/{id}: atualiza um item existente
  - DELETE /api/todos/{id}: deletar um item pelo id
 # Problemas encontrados/ soluções 
- Problema com o SDK: O projeto não construiu pois o SDK estava em java 24 - A solução foi baixar e configurar no projeto o SDK para java 17;
- Problema com o Railway:
  - Estrutura do projeto não deixava o Railway rodar o deploy - A solução foi reestruturar o projeto;
  - Problema gerando um domain - A solução foi adicionar em application.properties “server.port=${PORT:8080}”, para ter uma porta certa para o domain ser gerado;
- Problemas com o build: projeto não conseguia dar “build” por não conseguir apagar a pasta build existente - A solução foi apagar a pasta manualmente antes de construir o projeto; 
- Problema para abrir a URL do projeto:
  - Primeira solução que eu tentei foi adicionar a variável “RAILWAY_HEALTHCHECK_TIMEOUT_SEC=120” para dar mais tempo à aplicação, sem sucesso;
  - A segunda solução que eu tentei foi rever meu application.properties; 
  - A terceira foi perceber um erro nas próprias variáveis no Railway, isso fez o Postgresql finalmente ler a base de dados do código;
  - A quarta foi montar as “tables” manualmente;
  - A quinta e última solução foi ler atentamente os logs no railway e ir adicionando informações no Procfile e no application properties que finalmente resolveram o problema no acesso do Railway a base de dados.

  # Domain publicado
  https://todo-list-production-6ee1.up.railway.app/swagger-ui/index.html#/ 
  
![Capturar2](https://github.com/user-attachments/assets/10424f4e-a500-4bcc-949b-a3ba91a12829)
![Capturar3](https://github.com/user-attachments/assets/cf2d553d-34f9-40c2-8e48-118d77295642)
![Capturar4](https://github.com/user-attachments/assets/1ca2a904-5435-4d37-8fdd-cc1a124372e7)

