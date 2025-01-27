# Automação de Testes de Cadastro e Login com Selenium

Este repositório contém testes automatizados para verificar as funcionalidades de cadastro e login no site [Automation Exercise](https://automationexercise.com). Os testes foram desenvolvidos em Python, utilizando a biblioteca Selenium.

---

## Índice

1. [Pré-requisitos](#1-pré-requisitos)  
2. [Casos de Teste Implementados](#2-casos-de-teste-implementados)  
   - [Cadastro](#cadastro)  
   - [Login](#login)  
3. [Código](#3-código)  
   - [Testes de Cadastro](#cadastro)  
   - [Testes de Login](#login)
   - [Testes de Login](#Processo-de-compra)
4. [Resultado](#4-Resultado)

---

## 1. Pré-requisitos

- **Python**: Versão 3.7 ou superior.
- **Selenium**: Instale via pip:
  ```bash
  pip install selenium

---

## 2. Casos de Teste Implementados
### Cadastro:
1. **Cadastro Válido:** Cadastrar um novo usuário com dados válidos.
2. **E-mail Duplicado:** Testar a mensagem de erro ao cadastrar um e-mail já existente.
3. **E-mail Inválido:** Verificar a validação de formato de e-mail.
4. **Campos Vazios:** Garantir que o sistema exige preenchimento de todos os campos.
5. **Senha Curta:** Testar a validação para senhas com menos de 6 caracteres.
6. **Nome com Caracteres Especiais:** Verificar se nomes com caracteres especiais são rejeitados.
7. **Senha Sem Letras:** Testar a validação para senhas compostas apenas por números.
8. **E-mail com Espaços:** Verificar a rejeição de e-mails contendo espaços.

### Login:

1. **Login Válido:** Realizar login com credenciais corretas.
2. **Senha Incorreta:** Testar a mensagem de erro ao inserir senha incorreta.
3. **Campos Vazios:** Garantir que o sistema exige preenchimento de todos os campos.
4. **E-mail com Letras Maiúsculas:** Testar login com e-mail correto, mas com letras maiúsculas.
5. **Tempo de Bloqueio:** Verificar bloqueio após várias tentativas de login com senha errada.
6. **Timeout na Sessão:** Validar a expiração da sessão após inatividade de 30 minutos.

### Processo de Compra:
1. **Compra Válida:** Realizar a compra de um produto com um cartão de crédito válido.
2. **Carrinho Vazio:** Verificar o comportamento ao acessar o carrinho vazio.
3. **Cartão Inválido:** Tentar realizar uma compra com um cartão de crédito inválido.
4. **Cartão Vencido:** Tentar realizar uma compra com um cartão de crédito vencido.

---

## 3. Código
### Testes de Cadastro: 
```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
import time

# Configuração do WebDriver
driver = webdriver.Chrome()

# URL base do site de teste
base_url = "https://automationexercise.com/signup"

def test_cadastro_valido():
    driver.get(base_url)
    driver.find_element(By.ID, "signup-name").send_keys("Jefter")
    driver.find_element(By.ID, "signup-email").send_keys("jefter@gmail.com")
    driver.find_element(By.ID, "signup-password").send_keys("123456")
    driver.find_element(By.ID, "signup-submit").click()
    assert "Cadastro concluído com sucesso" in driver.page_source

def test_email_duplicado():
    driver.get(base_url)
    driver.find_element(By.ID, "signup-name").send_keys("Jefter")
    driver.find_element(By.ID, "signup-email").send_keys("jefter@gmail.com")  # E-mail duplicado
    driver.find_element(By.ID, "signup-password").send_keys("123456")
    driver.find_element(By.ID, "signup-submit").click()
    assert "E-mail já cadastrado" in driver.page_source

def test_email_invalido():
    driver.get(base_url)
    driver.find_element(By.ID, "signup-name").send_keys("Jefter")
    driver.find_element(By.ID, "signup-email").send_keys("jeftergmail.com")  # E-mail inválido
    driver.find_element(By.ID, "signup-password").send_keys("123456")
    driver.find_element(By.ID, "signup-submit").click()
    assert "Formato de e-mail inválido" in driver.page_source

def test_campos_vazios():
    driver.get(base_url)
    driver.find_element(By.ID, "signup-submit").click()  # Não preencher campos
    assert "Preencha todos os campos" in driver.page_source

def test_senha_curta():
    driver.get(base_url)
    driver.find_element(By.ID, "signup-name").send_keys("Jefter")
    driver.find_element(By.ID, "signup-email").send_keys("jefter@gmail.com")
    driver.find_element(By.ID, "signup-password").send_keys("123")  # Senha curta
    driver.find_element(By.ID, "signup-submit").click()
    assert "A senha deve ter no mínimo 6 caracteres" in driver.page_source

def test_nome_com_caracteres_especiais():
    driver.get(base_url)
    driver.find_element(By.ID, "signup-name").send_keys("@#$%")  # Nome com caracteres especiais
    driver.find_element(By.ID, "signup-email").send_keys("jefter@gmail.com")
    driver.find_element(By.ID, "signup-password").send_keys("123456")
    driver.find_element(By.ID, "signup-submit").click()
    assert "O nome deve conter apenas letras e espaços" in driver.page_source

def test_senha_sem_letras():
    driver.get(base_url)
    driver.find_element(By.ID, "signup-name").send_keys("Jefter")
    driver.find_element(By.ID, "signup-email").send_keys("jefter@gmail.com")
    driver.find_element(By.ID, "signup-password").send_keys("123456")  # Senha sem letras
    driver.find_element(By.ID, "signup-submit").click()
    assert "A senha deve conter letras e números" in driver.page_source

def test_email_com_espacos():
    driver.get(base_url)
    driver.find_element(By.ID, "signup-name").send_keys("Jefter")
    driver.find_element(By.ID, "signup-email").send_keys(" jefter @gmail.com ")  # E-mail com espaços
    driver.find_element(By.ID, "signup-password").send_keys("123456")
    driver.find_element(By.ID, "signup-submit").click()
    assert "Formato de e-mail inválido" in driver.page_source

# Executa os testes
if __name__ == "__main__":
    try:
        test_cadastro_valido()
        test_email_duplicado()
        test_email_invalido()
        test_campos_vazios()
        test_senha_curta()
        test_nome_com_caracteres_especiais()
        test_senha_sem_letras()
        test_email_com_espacos()
        print("Todos os testes foram concluídos com sucesso.")
    finally:
        driver.quit()
```

### Login:

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
import time

# Configuração do WebDriver
driver = webdriver.Chrome()

# URL base do site de teste
base_url = "https://automationexercise.com/login"

def test_login_valido():
    driver.get(base_url)
    driver.find_element(By.ID, "login-email").send_keys("jefter@gmail.com")
    driver.find_element(By.ID, "login-password").send_keys("12345")
    driver.find_element(By.ID, "login-submit").click()
    assert "Login concluído com sucesso" in driver.page_source

def test_senha_incorreta():
    driver.get(base_url)
    driver.find_element(By.ID, "login-email").send_keys("jefter@gmail.com")
    driver.find_element(By.ID, "login-password").send_keys("54321")  # Senha incorreta
    driver.find_element(By.ID, "login-submit").click()
    assert "E-mail ou senha inválidos" in driver.page_source

def test_campos_vazios():
    driver.get(base_url)
    driver.find_element(By.ID, "login-submit").click()  # Não preencher campos
    assert "Preencha os campos obrigatórios" in driver.page_source

def test_email_com_letras_maiusculas():
    driver.get(base_url)
    driver.find_element(By.ID, "login-email").send_keys("JEFTER@GMAIL.COM")  # E-mail com letras maiúsculas
    driver.find_element(By.ID, "login-password").send_keys("12345")
    driver.find_element(By.ID, "login-submit").click()
    assert "E-mail ou senha inválidos" in driver.page_source

def test_tempo_de_bloqueio():
    driver.get(base_url)
    for _ in range(5):  # Tentar 5 vezes com credenciais incorretas
        driver.find_element(By.ID, "login-email").send_keys("jefter@gmail.com")
        driver.find_element(By.ID, "login-password").send_keys("54321")  # Senha errada
        driver.find_element(By.ID, "login-submit").click()
        time.sleep(1)  # Aguardar 1 segundo entre tentativas
    assert "Conta temporariamente bloqueada por segurança" in driver.page_source

def test_timeout_na_sessao():
    driver.get(base_url)
    driver.find_element(By.ID, "login-email").send_keys("jefter@gmail.com")
    driver.find_element(By.ID, "login-password").send_keys("12345")
    driver.find_element(By.ID, "login-submit").click()
    time.sleep(1800)  # Aguarde 30 minutos (30 * 60 segundos)
    driver.refresh()  # Atualiza a página para verificar o timeout
    assert "Sessão expirada" in driver.page_source

# Executa os testes
if __name__ == "__main__":
    try:
        test_login_valido()
        test_senha_incorreta()
        test_campos_vazios()
        test_email_com_letras_maiusculas()
        test_tempo_de_bloqueio()
        test_timeout_na_sessao()
        print("Todos os testes foram concluídos com sucesso.")
    finally:
        driver.quit()
```

### Processo de compra:
```Python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

# Configuração do WebDriver
def setup_driver():
    driver = webdriver.Chrome()
    driver.maximize_window()
    base_url = "https://automationexercise.com"
    return driver, base_url

# Teste PC01: Compra Válida
def test_valid_purchase(driver, base_url):
    driver.get(base_url)
    WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.LINK_TEXT, "Products"))
    ).click()  # Ir para a página de produtos
    WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.CLASS_NAME, "add-to-cart"))
    ).click()  # Clicar em adicionar ao carrinho
    WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.LINK_TEXT, "View Cart"))
    ).click()  # Ir para o carrinho

    assert "Product successfully added to your cart" in driver.page_source
    WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.LINK_TEXT, "Proceed To Checkout"))
    ).click()

    # Preenchendo os detalhes de pagamento (simulados)
    driver.find_element(By.ID, "name-on-card").send_keys("Jefter Silva")
    driver.find_element(By.ID, "card-number").send_keys("1111-2222-3333-4444")
    driver.find_element(By.ID, "cvc").send_keys("123")
    driver.find_element(By.ID, "expiry-month").send_keys("10")
    driver.find_element(By.ID, "expiry-year").send_keys("2026")
    driver.find_element(By.ID, "submit").click()

    # Validar se o pedido foi concluído
    WebDriverWait(driver, 10).until(
        EC.presence_of_element_located((By.XPATH, "//*[contains(text(), 'Your order has been placed successfully!')]"))
    )

# Teste PC02: Carrinho Vazio
def test_empty_cart(driver, base_url):
    driver.get(f"{base_url}/view_cart")  # Acessar diretamente a página do carrinho
    WebDriverWait(driver, 10).until(
        EC.title_is("Shopping Cart"))  # Verificar se está na página do carrinho
    assert "Your Cart is Empty" in driver.page_source  # Certificar que o carrinho está vazio

# Teste PC03: Cartão Inválido
def test_invalid_card(driver, base_url):
    driver.get(base_url)
    WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.LINK_TEXT, "Products"))
    ).click()
    WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.CLASS_NAME, "add-to-cart"))
    ).click()
    WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.LINK_TEXT, "View Cart"))
    ).click()
    WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.LINK_TEXT, "Proceed To Checkout"))
    ).click()

    # Preenchendo os detalhes de pagamento com cartão inválido
    driver.find_element(By.ID, "name-on-card").send_keys("Jefter Silva")
    driver.find_element(By.ID, "card-number").send_keys("0000-0000-0000-0000")
    driver.find_element(By.ID, "cvc").send_keys("123")
    driver.find_element(By.ID, "expiry-month").send_keys("10")
    driver.find_element(By.ID, "expiry-year").send_keys("2026")
    driver.find_element(By.ID, "submit").click()

    # Validar mensagem de erro
    WebDriverWait(driver, 10).until(
        EC.presence_of_element_located((By.XPATH, "//*[contains(text(), 'Número de cartão inválido')]"))
    )

# Teste PC04: Cartão Vencido
def test_expired_card(driver, base_url):
    driver.get(base_url)
    WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.LINK_TEXT, "Products"))
    ).click()
    WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.CLASS_NAME, "add-to-cart"))
    ).click()
    WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.LINK_TEXT, "View Cart"))
    ).click()
    WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.LINK_TEXT, "Proceed To Checkout"))
    ).click()

    # Preenchendo os detalhes de pagamento com cartão vencido
    driver.find_element(By.ID, "name-on-card").send_keys("Jefter Silva")
    driver.find_element(By.ID, "card-number").send_keys("1111-2222-3333-4444")
    driver.find_element(By.ID, "cvc").send_keys("123")
    driver.find_element(By.ID, "expiry-month").send_keys("10")
    driver.find_element(By.ID, "expiry-year").send_keys("2024")
    driver.find_element(By.ID, "submit").click()

    # Validar mensagem de erro
    WebDriverWait(driver, 10).until(
        EC.presence_of_element_located((By.XPATH, "//*[contains(text(), 'Cartão vencido')]"))
    )

# Execução dos testes
def run_tests():
    driver, base_url = setup_driver()
    try:
        test_valid_purchase(driver, base_url)
        test_empty_cart(driver, base_url)
        test_invalid_card(driver, base_url)
        test_expired_card(driver, base_url)
        print("Todos os testes foram concluídos com sucesso.")
    finally:
        driver.quit()

if __name__ == "__main__":
    run_tests()
```

---

## 4. Resultados
Os resultados destes e de outros testes podem ser consultados no [arquivo](automacaodetestes.md)
