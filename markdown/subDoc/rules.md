## 7. Regras

Gerenciar informações das Regras da Casa

Endpoint: **`/rules`**



#### GET /rules

Recuperar as regras da Casa do usuário autenticado. Retorna os dados em formato `application/json`.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho da requisição.

* **Código de reposta de sucesso:**`200 OK`

  Regras encontradas com sucesso.

* **Corpo da resposta:**

  ```json
  [
    {
        "idRegra": 5,
        "nome": "Regra-1",
        "descricao": "Descrição Regra 1",
        "estado": true,
        "idUsuario": "idUsuario-2",
        "idCasa": 2,
        "data": "2019-11-20",
        "valor": 20
    },
    {
        "idRegra": 6,
        "nome": "Regra-2",
        "descricao": "Descrição Regra 2",
        "estado": false,
        "idUsuario": "idUsuario-1",
        "idCasa": 2,
        "data": "2019-11-20",
        "valor": 10
    }
  ]
  ```

* **Código de resposta de erro:**`404 NOT FOUND`

  Nenhuma Regra encontrada para casa do usuário autenticado.

* **Corpo da resposta:**

  ```Json
  {
  	"error":"Nenhuma regra encontrada"
  }
  ```
* **Código de resposta de erro:**`400 BAD REQUEST`

  Usuário autenticado não possui casa registrada em seu perfil

* **Corpo da resposta:**

  ```Json
  {
  	"error":"Usuário não possui casa"
  }
  ```

#### POST /rules

Executa o cadastro de uma nova regra na Casa. O corpo da requisição contém todos os parâmetros para cadastro da Regra em formato `application/json`. Retorna os dados em formado `json` da nova Regra cadastrada.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho da requisição.
  Os seguintes atributos são obrigatórios no corpo da requisição: `nome`, `descricao` e `data`.

* **Corpo da requisição:**

  ```json
  {
    "nome": "Regra-1",
    "descricao": "Descrição Regra 1",
    "data": "2019-11-20",
    "valor": 20
  }
  ```
  
* **Código de resposta de sucesso:**`201 CREATED`

  Regra cadastrada com sucesso.

* **Corpo da resposta:**

  ```json
  {
    "idRegra":5,
    "nome": "Regra-1",
    "descricao": "Descrição Regra 1",
    "estado": true,
    "idUsuario": "idUsuario-2",
    "idCasa": 2,
    "data": "2019-11-20",
    "valor": 20
  }
  ```
  
* **Código de resposta de erro:**`400 BAD REQUEST`

  Algum campo obrigatório não foi enviado no corpo da requisição.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Atributos Obrigatórios - nome, descricao e data"
  }
  ```
  
* **Código de resposta de erro:**`409 CONFLICT`

  Não foi possível cadastrar regra no banco de dados

* **Corpo da resposta:**

  ```json
  {
  	"error":"Não foi possível criar a Regra no banco"
  }
  ```


#### PUT /rules

Executa a alteração nas informações das regras da Casa. O corpo da requisição contém todos os parâmetros para alteração em formato `application/json`. 

* **Requisitos:**
  
  Token de autenticação enviado no cabeçalho da requisição.
  O atributo `idRegra` é obrigatório no corpo da requisição.

* **Corpo da requisição:**

  ```json
  {
	  "idRegra": 6,
    "descricao": "Regra 2 atualizada",
    "valor": 35
  }
  ```

* **Código de resposta de sucesso:**`204 NO CONTENT`

  Regra atualizada com sucesso. Sem corpo de resposta.
  
  
* **Código de resposta de erro:**`409 CONFLICT`

  Não foi possível atualizar a Regra no Banco de dados

* **Corpo da resposta:**

  ```json
  {
  	"error":"Não foi possível atualizar tarefa no banco."
  }
  ```

* **Código de resposta de erro:**`404 NOT FOUND`

  Se a Regra informada no corpo da requisição não for encontrada.

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
  	"error":"Atributos idRegra obrigatório"
  }
  ```
  
* **Código de resposta de erro:**`304 NOT MODIFIED`

  Não foi enviado nenhum campo no corpo da requisição para atualização

* **Corpo da resposta:**

  ```json
  {
  	"error":"Regra sem nenhum campo para alterar."
  }
  ```
