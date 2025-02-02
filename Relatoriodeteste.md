# Relatório de Testes - Cadastro, Login e Processo de Compra

---

## **Índice**

1. [Resumo](#1-resumo)  
   1.1. [Objetivo](#objetivo)  
   1.2. [Funcionalidades Testadas](#funcionalidades-testadas)  
   1.3. [Estratégia de Testes](#estrategia-de-testes)  

2. [Detalhamento dos Casos de Teste Executados](#2-detalhamento-dos-casos-de-teste-executados)  
   2.1. [Cadastro](#cadastro)  
   2.2. [Login](#login)  
   2.3. [Processo de Compra](#processo-de-compra)  
   2.4. [Casos Extremos](#casos-extremos)  

3. [Resumo de Resultados](#3-resumo-de-resultados)  
4. [Análise de Falhas](#4-analise-de-falhas)  
5. [Conclusão](#5-conclusao)  
6. [Recomendações](#6-recomendacoes)  

---

## 1. Resumo

### Objetivo:
O objetivo deste relatório é apresentar os resultados dos testes realizados nas funcionalidades de **Cadastro**, **Login**, **Processo de Compra** e alguns **Casos extremos** no site [Automation Exercise](https://www.automationexercise.com/). Os testes foram realizados com base nos casos de uso definidos previamente, com foco em garantir a estabilidade, usabilidade e segurança dessas funcionalidades.

### Funcionalidades Testadas:
- **Cadastro de Usuário**
- **Login de Usuário**
- **Processo de Compra**
- **Casos extremos**


### Estratégia de Testes:
Os testes foram realizados em dois tipos de fluxos:
- **Fluxo Positivo:** Cenários onde o usuário segue o fluxo correto de uso do sistema.
- **Fluxo Negativo:** Cenários onde o usuário fornece dados inválidos ou tenta contornar o sistema.

Foram testados também Casos extremos, como limites de caracteres e valores inválidos nos campos obrigatórios.

---

## 2. Detalhamento dos Casos de Teste Executados

### Cadastro

| ID   | Cenário                   | Etapas do Teste                                          | Entrada                                             | Resultado Esperado                          | Status  |
|------|---------------------------|---------------------------------------------------------|----------------------------------------------------|---------------------------------------------|---------|
| CD01 | Cadastro Válido           | Preencher todos os campos com dados válidos.            | Nome: "Jefter", E-mail: "jefter@gmail.com", Senha: "12345" | Cadastro concluído com sucesso.              | **Passou** |
| CD02 | E-mail Duplicado          | Tentar cadastrar um e-mail já existente no sistema.     | E-mail: "jefter@gmail.com"                         | Mensagem: "Endereço de e-mail já existe!."            | **Passou** |
| CD03 | Campos Vazios             | Deixar campos obrigatórios em branco.                   | Nome: "", E-mail: "", Senha: ""                   | Mensagem: "Preencha todos os campos."       | **Passou** |
| CD04 | E-mail Inválido           | Inserir um e-mail com formato inválido.                 | E-mail: "jeftergmail.com"                          | Mensagem: "Inclua um '@' no endereço de e-mail. 'jeftergmail.com' está com um '@' faltando". | **Passou** |
| CD05 | Senha Curta               | Inserir uma senha com menos caracteres que o permitido. | Senha: "abc"                                       | Mensagem: "A senha deve ter no mínimo 6 caracteres". | **Falhou** |
| CD06 | Nome com Caracteres Especiais | Preencher o nome com caracteres especiais.             | Nome: "@#$%"                                       | Mensagem: "O nome deve conter apenas letras e espaços". | **Falhou** |
| CD07 | Senha Sem Letras          | Inserir uma senha contendo apenas números.              | Senha: "123456"                                    | Mensagem: "A senha deve conter letras e números". | **Falhou** |
| CD08 | E-mail com Espaços        | Inserir um e-mail contendo espaços.                     | E-mail: " jefter @gmail.com "                      | Mensagem: "Uma parte seguida por '@' não deve conter o símbolo ' '". | **Passou** |

---

### Login

| ID   | Cenário                   | Etapas do Teste                                          | Entrada                                             | Resultado Esperado                          | Status  |
|------|---------------------------|---------------------------------------------------------|----------------------------------------------------|---------------------------------------------|---------|
| LG01 | Login Válido              | Inserir credenciais válidas e clicar em "Entrar".       | E-mail: "jefter@gmail.com", Senha: "12345"         | Login concluído com sucesso.               | **Passou** |
| LG02 | Senha Incorreta           | Inserir senha incorreta para um e-mail válido.         | E-mail: "jefter@gmail.com", Senha: "54321"         | Mensagem: "Credenciais inválidas".          | **Passou** |
| LG03 | Campo de Login Vazio      | Submeter o formulário com campos de login vazios.       | E-mail: "", Senha: ""                              | Mensagem: "Preencha os campos obrigatórios". | **Passou** |
| LG04 | E-mail com Letras Maiúsculas | Inserir e-mail correto, mas com letras maiúsculas misturadas. | E-mail: "Jefter@GMAIL.com", Senha: "12345"         | Login concluído com sucesso.                | **Passou** |
| LG05 | Tempo de Bloqueio         | Tentar realizar login com credenciais incorretas várias vezes consecutivas. | 5 tentativas com senha errada consecutivamente     | Mensagem: "Conta temporariamente bloqueada por segurança". | **Falhou** |
| LG06 | Timeout na Sessão         | Permanecer logado por 30 minutos sem realizar nenhuma ação. | Após 30 minutos de inatividade                     | Sessão expirada, redirecionar para a página de login. | **Falhou** |

---

### Processo de Compra

| ID   | Cenário                   | Etapas do Teste                                          | Entrada                                             | Resultado Esperado                          | Status  |
|------|---------------------------|---------------------------------------------------------|----------------------------------------------------|---------------------------------------------|---------|
| PC01 | Compra Válida             | Adicionar produtos ao carrinho e finalizar a compra com um cartão válido. | Cartão: "1111-2222-3333-4444", CVC: "123", Expiração: "01/2026" | Compra realizada com sucesso.               | **Passou** |
| PC02 | Carrinho Vazio            | Tentar finalizar a compra sem produtos no carrinho.     | Carrinho vazio                                      | Mensagem: "O carrinho está vazio! Clique aqui para comprar produtos.".   | **Passou** |
| PC03 | Cartão Inválido           | Inserir número de cartão incorreto no pagamento.        | Cartão: "0000-0000-0000-0000"                      | Mensagem: "Número de cartão inválido".       | **Falhou** |
| PC04 | Cartão Vencido            | Inserir cartão com validade expirada.                   | Expiração: "10/2024"                               | Mensagem: "Cartão vencido".                 | **Falhou** |
| PC05 | Produto com Estoque Insuficiente | Adicionar ao carrinho um item fora de estoque.         | Produto: "Topo Azul", Estoque: 0                  | Mensagem: "Produto indisponível".           | **Não foi possível testar, todos os produtos estavam em estoque** |
| PC06 | Alterar Quantidade no Carrinho | Adicionar produtos ao carrinho e alterar a quantidade para um número inválido. | Quantidade: "-1" ou "0"                           | Mensagem: "Quantidade inválida".            | **Falhou** |
| PC07 | Logout Durante Compra     | Realizar logout antes de concluir a compra.             | Logout realizado                                   | Redirecionar para a página de login e esvaziar o carrinho. | **Passou** |
| PC08 | Timeout na Página de Pagamento | Permanecer na página de pagamento por mais de 10 minutos sem interagir. | Após 10 minutos de inatividade                     | Sessão expirada, redirecionar para o carrinho. | **Falhou** |

---

### **Casos Extremos**

| ID   | Cenário                   | Etapas do Teste                                          | Entrada                                             | Resultado Esperado                          | Status  |
|------|---------------------------|---------------------------------------------------------|----------------------------------------------------|---------------------------------------------|---------|
| CE01 | Limite Máximo de Caracteres | Inserir dados no limite máximo de caracteres permitido. | Nome: "A" * 50, E-mail: "jefter@gmail.com"          | Cadastro ou operação realizada com sucesso.  | **Passou** |
| CE02 | Excesso de Caracteres     | Inserir dados que excedam o limite máximo permitido.    | Nome: "A" * 51                                      | Mensagem: "Campo excede o limite de caracteres permitidos". | **Falhou** |

---

## 3. Resumo de Resultados

| Funcionalidade            | Testes Executados | Testes Bem-Sucedidos | Testes com Falha | Percentual de Sucesso |
|---------------------------|-------------------|----------------------|------------------|-----------------------|
| **Cadastro**               | 8                 | 5                    | 3                | 62,5%                 |
| **Login**                  | 6                 | 4                    | 2                | 66,7%                 |
| **Processo de Compra**     | 8                 | 3                    | 5                | 37,5%                 |
| **Casos Extremos**         | 2                 | 1                    | 1                | 50,0%                 |

---

## 4. Análise de Falhas

- **Cadastro (CD05 - Senha Curta):** O teste falhou porque o sistema permitiu a criação de uma senha com menos de 6 caracteres. **Sugestão:** Revisar a validação do comprimento mínimo da senha no backend, garantindo que senhas curtas sejam rejeitadas.
  
- **Cadastro (CD06 - Nome com Caracteres Especiais):** O teste falhou, pois o sistema não impediu o cadastro com caracteres especiais no nome. **Sugestão:** Validar o campo de nome para aceitar apenas letras e espaços, rejeitando caracteres especiais.

- **Cadastro (CD07 - Senha Sem Letras):** A falha ocorreu porque o sistema aceitou uma senha contendo apenas números. **Sugestão:** Revisar a lógica de validação de senha para garantir que ela contenha tanto números quanto letras.

---

- **Login (LG05 - Tempo de Bloqueio):** O teste falhou porque o sistema não bloqueou a conta após 5 tentativas de login com credenciais incorretas. **Sugestão:** Implementar uma lógica de bloqueio temporário após múltiplas tentativas erradas para proteger contra ataques de força bruta.

- **Login (LG06 - Timeout na Sessão):** O teste falhou porque o sistema não expirou a sessão após 30 minutos de inatividade. **Sugestão:** Implementar um tempo de expiração de sessão após um período sem atividade para aumentar a segurança do sistema.

---

- **Processo de Compra (PC03 - Cartão Inválido):** O teste falhou porque o sistema não bloqueou a compra com um cartão inválido. **Sugestão:** Implementar validações adicionais de número de cartão no backend para garantir que cartões inválidos sejam rejeitados.

- **Processo de Compra (PC04 - Cartão Vencido):** O teste falhou porque o sistema não bloqueou compras com um cartão vencido. **Sugestão:** Adicionar validações de validade de cartão de crédito, impedindo transações com cartões expirados.

- **Processo de Compra (PC06 - Alterar Quantidade no Carrinho):** O teste falhou porque o sistema aceitou valores inválidos para a quantidade do produto no carrinho. **Sugestão:** Validar a quantidade de produtos no carrinho para garantir que valores inválidos (como "-1" ou "0") sejam rejeitados.

- **Processo de Compra (PC08 - Timeout na Página de Pagamento):** O teste falhou porque o sistema não expirou a sessão após 10 minutos de inatividade na página de pagamento. **Sugestão:** Implementar a expiração automática da sessão durante o processo de pagamento para melhorar a segurança.

---

- **Casos extremos (CE02 - Excesso de Caracteres):** O teste falhou porque o sistema aceitou um número de caracteres que excede o limite permitido no campo "Nome". **Sugestão:** Implementar validação para limitar o número de caracteres permitidos no campo "Nome" (por exemplo, 50 caracteres).
---

## 5. Conclusão

Após a execução de uma bateria de testes abrangentes, o sistema apresentou uma taxa geral de sucesso de 59,4%, considerando todas as funcionalidades avaliadas. Apesar do desempenho satisfatório em vários cenários, diversas falhas foram identificadas, principalmente relacionadas à validação de dados, segurança e comportamento em situações específicas. 

Entre os principais problemas encontrados, destacam-se:
- Falhas na validação de entrada, como aceitação de senhas curtas, nomes com caracteres especiais e valores inválidos em campos numéricos.
- Deficiências nos mecanismos de segurança, incluindo ausência de bloqueio de conta após tentativas repetidas de login incorreto, falta de expiração de sessão por inatividade e aceitação de cartões inválidos ou expirados.
- Inconsistências em casos extremos, como falta de limitação no número de caracteres em campos de entrada.

Essas falhas comprometem tanto a experiência do usuário quanto a confiabilidade do sistema. Contudo, elas podem ser corrigidas com ajustes específicos no backend, reforço nas validações e melhorias nos controles de segurança.

A implementação dessas correções não apenas aumentará o percentual de sucesso dos testes, mas também garantirá maior segurança e usabilidade do sistema

---

## 6. Recomendações

1. **Fortalecer as validações de entrada**: Melhorar as validações de senha (mínimo de 6 caracteres, letras e números), nome (sem caracteres especiais) e e-mail (formato válido) para garantir dados corretos.

2. **Reforçar a segurança**: Implementar bloqueio de conta após tentativas de login incorretas e validar rigorosamente cartões de crédito durante as transações para evitar fraudes.

3. **Revisar o controle de sessão**: Adicionar expiração de sessão em pontos críticos, como login, processo de compra e pagamento, além de alertar o usuário antes de expirar a sessão.

4. **Expandir os testes de compatibilidade**: Realizar testes em diferentes navegadores e dispositivos para garantir uma experiência consistente e sem falhas em diversas plataformas.

5. **Automatizar testes e monitoramento**: Investir na automação de testes e ferramentas de monitoramento contínuo para detectar falhas rapidamente e garantir a qualidade do sistema.
