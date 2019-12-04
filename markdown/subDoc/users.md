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
          "perfil": "Morador"
              
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
