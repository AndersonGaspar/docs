## Análise de Requisitos

### Descrição dos Casos de Uso

**1. Caso de Uso: Registrar Usuário**

- **Ator Primário:** Usuário

- **Ator Secundário:** Servidor

- **Resumo:** Registrar USUÁRIO para acesso as funcionalidades do sistema

- **Fluxo principal:**

  ```
  1. Após instalação do aplicativo USUÁRIO acessa clicando no ícone;
  2. Sistema apresenta tela de login e USUÁRIO clica no botão Registrar;
  3. Sistema apresenta tela para que USUÁRIO preencha suas informações;
  4. USUÁRIO preenche as informações e clica no botão Enviar;
  5. Sistema executa validações dos campos (cpf, e-mail, datas, etc.);
  6. Sistema envia solicitação de registro para SERVIDOR;
  7. SERVIDOR verifica se não existe USUÁRIO com mesma identificação;
  8. SERVIDOR grava resgistro no Banco de dados e retorna resultado;
  9. Sistema confirma registro para o USUÁRIO e apresenta tela de Login.
  ```

- **Exceções:**
  
  - Se a validação dos campos no item 5 ou verificação do item 7 não ocorrer com sucesso, sistema apresenta resultado negativo para USUÁRIO e fluxo retorna para item 3.

***

**2. Caso de Uso: Autenticar Usuário**

* **Ator Primário:** Usuário
* **Ator Secundário:** Servidor
* **Resumo:** Autenticação do USUÁRIO junto ao sistema
* **Fluxo principal:**

        1. USUÁRIO abre aplicativo clicando no ícone;
        2. Sistema apresenta tela para que USUÁRIO digite login e senha para autenticação;
        3. USUÁRIO digita login e senha e clica no botão acessar;
        4. Sistema envia credenciais do USUÁRIO para o SERVIDOR autenticar;
        5. SERVIDOR retorna confirmação da autenticação para o sistema;
        6. Sistema apresenta tela principal para o USUÁRIO.

* **Exceções:**
  
  * Caso USUÁRIO digite de forma incorreta o login e/ou senha. Sistema exibe mensagem de erro para USUÁRIO e fluxo volta para item 2.

***

**3. Caso de Uso: Alterar dados do Usuário**


* **Ator Primário:** Usuário

* **Ator Secundário:** Servidor

* **Resumo:** Alterar informações cadastrais do USUÁRIO

* **Fluxo principal:**
  
        1. Na tela principal, USUÁRIO clica no menu e seleciona a opção perfil;
        2. Sistema apresenta tela de perfil do USUÁRIO;
        3. USUÁRIO clica no botão flutuante Editar;
        4. Sistema apresenta tela de edição com informações possíveis de alterar;
        5. USUÁRIO altera informações desejadas e clica no botão Salvar;
        6. Sistema executa validações dos campos alterados;
        7. Sistema envia solicitação de alteração para o SERVIDOR;
        8. SERVIDOR executa alteração no Banco de dados e retorna resultado;
        9. Sistema apresenta confirmação e retorna para tela de perfil do USUÁRIO ;
    
* **Exceções:**
  
  * Se a validação dos campos no item 6 não ocorrer com sucesso, sistema apresenta resultado negativo e fluxo retorna para item 4.

***

**4. Caso de Uso: Cadastrar Tarefa**

* **Ator Primário:** Usuário
* **Ator Secundário:** Servidor

* **Resumo:** Cadastro de tarefa pelo USUÁRIO

* **Fluxo Principal:** 
  
        1. Na tela principal, USUÁRIO clica no botão flutuante Adicionar;
        2. Sistema apresenta tela de cadastro de tarefa;
        3. USUÁRIO preenche informações da tarefa e clica em Salvar;
        4. Sistema executa validação dos campos;
        5. Sistema envia solicitação de cadastro de tarefa para o SERVIDOR;
        6. SERVIDOR executa gravação da tarefa no Banco de Dados e retorna resultado;
        7. Sistema apresenta confirmação e apresenta tela de informações da tarefa;
    
* **Exceções:**
  
  * Se a validação dos campos não ocorrer com sucesso ou gravação da tarefa no banco de dados retornar erro, sistema apresenta resultado negativo e fluxo retorna para item 2.

***

**5. Caso de Uso: Editar Tarefa**

* **Ator Primário:** Usuário
* **Ator Secundário:** Servidor

* **Resumo:** Edição de tarefa pelo USUÁRIO

* **Fluxo Principal:** 
  
        1. Na tela principal, USUÁRIO clica na tarefa que deseja editar;
        2. Sistema apresenta tela de informações da tarefa;
        3. USUÁRIO clica no botão flutuante Editar;
        4. Sistema apresenta tela de edição da tarefa com campos possíveis de alterar;
        5. USUÁRIO altera informações desejadas e clica em Salvar;
        6. Sistema executa validação dos campos;
        7. Sistema envia solicitação de alteração de tarefa para o SERVIDOR;
        8. SERVIDOR executa gravação da alteração no Banco de Dados e retorna resultado;
        9. Sistema apresenta confirmação e retorna para tela de informações da tarefa;
    
* **Exceções:**
  
  * Se a validação dos campos não ocorrer com sucesso ou gravação da tarefa no banco de dados retornar erro, sistema apresenta resultado negativo e fluxo retorna para item 4.

***

**6. Caso de Uso: Excluir Tarefa**

* **Ator Primário:** Usuário
* **Ator Secundário:** Servidor

* **Resumo:** Solicitação de exclusão da tarefa pelo USUÁRIO

* **Fluxo Principal:** 
  
        1. Na tela principal, USUÁRIO clica na tarefa que deseja excluir;
        2. Sistema apresenta tela de informações da tarefa;
        3. USUÁRIO clica no botão flutuante Excluir
        4. Sistema apresenta notificação sobre Exclusão da tarefa;
        5. USUÁRIO clica em enviar solicitação de exclusão da tarefa;
        6. Sistema envia solicitação de exclusão da tarefa para o SERVIDOR
        7. Sistema apresenta tela de informações da tarefa com status, exclusão pedentente.
    
* **Exceções:**
  
  * Se a exclusão não for confirmada pelos membros do grupo, a tarefa volta a ficar com status ativa - ver caso de uso **Confirmar Exclusão da Tarefa**.

***
**7. Caso de Uso: Confirmar Exclusão da Tarefa**

* **Ator Primário:** Servidor

* **Ator Secundário:** Usuário

* **Resumo:** Confirmar solicitação de exclusão da tarefa de outro USUÁRIO

* **Fluxo Principal:** 
  
        1. SERVIDOR recebe solicitação de exclusão da tarefa;
        2. SERVIDOR registra no banco de dados status de exclusão pendente para a tarefa;
        3. SERVIDOR envia notificação para Sistema dos demais usuários solicitando confirmação de exclusão da tarefa;
        4. Sistema apresenta notificação da solicitação de exclusão ao USUÁRIO;
        5. USUÁRIO confirma solicitação de exclusão;
        6. Sistema envia confirmação da exclusão para o SERVIDOR;
        7. SERVIDOR verifica se os demais membros já confirmaram;
        8. SERVIDOR executa a exclusão da tarefa do banco de dados;
        9. SERVIDOR envia ao sistema do usuário solicitante a confirmação da exclusão;
        10. Sistema apresenta notificação ao usuário solicitante.
    
* **Exceções:**
  
  * Se no item 7, os membros optarem por negar a exclusão, o seguinte fluxo é executado:
  
  ```
  8. SERVIDOR altera no banco de dados status da tarefa para ativa;
  9. SERVIDOR envia ao sistema do usuário solicitante a negação da exclusão;
  10. Sistema apresenta notificação ao usuário solicitante;
  ```
***
**8. Caso de Uso: Iniciar execução da Tarefa**

* **Ator Primário:** Usuário

* **Ator Secundário:** Servidor

* **Resumo:** Registrar inicio de execução da tarefa

* **Fluxo Principal:** 

  ```
  1. Na tela principal, USUÁRIO clica na tarefa que deseja iniciar;
  2. Sistema apresenta tela de informações da tarefa;
  3. USUÁRIO clica no botão iniciar;
  4. Sistema apresenta notificação de início da execução da tarefa;
  5. Sistema envia para SERVIDOR alteração de status e informações da execução da tarefa;
  6. SERVIDOR registra alterações no banco de dados;
  7. Sistema apresenta tela de informações da tarefa com status em andamento e habilita botões de pausa e finalização da execução da tarefa;
  ```
***
**9. Caso de Uso: Pausar execução da Tarefa**

* **Ator Primário:** Usuário

* **Ator Secundário:** Servidor

* **Resumo:** Registrar pausa de execução da tarefa

* **Fluxo Principal:** 

  ```
  1. Na tela principal, USUÁRIO clica na tarefa que deseja pausar;
  2. Sistema apresenta tela de informações da tarefa;
  3. USUÁRIO clica no botão pausar;
  4. Sistema apresenta notificação de pausa da execução da tarefa;
  5. Sistema envia para SERVIDOR alteração de status e informações da execução da tarefa;
  6. SERVIDOR registra alterações no banco de dados;
  7. Sistema apresenta tela de informações da tarefa com status pausada e habilita botões de reinício e finalização da execução da tarefa;
  ```
***
**10. Caso de Uso: Finalizar execução da Tarefa**

* **Ator Primário:** Usuário

* **Ator Secundário:** Servidor

* **Resumo:** Registrar finalização de execução da tarefa

* **Fluxo Principal:** 

  ```
  1. Na tela principal, USUÁRIO clica na tarefa que deseja pausar;
  2. Sistema apresenta tela de informações da tarefa;
  3. USUÁRIO clica no botão finalizar;
  4. Sistema apresenta notificação de finalização da execução da tarefa;
  5. Sistema envia para SERVIDOR solicitação para confirmação da finalização;
  6. Sistema apresenta tela de informações da tarefa com status finalização pendente;
  ```
  
* **Exceções:**
  
  * Se a finalização não for confirmada pelos membros do grupo, a tarefa fica com status finalização rejeitada - ver caso de uso **Confirmar Finalização da Tarefa**.
***
**11. Caso de Uso: Confirmar Finalização da Tarefa**

* **Ator Primário:** Servidor

* **Ator Secundário:** Usuário

* **Resumo:** Confirmar solicitação de finalização da tarefa de outro USUÁRIO

* **Fluxo Principal:** 
  
        1. SERVIDOR recebe solicitação de finalziação da tarefa;
        2. SERVIDOR registra no banco de dados status de finalziação pendente para a tarefa;
        3. SERVIDOR envia notificação para Sistema dos demais usuários solicitando confirmação de finalização da tarefa;
        4. Sistema apresenta notificação da solicitação de finalziação ao USUÁRIO;
        5. USUÁRIO confirma solicitação de finalização;
        6. Sistema envia confirmação da finalização para o SERVIDOR;
        7. SERVIDOR verifica se os demais membros já confirmaram;
        8. SERVIDOR altera status da tarefa para finalizada no banco de dados;
        9. SERVIDOR envia ao sistema do usuário solicitante a confirmação da finalização;
        10. Sistema apresenta notificação ao usuário solicitante.
    
* **Exceções:**
  
  * Se no item 7, os membros optarem por negar a finalziação, o seguinte fluxo é executado:
  
  ```
  8. SERVIDOR altera no banco de dados status da tarefa para finalização rejeitada;
  9. SERVIDOR envia ao sistema do usuário solicitante a rejeição da finalziação;
  10. Sistema apresenta notificação ao usuário solicitante;
  ```

***
