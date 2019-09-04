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
  8. SERVIDOR grava registro no Banco de dados e retorna resultado;
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

**4. Caso de Uso: Visualizar Perfil**

* **Ator Primário:** Usuário
* **Ator Secundário:** Servidor

* **Resumo:** Visualização de perfil pelo USUÁRIO

* **Fluxo Principal:** 
  
        1. Na tela principal, USUÁRIO clica no menu e seleciona a opção perfil;
        2. Sistema envia o pedido das informações do perfil registrado para o SERVIDOR;
        3. SERVIDOR envia as informações sobre o perfil para o Sistema; 
        4. Sistema apresenta tela com as informações do perfil do usuário;
        
* **Exceções:**
  
* Se a validação dos campos no item 3 não ocorrer com sucesso, sistema apresenta resultado negativo e o fluxo retorna para o item 1.
***


**5. Caso de Uso: Cadastrar Tarefa**

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

**6. Caso de Uso: Editar Tarefa**

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

**7. Caso de Uso: Pontuar Tarefa**

* **Ator Primário:** Usuário
* **Ator Secundário:** Servidor

* **Resumo:** Pontuação de tarefa pelo USUÁRIO

* **Fluxo Principal:** 
  
        1. Na tela principal, o sistema apresenta tela de tarefas para avaliação;
        2. USUÁRIO clica no botão flutuante Feito/Não Feito de determinada tarefa;
        3. Sistema executa validação do campo;
        4. Sistema envia solicitação de alteração de tarefa para o SERVIDOR;
        5. SERVIDOR executa gravação da alteração no Banco de Dados e retorna resultado;
        6. Sistema apresenta confirmação e retorna para tela de informações da tarefa;
    
* **Exceções:**
  
  * Se a validação dos campos não ocorrer com sucesso ou gravação da tarefa no banco de dados retornar erro, sistema apresenta resultado negativo e fluxo retorna para item 1.

***

**8. Caso de Uso: Finalizar Tarefa**

* **Ator Primário:** Usuário
* **Ator Secundário:** Servidor

* **Resumo:** Solicitação de exclusão/conclusão da tarefa pelo USUÁRIO

* **Fluxo Principal:** 
  
        1. Na tela principal, USUÁRIO clica na tarefa que deseja finalizar;
        2. Sistema apresenta tela de informações da tarefa;
        3. USUÁRIO clica no botão flutuante Finalizar;
        4. Sistema envia solicitação de finalização da tarefa para o SERVIDOR;
        5. Sistema apresenta notificação sobre finalização da tarefa;
        6. SERVIDOR atualiza o estado da tarefa de "Aberta" para "Finalizada"; 
        7. Sistema volta para a tela principal.

* **Exceções:**
  
  * Se a validação dos campos não ocorrer com sucesso ou gravação da tarefa no banco de dados retornar erro, sistema apresenta resultado negativo e fluxo retorna para item 2.

***

**9. Caso de Uso: Configurar Rotina**

* **Ator Primário:** Usuário
* **Ator Secundário:** Servidor

* **Resumo:** Configuração de rotina pelo USUÁRIO

* **Fluxo Principal:** 
  
        1. Na tela principal, USUÁRIO clica no menu e seleciona a opção rotinas;
        2. Sistema apresenta tela com as rotinas que envolvem o usuário;
        3. USUÁRIO clica no na opção Criar/Editar;
        4. Sistema apresenta as opções de configuração da rotina;
        5. USUÁRIO configura a rotina e clica em Aplicar;
        6. Sistema faz uma validação inicial da configuração e envia as configurações para o SERVIDOR;        
        7. SERVIDOR valida as configurações recebidas e atualiza ou cria a rotina;
        8. SERVIDOR envia uma notificação de sucesso para o USUÁRIO; 
        9. Sistema retorna para a tela de rotinas.
        
* **Exceções:**
  
  * Se a validação dos campos no item 6 não tiver sucesso será evidenciado o campo com entrada inválida e o sistema continuará neste item.
  * Se a validação dos campos no item 7 não tiver sucesso será retornado uma mensagem de falha para o usuário e o sistema retornará para o item 4.
***

**10. Caso de Uso: Visualizar Rotina**

* **Ator Primário:** Usuário
* **Ator Secundário:** Servidor

* **Resumo:** Visualização de rotina pelo USUÁRIO

* **Fluxo Principal:** 
  
        1. Na tela principal, USUÁRIO clica no menu e seleciona a opção rotinas;
        2. Sistema envia o pedido das rotinas registradas para o SERVIDOR;
        3. SERVIDOR envia as informações sobre as rotinas para o Sistema; 
        4. Sistema apresenta tela com as rotinas que envolvem o usuário;
        5. USUÁRIO clica na rotina que deseja visualizar detalhadamente;
        6. Sistema apresenta as informações da rotina;
        
* **Exceções:**
  
* Se a validação dos campos no item 3 não ocorrer com sucesso, sistema apresenta resultado negativo.
***

**11. Caso de Uso: Configurar Grupo/Residencia**

* **Ator Primário:** Usuário
* **Ator Secundário:** Servidor

* **Resumo:** Configuração de Grupo/Residencia pelo USUÁRIO

* **Fluxo Principal:** 
  
        1. Na tela principal, USUÁRIO clica no menu e seleciona a Casa;
        2. Sistema apresenta tela com as possíveis configurações da Casa;
        3. USUÁRIO edita as configurações e clica em Aplicar;
        4. Sistema faz uma validação inicial da configuração e envia as configurações para o SERVIDOR;        
        5. SERVIDOR valida as configurações recebidas e atualiza o registro da casa;
        6. SERVIDOR envia uma notificação de sucesso para o USUÁRIO;
        7. Sistema apresenta tela com as possíveis configurações da Casa;
        
* **Exceções:**
   
   * Se a validação dos campos no item 4 não tiver sucesso será evidenciado o campo com entrada inválida e o sistema continuará neste item.
  * Se a validação dos campos no item 7 não tiver sucesso será retornado uma mensagem de falha para o usuário e o sistema retornará para o item 2.
***

**12. Caso de Uso: Visualizar Grupo/Residencia**

* **Ator Primário:** Usuário
* **Ator Secundário:** Servidor

* **Resumo:** Visualização de Grupo/Residencia pelo USUÁRIO

* **Fluxo Principal:** 
  
        1. Na tela principal, USUÁRIO clica no menu e seleciona a Casa;
        2. Sistema faz um pedido das informações do Grupo/Residencia para o SERVIDOR;        
        3. SERVIDOR envia as atualizações do Grupo/Residencia;
        4. Sistema apresenta tela com as possíveis configurações da Casa;
        
* **Exceções:**
   
   * Se a validação dos campos no item 3 não tiver sucesso, o sistema retorna um erro e continuará neste item.
***


**13. Caso de Uso: Pesquisar Usuário**

* **Ator Primário:** Usuário
* **Ator Secundário:** Servidor

* **Resumo:** Configuração de rotina pelo USUÁRIO

* **Fluxo Principal:** 
  
        1. Na tela principal, USUÁRIO clica no menu e seleciona a opção perfil;
        2. Sistema apresenta tela com informações de perfil do USUÁRIO;
        3. USUÁRIO escreve o nome de um perfil no campo Buscar e clica na opção;
        4. Sistema envia o nome do perfil solcitado para o servidor;
        5. Servidor faz uma consulta no banco de dados e retorna o resultado para o sistema;
        6. Sistema exibe as informações do perfil buscado pelo usuário;
        
* **Exceções:**
   
   * Se a consulta realizada pelo servidor não tiver resutltados será retornado para o sistema uma mensagem de erro.
***

**14. Caso de Uso: Cadastrar membros para Grupo/Residencia**

* **Ator Primário:** Usuário
* **Ator Secundário:** Servidor

* **Resumo:** Cadastro de Membros para Grupo/Residencia pelo USUÁRIO

* **Fluxo Principal:** 
  
        1. Na tela principal, USUÁRIO clica no menu e seleciona a Casa;
        2. Sistema apresenta tela com as possíveis configurações da Casa e exibe a opção visualizar Membros;
        3. USUÁRIO clica na opção visualizar membros;
        4. Sistema apresenta tela com os possíveis membros da Casa e exibe a opção adicionar um novo membro;
        5. USUÁRIO clica na opção adicionar um novo membro e digita o usuario a ser adicionado;
        6. Sistema faz um pedido de convite do membro para determinado Grupo/Residencia para o SERVIDOR;
        7. Servidor faz uma consulta no banco de dados e retorna o resultado para o sistema;
        8. Sistema exibe as informações para o usuário;
    
* **Exceções:**
  
  * Se a consulta realizada pelo servidor não tiver resutltados será retornado para o sistema uma mensagem de erro.
***

**15. Caso de Uso: Visualizar membros para Grupo/Residencia**

* **Ator Primário:** Usuário
* **Ator Secundário:** Servidor

* **Resumo:** Visualização de Grupo/Residencia pelo USUÁRIO

* **Fluxo Principal:** 
  
        1. Na tela principal, USUÁRIO clica no menu e seleciona a Casa;
        2. Sistema apresenta tela com as possíveis configurações da Casa e exibe a opção visualizar Membros;
        3. USUÁRIO clica na opção;
        4. Sistema faz um pedido das informações dos membros de determinado Grupo/Residencia para o SERVIDOR;        
        5. SERVIDOR envia as atualizações dos membros da casa;
        6. Sistema apresenta tela com os possíveis membros da Casa;
        
* **Exceções:**
   
   * Se a consulta realizada pelo servidor não tiver resutltados será retornado para o sistema uma mensagem de erro.
***
