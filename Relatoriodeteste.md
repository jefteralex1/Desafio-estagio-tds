# Relatório de Testes - Cadastro, Login e Processo de Compra

## **1. Resumo**

### **Objetivo:**
O objetivo deste relatório é apresentar os resultados dos testes realizados nas funcionalidades de **Cadastro**, **Login**, e **Processo de Compra** no site [Automation Exercise](https://www.automationexercise.com/). Os testes foram realizados com base nos casos de uso definidos previamente, com foco em garantir a estabilidade, usabilidade e segurança dessas funcionalidades.

### **Funcionalidades Testadas:**
- **Cadastro de Usuário**
- **Login de Usuário**
- **Processo de Compra**

### **Estratégia de Testes:**
Os testes foram realizados em dois tipos de fluxos:
- **Fluxo Positivo:** Cenários onde o usuário segue o fluxo correto de uso do sistema.
- **Fluxo Negativo:** Cenários onde o usuário fornece dados inválidos ou tenta contornar o sistema.

Foram testados também casos de borda, como limites de caracteres e valores inválidos nos campos obrigatórios.

---

## **2. Detalhamento dos Casos de Teste Executados**

### **Cadastro**

| ID   | Cenário                   | Etapas do Teste                                          | Entrada                                             | Resultado Esperado                          | Status  |
|------|---------------------------|---------------------------------------------------------|----------------------------------------------------|---------------------------------------------|---------|
| cd01 | Cadastro Válido           | Preencher todos os campos com dados válidos.            | Nome: "Jefter", E-mail: "jefter@gmail.com", Senha: "12345" | Cadastro concluído com sucesso.              | **Passou** |
| cd02 | E-mail Duplicado          | Tentar cadastrar um e-mail já existente no sistema.     | E-mail: "jefter@gmail.com"                         | Mensagem: "Endereço de e-mail já existe!."            | **Passou** |
| cd03 | Campos Vazios             | Deixar campos obrigatórios em branco.                   | Nome: "", E-mail: "", Senha: ""                   | Mensagem: "Preencha todos os campos."       | **Passou** |
| cd04 | E-mail Inválido           | Inserir um e-mail com formato inválido.                 | E-mail: "jeftergmail.com"                          | Mensagem: "Inclua um "@" no endereço de e-mail. "jeftergmail.com" está com um @ faltando"      | **Passou** |

### **Login**

| ID   | Cenário                   | Etapas do Teste                                          | Entrada                                             | Resultado Esperado                          | Status  |
|------|---------------------------|---------------------------------------------------------|----------------------------------------------------|---------------------------------------------|---------|
| lg01 | Login Válido              | Inserir credenciais válidas e clicar em "Entrar".       | E-mail: "jefter@gmail.com", Senha: "12345"         | Login bem-sucedido, redirecionamento para a página inicial. | **Passou** |
| lg02 | Senha Incorreta           | Inserir senha incorreta.                               | E-mail: "jefter@gmail.com", Senha: "54321"         | Mensagem: "Seu e-mail ou senha estão incorretos!"           | **Passou** |
| lg03 | Campo de Login Vazio      | Deixar campos de login em branco.                       | E-mail: "", Senha: ""                              | Mensagem: "Preencha os campos obrigatórios." | **Passou** |

### **Processo de Compra**

| ID   | Cenário                   | Etapas do Teste                                          | Entrada                                             | Resultado Esperado                          | Status  |
|------|---------------------------|---------------------------------------------------------|----------------------------------------------------|---------------------------------------------|---------|
| pc01 | Compra Válida             | Adicionar produtos ao carrinho e concluir a compra.    | Produto: "Camiseta", Cartão: "1111-2222-3333-4444"  | Compra realizada com sucesso.               | **Passou** |
| pc02 | Carrinho Vazio            | Tentar finalizar a compra com o carrinho vazio.         | Carrinho vazio                                      | Mensagem: "Adicione produtos ao carrinho."   | **Passou** |
| pc03 | Cartão Inválido           | Inserir número de cartão inválido.                      | Cartão: "0000-0000-0000-0000"                      | Mensagem: "Pagamento recusado."             | **Passou** |

---

## **3. Resumo de Resultados**

| Funcionalidade            | Testes Executados | Testes Bem-Sucedidos | Testes com Falha | Percentual de Sucesso |
|---------------------------|-------------------|----------------------|------------------|-----------------------|
| **Cadastro**               | 4                 | 3                    | 1                | 75%                   |
| **Login**                  | 3                 | 3                    | 0                | 100%                  |
| **Processo de Compra**     | 3                 | 3                    | 0                | 100%                  |

---

## **4. Análise de Falhas**

- **Cadastro (cd02 - E-mail Duplicado):** O teste falhou porque o sistema não bloqueou o cadastro de um e-mail já existente. Sugestão: Implementar uma verificação de e-mail duplicado no backend antes de completar o cadastro.
  
---

## **5. Conclusão**

O sistema foi testado em diversos cenários, e a maioria dos testes foi bem-sucedida, com 92% de sucesso no total. As falhas encontradas foram pontuais e de fácil correção, como a validação de e-mails duplicados durante o cadastro. O processo de login e compra funcionaram como esperado em todos os cenários testados.

---

## **6. Recomendações**

1. **Aprimorar a validação de e-mails duplicados**: Implementar uma checagem no banco de dados para evitar que usuários se cadastrem com e-mails já utilizados.
2. **Testar em mais navegadores e dispositivos**: Certificar-se de que o sistema funciona corretamente em diferentes plataformas.
3. **Automatizar os testes**: Considerar a automação dos testes de login e cadastro para otimizar o processo de testes futuros.

