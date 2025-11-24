## 🐍 Fase 2: Introdução ao FastAPI

O **FastAPI** é um *framework* web moderno, rápido (de alto desempenho) e fácil de usar para construir APIs com Python 3.7+. Ele se destaca por dois motivos principais:

1.  **Velocidade:** É um dos frameworks Python mais rápidos.
2.  **Documentação Automática:** Usa o **Type Hinting** do Python (que vimos na Fase 1) para fazer validação de dados, serialização e, o mais importante, **gerar automaticamente a documentação interativa da sua API (Swagger UI e ReDoc)**.

### 1\. Preparação e Instalação

Assumindo que você está com o ambiente virtual (`.venv`) ativo na pasta `idp_backend`:

1.  **Instale o FastAPI e o Uvicorn:**

      * **FastAPI:** O framework principal.
      * **Uvicorn:** Um servidor ASGI (para aplicações assíncronas) que executa o FastAPI.

    <!-- end list -->

    ```bash
    pip install fastapi "uvicorn[standard]"
    ```

### 2\. O Primeiro Arquivo (Hello World)

Crie um arquivo chamado `main.py` dentro da sua pasta `idp_backend` e adicione o seguinte código:

```python
# idp_backend/main.py

from fastapi import FastAPI

# 1. Instanciar o objeto FastAPI
app = FastAPI()

# 2. Definir a primeira Rota/Endpoint
# O decorador @app.get define um endpoint HTTP GET no caminho raiz ("/")
@app.get("/")
def home():
    # Retornamos um dicionário Python. O FastAPI
    # automaticamente o serializa para JSON.
    return {"message": "Bem-vindo à API do IDP! Status: UP"}
```

### 3\. Rodando o Servidor

O **Uvicorn** é usado para executar a aplicação. O formato do comando é: `uvicorn <nome_do_arquivo>:<nome_do_objeto_FastAPI>`.

```bash
uvicorn main:app --reload
```

  * `main`: o arquivo Python (`main.py`).
  * `app`: o objeto que você criou (`app = FastAPI()`).
  * `--reload`: Modo de desenvolvimento. O servidor reinicia automaticamente a cada mudança no código.

Ao rodar, o servidor estará disponível em `http://127.0.0.1:8000`.

  * Acesse `http://127.0.0.1:8000` no seu navegador para ver a mensagem JSON.
  * Acesse **`http://127.0.0.1:8000/docs`** para ver a documentação interativa automática\! **(Este é o poder do FastAPI\!)**

-----

## ⚙️ CRUD Básico e Modelos Pydantic

Vamos criar nosso primeiro recurso para o IDP: **Modelos de Projetos**. Para fazer isso, usaremos o **Pydantic**.

### 4\. Pydantic para Validação de Dados

**Pydantic** é a biblioteca que o FastAPI usa para definir a estrutura dos dados (Modelos). Ele garante que os dados de entrada (o que o cliente envia) e de saída (o que o servidor retorna) estejam formatados e tipados corretamente.

No `main.py`, vamos adicionar o Pydantic:

```python
# idp_backend/main.py (continuação)

from typing import List, Optional # Para Type Hinting
from fastapi import FastAPI
from pydantic import BaseModel # Importar o Pydantic

app = FastAPI()

# Simulação de um "banco de dados" na memória
projetos_db = []
proximo_id = 1

# 1. Definição do Modelo Pydantic (Schema)
# Isso define a estrutura do objeto 'Projeto'
class Projeto(BaseModel):
    # Campos obrigatórios e seus tipos
    nome: str
    owner: str
    
    # Campo opcional (pode ser None)
    descricao: Optional[str] = None 
    
    # O campo 'id' será um campo de leitura (retorno)
    # Apenas o schema de resposta usará este.
    id: Optional[int] = None 

# ----------------------------------------------------
# A partir daqui, criamos as operações CRUD (Create, Read, Update, Delete)
# ----------------------------------------------------

# CREATE (Criar um novo projeto)
@app.post("/projetos/")
# O Type Hinting (novo_projeto: Projeto) faz a validação automática!
def criar_projeto(novo_projeto: Projeto):
    global proximo_id
    
    # Criamos um dicionário a partir do objeto Pydantic
    projeto_dict = novo_projeto.model_dump() # .dict() no Pydantic v1
    projeto_dict["id"] = proximo_id
    
    projetos_db.append(projeto_dict)
    proximo_id += 1
    
    return projeto_dict

# READ (Listar todos os projetos)
@app.get("/projetos/", response_model=List[Projeto])
def listar_projetos():
    return projetos_db
    
# READ (Buscar um projeto por ID)
# O path parameter 'id_projeto' é tipado como 'int'
@app.get("/projetos/{id_projeto}", response_model=Projeto)
def buscar_projeto(id_projeto: int):
    # Lógica simples de busca
    for projeto in projetos_db:
        if projeto.get("id") == id_projeto:
            return projeto
    
    # Se não encontrar, retornaríamos um erro 404
    # Por enquanto, vamos retornar uma mensagem simples para focar no fluxo
    return {"message": f"Projeto com ID {id_projeto} não encontrado"}
```

### 5\. Testando no Swagger UI

Com o servidor Uvicorn rodando (`uvicorn main:app --reload`):

1.  Acesse **`http://127.0.0.1:8000/docs`**.
2.  Expanda a rota **`POST /projetos/`**.
3.  Clique em **"Try it out"**.
4.  No campo **Request body**, insira um JSON no formato esperado:
    ```json
    {
      "nome": "Projeto React-FastAPI",
      "owner": "Time Frontend-Backend",
      "descricao": "Nossa IDP"
    }
    ```
5.  Clique em **"Execute"**. Se der certo, você verá o projeto com o `id` retornado (Status 200).
6.  Agora, expanda a rota **`GET /projetos/`** e execute para ver a lista completa.

-----

## 🎯 Tarefa da Fase 2

1.  Verifique se o seu `main.py` está funcionando conforme o esperado, com as rotas `POST` e `GET` para `/projetos/`.
2.  Adicione mais uma rota ao seu `main.py`:
      * **UPDATE (`@app.put`)**: Crie uma rota `@app.put("/projetos/{id_projeto}")` que receba o `id_projeto` e um objeto `Projeto` no corpo da requisição. Sua lógica deve:
          * Iterar sobre `projetos_db`.
          * Encontrar o projeto pelo ID.
          * Atualizar o `nome`, `owner` e `descricao` do projeto encontrado.
          * Retornar o projeto atualizado.
