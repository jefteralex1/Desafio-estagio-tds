# **Caderno de Testes - Cadastro, Login e Processo de Compra**

---

## **1. Introdução**

**Objetivo:**  
Garantir que as seguintes funcionalidades: Cadastro, Login e Processo de Compra no site [Automation Exercise](https://www.automationexercise.com/) funcionem conforme o esperado, considerando cenários de sucesso e erro.

**Estratégia:**  
- Criar histórias de usuário representando cenários reais de uso.  
- Dividir os testes entre fluxos positivos e negativos.  
- Cobrir entradas válidas, inválidas e casos de borda.  
- Focar na clareza e organização para que os resultados possam ser facilmente replicados e interpretados.

---

## **2. Histórias de Usuário**

### **A. Cadastro**

**Cenário Feliz:**  
- Como **novo usuário**, quero **me cadastrar** no site fornecendo informações válidas, para poder acessar as funcionalidades disponíveis.  

**Critérios de Aceitação:**  
- O sistema deve aceitar campos válidos e exibir uma mensagem de sucesso.  
- O e-mail cadastrado deve ser único.  

**Cenário Triste:**  
- Como **novo usuário**, quero **tentar me cadastrar** com informações inválidas, para saber como o sistema responde.  

**Critérios de Aceitação:**  
- O sistema deve exibir mensagens de erro claras para os seguintes casos:  
  - Campos obrigatórios vazios.  
  - Senha e confirmação de senha diferentes.  
  - Formato inválido de e-mail.  
  - E-mail já cadastrado.

---

### **B. Login**

**Cenário Feliz:**  
- Como **usuário cadastrado**, quero **fazer login com minhas credenciais válidas**, para acessar minha conta.  

**Critérios de Aceitação:**  
- O sistema deve autenticar o usuário e redirecioná-lo para a página inicial com uma mensagem de boas-vindas.  

**Cenário Triste:**  
- Como **usuário**, quero **tentar fazer login com credenciais inválidas**, para verificar a resposta do sistema.  

**Critérios de Aceitação:**  
- O sistema deve exibir mensagens de erro apropriadas para os seguintes casos:  
  - Senha incorreta.  
  - E-mail não cadastrado.  
  - Campos de login vazios.

---

### **C. Processo de Compra**

**Cenário Feliz:**  
- Como **usuário logado**, quero **selecionar produtos, adicioná-los ao carrinho e finalizar a compra com sucesso**, para receber os itens escolhidos.  

**Critérios de Aceitação:**  
- O sistema deve permitir:  
  - Adicionar itens ao carrinho.  
  - Atualizar a quantidade no carrinho.  
  - Concluir a compra com um método de pagamento válido.  

**Cenário Triste:**  
- Como **usuário logado**, quero **tentar comprar sem seguir o fluxo correto**, para entender as validações do sistema.  

**Critérios de Aceitação:**  
- O sistema deve exibir mensagens de erro quando:  
  - O carrinho estiver vazio.  
  - O pagamento for cancelado ou inválido.

---

## **3. Test cases**

### **Cadastro**

| ID   | Cenário                       | Etapas do Teste                                                                                           | Entrada                                   | Resultado Esperado                  |
|------|-------------------------------|----------------------------------------------------------------------------------------------------------|------------------------------------------|-------------------------------------|
| TC01 | Cadastro Válido               | Preencher nome, e-mail, senha e confirmar cadastro.                                                      | Nome: "Jefter", E-mail: "jefter@gmail.com"   | Cadastro concluído com sucesso.    |
| TC02 | E-mail Duplicado              | Preencher formulário com e-mail já cadastrado.                                                           | E-mail: "jefter@gmail.com"                 | Mensagem: "E-mail já cadastrado".  |
| TC03 | Campos Vazios                 | Submeter formulário sem preencher campos obrigatórios.                                                   | Nome: "", E-mail: "", Senha: ""          | Mensagem: "Preencha todos os campos". |
| TC4 | Formato Inválido de E-mail    | Inserir e-mail com formato inválido (ex: "jeftergmail.com").                                                | E-mail: "jeftergmail.com"                  | Mensagem: "Formato de e-mail inválido". |

---

### **Login**

| ID   | Cenário                       | Etapas do Teste                                                                                           | Entrada                                   | Resultado Esperado                  |
|------|-------------------------------|----------------------------------------------------------------------------------------------------------|------------------------------------------|-------------------------------------|
| TC05 | Login Válido                  | Inserir e-mail e senha válidos e clicar em "Entrar".                                                     | E-mail: "jefter@gmail.com", Senha: "12345" | Login concluído com sucesso.        |
| TC06 | Senha Incorreta               | Inserir senha incorreta para e-mail válido.                                                              | E-mail: "jefter@gmail.com", Senha: "54321" | Mensagem: "Credenciais inválidas". |
| TC07 | Campo de Senha Vazio          | Inserir senha válida para e-mail válido.                                                              | E-mail: "jefter@gmail.com", Senha: "" | Mensagem: "Preencha este campo" (campo de senha). |
| TC08 | E-mail Não Cadastrado         | Inserir e-mail que não existe no sistema.                                                                | E-mail: "maria@gmail.com", Senha: "12345"| Mensagem: "E-mail não cadastrado". |

---

### **Processo de Compra**

| ID   | Cenário                       | Etapas do Teste                                                                                           | Entrada                                   | Resultado Esperado                  |
|------|-------------------------------|----------------------------------------------------------------------------------------------------------|------------------------------------------|-------------------------------------|
| TC09 | Compra Válida                 | Adicionar produtos ao carrinho, preencher dados de pagamento e finalizar a compra.                       | Produto: "Camiseta", Cartão: "Válido"    | Mensagem: "Compra realizada".      |
| TC10 | Carrinho Vazio                | Tentar finalizar a compra com o carrinho vazio.                                                          | Carrinho vazio                           | Mensagem: "Adicione produtos ao carrinho". |
| TC11 | Pagamento Inválido            | Inserir dados de pagamento inválidos (ex: cartão com número incorreto).                                  | Cartão: "0000-0000-0000-0000"            | Mensagem: "Pagamento recusado".    |
| TC12 | Pagamento Inválido            | Inserir dados de pagamento inválidos (ex: cartão com data de validade expirada).                                  | Expiração: "10/2024"            | Mensagem: "Cartão vencido. Use outro método de pagamento".    |

---

## **4. Critérios de Cobertura**

- **Validação de Entrada**: Cobertura para inputs válidos, inválidos e campos obrigatórios.  
- **Fluxos Alternativos**: Casos de e-mail duplicado, credenciais inválidas e erros no processo de pagamento.
  
---
