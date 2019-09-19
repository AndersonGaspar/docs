# Documentação da API do Web Service

> O documento descreve a forma de utilização da API REST do Serviço Web fornecido pelo servidor da solução. 



## 1. Usuário

Gerenciar informações sobre o usuário e verificar informações dos demais usuários.

Endpoint: **`/api/user`**



#### GET /api/user/{name or email}

Recuperar as informações do usuário solicitado por {name} ou {email} enviado na url. Retorna os dados em formato `application/json`.

```json
{
    "id": 1,
    "full_name": "username",
    "cpf": "123.456.789-00",
    "login":"login",
    "telephone":"9999-9999",
    "genre":"male",
	"date_nasc":"01/01/1900"
}
```



#### POST /api/user

Executa o registro de um novo usuário no servidor. O corpo da requisição contém todos os parâmetros do Usuário em formato `application/json`.

```json
{
    "full_name": "username",
    "cpf": "123.456.789-00",
    "login":"login",
    "telephone":"9999-9999",
    "genre":"male",
	"date_nasc":"01/01/1900"
}
```



#### POST /api/user/{username:password}

Realiza a autenticação do usuário junto ao servidor.



#### UPDATE /api/user

Executa a alteração do dados do usuário no servidor. O corpo da requisição contém todos os parâmetros do Usuário em formato `application/json`.

```json
{
    "id":1,
    "full_name": "username",
    "cpf": "123.456.789-00",
    "login":"login",
    "telephone":"9999-9999",
    "genre":"male",
	"date_nasc":"01/01/1900"
}
```



***



## 2. Tarefa

Gerenciar informações sobre as tarefas

Endpoint: **`/api/task`**



#### GET /api/task/{user}

Recuperar as tarefas relacionadas ao usuário informado pelo parâmetro {user}. Retorna os dados em formato `application/json`.

```json
[
	{
    	"id":1,
    	"task_name": "lavar louça",
    	"description": "Lavar louça do almoço todos os dias",
    	"user":"usename",
        "status":"aberta",
		"date_limit":"01/01/1900 23:23",
        "Pontos":60
	},
    {
    	"id":2,
    	"task_name": "recolher lixo",
    	"description": "recolher lixo da casa",
        "status":"finalizada",
    	"user":"usename",
		"date_limit":"01/01/1900 23:23",
        "Pontos":60
    }
]
```



#### POST /api/task

Executa o cadastro de uma nova tarefa no servidor. O corpo da requisição contém todos os parâmetros da tarefa em formato `application/json`.

```json
{
    "task_name": "recolher lixo",
    "description": "recolher lixo da casa",
    "user":"usename",
	"date_limit":"01/01/1900 23:23",
    "Pontos":60
}
```



#### UPDATE /api/task

Executa a alteração do dados do usuário no servidor. O corpo da requisição contém todos os parâmetros da tarefa em formato `application/json`. Método chamado na edição, finalização e pontuação da tarefa.

```json
{
    "id":1,
    "task_name": "lavar louça",
    "description": "Lavar louça do almoço todos os dias",
    "user":"usename",
    "status":"finalizada",
	"date_limit":"01/01/1900 23:23",
    "Pontos":60,
    "Comentarios":[
    	{
            "comentario1":"Tarefa bem realizada",
             "comentario2":"OK"
        }
    ]
}
```



***



## 3. Rotina

Gerenciar informações das Rotinas

Endpoint: **`/api/routine`**



#### GET /api/routine/{user}

Recuperar as rotinas relacionadas ao usuário informado pelo parâmetro {user}. Retorna os dados em formato `application/json`.

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



#### POST /api/routine

Executa o cadastro de uma nova rotina no servidor. O corpo da requisição contém todos os parâmetros da rotina em formato `application/json`.

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



#### UPDATE /api/routine

Executa a alteração do dados da rotina no servidor. O corpo da requisição contém todos os parâmetros do rotina em formato `application/json`. 

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



***



## 4. Casa

Gerenciar informações da Casa

Endpoint: **`/api/home`**



#### GET /api/home/{name_home}

Recuperar as informações da casa solicitada pelo parâmetro {name_home}. Retorna os dados em formato `application/json`.

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



#### POST /api/home

Executa o cadastro de uma nova Casa no servidor. O corpo da requisição contém todos os parâmetros para cadastro da Casa em formato `application/json`.

```json
{
    "home_name": "Casa 2",
    "address": "Endereço 2",
    "responsavel":"name",
	"aluguel":200,
    "foto":"foto.png"
}
```



#### UPDATE /api/home

Executa a alteração do dados da Casa no servidor. O corpo da requisição contém todos os parâmetros para alteração em formato `application/json`. 

```json
{
    "id":1,
    "home_name": "Casa 1",
    "address": "Endereço 1",
    "responsavel":"name",
	"aluguel":200,
    "foto":"foto.png"
}
```



## 5. Conta

Gerenciar informações da Conta do Usuário

Endpoint: **`/api/conta`**



#### GET /api/conta/{user}

Recuperar as informações da Conta do usuário informado pelo parâmetro {user}. Retorna os dados em formato `application/json`.

```json
[
    {
    	"id":1,
    	"user_cred": "User",
    	"valor": 10,
    	"pago":true,
	},
    {
    	"id":2,
    	"user_cred": "User x",
    	"valor": 25,
    	"pago":false,
	}
]
```



#### UPDATE /api/conta

Executa a alteração nas informações da Conta do Usuário. O corpo da requisição contém todos os parâmetros para alteração em formato `application/json`. 

```json
{
   	"id":2,
   	"user_cred": "User x",
   	"valor": 25,
  	"pago":true,
}
```



***



## 6. Regras

Gerenciar informações das Regras da Casa

Endpoint: **`/api/rules`**



#### GET /api/rules/{home_id}

Recuperar as regras da Casa informado pelo parâmetro {home_id}. Retorna os dados em formato `application/json`.

```json
{
    "id_regras":1,
    "id_home":4,
   	"Regra 1":"Porta sempre trancada",
    "Regra 2":"Não execução da tarefa acrescenta 10 reais no aluguel"
}
```



#### UPDATE /api/rules

Executa a alteração nas regras da Casa. O corpo da requisição contém todos os parâmetros para alteração em formato `application/json`. 

```json
{
    "id_regras":1,
    "id_home":4,
   	"Regra 1":"Porta sempre trancada",
    "Regra 2":"Não execução da tarefa acrescenta 30 reais no aluguel"
}
```
