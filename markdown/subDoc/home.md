## 5. Casa

Gerenciar informações da Casa

Endpoint: **`/home`**



#### GET /home/list/{nome ou endereço}

Recuperar as informações das casas que tenham o nome/endereço iguais ou parecidos ao parâmetro {nome ou endereço} informado na URL. Retorna os dados em formato `application/json`.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho.

* **Código de resposta de sucesso:**`200 OK`

  Casa(s) encontrada(s).

* **Corpo da resposta:**

  ```json
  [
      {
          "idCasa": 6,
          "nome": "Casa 1",
          "endereco": "rua da casa 1",
          "aluguel": 500,
          "descricao": "Casa com 2 garagens",
          "foto": null
      },
      {
          "idCasa": 7,
          "nome": "Casa 2",
          "endereco": "rua da casa 2",
          "aluguel": 500,
          "descricao": "Casa com 3 quartos",
          "foto": null
      }
  ]
  ```

* **Código de resposta de erro:**`404 NOT FOUND`

  Casa não encontrada de acordo com o parâmetro informado na URL da requisição.

* **Corpo da resposta:**

  ```Json
  {
      "error": "Nenhuma casa encontrada de acordo com o nome ou endereço informado"
  }
  ```



#### GET /home/{idCasa}

Recuperar as informações da casa com o idCasa igual ao parâmetro {idCasa} informado na URL. Retorna os dados em formato `application/json`.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho.

* **Código de resposta de sucesso:**`200 OK`

  Casa encontrada.

* **Corpo da resposta:**

  ```json
  {
      "idCasa": 7,
      "nome": "Casa 2",
      "endereco": "rua da casa 2",
      "aluguel": 500,
      "descricao": "Casa com 3 quartos",
      "foto": null
  }
  ```
  
* **Código de resposta de erro:**`404 NOT FOUND`

  Casa não encontrada de acordo com o parâmetro informado na URL da requisição.

* **Corpo da resposta:**

  ```Json
  {
      "error": "Nenhuma casa encontrada de acordo com o id informado"
  }
  ```

* **Código de resposta de erro:**`405 METHOD NOT ALLOWED `

  Nenhum parâmetro foi informado na URL
  
  

#### POST /home

Executa o cadastro de uma nova Casa no servidor. O corpo da requisição contém todos os parâmetros para cadastro da Casa em formato `application/json`. Retorna os dados em formado `json` da Casa cadastrada.

* **Requisitos:**

  Token de autenticação enviado no cabeçalho.

  Os seguintes atributos são obrigatórios no corpo da requisição: `nome`, `endereco`, `aluguel` e `descricao`.

* **Corpo da requisição:**

  ```json
  {
      "nome": "Casa 2",
      "endereco": "rua da casa 2",
      "aluguel": 500,
      "descricao": "Casa com 3 quartos",
      "foto": null
  }
  ```

* **Código de resposta de sucesso:**`201 CREATED`

  Casa cadastrada com sucesso.

* **Corpo da resposta:**

  ```json
  {
      "idCasa": 7,
      "nome": "Casa 2",
      "endereco": "rua da casa 2",
      "aluguel": 500,
      "descricao": "Casa com 3 quartos",
      "foto": null
  }
  ```

* **Código de resposta de erro:**`400 BAD REQUEST`

  Algum campo obrigatório não foi enviado no corpo da requisição.

* **Corpo da resposta:**

  ```json
  {
      "error": "Atributos Obrigatórios - nome, endereco, descricao e aluguel"
  }
  ```

* **Código de resposta de erro:**`409 CONFLICT`

  Erro ao criar Casa no banco.

* **Corpo da resposta:**

  ```json
  {
      "error": "Não foi possível criar a Casa no banco de dados"
  }
  ```
  



#### PUT /home

Executa a alteração do dados da Casa no servidor. O corpo da requisição deve conter os parâmetros para alteração em formato `application/json`. 

* **Requisitos:**

  Token de autenticação enviado no cabeçalho.

  É obrigatório o envio do atributo `idCasa` no corpo da requisição.

* **Corpo da requisição:**
  ```json 
  {
      "idCasa": 7,
      "nome": "Nova Casa 2",
  }
  ```
  
* **Código de resposta de sucesso:**`204 NO CONTENT`

  Casa atualizada com sucesso. Sem corpo de resposta.

* **Código de resposta de erro:**`404 NOT FOUND`

  Se a Casa com id informado não for encontrada.

* **Corpo da resposta:**

  ```json
  {
  	"error":"A casa informada não foi encontrada"
  }
  ```

* **Código de resposta de erro:**`400 BAD REQUEST`

  Se o atributo obrigatório não foi informado no corpo da requisição.

* **Corpo da resposta:**

  ```json
  {
  	"error":"Atributos idCasa é obrigatório"
  }
  ```
* **Código de resposta de erro:**`409 CONFLICT`

  Erro ao atualizar Casa no banco.

* **Corpo da resposta:**

  ```json
  {
      "error": "Não foi possível atualizar a Casa no banco de dados"
  }
  ```