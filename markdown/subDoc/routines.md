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