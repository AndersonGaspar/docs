## 5. Casa

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