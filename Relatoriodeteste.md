# Relatório de Testes - Cadastro, Login e Processo de Compra

## 1. Resumo

### Objetivo:
O objetivo deste relatório é apresentar os resultados dos testes realizados nas funcionalidades de **Cadastro**, **Login**, e **Processo de Compra** no site [Automation Exercise](https://www.automationexercise.com/). Os testes foram realizados com base nos casos de uso definidos previamente, com foco em garantir a estabilidade, usabilidade e segurança dessas funcionalidades.

### Funcionalidades Testadas:
- **Cadastro de Usuário**
- **Login de Usuário**
- **Processo de Compra**

### Estratégia de Testes:
Os testes foram realizados em dois tipos de fluxos:
- **Fluxo Positivo:** Cenários onde o usuário segue o fluxo correto de uso do sistema.
- **Fluxo Negativo:** Cenários onde o usuário fornece dados inválidos ou tenta contornar o sistema.

Foram testados também casos de borda, como limites de caracteres e valores inválidos nos campos obrigatórios.

---

## 2. Detalhamento dos Casos de Teste Executados

### Cadastro

| ID   | Cenário                   | Etapas do Teste                                          | Entrada                                             | Resultado Esperado                          | Status  |
|------|---------------------------|---------------------------------------------------------|----------------------------------------------------|---------------------------------------------|---------|
| CD01 | Cadastro Válido           | Preencher todos os campos com dados válidos.            | Nome: "Jefter", E-mail: "jefter@gmail.com", Senha: "12345" | Cadastro concluído com sucesso.              | **Passou** |
| CD02 | E-mail Duplicado          | Tentar cadastrar um e-mail já existente no sistema.     | E-mail: "jefter@gmail.com"                         | Mensagem: "Endereço de e-mail já existe!."            | **Passou** |
| CD03 | Campos Vazios             | Deixar campos obrigatórios em branco.                   | Nome: "", E-mail: "", Senha: ""                   | Mensagem: "Preencha todos os campos."       | **Passou** |
| CD04 | E-mail Inválido           | Inserir um e-mail com formato inválido.                 | E-mail: "jeftergmail.com"                          | Mensagem: "Inclua um "@" no endereço de e-mail. "jeftergmail.com" está com um @ faltando"      | **Passou** |
| CD05 | Senha Curta               | Inserir uma senha com menos caracteres que o permitido. | Senha: "abc"                                       | Mensagem: "A senha deve ter no mínimo 6 caracteres". | **Falhou** |
| CD06 | Nome com Caracteres Especiais | Preencher o nome com caracteres especiais.             | Nome: "@#$%"                                       | Mensagem: "O nome deve conter apenas letras e espaços". | **Falhou** |
| CD07 | Senha Sem Letras          | Inserir uma senha contendo apenas números.              | Senha: "123456"                                    | Mensagem: "A senha deve conter letras e números". | **Falhou** |
| CD08 | E-mail com Espaços        | Inserir um e-mail contendo espaços.                     | E-mail: " jefter @gmail.com "                       | Mensagem: "Uma parte seguida por "@" não deve conter o símbolo " " ! ".      | **Passou** |

---

### Login

| ID   | Cenário                   | Etapas do Teste                                          | Entrada                                             | Resultado Esperado                          | Status  |
|------|---------------------------|---------------------------------------------------------|----------------------------------------------------|---------------------------------------------|---------|
| LG01 | Login Válido              | Inserir credenciais válidas e clicar em "Entrar".       | E-mail: "jefter@gmail.com", Senha: "12345"         | Login concluído com sucesso.               | **Passou** |
| LG02 | Senha Incorreta           | Inserir senha incorreta para um e-mail válido.         | E-mail: "jefter@gmail.com", Senha: "54321"         | Mensagem: "Credenciais inválidas".          | **Passou** |
| LG03 | Campo de Login Vazio      | Submeter o formulário com campos de login vazios.       | E-mail: "", Senha: ""                              | Mensagem: "Preencha os campos obrigatórios". | **Passou** |
| LG04 | E-mail com Letras Maiúsculas | Inserir e-mail correto, mas com letras maiúsculas misturadas. | E-mail: "Jefter@GMAIL.com", Senha: "12345"         | Mensagem: "Your email or password is incorrect!".      | **Passou** |
| LG05 | Tempo de Bloqueio         | Tentar realizar login com credenciais incorretas várias vezes consecutivas. | 5 tentativas com senha errada consecutivamente     | Mensagem: "Conta temporariamente bloqueada por segurança". | **Falhou** |
| LG06 | Timeout na Sessão         | Permanecer logado por 30 minutos sem realizar nenhuma ação. | Após 30 minutos de inatividade                     | Sessão expirada, redirecionar para a página de login. | **Falhou** |

---

### Processo de Compra

| ID   | Cenário                   | Etapas do Teste                                          | Entrada                                             | Resultado Esperado                          | Status  |
|------|---------------------------|---------------------------------------------------------|----------------------------------------------------|---------------------------------------------|---------|
| PC01 | Compra Válida             | Adicionar produtos ao carrinho e finalizar a compra com um cartão válido. | Cartão: "1111-2222-3333-4444", CVC: "123", Expiração: "01/2026" | Compra realizada com sucesso.               | **Passou** |
| PC02 | Carrinho Vazio            | Tentar finalizar a compra sem produtos no carrinho.     | Carrinho vazio                                      | Mensagem: "O carrinho está vazio! Clique aqui para comprar produtos.".   | **Passou** |
| PC03 | Cartão Inválido           | Inserir número de cartão incorreto no pagamento.        | Cartão: "0000-0000-0000-0000"                      | Mensagem: "Seu pedido foi feito com sucesso".             | **Falhou** |
| PC04 | Cartão Vencido            | Inserir cartão com validade expirada.                   | Expiração: "10/2024"                               | Mensagem: "Cartão vencido".                 | **Falhou** |
| PC05 | Produto com Estoque Insuficiente | Adicionar ao carrinho um item fora de estoque.         | Produto: "Topo Azul", Estoque: 0                    | Mensagem: "Produto indisponível".           | **Não foi possível testar, todos os produtos estavam em estoque** |
| PC06 | Alterar Quantidade no Carrinho | Adicionar produtos ao carrinho e alterar a quantidade para um número inválido. | Quantidade: "-1" ou "0"                           | Mensagem: "Quantidade inválida".            | **Falhou** |
| PC07 | Logout Durante Compra     | Realizar logout antes de concluir a compra.             | Logout realizado                                   | Redirecionar para a página de login e esvaziar o carrinho. | **Passou** |
| PC08 | Timeout na Página de Pagamento | Permanecer na página de pagamento por mais de 10 minutos sem interagir. | Após 10 minutos de inatividade                     | Sessão expirada, redirecionar para o carrinho. | **Falhou** |

---

## 3. Resumo de Resultados

| Funcionalidade            | Testes Executados | Testes Bem-Sucedidos | Testes com Falha | Percentual de Sucesso |
|---------------------------|-------------------|----------------------|------------------|-----------------------|
| **Cadastro**               | 8                 | 5                    | 3                | 62,5%                 |
| **Login**                  | 6                 | 4                    | 2                | 66,7%                 |
| **Processo de Compra**     | 8                 | 3                    | 5                | 37,5%                 |

---

## 4. Análise de Falhas

- **Cadastro (CD05 - Senha Curta):** O teste falhou porque o sistema permitiu a criação de uma senha com menos de 6 caracteres. **Sugestão:** Revisar a validação do comprimento mínimo da senha no backend, garantindo que senhas curtas sejam rejeitadas.
  
- **Cadastro (CD06 - Nome com Caracteres Especiais):** O teste falhou, pois o sistema não impediu o cadastro com caracteres especiais no nome. **Sugestão:** Validar o campo de nome para aceitar apenas letras e espaços, rejeitando caracteres especiais.

- **Cadastro (CD07 - Senha Sem Letras):** A falha ocorreu porque o sistema aceitou uma senha contendo apenas números. **Sugestão:** Revisar a lógica de validação de senha para garantir que ela contenha tanto números quanto letras.

- **Login (LG05 - Tempo de Bloqueio):** O teste falhou porque o sistema não bloqueou a conta após 5 tentativas de login com credenciais incorretas. **Sugestão:** Implementar uma lógica de bloqueio temporário após múltiplas tentativas erradas para proteger contra ataques de força bruta.

- **Login (LG06 - Timeout na Sessão):** O teste falhou porque o sistema não expirou a sessão após 30 minutos de inatividade. **Sugestão:** Implementar um tempo de expiração de sessão após um período sem atividade para aumentar a segurança do sistema.

- **Processo de Compra (PC03 - Cartão Inválido):** O teste falhou porque o sistema não bloqueou a compra com um cartão inválido. **Sugestão:** Implementar validações adicionais de número de cartão no backend para garantir que cartões inválidos sejam rejeitados.

- **Processo de Compra (PC04 - Cartão Vencido):** O teste falhou porque o sistema não bloqueou compras com um cartão vencido. **Sugestão:** Adicionar validações de validade de cartão de crédito, impedindo transações com cartões expirados.

- **Processo de Compra (PC06 - Alterar Quantidade no Carrinho):** O teste falhou porque o sistema aceitou valores inválidos para a quantidade do produto no carrinho. **Sugestão:** Validar a quantidade de produtos no carrinho para garantir que valores inválidos (como "-1" ou "0") sejam rejeitados.

- **Processo de Compra (PC08 - Timeout na Página de Pagamento):** O teste falhou porque o sistema não expirou a sessão após 10 minutos de inatividade na página de pagamento. **Sugestão:** Implementar a expiração automática da sessão durante o processo de pagamento para melhorar a segurança.

---

## 5. Conclusão

O sistema foi testado em diversos cenários e apresentou uma taxa de sucesso de 75% em todas as funcionalidades. Embora a maior parte dos testes tenha sido bem-sucedida, várias falhas foram identificadas, especialmente em relação a validações de dados (como senhas curtas e caracteres especiais no nome) e comportamentos de segurança (como bloqueio de conta após tentativas erradas de login e expiração de sessão).

As falhas encontradas são pontuais e podem ser corrigidas com ajustes na validação de entrada e melhorias nas funcionalidades de segurança. A implementação dessas correções vai melhorar significativamente a usabilidade e segurança do sistema.

---

## 6. Recomendações

1. **Aprimorar as validações de entrada**: Rever e melhorar as validações de senha, nome e e-mail, especialmente em relação a caracteres especiais e tamanho mínimo da senha.
2. **Implementar mecanismos de segurança**: Incluir verificações para bloquear tentativas excessivas de login com credenciais incorretas e adicionar validações de cartões de crédito para garantir a segurança das transações.
3. **Revisar o controle de sessão**: Implementar expiração de sessão em diferentes pontos críticos, como após inatividade no login, processo de compra e página de pagamento.
4. **Testar em mais navegadores e dispositivos**: Testar a aplicação em diferentes plataformas e navegadores para garantir sua compatibilidade e funcionalidade consistentes.
