# Automação de Testes de Cadastro e Login com Selenium

Este repositório contém testes automatizados para verificar as funcionalidades de cadastro e login no site [Automation Exercise](https://automationexercise.com). Os testes foram desenvolvidos em Python, utilizando a biblioteca Selenium.

---

## Índice

1. [Pré-requisitos](#pré-requisitos)  
2. [Casos de Teste Implementados](#casos-de-teste-implementados)  
   - [Cadastro](#cadastro)  
   - [Login](#login)  
3. [Código](#código)  
   - [Testes de Cadastro](#testes-de-cadastro)  
   - [Testes de Login](#testes-de-login)

---

## Pré-requisitos

- **Python**: Versão 3.7 ou superior.
- **Selenium**: Instale via pip:
  ```bash
  pip install selenium

## Casos de Teste Implementados
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

---

## Código
### Testes de Cadastro: 
```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
import time

# Configuração do WebDriver
driver = webdriver.Chrome()  # Certifique-se de ter o ChromeDriver instalado e configurado.

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
driver = webdriver.Chrome()  # Certifique-se de ter o ChromeDriver instalado e configurado.

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
