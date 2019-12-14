## 4. Rotina

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
        "idRotina": 1,
        "validade": "2019-11-20",
        "alternar": false,
        "nome": "Rotina 1",
        "descricao": "Descrição da rotina 1",
        "idUsuario": "idUsuario-1"
    },
    {
        "idRotina": 3,
        "validade": "2019-11-20",
        "alternar": true,
        "nome": "Rotina 2",
        "descricao": "Descrição da rotina 2",
        "idUsuario": "idUsuario-1"
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

Executa o cadastro de uma nova rotina no servidor. O corpo da requisição contém todos os parâmetros da rotina em formato `application/json`. Retorna os dados da Rotina recém criada.

* **Requisitos:**
  Token de autenticação enviado no cabeçalho.
  Atributos `nome`, `descricao` e `validade` são obrigatórios no corpo da requisição

* **Corpo da requisição:**

  ```json
  {
	"nome": "Rotina 2",
	"descricao": "Descrição da rotina 2",
	"validade":"2019-11-20",
	"alternar" : true
  }
  ```

* **Código de resposta de sucesso:**`201 CREATED`

  Rotina criada com sucesso.

* **Corpo da resposta:**

  ```json
  {
    "idRotina": 3,
    "validade": "2019-11-20",
    "alternar": true,
    "nome": "Rotina 2",
    "descricao": "Descrição da rotina 2",
    "idUsuario": "idUsuario-1"
  }
  ```

* **Código de resposta de erro:**`400 BAD REQUEST`

  Se os atributos obrigatórios não forem enviados no corpo da requisição.

* **Corpo da resposta:**

  ```
  {
  	"error" : "Atributos Obrigatórios - nome, descricao e validade"
  }
  ```
  
* **Código de resposta de erro:**`409 CONFLICT`

  Não foi possível criar a Rotina no banco de dados

* **Corpo da resposta:**

  ```
  {
  	"error" : "Não foi possível criar a Rotina no banco de dados"
  }
  ```
