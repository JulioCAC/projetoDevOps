# projetoDevOps

Repositório para a disciplina de DevOps do quinto período do curso de Sistemas de Informação. Este projeto implementa um [Descreva brevemente o que o sistema faz, por exemplo: "um gerenciador de produtos com frontend e backend"].

## Tecnologias Utilizadas

* **Backend:** Java com Spring Boot (especificar outras bibliotecas importantes)
* **Frontend:** JavaScript com React (ou Vue, Angular, etc. - especificar)
* **Banco de Dados:** PostgreSQL
* **Containerização:** Docker, Docker Compose

## Pré-requisitos

Antes de começar, garanta que você tem os seguintes softwares instalados:
* [Docker](https://www.docker.com/get-started)
* [Docker Compose](https://docs.docker.com/compose/install/) (geralmente vem com o Docker Desktop)
* [Git](https://git-scm.com/downloads) (para clonar o repositório)
* [Opcional: Java JDK (ex: 11, 17) e Maven/Gradle, se for buildar o backend localmente fora do Docker]
* [Opcional: Node.js e npm/yarn, se for buildar o frontend localmente fora do Docker]

## Como Configurar e Rodar o Projeto

1.  **Clone o Repositório:**
    ```bash
    git clone [URL_DO_SEU_REPOSITORIO_GIT]
    cd projetoDevOps
    ```

2.  **Configure as Variáveis de Ambiente:**
    * Crie um arquivo chamado `.env` na raiz do projeto.
    * Copie o conteúdo do arquivo `env.example` (se você criar um) ou use o modelo abaixo, substituindo os valores conforme necessário, especialmente as senhas:
        ```env
        # Variáveis de Ambiente para o Projeto DevOps

        # Configurações do PostgreSQL
        POSTGRES_DB=gerenciador_de_produtos
        POSTGRES_USER=postgres
        POSTGRES_PASSWORD=suaSenhaSeguraParaOBanco

        # Configurações da Aplicação Backend (Spring Boot)
        SPRING_DATASOURCE_USERNAME=postgres
        SPRING_DATASOURCE_PASSWORD=suaSenhaSeguraParaOBanco
        ```
    * **Importante:** Adicione o arquivo `.env` ao seu `.gitignore` para evitar que senhas e informações sensíveis sejam enviadas ao repositório Git.

3.  **Construa e Inicie os Containers:**
    Na raiz do projeto (onde está o arquivo `docker-compose.yml`), execute:
    ```bash
    docker-compose up -d --build
    ```
    * O comando `--build` força a reconstrução das imagens caso haja alterações nos Dockerfiles.
    * O `-d` executa os containers em modo "detached" (em segundo plano).

4.  **Verifique os Logs (Opcional):**
    Para ver os logs dos containers:
    ```bash
    docker-compose logs -f
    ```
    Para ver os logs de um serviço específico (ex: backend):
    ```bash
    docker-compose logs -f backend
    ```

5.  **Parando os Containers:**
    Para parar os containers:
    ```bash
    docker-compose down
    ```
    Para parar e remover os volumes (cuidado, isso apagará os dados do banco de dados se o volume `postgres_data` for anônimo ou removido explicitamente):
    ```bash
    docker-compose down -v
    ```

## Acessando as Aplicações

* **Frontend:** Abra seu navegador e acesse `http://localhost:3000`
* **Backend API (Exemplo):** A API do backend estará disponível em `http://localhost:8080`. (Você pode listar alguns endpoints principais aqui se desejar).
* **Banco de Dados (se exposto e necessário):** Se a porta do PostgreSQL estiver mapeada no `docker-compose.yml` (ex: `5439:5432`), você pode acessá-lo em `localhost:5439` com uma ferramenta de gerenciamento de banco de dados.

## Estrutura do Projeto (Exemplo)
├── backend/                # Código-fonte e Dockerfile do Backend
│   ├── src/
│   └── Dockerfile
├── frontend/               # Código-fonte e Dockerfile do Frontend
│   ├── src/
│   └── Dockerfile
├── .env                    # Arquivo de variáveis de ambiente (NÃO COMMITAR)
├── .gitignore              # Arquivos e pastas a serem ignorados pelo Git
├── docker-compose.yml      # Arquivo de orquestração dos containers
└── README.md               # Este arquivo

## API Endpoints (Exemplo - se aplicável)

* `GET /api/produtos`: Lista todos os produtos.
* `POST /api/produtos`: Cria um novo produto.
* `GET /api/produtos/{id}`: Obtém um produto específico.

## Contribuição

[Se aplicável, adicione diretrizes sobre como contribuir para o projeto.]

## Testes

[Se aplicável, explique como executar os testes automatizados.]