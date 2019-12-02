## 7. Regras

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