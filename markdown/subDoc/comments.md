## 3. Comentário

Gerenciar as informações dos Comentários das tarefas

Endpoint: **`/comments`**


#### GET /comments/{idTarefa}

Recuperar os comentários relacionados à tarefa informada como parâmetro {idTarefa} na URL da requisição. Retorna os dados dos comentários em formato `application/json`.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho.

* **Código de resposta de sucesso:**`200 OK`

  Comentários relacionados à tarefa informada encontrados

* **Corpo da resposta:**
  ```json
  [
      {
          "idComentario": 4,
          "texto": "Comentario da tarefa 1",
          "midia": null,
          "data": "2019-01-01 00:00:00",
          "idTarefa": 32,
          "idUsuario": "idUsuario-2"
      },
      {
          "idComentario": 5,
          "texto": "Comentario 2 da tarefa 1",
          "midia": null,
          "data": "2019-01-01 00:00:00",
          "idTarefa": 32,
          "idUsuario": "idUsuario-2"
      }
  ]
  ```
* **Código de resposta de sucesso:**`404 NOT FOUND`

  1. Nenhum comentário encontrado.
  * **Corpo da resposta:**

    ```json
    {
        "error": "Nenhum comnetário encontrado"
    }
    ```
  2. Tarefa informada não foi encontrada
  * **Corpo da resposta:**

    ```json
    {
        "error": "A tarefa não foi encontrada"
    }
    ```
  



#### POST /comments

Executa o cadastro de uma novo comentário em uma tarefa. O corpo da requisição contém todos os parâmetros do comentário em formato `application/json`. Retorna os dados do comentário em `json` caso seja criado com sucesso.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho `token` da requisição.

  Os seguintes atributos são obrigatórios no corpo da requisição:`texto`, `data` e `idTarefa`.

* **Corpo da requisição:**

  ```json
  {
      "texto": "Comentario da tarefa 3",
      "data": "2019-01-01",
      "idTarefa": 34,
      "midia": null
  }
  ```
  
* **Código de resposta de sucesso:**`201 CREATED`

  Comentário inserido com sucesso.

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

* **Código de resposta de erro:**`409 CONFLICT`

  Erro ao adicionar comentário no banco de dados.

* **Corpo da resposta:**
  ```json
  {
      "error": "Não foi possível adicionar o comentário"
  }
  ```
* **Código de resposta de erro:**`404 NOT FOUND`

  A tarefa não informada não foi encontrada

* **Corpo da resposta:**
  ```json
  {
      "error": "A tarefa não foi encontrada"
  }
  ```
* **Código de resposta de erro:**`400 BAD REQUEST`

  Campos obrigatórios não informados.

* **Corpo da resposta:**
  ```json
  {
      "error": "Atributos Obrigatórios - texto, data e idTarefa"
  }
  ```


#### PUT /comments

Executa a atualização dos dados de um comentário. O corpo da requisição contém todos os atributos do comentário que serão alterados em formato `application/json`.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho `token` da requisição.

  Os seguintes atributos são obrigatórios no corpo da requisição:`idComentario`.

* **Corpo da requisição:**

  ```json
  {
      "idComentario": 4,
      "texto": "Comentario atualizado da tarefa 1"
  }
  ```
  
* **Código de resposta de sucesso:**`204 NO CONTENT`

  Comentário atualizado com sucesso. Sem corpo de resposta

* **Código de resposta de erro:**`409 CONFLICT`

  Erro ao atualizar comentário no banco de dados.
  
* **Corpo da resposta:**
  
  ```json
  {
      "error": "Não foi possível atualizar comentário no banco."
  }
  ```
* **Código de resposta de erro:**`404 NOT FOUND`

  O comentário informado não foi encontrado

* **Corpo da resposta:**
  ```json
  {
      "error": "Comentário não encontrado"
  }
  ```
* **Código de resposta de erro:**`400 BAD REQUEST`

  Campo obrigatório não informado.

* **Corpo da resposta:**
  ```json
  {
      "error": "Atributo idComentario obrigatório"
  }
  ```

* **Código de resposta de erro:**`304 NOT MODIFIED`

  Nenhum campo foi enviado para atualização. Sem corpo de resposta.
