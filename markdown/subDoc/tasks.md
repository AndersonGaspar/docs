## 2. Tarefa

Gerenciar informações sobre as tarefas

Endpoint: **`/tasks`**



#### GET /tasks/{estado}

Recuperar as tarefas relacionadas ao usuário autenticado com estado informado pelo parâmetro {estado} da URL. Retorna uma lista de tarefas no formato `application/json`.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho.

* **Código de resposta de sucesso:**`200 OK`

  Tarefas relacionadas ao usuário encontradas.
* **Corpo da resposta:**
	
  ```json
  [
      {
          "idTarefa": 32,
          "nome": "Nome Tarefa 1",
          "descricao": "Descricao tarefa 1",
          "idResponsavel": "idUsuario-1",
          "idRelator": "idUsuario-2",
          "estado": "aberta",
          "data": "1902-02-02",
          "valor": 0
      },
      {
          "idTarefa": 34,
          "nome": "Nome Tarefa 3",
          "descricao": "Descricao tarefa 3",
          "idResponsavel": "idUsuario-1",
          "idRelator": "idUsuario-1",
          "estado": "aberta",
          "data": "1902-02-02",
          "valor": 0
      }
]
	```
	
* **Código de resposta de erro:** `404 NOT FOUND`

  Caso o usuário autenticado não possua nenhuma tarefa com status com o estado informado no parâmetro da URL.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Nenhuma tarefa encontrada"
  }
  ```
* **Código de resposta de erro:**`405 METHOD NOT ALLOWED `

  Nenhum parâmetro foi informado na URL



#### POST /tasks

Executa o cadastro de uma nova tarefa no servidor. O corpo da requisição contém todos os parâmetros da tarefa em formato `application/json`. Retorna os dados da tarefa em `json` caso sejá criada com sucesso.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho `token` da requisição.

  Os seguintes atributos são obrigatórios no corpo da requisição:`nome`, `descricao`, `idResponsavel`, `estado`, `data` e `valor`.

* **Corpo da requisição:**

  ```json
  {
      "nome": "Nome Tarefa 1",
      "descricao": "Descricao tarefa 1",
      "idResponsavel": "idUsuario-1",
      "estado": "aberta",
      "data": "1902-02-02",
      "valor": 0
  }
  ```

* **Código de resposta de sucesso:**`201 CREATED`

  Tarefa criada com sucesso.

* **Corpo da resposta:**

  ```json
  {
      "idTarefa": 32,
      "nome": "Nome Tarefa 1",
      "descricao": "Descricao tarefa 1",
      "idResponsavel": "idUsuario-1",
      "idRelator": "idUsuario-2",
      "estado": "aberta",
      "data": "1902-02-02",
      "valor": 0
  }
  ```

* **Código de resposta de erro:**`400 BAD REQUEST`

  Caso algum atributo obrigatório não tenha sido enviado no corpo da requisição.

* **Corpo da resposta:**

  ```json
  {
      "error": "Atributos Obrigatórios - nome, descricao, data, valor, ..."
  }
  ```

* **Código de resposta de erro:**`409 CONFLICT`

  Caso não consiga criar a Tarefa no banco

* **Corpo da resposta:**

  ```json
  {
      "error": "Não foi possível criar a tarefa no banco. idResponsavel inválido"
  }
  ```



#### PUT /tasks

Executa a alteração dos dados tarefa no servidor. O corpo da requisição deve conter todos os parâmetros da tarefa que serão atualizados em formato `application/json`.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho `token` da requisição.

  O atributo `idTarefa` é obrigatório no corpo da requisição.

* **Corpo da requisição:**

  ```json
  {
      "idTarefa": 32,
      "estado": "finalizada"
  }
  ```
  
* **Código de resposta de sucesso:**`204 NO CONTENT`

  Tarefa atualizada com sucesso. Sem corpo de resposta.

* **Código de resposta de erro:**`404 NOT FOUND`

  Tarefa não encontrada para atualização.

* **Corpo da resposta:**

  ```json
  {
  	"error":"A Tarefa não foi encontrada"
  }
  ```
  
* **Código de resposta de erro:**`409 CONFLICT`

  Não foi possível atualizar tarefa no banco.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Não foi possível atualizar tarefa no banco"
  }
  ```

* **Código de resposta de erro:**`400 BAD REQUEST`

  Atributo `idTarefa` não informado no corpo da requisição.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Atributo idTarefa obrigatório"
  }
  ```
  
* **Código de resposta de erro:**`304 NOT MODIFIED`

  Nenhum campo foi enviado para atualização. Sem corpo de resposta.