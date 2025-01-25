# **Caderno de Testes - Cadastro, Login e Processo de Compra**

---

## **Índice**

1. [Introdução](#1-introdução)  
   1.1. [Objetivo](#objetivo)  
   1.2. [Estratégia](#estratégia)  

2. [Histórias de Usuário](#2-histórias-de-usuário)  
   2.1. [Cadastro](#cadastro)  
   2.2. [Login](#login)  
   2.3. [Processo de Compra](#processo-de-compra)  

3. [Casos de Teste](#3-casos-de-teste)  
   3.1. [Cadastro](#cadastro)  
   3.2. [Login](#login)  
   3.3. [Processo de Compra](#processo-de-compra)  
   3.4. [Casos de Borda](#casos-de-borda)  

4. [Critérios de Cobertura](#4-critérios-de-cobertura)  
5. [Relatórios de Teste](#5-relatórios-de-teste)  
6. [Conclusão](#6-conclusão)

---

## **1. Introdução**

### **Objetivo**  
Garantir o funcionamento adequado das funcionalidades de Cadastro, Login e Processo de Compra no site [Automation Exercise](https://www.automationexercise.com/), considerando cenários de sucesso, erro e casos extremos.

### **Estratégia**  
- Criar histórias de usuário que simulem cenários reais de uso.  
- Testar fluxos positivos e negativos.  
- Cobrir entradas válidas, inválidas e casos de borda.  
- Garantir clareza e organização para facilitar a interpretação e replicação dos resultados.

---

## **2. Histórias de Usuário**

### **Cadastro**

**Cenário: Cadastro bem-sucedido**  
Como **novo usuário**, quero **me cadastrar no site** com informações válidas para acessar as funcionalidades.

**Critérios de Aceitação**  
- O sistema deve aceitar campos válidos e exibir uma mensagem de sucesso.  
- O e-mail deve ser único.

**Cenário: Cadastro com erro**  
Como **novo usuário**, quero **ver a resposta do sistema ao fornecer dados inválidos**.

**Critérios de Aceitação**  
- O sistema deve exibir mensagens de erro claras para:  
  - Campos obrigatórios vazios.  
  - Senha e confirmação de senha diferentes.  
  - Formato inválido de e-mail.  
  - E-mail já cadastrado.

### **Login**

**Cenário: Login bem-sucedido**  
Como **usuário cadastrado**, quero **fazer login com minhas credenciais válidas** para acessar minha conta.

**Critérios de Aceitação**  
- O sistema deve autenticar o usuário e redirecioná-lo para a página inicial com uma mensagem de boas-vindas.

**Cenário: Login com erro**  
Como **usuário**, quero **ver a resposta do sistema ao tentar fazer login com credenciais inválidas**.

**Critérios de Aceitação**  
- O sistema deve exibir mensagens de erro claras para:  
  - Senha incorreta.  
  - E-mail não cadastrado.  
  - Campos de login vazios.

### **Processo de Compra**

**Cenário: Compra bem-sucedida**  
Como **usuário logado**, quero **adicionar produtos ao carrinho e concluir a compra** para receber os itens.

**Critérios de Aceitação**  
- O sistema deve permitir:  
  - Adicionar produtos ao carrinho.  
  - Atualizar a quantidade no carrinho.  
  - Finalizar a compra com um método de pagamento válido.

**Cenário: Compra com erro**  
Como **usuário logado**, quero **ver a resposta do sistema ao tentar comprar sem seguir o fluxo correto**.

**Critérios de Aceitação**  
- O sistema deve exibir mensagens de erro quando:  
  - O carrinho estiver vazio.  
  - O pagamento for cancelado ou inválido.

---

## **3. Casos de Teste**

### **Cadastro**

| ID    | Cenário                       | Etapas do Teste                                                                 | Entrada                                   | Resultado Esperado                      |
|-------|-------------------------------|--------------------------------------------------------------------------------|------------------------------------------|-----------------------------------------|
| **CD01** | Cadastro Válido               | Preencher os campos obrigatórios com dados válidos.                            | Nome: "Jefter", E-mail: "jefter@gmail.com", Senha: "12345" | Cadastro concluído com sucesso.        |
| **CD02** | E-mail Duplicado              | Tentar cadastrar um e-mail já existente no sistema.                            | E-mail: "jefter@gmail.com"                | Mensagem: "E-mail já cadastrado".       |
| **CD03** | Campos Vazios                 | Submeter o formulário sem preencher os campos obrigatórios.                    | Nome: "", E-mail: "", Senha: ""          | Mensagem: "Preencha todos os campos".   |
| **CD04** | E-mail Inválido               | Inserir um e-mail com formato inválido.                                        | E-mail: "jeftergmail.com"                 | Mensagem: "Formato de e-mail inválido". |
| **CD05** | Senha Curta                   | Inserir uma senha com menos caracteres que o permitido (ex.: 3 caracteres).    | Senha: "abc"                              | Mensagem: "A senha deve ter no mínimo 6 caracteres". |
| **CD06** | Nome com Caracteres Especiais | Preencher o nome com caracteres especiais (ex.: "@#$").                        | Nome: "@#$%"                              | Mensagem: "O nome deve conter apenas letras e espaços". |
| **CD07** | Senha Sem Letras              | Inserir uma senha contendo apenas números.                                     | Senha: "123456"                           | Mensagem: "A senha deve conter letras e números".      |
| **CD08** | E-mail com Espaços            | Inserir um e-mail contendo espaços.                                            | E-mail: " jefter @gmail.com "             | Mensagem: "Formato de e-mail inválido". |

---

### **Login**

| ID    | Cenário                       | Etapas do Teste                                                                 | Entrada                                   | Resultado Esperado                      |
|-------|-------------------------------|--------------------------------------------------------------------------------|------------------------------------------|-----------------------------------------|
| **LG01** | Login Válido                  | Inserir credenciais válidas e clicar em "Entrar".                              | E-mail: "jefter@gmail.com", Senha: "12345" | Login concluído com sucesso.            |
| **LG02** | Senha Incorreta               | Inserir senha incorreta para um e-mail válido.                                 | E-mail: "jefter@gmail.com", Senha: "54321" | Mensagem: "Credenciais inválidas".      |
| **LG03** | Campo de Login Vazio          | Submeter o formulário com campos de login vazios.                              | E-mail: "", Senha: ""                    | Mensagem: "Preencha os campos obrigatórios". |
| **LG04** | E-mail com Letras Maiúsculas  | Inserir e-mail correto, mas com letras maiúsculas misturadas.                  | E-mail: "Jefter@GMAIL.com", Senha: "12345" | Mensagem: "E-mail ou senha inválidos".  |
| **LG05** | Tempo de Bloqueio             | Tentar realizar login com credenciais incorretas várias vezes consecutivas.    | 5 tentativas com senha errada consecutivamente | Mensagem: "Conta temporariamente bloqueada por segurança". |
| **LG06** | Timeout na Sessão             | Permanecer logado por 30 minutos sem realizar nenhuma ação.                    | Após 30 minutos de inatividade            | Sessão expirada, redirecionar para a página de login. |

---

### **Processo de Compra**

| ID    | Cenário                       | Etapas do Teste                                                                 | Entrada                                   | Resultado Esperado                      |
|-------|-------------------------------|--------------------------------------------------------------------------------|------------------------------------------|-----------------------------------------|
| **PC01** | Compra Válida                 | Adicionar produtos ao carrinho e finalizar a compra com um cartão válido.       | Produto: "Camiseta", Cartão: "1111-2222-3333-4444" | Compra realizada com sucesso.           |
| **PC02** | Carrinho Vazio                | Tentar finalizar a compra sem produtos no carrinho.                            | Carrinho vazio                           | Mensagem: "Adicione produtos ao carrinho". |
| **PC03** | Cartão Inválido               | Inserir número de cartão incorreto no pagamento.                               | Cartão: "0000-0000-0000-0000"            | Mensagem: "Pagamento recusado".         |
| **PC04** | Cartão Vencido                | Inserir cartão com validade expirada.                                          | Expiração: "10/2024"                     | Mensagem: "Cartão vencido".             |
| **PC05** | Produto com Estoque Insuficiente | Adicionar ao carrinho um item fora de estoque.                                | Produto: "Notebook", Estoque: 0          | Mensagem: "Produto indisponível".       |
| **PC06** | Alterar Quantidade no Carrinho | Adicionar produtos ao carrinho e alterar a quantidade para um número inválido. | Quantidade: "-1" ou "0"                  | Mensagem: "Quantidade inválida".        |
| **PC07** | Logout Durante Compra         | Realizar logout antes de concluir a compra.                                    | Logout realizado                         | Redirecionar para a página de login e esvaziar o carrinho. |
| **PC08** | Timeout na Página de Pagamento | Permanecer na página de pagamento por mais de 10 minutos sem interagir.        | Após 10 minutos de inatividade           | Sessão expirada, redirecionar para o carrinho. |

---

### **Casos de Borda**

| ID    | Cenário                       | Etapas do Teste                                                                 | Entrada                                   | Resultado Esperado                      |
|-------|-------------------------------|--------------------------------------------------------------------------------|------------------------------------------|-----------------------------------------|
| **CB01** | Limite Máximo de Caracteres   | Inserir dados no limite máximo de caracteres permitido.                         | Nome: "A" * 50, E-mail: "jefter@gmail.com" | Cadastro ou operação realizada com sucesso. |
| **CB02** | Excesso de Caracteres         | Inserir dados que excedam o limite máximo permitido.                           | Nome: "A" * 51                           | Mensagem: "Campo excede o limite de caracteres permitidos". |

---

## **4. Critérios de Cobertura**

- **Validação de Entrada**: Cobertura para inputs válidos, inválidos e campos obrigatórios.  
- **Fluxos Alternativos**: Casos de e-mail duplicado, credenciais inválidas e erros no processo de pagamento.

---
