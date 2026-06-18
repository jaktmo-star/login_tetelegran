# 🎓 Consulta de Cursos SENAI EAD com Envio para Telegram

## 📌 Descrição

Este projeto realiza o acesso automático ao portal do SENAI EAD utilizando Selenium, consulta a quantidade de cursos matriculados e envia a informação para um chat do Telegram.

O objetivo é demonstrar a utilização de automação web com Python, integração com APIs e armazenamento seguro de configurações através de um arquivo JSON.

---

## 🚀 Tecnologias Utilizadas

### Selenium

Biblioteca utilizada para automatizar a navegação no navegador.

Funções utilizadas no projeto:

* Abrir o site do SENAI EAD.
* Preencher CPF e senha.
* Clicar nos botões de acesso.
* Fechar janelas modais.
* Ler informações da página após o login.

---

### WebDriver Manager

Responsável por baixar e configurar automaticamente a versão correta do ChromeDriver.

Sem essa biblioteca seria necessário baixar e configurar o driver manualmente.

---

### Requests

Biblioteca utilizada para realizar requisições HTTP.

Neste projeto ela é responsável por enviar mensagens para a API do Telegram.

Exemplo:

```python
requests.post(...)
```

---

### JSON

Biblioteca utilizada para ler o arquivo de configurações do projeto.

Ela permite armazenar informações sensíveis fora do código, como:

* CPF
* Senha
* Token do Telegram
* Chat ID

Exemplo:

```python
with open("config.json") as arquivo:
    config = json.load(arquivo)
```

---

## 📂 Estrutura do Projeto

```text
projeto/
│
├── main.py
├── config.json
└── README.md
```

---

## ⚙️ Arquivo config.json

Crie um arquivo chamado:

```text
config.json
```

Com a seguinte estrutura:

```json
{
    "cpf": "SEU_CPF",
    "senha": "SUA_SENHA",
    "telegram_token": "SEU_TOKEN",
    "telegram_chat_id": "SEU_CHAT_ID"
}
```

### Por que utilizar um arquivo JSON?

Separar as configurações do código possui diversas vantagens:

* Maior segurança.
* Facilita a manutenção.
* Evita exposição de senhas no código-fonte.
* Permite reutilizar o programa com diferentes usuários sem alterar o código.

---

## 📥 Instalação

Instale as dependências:

```bash
pip install selenium
pip install webdriver-manager
pip install requests
```

Ou:

```bash
pip install selenium webdriver-manager requests
```

---

## ▶️ Execução

Execute o programa:

```bash
python main.py
```

O sistema irá:

1. Abrir o navegador.
2. Acessar o portal do SENAI EAD.
3. Realizar login.
4. Fechar a janela inicial.
5. Consultar a quantidade de cursos.
6. Enviar a informação para o Telegram.
7. Encerrar o navegador.

---

## 📨 Exemplo de Mensagem

```text
📚 SENAI EAD

Cursos matriculados: (0)
```

---

## 🔍 Explicação do Fluxo do Código

### Leitura das configurações

O programa abre o arquivo JSON e carrega os dados necessários para login e integração com o Telegram.

```python
with open("config.json", encoding="utf-8") as arquivo:
    config = json.load(arquivo)
```

---

### Inicialização do navegador

O Selenium cria uma instância do Google Chrome para executar a automação.

```python
driver = webdriver.Chrome(
    service=Service(ChromeDriverManager().install())
)
```

---

### Login no portal

O sistema localiza os campos de CPF e senha através do ID dos elementos da página.

```python
driver.find_element(...)
```

Após preencher os campos, os botões são acionados automaticamente.

---

### Esperas Inteligentes

O projeto utiliza WebDriverWait para aguardar o carregamento dos elementos antes de interagir com eles.

Isso evita erros causados por páginas ainda não carregadas.

Exemplo:

```python
wait.until(
    EC.visibility_of_element_located(...)
)
```

---

### Consulta dos Cursos

Após o login, o programa localiza o elemento responsável por exibir a quantidade de cursos matriculados.

```python
cursos = driver.find_element(
    id,
    "contador-cursos"
).text
```

---

### Envio para o Telegram

A biblioteca Requests envia uma requisição POST para a API oficial do Telegram.

```python
requests.post(
    f"https://api.telegram.org/bot{TOKEN}/sendMessage",
    data={
        "chat_id": CHAT_ID,
        "text": mensagem
    }
)
```

---

## 🎯 Objetivos de Aprendizado

Este projeto demonstra conceitos importantes de automação:

* Automação Web com Selenium.
* Manipulação de arquivos JSON.
* Integração com APIs.
* Utilização de requisições HTTP.
* Uso de esperas explícitas.
* Boas práticas para armazenamento de credenciais.

---

## 👨‍💻 Autor

Elcio Mello

Projeto desenvolvido para fins de estudo e prática de automação com Python.
