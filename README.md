# API Livraria

![Badge em Desenvolvimento](http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=GREEN)

## Resumo do projeto

Projeto de API REST para prática de JavaScript.
Livraria com sistema de cadastro e manejo de livros, autores e editoras.

```
npm run test
```

npm install --save-exact jest@28.1.0 --save-dev

npm i @jest/globals

## Stack utilizada

* `Node.js` v16.14.2
* `express` v4.18.1,
* `knex` v2.1.0
* `sqlite3` v5.0.8


## Instalação

Este projeto já conta com o código necessário para subir a API em um servidor local:

```
├── package.json
├── package-lock.json
├── README.md
├── server.js
├── src
│   ├── app.js
│   ├── controllers
│   │   └── livrosController.js
│   │   └── autoresController.js
│   │   └── editorasController.js
│   ├── db
│   │   ├── dbconfig.js
│   │   └── livraria.sqlite
│   ├── models
│   │   └── livro.js
│   │   └── autor.js
│   │   └── editora.js
│   └── routes
│       ├── autoresRoutes.js
│       ├── editorasRoutes.js
│       ├── index.js
│       └── livrosRoutes.js
```


### Instalação do projeto
* Baixe o repositório do projeto, navegue via terminal até a pasta e instale as dependências necessárias com `npm install`.
* Confira se a pasta `node_modules` foi criada na raiz do projeto.


### Instalação dos drivers do SQLite (Linux Debian/Ubuntu)

Este projeto utiliza o SQLite como gerenciador de banco de dados SQL. O SQLite utiliza um arquivo, normalmente de extensão `.sqlite` ou `.db`, para guardar os dados.

O projeto já conta com uma base de dados configurada e populada com alguns dados iniciais, localizado na pasta `src/db/livraria.sqlite`. Para utilizar estes dados é necessário ter os drivers do SQLite instalados localmente no computador; você pode seguir os passos abaixo para instalar e acessar os dados: 

* Instalar o `sqlite` globalmente no computador:
  `sudo apt update`
  `sudo apt install sqlite3`
  
* Verifique a instalação com:
  `sqlite3 --version`

* Utilize o cli do SQLite para acessar o arquivo `src/db/livraria.sqlite` e fazer consultas via terminal:
  `sqlite3 ./src/db/livraria.sqlite`. O terminal deverá exibir a seguinte mensagem (a data e hora do acesso serão as locais do momento em que você acessar):
  ```
  SQLite version 3.31.1 2020-01-27 19:55:54
  Enter ".help" for usage hints.
  sqlite>
  ```
  
  ### Instalação dos drivers do SQLite (Linux Debian/Ubuntu)

Este projeto utiliza o SQLite como gerenciador de banco de dados SQL. O SQLite utiliza um arquivo, normalmente de extensão `.sqlite` ou `.db`, para guardar os dados.

O projeto já conta com uma base de dados configurada e populada com alguns dados iniciais, localizado na pasta `src/db/livraria.sqlite`. Para utilizar estes dados é necessário ter os drivers do SQLite instalados localmente no computador; você pode seguir os passos abaixo para instalar e acessar os dados: 

* Instalar o `sqlite` globalmente no computador:
  `sudo apt update`
  `sudo apt install sqlite3`
  

### Instalação dos drivers do SQLite (Windows)
* Faça o download dos drivers SQLite na página: https://www.sqlite.org/download.html

* Selecione o sistema operacional e faça o download do arquivo [Precompiled binaries for Windows - SQLite Tools](https://sqlite.org/2022/sqlite-tools-win32-x86-3380500.zip)

* Crie uma pasta chamada  ```sqlite3```na unidade C:\ do seu computador. O caminho final será: ``` C:\sqlite3```.

* Insira os arquivos SQLite descompactados na pasta C:\sqlite3 (você deverá extrair os arquivos para a pasta C:\sqlite3)
* Para permitir que a CLI do SQLite3 possa ser utilizada em diferentes locais, precisamos adicionar uma variável de ambiente ao windows. Siga os passos:
				
	 * Abra "Exibir configurações avançadas do Sistema" (Advanced System Properties). Painel de controle (Control Panel) > Sistema (System) > Configurações avançadas do Sistema (Advanced System Settings).
	* Selecione "Variáveis de Ambiente"
	* Em variáveis de sistema, selecione a variável PATH e clique em **Editar..** 
	* **Adicione C:\sqlite3 ao final** e selecione a opção ok

[![Add sqlite3 to Windows PATH Variable ](https://storage.googleapis.com/static.configserverfirewall.com/images/windows10/sqlite3/sqlite3path.png)](https://storage.googleapis.com/static.configserverfirewall.com/images/windows10/sqlite3/sqlite3path.png)


Depois execute o cmd como administrador e rode o comando ```sqlite3```

### Configuração dos drivers SQLite

* Verifique a instalação com:
  `sqlite3 --version`

* Utilize o cli do SQLite para acessar o arquivo `src/db/livraria.sqlite` e fazer consultas via terminal:
  `sqlite3 ./src/db/livraria.sqlite`. O terminal deverá exibir a seguinte mensagem (a data e hora do acesso serão as locais do momento em que você acessar):
  ```
  SQLite version 3.31.1 2020-01-27 19:55:54
  Enter ".help" for usage hints.
  sqlite>
  ```

* Digite os seguintes comandos no terminal do SQLite para verificar se a versão instalada tem suporte a FKs (*foreign keys*):
  ```
  PRAGMA foreign_keys;
  ```

  Deve retornar `1` se o suporte estiver habilitado e `0` se não estiver.
  Caso não esteja, insira o seguinte comando no terminal do SQLite para ativar:

  ```
  PRAGMA foreign_keys = ON;
  ```

  Você pode rodar novamente o comando `PRAGMA foreign_keys;` para verificar novamente se o suporte está habilitado. Agora deve retornar `1`.


### Acesso ao banco de dados

Você pode utilizar o CLI do SQLite para fazer consultas ao banco e conferir se os dados iniciais estão retornando.

* Utilize o cli do SQLite para acessar o arquivo `src/db/livraria.sqlite`: 
  `sqlite3 ./src/db/livraria.sqlite`

* Digite `.tables` para exibir as tabelas já criadas no banco:
  ```
  sqlite> .tables
  autores   editoras  livros 
  ```

* Digite `SELECT * FROM autores;` para exibir o conteúdo da tabela `autores`:
  ```
  sqlite> SELECT * FROM autores;
  1|JRR Tolkien|sul-africano|2022-06-06 19:30:55
  2|Ursula LeGuin|estadunidense|2022-06-06 19:30:55
  3|Machado de Assis|brasileira|2022-06-06 19:30:55
  sqlite> 
  ```

* Você pode testar os comandos `SELECT * FROM livros;` e `SELECT * FROM editoras;` para conferir os dados destas tabelas que já deixamos prontos para serem usados na API.

> Importante: Usaremos a API para consultar, criar, atualizar e excluir dados do banco. Não utilize o terminal do SQLite para fazer estas alterações direto nas tabelas.


## Como rodar a API

* No terminal, acesse a pasta raiz do projeto e insira o comando `npm run dev` para rodar o projeto em modo de desenvolvimento. Você deverá ver no terminal a seguinte mensagem:
  ```
  > api-js-local@1.0.0 dev
  > nodemon server.js

  [nodemon] 2.0.16
  [nodemon] to restart at any time, enter `rs`
  [nodemon] watching path(s): *.*
  [nodemon] watching extensions: js,mjs,json
  [nodemon] starting `node server.js`
  Servidor escutando em http://localhost:3000
  ```

* Os recursos da API poderão ser acessados a partir da *base URL* `http://localhost:3000`.

  > Esta API está programada para ser acessada a partir de `http://localhost:3000`. Certifique-se de que não existem outros recursos ocupando a porta `3000` antes de subir o projeto.


### Endpoints

A API expõe os seguintes *endpoints* a partir da *base URL* `localhost:3000`:

`/livros`
* `GET /livros`
* `GET /livros/:id`
* `POST /livros`
* `PUT /livros/:id`
* `DELETE /livros/:id`

`/autores`
* `GET /autores`
* `GET /autores/:id`
* `GET /autores/:id/livros`
* `POST /autores`
* `PUT /autores/:id`
* `DELETE /autores/:id`

`/editoras`
* `GET /editoras`
* `GET /editoras/:id`
* `GET /editoras/:id/livros`
* `POST /editoras`
* `PUT /editoras/:id`
* `DELETE /editoras/:id`


## Roadmap

* Autenticação
* Tratamento de erros
* Validações


## Conteúdo

___
### 01.

-O porquê de testamos aplicações e sistemas, isto é, para aumentar a confiabilidade e qualidade do código
Alguns dos tipos de testes que podemos implementar, como: os estáticos, unitários, de integração e E2E. Sendo:
-Testes estáticos - voltados para analisar o código sem necessariamente executá-lo, verificando se algumas boas práticas e formatação padronizada foram adotadas na implementação
-Testes unitários- são utilizados para verificar o comportamento das menores unidades de código da aplicação
-Testes de integração - são as fases do teste de software em que módulos são combinados e testados como um conjunto
Teste E2E (End-to-End) - é um método de teste utilizado para testar um fluxo da aplicação desde o começo até o fim.
-O que é ter uma cultura de testes e alguns de seus benefícios, como a padronização e estabelecimento de processos para o nosso projeto
Como utilizar o ESLint para fazer testes estáticos em JS estabelecendo um padrão de escrita para o código, verificando se há divergências entre o código escrito e o padrão adotado e também analisando a -estrutura do projeto em busca de problemas como módulos inexistentes, falta de clareza nas declarações etc
-A implementar os primeiros testes de unidade utilizando um código implementado do zero

___
### 02.

-Utilizar métodos nativos de asserções para fins de comparação de igualdade
-Instalar e executar o Jest com a flag --experimental
-Criar arquivos de testes com o Jest e analisar erros
Usar a função describe um método do Jest usado para conjunto de testes relacionados. O describe possui a sintaxe de dois argumentos:
-Uma string para descrever
Uma função callback para executar o teste.
-Gerar relatório com o coverage, uma ferramenta integrada do jest para cobertura de testes, que possibilita identificar caminhos não testados no código

___
### 03.

-Usar Matchers para diferentes formas de testes, comparando igualdade, inclusão, erros e propriedades de valores
-Alinhar o uso do matcher com asserções e estrutura de dados para utilizar em arrays, partes de objetos e conjuntos
-Identificar as situações de "falso positivo", por meio da análise do percentual de cobertura com a flag --coverage
-Reconhecer que nem sempre quando obtivermos 100% de cobertura de acordo com um relatório estaremos realmente testando todo o código
-Conhecemos algumas formas que falso-positivos podem existir nos nossos testes

___
### 04.

-Implementar os primeiros testes unitários em uma API
-Utilizar o método "skip", que serve para pular temporariamente os testes que constam na coleção de asserções
-Rodar testes de forma assíncrona (com o then e await)
-Criar funções de simulação (mocks), com o jest. fn(), para simular um novo comportamento no teste

___
### 05.

-O que são e qual a utilidade dos hooks, para configurar as condições iniciais e finais dos nossos testes
-A utilizar o supertest, para simplificar as requisições e asserções lidando com o HTTP
-Lembrar dos casos de contorno e os motivos pelos quais queremos testá-los
-Utilizar o test.each() para fornecer tabelas e simplificar as entradas para testes mais repetitivos
-Conhecer o método jest.spyOn() para acompanhar melhor chamadas de métodos e fazer outras asserções