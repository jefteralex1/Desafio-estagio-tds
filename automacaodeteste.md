# Automação de Testes com Selenium

Este arquivo contém exemplos de testes automatizados usando **Selenium WebDriver** com Python. O objetivo é realizar testes no site **Automation Exercise** para verificar funcionalidades como cadastro de usuários.

## 1. Execução

Executei o código no google colab, instalando as seguintes dependências:
- **selenium**: A biblioteca que permite a automação de navegação em sites.
- **webdriver-manager**: Ferramenta para gerenciar o download do ChromeDriver.

## código

```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from webdriver_manager.chrome import ChromeDriverManager

# Configuração do ChromeDriver
chrome_options = Options()
chrome_options.add_argument("--headless")
chrome_options.add_argument("--no-sandbox")
chrome_options.add_argument("--disable-dev-shm-usage")

# Configurações do ChromeDriver
service = Service(ChromeDriverManager().install())
driver = webdriver.Chrome(service=service, options=chrome_options)
wait = WebDriverWait(driver, 10)

# URL do site Automation Exercise
URL = "https://www.automationexercise.com/"

def acessar_site():
    driver.get(URL)
    wait.until(EC.presence_of_element_located((By.ID, "header")))

def acessar_pagina_cadastro():
    """Navega até a página de cadastro."""
    driver.find_element(By.LINK_TEXT, "Signup / Login").click()
    wait.until(EC.presence_of_element_located((By.CSS_SELECTOR, "[data-qa='signup-name']")))

def preencher_formulario_cadastro(nome, email):
    driver.find_element(By.CSS_SELECTOR, "[data-qa='signup-name']").send_keys(nome)
    driver.find_element(By.CSS_SELECTOR, "[data-qa='signup-email']").send_keys(email)
    driver.find_element(By.CSS_SELECTOR, "[data-qa='signup-button']").click()

def verificar_mensagem(mensagem_esperada):
    body_text = driver.find_element(By.TAG_NAME, "body").text
    assert mensagem_esperada in body_text, f"Erro esperado: '{mensagem_esperada}', mas não encontrado na página."

# Casos de Teste
def teste_cadastro_valido():
    acessar_pagina_cadastro()
    preencher_formulario_cadastro("Jefter", "jefter@gmail.com")
    verificar_mensagem("Login to your account")
    print("Teste Cadastro Válido: PASSOU")

def teste_email_duplicado():
    acessar_pagina_cadastro()
    preencher_formulario_cadastro("Jefter", "jefter@gmail.com")
    verificar_mensagem("Email Address already exist!")
    print("Teste E-mail Duplicado: PASSOU")

try:
    acessar_site()

    teste_cadastro_valido()
    teste_email_duplicado()

finally:
    driver.quit()
```


---

### 3. Conclusão
Esse script de automação de testes com Selenium pode ser usado como base para validar funcionalidades em sites. Com Selenium, é possível simular interações de usuários e verificar se o comportamento do site está correto.
