Aula prática - Docker e GitHub Codespaces

 1. Identificação

Nome do aluno: Guilherme Tavares

2. Docker no Codespaces

Versão do Docker utilizada: Docker version 29.3.0-1

O comando `docker info` foi executado com sucesso no GitHub Codespaces.

3. Contêiner Nginx

Foi utilizada a imagem `nginx:latest` para criar o contêiner chamado `meu_nginx`. O contêiner foi executado utilizando o mapeamento da porta `8080:80` e foi possível acessar a página padrão do Nginx pelo navegador através da aba PORTS do GitHub Codespaces.

Também foi realizado o acesso ao contêiner pelo terminal utilizando o comando `docker exec`. Após os testes, o contêiner foi parado e removido.

4. Imagem personalizada

Foi criada uma imagem Docker personalizada utilizando um `Dockerfile` baseado na imagem `ubuntu:24.04`.

Nome/tag da imagem: `aula-docker:1.0`

O comando `docker run --rm aula-docker:1.0` foi executado com sucesso e exibiu a mensagem armazenada no arquivo `hello.txt`.

5. Docker Compose

Foi criado o arquivo `compose.yaml` para executar dois serviços:

* MySQL 8.4;
* phpMyAdmin.

Os serviços foram iniciados utilizando `docker compose up -d` e verificados através do comando `docker compose ps`.

O phpMyAdmin foi acessado pela porta 8080 através da aba PORTS do GitHub Codespaces. O banco de dados `aula_db` foi criado pelo serviço MySQL e ficou disponível para utilização no phpMyAdmin.

6. Persistência

Foi criada a tabela `mensagem` no banco `aula_db` e inserido um registro.

Depois, os contêineres foram encerrados utilizando `docker compose down` e iniciados novamente com `docker compose up -d`.

O registro continuou disponível após a recriação dos contêineres porque os dados do MySQL foram armazenados no volume `mysql-data`. O volume não é removido pelo comando `docker compose down`, permitindo que os dados permaneçam mesmo após a remoção e recriação dos contêineres.

7. Evidências

As evidências da atividade incluem:

* Versão do Docker no Codespaces;
* Execução do contêiner Nginx;
* Acesso à página do Nginx;
* Execução da imagem `aula-docker:1.0`;
* Execução dos serviços MySQL e phpMyAdmin;
* Banco `aula_db` no phpMyAdmin;
* Tabela `mensagem` com o registro inserido;
* Persistência do registro após `docker compose down` e `docker compose up -d`.

8. Perguntas

 1. Qual é a diferença entre uma imagem Docker e um contêiner?

A imagem Docker é um modelo imutável utilizado como base para criar contêineres. O contêiner é uma instância em execução criada a partir de uma imagem.

 2. O que significa o mapeamento de portas 8080:80?

Significa que a porta 8080 do ambiente do Codespaces está associada à porta 80 dentro do contêiner. Dessa forma, o serviço que funciona na porta 80 do contêiner pode ser acessado através da porta 8080.

3. Qual é a função do Dockerfile neste exercício?

O Dockerfile descreve as instruções utilizadas para construir uma imagem Docker personalizada. Neste exercício, ele define a imagem base Ubuntu, cria o diretório `/app`, copia o arquivo `hello.txt` e define o comando que será executado quando o contêiner iniciar.

 4. Por que o serviço phpMyAdmin consegue acessar o MySQL usando PMA_HOST: mysql?

O `PMA_HOST` indica ao phpMyAdmin qual serviço deve ser utilizado como servidor MySQL. Neste exercício, `mysql` corresponde ao nome do serviço definido no `compose.yaml`, permitindo que o phpMyAdmin encontre o MySQL dentro do ambiente criado pelo Docker Compose.

 5. Qual é a função do volume mysql-data?

O volume `mysql-data` serve para manter os dados do MySQL fora do ciclo de vida dos contêineres. Assim, os dados podem continuar disponíveis mesmo quando os contêineres são removidos e recriados.

 6. O que aconteceria com os dados se o ambiente fosse encerrado com docker compose down -v?

O comando `docker compose down -v` também remove os volumes associados ao ambiente. Portanto, os dados armazenados no volume `mysql-data` seriam apagados.
