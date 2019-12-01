# Documentação da API do Web Service

> O documento descreve API REST do Serviço Web fornecido pela solução Home Tasks. 

***

**OBS.:** Todas as requisições efetuadas, com exceção do Registro, necessitam que o usuário esteja previamente autenticado. Por isso o envio de um Token, retornado do processo de autenticação, no cabeçalho é `OBRIGATÓRIO`. `token: "token"`

***

Os seguintes erros podem ser retornados em qualquer requisição, que necessite de autenticação, caso o Usuário não informe o token ou não tenha permissão.

**Código de resposta de erro:**`401 UNAUTHORIZED`

Quando é feita a requisição sem informar o token ou o mesmo não é válido.

**Corpo da resposta:**

```json
{
	"error": "Autenticação Necessária"
}
```

**Código de resposta de erro:**`403 FORBIDDEN`

Caso o usuário autenticado tenha um token válido, mas não tenha permissão para efetuar a requisição.

**Corpo da resposta:**

```json
{
	"error": "Permissão Negada"
}
```



**URL Base:** `/hometasks/api/v1/`



## Autenticação

Endpoint: **`/login`**


#### POST /login

Realiza a autenticação do usuário junto ao servidor. Necessário o envio das credenciais do usuário no cabeçalho da requisição. Retorna o token de autenticação caso a autenticação tenha ocorrido com sucesso.

* **Requisitos:** 

  Cabeçalho `Authorization: Basic <idUsuario:senha>`, com `idUsuario:senha` codificados em Base 64, na requisição.

* **Código  de resposta de sucesso:**`200 OK`

  Autenticação realizada com sucesso.

* **Corpo da resposta:**

  ```json
  {
      "token": "7ba40d1a6034ac67a2805bfca21cbbf723d0311b"
  }
  ```

* **Código de resposta de erro:**`400 BAD REQUEST`

  1. Credenciais não enviadas no cabeçalho Authorization da Requisição.
  * **Corpo da resposta:**

    ```json
  {
        "error": "Credenciais não enviadas no cabeçalho Authorization"
  }
    ```
  2. Formato de envio das credenciais não foi reconhecido.
  * **Corpo da resposta:**

    ```json
  {
        "error": "Formato das credenciais inválido. Correto - Base64(idUsuario:senha)"
  }
    ```
* **Código de resposta de erro:**`404 NOT FOUND`

	Usuário não encontrado.

* **Corpo da resposta:**

  ```json
  {
        "error": "idUsuario inválido ou inexistente"
  }
  ```
  
* **Código de resposta de erro:**`401 UNAUTHORIZED`
  
	Senha inválida.
  
* **Corpo da resposta:**
  
  ```json
  {
        "error": "senha inválida"
  }
  ```



***



## 1. Usuário

Gerenciar informações sobre o usuário e verificar informações dos demais usuários.

Endpoint: **`/users`**

#### POST /users

Executa o registro de um novo usuário no servidor. O corpo da requisição contém todos os parâmetros do Usuário em formato `application/json`. Retorna também em formato `application/json ` os dados do Usuário recém criado.

* **Requisitos:**

  Os seguintes atributos são obrigatórios no corpo da requisição:`idUsuario`, `nome`, `senha`, `data`, `genero`, `perfil`, `telefone` e `email` 	

* **Corpo da requisição:**
	
  ```json
  {
	        "idUsuario": "idUsuario-2",
	        "nome": "Usuario 2",
	        "data": "1900-02-02",
	        "genero": "Feminino",
	        "pontos": 0,
	        "telefone": "88888888",
	        "senha": "senha",
	        "email": "usuario2@bsc.com",
	        "perfil": "Morador",
	        "idCasa": 0,
          "foto": null,
          "token": null
}
	```
	
* **Código de resposta de sucesso:**`201 CREATED`

  Usuário criado com sucesso.

* **Corpo da resposta:**

  ```json
  {
          "idUsuario": "idUsuario-2",
          "nome": "Usuario 2",
          "data": "1900-02-02",
          "genero": "Feminino",
          "pontos": 0,
          "telefone": "88888888",
          "senha": null,
          "email": "usuario2@bsc.com",
          "perfil": "Morador",
	        "idCasa": 0,
	        "foto": null,
	        "token": null
	}
	```
	
* **Código de resposta de erro:**`400 BAD REQUEST`

  Quando algum campo obrigatório não foi informado no corpo da solicitação. 

* **Corpo da resposta:**

  ```json
  {
      "error": "Atributos Obrigatórios - idUsuario, nome, senha, data, genero, ..."
  }
  ```

* **Código de resposta de erro:**`409 CONFLICT`

  Quando já existe um usuário com mesmo idUsuario registrado.

* **Corpo da resposta:**

  ```json
  {
  	"error": "Login já existe"
  }
  ```



#### GET /users/{idUsuario}

Recuperar as informações do usuário solicitado por {idUsuario} enviado como parâmetro da URL. Retorna os dados em formato `application/json`.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho `token` da requisição.

* **Código de resposta de sucesso:**`200 OK`

  Usuário encontrado

* **Corpo da resposta:**

  ```json
  {
      "idUsuario": "idUsuario-1",
      "nome": "Usuario 1",
      "data": "1900-02-02",
      "genero": "Feminino",
      "pontos": 0,
      "telefone": "777",
      "senha": null,
      "email": "usuario2@bsc.com",
      "perfil": "morador",
      "idCasa": 0,
      "foto": null,
      "token": null
  }
  ```
  
* **Código de resposta de erro:**`404 NOT FOUND`

  Usuário não encontrado de acordo com idUsuario informado na URL da requisição.

* **Corpo da resposta:**

  ```json
  {
      "error": "Usuário não encontrado"
  }
  ```
* **Código de resposta de erro:**`405 METHOD NOT ALLOWED `

  Nenhum parâmetro foi informado na URL

#### GET /users/list/{idUsuario}

Recuperar as informações de usuários com {idUsuario} parecidos. Retorna os dados em formato `application/json`.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho `token` da requisição.

* **Código de resposta de sucesso:**`200 OK`

  Usuário(s) encontrado(s).

* **Corpo da resposta:**

  ```json
  [
      {
          "idUsuario": "idUsuario-1",
          "nome": "Usuario 1",
          "data": "1900-01-01",
          "genero": "Masculino",
          "pontos": 0,
          "telefone": "9999999",
          "senha": null,
          "email": "usuario1@bsc.com",
          "perfil": "Morador",
          "idCasa": 0,
          "foto": null,
          "token": null
      },
      {
          "idUsuario": "idUsuario-2",
          "nome": "Usuario 2",
          "data": "1900-02-02",
          "genero": "Feminino",
          "pontos": 0,
          "telefone": "88888888",
          "senha": null,
          "email": "usuario2@bsc.com",
          "perfil": "Morador",
          "idCasa": 0,
          "foto": null,
          "token": null
      }
  ]
  ```

* **Código de resposta de erro:**`404 NOT FOUND`

  Usuário(s) não encontrado(s) de acordo com idUsuario informado na URL da requisição.

* **Corpo da resposta:**

  ```json
  {
      "error": "Nenhum usuário encontrado"
  }
  ```
* **Código de resposta de erro:**`405 METHOD NOT ALLOWED `

  Nenhum parâmetro foi informado na URL

#### PUT /users

Executa a alteração dos dados do usuário no servidor. O corpo da requisição deve conter todos os parâmetros do Usuário que deseja ser alterado em formato `application/json`. 

* **Requisitos:**

  Token de autenticação enviado no cabeçalho `token` da requisição.

  Os seguintes atributos são obrigatórios no corpo da requisição:`idUsuario`, `nome`, `data`, `genero`, `perfil`, `telefone` e `email`

* **Corpo da requisição:**

  ```json
  {
          "idUsuario": "idUsuario-1",
          "nome": "Usuario 1",
          "data": "1900-02-02",
          "genero": "Feminino",
          "telefone": "7777777",
          "email": "usuario2@bsc.com",
          "perfil": "Morador",
              
  }
  ```

* **Código de resposta de sucesso:**`204 NO CONTENT`

  Usuário atualizado com sucesso. Sem corpo de resposta.

* **Código de resposta de erro:**`400 BAD REQUEST`
  
  Quando algum campo obrigatório não foi informado no corpo da solicitação.
  
* **Corpo da resposta:**

  ```json
  {
      "error": "Atributos Obrigatórios - idUsuario, nome, senha, data, genero, ..."
  }
  ```
* **Código de resposta de erro:**`404 NOT FOUND`
  
  Quando ocorre algum erro na atualização do Usuário no Banco de Dados.
  
* **Corpo da resposta:**

  ```json
  {
      "error": "Erro ao atualizar Usuário no Banco"
  }
  ```

  
***



## 2. Tarefa

Gerenciar informações sobre as tarefas

Endpoint: **`/tasks`**



#### GET /tasks/{estado}

Recuperar as tarefas com status `aberta` relacionadas ao usuário autenticado e as tarefas com status `finalizada` da Casa para avaliação. Retorna uma lista de tarefas no formato `application/json`.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho.

* **Código de resposta de sucesso:**`200 OK`

  Tarefas relacionadas ao usuário encontradas.
* **Corpo da resposta:**
	
  ```json
  [
  	{
  		"id":1,
  		"task_name": "lavar louça",
  		"description": "Lavar louça do almoço todos os dias",
  		"user_id":1,
  		"status":"aberta",
  		"date_limit":"01/01/1900 23:23",
  		"Pontos":60
  	},
  	{
  		"id":2,
  		"task_name": "recolher lixo",
  		"description": "recolher lixo da casa",
  		"status":"finalizada",
  		"user_id":3,
  		"date_limit":"01/01/1900 23:23",
  		"Pontos":60
  	}
  ]
  ```

* **Código de resposta de erro:** `404 NOT FOUND`

  Caso o usuário autenticado não possua nenhuma tarefa com status `aberta` ou não possuir nenhuma tarefa com status `finalizada` para avalização.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Nenhuma tarefa encontrada"
  }
  ```

  

#### POST /tasks

Executa o cadastro de uma nova tarefa no servidor. O corpo da requisição contém todos os parâmetros da tarefa em formato `application/json`. Retorna os dados da tarefa em `json` caso sejá criada com sucesso.

* **Requisitos:**

Os atributos `task_name` e `user_id` são obrigatórios no corpo da requisição.

* **Corpo da requisição:**

  ```json
  {
  	"task_name": "recolher lixo",
  	"description": "recolher lixo da casa",
  	"user_id":1,
  	"date_limit":"01/01/1900 23:23",
  	"Pontos":60
  }
  ```

* **Código de resposta de sucesso:**`201 CREATED`

  Tarefa criada com sucesso.

* **Corpo da resposta:**

  ```json
  {
  	"id":5,
  	"task_name": "recolher lixo",
  	"description": "recolher lixo da casa",
  	"status":"finalizada",
  	"user_id":3,
  	"date_limit":"01/01/1900 23:23",
  	"Pontos":60
  }
  ```

* **Código de resposta de erro:**`400 BAD REQUEST`

  Caso algum atributo obrigatório não tenha sido enviado no corpo da requisição.

* **Corpo da resposta:**

  ```json
  {
  	"error": "Atributos Obrigatórios:task_name e user_id"
  }
  ```

  
#### PUT /tasks

Executa a alteração dos dados tarefa no servidor. O corpo da requisição deve conter todos os parâmetros da tarefa que serão atualizado em formato `application/json`.

* **Requisitos:**

  O atributo `id` da tarefa é obrigatório no corpo da requisição.

* **Corpo da requisição:**

  ```json
  {
  	"id":5,
  	"status":"finalizada",
  	"Comentarios":
  	[
  		{
  			"comentario1":"Tarefa bem realizada",
  			"comentario2":"OK"
  		}
  	]
  }
  ```

* **Código de resposta de sucesso:**`204 NO CONTENT`

  Tarefa atualizada com sucesso. Sem corpo de resposta.

* **Código de resposta de erro:**`404 NOT FOUND`

  Tarefa não encontrada para atualização.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Tarefa não encontrada"
  }
  ```

* **Código de resposta de erro:**`400 BAD REQUEST`

  Atributo `id` não informado no corpo da requisição.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Atributo id obrigatório"
  }
  ```

***

## 3. Rotina

Gerenciar informações das Rotinas do usuário

Endpoint: **`/routines`**



#### GET /routines

Recuperar as rotinas relacionadas ao usuário autenticado. Retorna os dados em formato `application/json`.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho.

* **Código de resposta de sucesso:**`200 OK`

  Rotinas do usuário encontradas.

* **Corpo da resposta:**
  ```json
  [
  	{
  		"id":1,
  		"routine_name": "Rotina 1",
  		"description": "Descrição da rotina",
  		"days":"seg,ter,qui",
  		"hour_limit":"23:23",
  		"responsavel":"alternar",
  		"date_val":"01/01/2000"
  	},
  	{
  		"id":2,
  		"routine_name": "Rotina 2",
  		"description": "Descrição da rotina 2",
  		"days":"seg,sex",
  		"hour_limit":"23:23",
  		"responsavel":"todos",
  		"date_val":"01/01/2000"
  	}
  ]
  ```

* **Código de resposta de erro:**`404 NOT FOUND`

  Caso usuário autenticado não possua nenhuma rotina registrada.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Nenhuma rotina registrada"
  }
  ```

  
#### POST /routines

Executa o cadastro de uma nova rotina no servidor. O corpo da requisição contém todos os parâmetros da rotina em formato `application/json`. Retorna os dados da Rotina recem criada.

* **Requisitos:**

  Atributo `routine_name` é obrigatório no corpo da requisição

* **Corpo da requisição:**

  ```json
  {
  	"routine_name": "Rotina 2",
  	"description": "Descrição da rotina 2",
  	"days":"seg,sex",
  	"hour_limit":"23:23",
  	"responsavel":"todos",
  	"date_val":"01/01/2000"
  }
  ```

* **Código de resposta de sucesso:**`201 CREATED`

  Rotina criada com sucesso.

* **Corpo da resposta:**

  ```json
  {
  	"id":3,
  	"routine_name": "Rotina 2",
  	"description": "Descrição da rotina 2",
  	"days":"seg,sex",
  	"hour_limit":"23:23",
  	"responsavel":"todos",
  	"date_val":"01/01/2000"
  }
  ```

* **Código de resposta de erro:**`400 BAD REQUEST`

  Se o atributo obrigatório não for enviado no corpo da requisição.

* **Corpo da resposta:**

  ```
  {
  	"error" : "Atributo routine_name obrigatório"
  }
  ```

  
#### PUT /routines

Executa a alteração do dados da rotina no servidor. Os atributos que irão ser atualizados devem ser enviados no corpo da requisição em formato `application/json`. 

* **Requisitos:**

  Atributo `id` da rotina é obrigatório no corpo da requisição.

* **Corpo da requisição:**

  ```json
  {
  	"id":2,
  	"routine_name": "Rotina 2",
  	"description": "Descrição da rotina 2",
  	"days":"seg,sex",
  	"hour_limit":"23:23",
  	"responsavel":"todos",
  	"date_val":"01/01/2000"
  }
  ```
  
* **Código de resposta de sucesso:**`204 NO CONTENT`

  Rotina atualizada com sucesso. Sem corpo de resposta.

* **Código de resposta de erro:**`404 NOT FOUND`

  Rotina não encontrada para atualização.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Rotina não encontrada"
  }
  ```

* **Código de resposta de erro:**`400 BAD REQUEST`

  Atributo `id` da rotina não informado no corpo da requisição.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Atributo id obrigatório"
  }
  ```

***



## 4. Casa

Gerenciar informações da Casa

Endpoint: **`/home`**



#### GET /home/{name_home}

Recuperar as informações da casa solicitada pelo parâmetro {name_home}. Retorna os dados em formato `application/json`.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho.

* **Código de resposta de sucesso:**`200 OK`

  Casa encontrada.

* **Corpo da resposta:**

  ```json
  {
  	"id":1,
  	"home_name": "Casa 1",
  	"address": "Endereço",
  	"responsavel":"name",
  	"aluguel":200,
  	"foto":"foto.png"
  } 
  ```

* **Código de resposta de erro:**`404 NOT FOUND`

  Casa não encontrada de acordo com o parâmetro informado na URL da requisição.

* **Corpo da resposta:**

  ```Json
  {
  	"error":"Rotina não encontrada"
  }
  ```

  
#### POST /home

Executa o cadastro de uma nova Casa no servidor. O corpo da requisição contém todos os parâmetros para cadastro da Casa em formato `application/json`. Retorna os dados em formado `json` da Casa cadastrada.

* **Requisitos:**

  Os seguintes atributos são obrigatórios no corpo da requisição: `home_name`, `address`, `responsavel` e `aluguel`.

* **Corpo da requisição:**

  ```json
  {
  	"home_name": "Casa 2",
  	"address": "Endereço 2",
  	"responsavel":"name",
  	"aluguel":200,
  	"foto":"foto.png"
  }
  ```

* **Código de resposta de sucesso:**`201 CREATED`

  Casa cadastrada com sucesso.

* **Corpo da resposta:**

  ```json
  {
  	"id":2,
  	"home_name": "Casa 2",
  	"address": "Endereço",
  	"responsavel":"name",
  	"aluguel":200,
  	"foto":"foto.png"
  }
  ```

* **Código de resposta de erro:**`400 BAD REQUEST`

  Algum campo obrigatório não foi enviado no corpo da requisição.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Atributos obrigatórios - home_name, address, responsavel e aluguel"
  }
  ```

  

#### PUT /home

Executa a alteração do dados da Casa no servidor. O corpo da requisição deve conter os parâmetros para alteração em formato `application/json`. 

* **Requisitos:**

  É obrigatório o envio do atributo `id` no corpo da requisição.

* **Corpo da requisição:**
  ```json 
  {
  	"id":1,
  	"home_name": "Casa 1",
  	"aluguel":300,
  	"foto":"foto.png"
  }
  ```

* **Código de resposta de sucesso:**`204 NO CONTENT`

  Casa atualizada com sucesso. Sem corpo de resposta.

* **Código de resposta de erro:**`404 NOT FOUND`

  Se a Casa com id informado não for encontrada.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Casa não encontrada"
  }
  ```

* **Código de resposta de erro:**`400 BAD REQUEST`

  Se o atributo obrigatório não foi informado no corpo da requisição.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Atributo id obrigatório"
  }
  ```

***
## 5. Conta

Gerenciar informações da Conta do Usuário

Endpoint: **`/account`**



#### GET /account/

Recuperar as informações da Conta do usuário autenticado. Retorna os dados em formato `application/json`.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho da requisição.

* **Código de resposta de sucesso:**`200 OK`

  Contas dos usuários encontradas com sucesso.

* **Corpo da resposta:**

  ```json
  [
  	{
  		"id":1,
  		"id_user_cred": 4,
  		"valor": 10,
  		"pago":true,
  	},
  	{
  		"id":2,
  		"id_user_cred": 3,
  		"valor": 25,
  		"pago":false,
  	}
  ]
  ```
  
* **Código de resposta de erro:**`404 NOT FOUND`

  Caso o usuário autenticado ainda não possua nenhuma conta.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Conta não encontrada"
  }
  ```



#### PUT /account

Executa a alteração nas informações da Conta do Usuário. O corpo da requisição contém todos os parâmetros para alteração em formato `application/json`. 

* **Requisitos:**

  O atributo `id` da conta é obrigatório no corpo da requisição.

* **Corpo da requisição:**

  ```json
  {
  	"id":2,
  	"valor": 25,
  	"pago":true,
  }
  ```

* **Código de resposta de sucesso:**`204 NO CONTENT`

  Conta atualizada com sucesso. Sem corpo de resposta.

* **Código de resposta de erro:**`404 NOT FOUND`

  Se a Conta com `id` informado não for encontrada.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Conta não encontrada"
  }
  ```

* **Código de resposta de erro:**`400 BAD REQUEST`

  Se o atributo obrigatório não foi informado no corpo da requisição.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Atributo id obrigatório"
  }
  ```
***



## 6. Regras

Gerenciar informações das Regras da Casa

Endpoint: **`/rules`**



#### GET /rules/{home_id}

Recuperar as regras da Casa informado pelo parâmetro {home_id}. Retorna os dados em formato `application/json`.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho da requisição.

* **Código de reposta de sucesso:**`200 OK`

  Regras encontradas com sucesso.

* **Corpo da resposta:**

  ```json
  [
  	{
  		"id_regra":1,
  		"id_home":4,
  		"descricao":"Porta sempre trancada"
  	},
  	{
  		"id_regra":2,
  		"id_home":4,
  		"descricao":"Tarefa não executada acrescenta 10 reais no aluguel"
  	}
  ]
  ```

* **Código de resposta de erro:**`404 NOT FOUND`

  Regras não encontradas de acordo com o parâmetro informado na URL da requisição.

* **Corpo da resposta:**

  ```Json
  {
  	"error":"Regras não encontradas"
  }
  ```

#### POST /rules

Executa o cadastro de uma nova regra na Casa. O corpo da requisição contém todos os parâmetros para cadastro da Regra em formato `application/json`. Retorna os dados em formado `json` da nova Regra cadastrada.

* **Requisitos:**

  Os seguintes atributos são obrigatórios no corpo da requisição: `id_home` e `descricao`.

* **Corpo da requisição:**

  ```json
  {
  	"id_home":4,
  	"descricao":"Nova regra"
  }
  ```
  
* **Código de resposta de sucesso:**`201 CREATED`

  Casa cadastrada com sucesso.

* **Corpo da resposta:**

  ```json
  {
  	"id_regra":3,
  	"id_home":4,
  	"descricao":"nova regra"
  }
  ```
  
* **Código de resposta de erro:**`400 BAD REQUEST`

  Algum campo obrigatório não foi enviado no corpo da requisição.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Atributos obrigatórios - id_home e descricao"
  }
  ```



#### PUT /rules

Executa a alteração nas informações das regras da Casa. O corpo da requisição contém todos os parâmetros para alteração em formato `application/json`. 

* **Requisitos:**

  O atributo `id_regra`  e `id_home` são obrigatórios no corpo da requisição.

* **Corpo da requisição:**

  ```json
  {
  	"id_regra":2,
  	"id_home":4,
  	"descricao":"Tarefa não executada acrescenta 20 reais no aluguel"
  }
  ```

* **Código de resposta de sucesso:**`204 NO CONTENT`

  Regra atualizada com sucesso. Sem corpo de resposta.

* **Código de resposta de erro:**`404 NOT FOUND`

  Se a Regra com `id_regra` informado não for encontrada.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Regra não encontrada"
  }
  ```

* **Código de resposta de erro:**`400 BAD REQUEST`

  Se o atributo obrigatório não foi informado no corpo da requisição.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Atributos id_regra e id_home são obrigatórios"
  }
  ```
