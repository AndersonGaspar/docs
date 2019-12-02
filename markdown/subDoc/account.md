## 6. Conta

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