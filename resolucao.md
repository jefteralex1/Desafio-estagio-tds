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

**Cenário cadastro bem-sucedido:**  
- Como **novo usuário**, quero **me cadastrar** no site fornecendo informações válidas, para poder acessar as funcionalidades disponíveis.  

**Critérios de Aceitação:**  
- O sistema deve aceitar campos válidos e exibir uma mensagem de sucesso.  
- O e-mail cadastrado deve ser único.  

**Cenário cadastro inválido:**  
- Como **novo usuário**, quero **tentar me cadastrar** com informações inválidas, para saber como o sistema responde.  

**Critérios de Aceitação:**  
- O sistema deve exibir mensagens de erro claras para os seguintes casos:  
  - Campos obrigatórios vazios.  
  - Senha e confirmação de senha diferentes.  
  - Formato inválido de e-mail.  
  - E-mail já cadastrado.

---

### **B. Login**

**Cenário login bem-sucedido:**  
- Como **usuário cadastrado**, quero **fazer login com minhas credenciais válidas**, para acessar minha conta.  

**Critérios de Aceitação:**  
- O sistema deve autenticar o usuário e redirecioná-lo para a página inicial com uma mensagem de boas-vindas.  

**Cenário login inválido:**  
- Como **usuário**, quero **tentar fazer login com credenciais inválidas**, para verificar a resposta do sistema.  

**Critérios de Aceitação:**  
- O sistema deve exibir mensagens de erro apropriadas para os seguintes casos:  
  - Senha incorreta.  
  - E-mail não cadastrado.  
  - Campos de login vazios.

---

### **C. Processo de Compra**

**Cenário Compra bem-sucedida:**  
- Como **usuário logado**, quero **selecionar produtos, adicioná-los ao carrinho e finalizar a compra com sucesso**, para receber os itens escolhidos.  

**Critérios de Aceitação:**  
- O sistema deve permitir:  
  - Adicionar itens ao carrinho.  
  - Atualizar a quantidade no carrinho.  
  - Concluir a compra com um método de pagamento válido.  

**Cenário Compra mal-sucedida:**  
- Como **usuário logado**, quero **tentar comprar sem seguir o fluxo correto**, para entender as validações do sistema.  

**Critérios de Aceitação:**  
- O sistema deve exibir mensagens de erro quando:  
  - O carrinho estiver vazio.  
  - O pagamento for cancelado ou inválido.

---

## **3. Casos de Teste**

### **Cadastro**

| ID   | Cenário                       | Etapas do Teste                                                                 | Entrada                                   | Resultado Esperado                      |
|------|-------------------------------|--------------------------------------------------------------------------------|------------------------------------------|-----------------------------------------|
| TC01 | Cadastro Válido               | Preencher os campos obrigatórios com dados válidos.                            | Nome: "Jefter", E-mail: "jefter@gmail.com", Senha: "12345" | Cadastro concluído com sucesso.        |
| TC02 | E-mail Duplicado              | Tentar cadastrar um e-mail já existente no sistema.                            | E-mail: "jefter@gmail.com"                 | Mensagem: "E-mail já cadastrado".       |
| TC03 | Campos Vazios                 | Submeter o formulário sem preencher os campos obrigatórios.                    | Nome: "", E-mail: "", Senha: ""          | Mensagem: "Preencha todos os campos".   |
| TC04 | E-mail Inválido               | Inserir um e-mail com formato inválido.                                        | E-mail: "jeftergmail.com"                  | Mensagem: "Formato de e-mail inválido". |
| TC05 | Senha Curta                   | Inserir uma senha com menos caracteres que o permitido (ex.: 3 caracteres).     | Senha: "abc"                             | Mensagem: "A senha deve ter no mínimo 6 caracteres". |
| TC06 | Nome com Caracteres Especiais | Preencher o nome com caracteres especiais (ex.: "@#$").                        | Nome: "@#$%"                             | Mensagem: "O nome deve conter apenas letras e espaços". |
| TC07 | Senha Sem Letras              | Inserir uma senha contendo apenas números.                                     | Senha: "123456"                          | Mensagem: "A senha deve conter letras e números".      |
| TC08 | E-mail com Espaços            | Inserir um e-mail contendo espaços.                                            | E-mail: " jefter @gmail.com "            | Mensagem: "Formato de e-mail inválido". |

---

### **Login**

| ID   | Cenário                       | Etapas do Teste                                                                 | Entrada                                   | Resultado Esperado                      |
|------|-------------------------------|--------------------------------------------------------------------------------|------------------------------------------|-----------------------------------------|
| TC09 | Login Válido                  | Inserir credenciais válidas e clicar em "Entrar".                              | E-mail: "jefter@gmail.com", Senha: "12345" | Login concluído com sucesso.            |
| TC10 | Senha Incorreta               | Inserir senha incorreta para um e-mail válido.                                 | E-mail: "jefter@gmail.com", Senha: "54321" | Mensagem: "Credenciais inválidas".      |
| TC11 | Campo de Login Vazio          | Submeter o formulário com campos de login vazios.                              | E-mail: "", Senha: ""                    | Mensagem: "Preencha os campos obrigatórios". |
| TC12 | E-mail com Letras Maiúsculas  | Inserir e-mail correto, mas com letras maiúsculas misturadas.                  | E-mail: "Jefter@GMAIL.com", Senha: "12345" | Mensagem "E-mail ou senha inválidos".            |
| TC13 | Tempo de Bloqueio             | Tentar realizar login com credenciais incorretas várias vezes consecutivas.    | 5 tentativas com senha errada consecutivamente | Mensagem: "Conta temporariamente bloqueada por segurança". |
| TC14 | Timeout na Sessão             | Permanecer logado por 30 minutos sem realizar nenhuma ação.                    | Após 30 minutos de inatividade            | Sessão expirada, redirecionar para a página de login. |

---

### **Processo de Compra**

| ID   | Cenário                       | Etapas do Teste                                                                 | Entrada                                   | Resultado Esperado                      |
|------|-------------------------------|--------------------------------------------------------------------------------|------------------------------------------|-----------------------------------------|
| TC15 | Compra Válida                 | Adicionar produtos ao carrinho e finalizar a compra com um cartão válido.       | Produto: "Camiseta", Cartão: "1111-2222-3333-4444" | Compra realizada com sucesso.           |
| TC16 | Carrinho Vazio                | Tentar finalizar a compra sem produtos no carrinho.                            | Carrinho vazio                           | Mensagem: "Adicione produtos ao carrinho". |
| TC17 | Cartão Inválido               | Inserir número de cartão incorreto no pagamento.                               | Cartão: "0000-0000-0000-0000"            | Mensagem: "Pagamento recusado".         |
| TC18 | Cartão Vencido                | Inserir cartão com validade expirada.                                          | Expiração: "10/2024"                     | Mensagem: "Cartão vencido".             |
| TC19 | Produto com Estoque Insuficiente | Adicionar ao carrinho um item fora de estoque.                                | Produto: "Notebook", Estoque: 0          | Mensagem: "Produto indisponível".       |
| TC20 | Alterar Quantidade no Carrinho | Adicionar produtos ao carrinho e alterar a quantidade para um número inválido. | Quantidade: "-1" ou "0"                  | Mensagem: "Quantidade inválida".        |
| TC21 | Logout Durante Compra         | Realizar logout antes de concluir a compra.                                    | Logout realizado                         | Redirecionar para a página de login e esvaziar o carrinho. |
| TC22 | Timeout na Página de Pagamento | Permanecer na página de pagamento por mais de 10 minutos sem interagir.        | Após 10 minutos de inatividade           | Sessão expirada, redirecionar para o carrinho. |

---

### **Casos de Borda**

| ID   | Cenário                       | Etapas do Teste                                                                 | Entrada                                   | Resultado Esperado                      |
|------|-------------------------------|--------------------------------------------------------------------------------|------------------------------------------|-----------------------------------------|
| TC23 | Limite Máximo de Caracteres   | Inserir dados no limite máximo de caracteres permitido.                         | Nome: "A" * 50, E-mail: "jefter@gmail.com" | Cadastro ou operação realizada com sucesso. |
| TC24 | Excesso de Caracteres         | Inserir dados que excedam o limite máximo permitido.                           | Nome: "A" * 51                           | Mensagem: "Campo excede o limite de caracteres permitidos". |

---

## **4. Critérios de Cobertura**

- **Validação de Entrada**: Cobertura para inputs válidos, inválidos e campos obrigatórios.  
- **Fluxos Alternativos**: Casos de e-mail duplicado, credenciais inválidas e erros no processo de pagamento.
  
---
