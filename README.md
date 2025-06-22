[🇺🇸 English](#developer-toolbox-en) | [🇧🇷 Português](#developer-toolbox-pt)

# ![logo](https://raw.githubusercontent.com/blogdoft/developer-toolbox/refs/heads/main/frontend/public/favicon.png) Developer Toolbox

## 🇺🇸 Developer Toolbox (EN)

This repository contains only _docker compose_ files that allow you to run the [Developer Toolbox](https://github.com/blogdoft/developer-toolbox/tree/develop) locally. If you want to explore its actual features, suggest improvements, report bugs or vulnerabilities, please open an issue in the original repository.

> ## TLDR  
> From the root of the directory, run `docker compose up -d`, wait until all containers are ready, and access `http://localhost:8080` in your browser.

### How to run it?

Make sure you have Docker Compose installed and updated.

From the root directory, run `docker compose up -d` and wait for the services to become available. The Service Bus Emulator, by default, waits 15 seconds before attempting the first connection to **SqlEdge**, so you may need to wait at least that long before sending or receiving messages from the Sbus Viewer.

If you encounter issues when starting the containers, you can try running without `-d` to view the logs more easily.

### Accessing Developer Toolbox

Once all services are up, Developer Toolbox will be accessible at `http://localhost:8080`.

### How to configure?

Before running the containers, check the configuration in the available `.env` files.

#### .env

The `.env` file at the project root contains values reused by multiple services. It includes configurations for both the Service Bus Emulator and Postgres. Service Bus Emulator configs are used by itself and by SqlEdge, while Postgres configs are used by both itself and the Developer Toolbox API.

> **💡Tip:** If you want to use your own instance of Postgres (or any other container in this setup), just comment out or remove the provided container.

#### backend.env

The `backend.env` file contains environment variables needed by the API. Highlights include:

- `ServiceBus__ConnectionString:` Sets the connection string for the Service Bus Emulator. By default, a valid string for the provided emulator is included. If your team has a shared instance, replace it here.
- `ServiceBus__EmulatorConfigFile:` Path to the file that defines the topics and queues in the emulated namespace. This file should be mounted into the backend container, and its path provided in this variable. Changes require container restart.
- `ConnectionStrings__Default:` Sets the address of the Postgres database. If you’re using your own Postgres instance, adjust this value accordingly.

> **💡Tip:** Instead of running several local Postgres containers, consider using just one instance with multiple databases. This saves local resources.

> **💡Tip:** Your team may have a shared Postgres instance on an internal network or dev environment. Sharing secrets helps reduce onboarding time.

#### postgres/.env

Add Postgres-specific variables here. Many values are already referenced from the root `.env`:

```.env
POSTGRES_DB=${POSTGRES_DB}
POSTGRES_USER=${POSTGRES_USER}
POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
PGPORT=${PGPORT}
``` 

Add only values you want to override. For a full list of available variables, [check the Postgres docs](https://www.postgresql.org/docs/current/libpq-envars.html).

#### Changing reverse proxy port

If port `8080` is already in use, you can change it in `./nginx/reverse-proxy.conf`, line 2: replace `listen 8080` with another port.

Since the containers run on Docker Compose’s internal network, port conflicts are unlikely. But if you change Docker Compose to run containers in `host` mode, refer to this list:

- **backend:** 9090  
- **frontend:** 4300  
- **emulator:** 5672, 5300  
- **sqledge:** 1433  
- **postgres:** 5432  

>**❗Attention:** Services not behind the reverse proxy or exposing ports won’t be accessible from your host machine. You’ll need to explicitly expose ports to access them.

---

## 🇧🇷 Developer Toolbox (PT)

Este repositório contém apenas arquivos _docker compose_ que possibilitam rodar localmente o [Developer Toolbox](https://github.com/blogdoft/developer-toolbox/tree/develop). Caso queira verificar as reais funcionalidades disponíveis, sugerir novas features, relatar bugs ou vulnerabilidades, por favor, abra uma issue no repositório original.

> ## TLDR  
> Na raiz do diretório, rode o comando `docker compose up -d`, aguarde até que todos os containeres estejam prontos e acesse `http://localhost:8080` no seu navegador.

### Como executar?

Garanta que você possui docker compose disponível na versão mais atualizada.

Na raiz do diretório, rode o comando `docker compose up -d` e aguarde os serviços estarem disponíveis. O Service Bus Emulator, por padrão, aguarda 15 segundos antes de tentar a primeira conexão com o **SqlEdge**, portanto, é possível que você tenha que aguardar um tempo igual ou superior a esse antes de enviar ou receber mensagens do Sbus Viewer.

Caso encontre problemas na execução dos containers, uma opção é executar o comando sem a opção `-d` e observar o log dos serviços.

### Acessando o Developer Toolbox

Após todos os serviços estarem disponíveis, o Developer Toolbox estará acessível em `http://localhost:8080`.

### Como configurar?

Antes de executar os containeres, verifique as configurações presentes nos arquivos `.env` disponíveis.

#### .env

O arquivo `.env`, disponível na raiz, contém valores que podem ser reaproveitados por um ou mais serviços. Hoje se encontram lá as configurações do Service Bus Emulator e do Postgres. As configurações do Service Bus Emulator são utilizadas por ele mesmo e pelo SqlEdge. As do Postgres são usadas por ele mesmo e pela API do Developer Toolbox.

> **💡Dica:** Se você for utilizar sua própria instância do postgres (ou de qualquer outro container deste compose), simplesmente comente ou apague o container que disponibilizamos.

#### backend.env

O arquivo `backend.env` contém todas as variáveis de ambiente relevantes para o correto funcionamento da API. Entre elas destacamos:

- `ServiceBus__ConnectionString:` Define a string de conexão com o Service Bus Emulator. Por padrão, fornecemos uma string de conexão compatível com o container levantado. Caso seu time disponha de uma versão compartilhada, informe aqui a string de conexão correta.
- `ServiceBus__EmulatorConfigFile:` Arquivo que define a estrutura dos tópicos e filas no namespace emulado. Esse arquivo deve ser mapeado para dentro do container do backend e o seu path informado nessa variável. As alterações só surtirão efeito com a reinicialização do container.
- `ConnectionStrings__Default:` Define o endereço do banco de dados postgres. Caso possua sua própria instância do postgres rodando, modifique esse valor.

> **💡Dica:** Ao invés de ter várias instâncias do postgres rodando localmente, opte por ter apenas uma e crie vários bancos de dados nela. Isso ajuda a economizar recursos da sua máquina.

> **💡Dica:** Você pode ter uma instância do postgres que seja compartilhada pelo seu time; seja na rede interna ou no ambiente de desenvolvimento. Isso fará com que todas as secrets sejam compartilhadas entre o seu time, diminuindo o tempo de onboarding e configuração de ambientes locais.

#### postgres/.env

Neste arquivo adicione as variáveis de configuração do postgres. Como você pode ver, parte dos seus valores já estão configurados no `.env` da raiz. Por isso temos apenas as referências de variáveis:

```.env
POSTGRES_DB=${POSTGRES_DB}
POSTGRES_USER=${POSTGRES_USER}
POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
PGPORT=${PGPORT}
```

Por isso, adicione apenas configurações que achar interessantes. Para uma lista completa de variáveis disponíveis, [acesse a documentação do postgres](https://www.postgresql.org/docs/current/libpq-envars.html).

#### Alterando a porta do proxy reverso

Caso a porta `8080` já esteja sendo utilizada por outro serviço, você pode modificá-la alterando o arquivo `./nginx/reverse-proxy.conf`, na linha 2, alterando a cláusula `listen 8080` para a porta desejada.

Como os containeres rodam na própria rede interna do docker compose, não deverá haver conflito entre portas. Contudo, caso você tenha que alterar o docker compose para que todos os conteineres trabalhem em modo `host`, as portas utilizadas pelos serviços podem ser conferidas no arquivo `./nginx/reverse-proxy.conf` (para os serviços disponíveis via proxy) ou na lista a seguir:

- **backend:** 9090  
- **frontend:** 4300  
- **emulator:** 5672, 5300  
- **sqledge:** 1433  
- **postgres:** 5432  

> **❗Atenção:** Os serviços fora do proxy reverso ou que não estejam expondo suas portas não estarão acessíveis para a máquina host. Para que isso seja possível, você precisará expor as portas dos serviços desejados.

