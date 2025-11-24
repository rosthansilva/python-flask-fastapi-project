## 🐍 Fase 1: Fundamentos Python Essenciais

Neste passo, o foco é entender os blocos de construção de qualquer programa Python.

### 1\. Variáveis e Tipos de Dados

No Python, você não precisa declarar o tipo de uma variável; ele é inferido.

| Tipo | O que é | Exemplo |
| :--- | :--- | :--- |
| **`int`** | Números inteiros. | `idade = 30` |
| **`float`** | Números com casas decimais. | `preco = 19.99` |
| **`str`** | Texto (string). | `nome = "João Silva"` |
| **`bool`** | Valor booleano (`True` ou `False`). | `esta_ativo = True` |

**Exemplo Prático:**

```python
# Atribuição de variáveis
linguagem = "Python" # str
ano = 1991           # int
versao = 3.10        # float
gostou = True        # bool

print(f"Eu uso a linguagem {linguagem} (Criada em {ano}) na versão {versao}. Isso é {gostou}.")
```

### 2\. Estruturas de Dados Fundamentais

Esses são os "contêineres" onde você armazena coleções de dados.

#### A. Listas (`list`)

  * Coleção **ordenada** e **mutável** (pode ser modificada).
  * É o tipo mais comum e flexível.

<!-- end list -->

```python
# Lista de tecnologias para o IDP
tecnologias = ["React", "FastAPI", "TypeScript", "Python"]

# Acessando um item (indexação começa em 0)
print(tecnologias[1]) # Saída: FastAPI

# Adicionando um item (mutabilidade)
tecnologias.append("Docker")
print(tecnologias) 
# Saída: ['React', 'FastAPI', 'TypeScript', 'Python', 'Docker']
```

#### B. Dicionários (`dict`) - **Crucial para APIs\!**

  * Coleção **não ordenada** (no Python moderno, mantém a ordem de inserção) de pares **chave: valor**.
  * **As chaves devem ser únicas e imutáveis** (geralmente strings).
  * **É assim que os dados JSON (trocados por APIs) são representados em Python.**

<!-- end list -->

```python
# Representação de um Usuário (como um objeto JSON viria)
usuario = {
    "id": 101,
    "nome": "Alice",
    "email": "alice@exemplo.com",
    "ativo": True
}

# Acessando um valor pela chave
print(usuario["nome"]) # Saída: Alice

# Modificando um valor
usuario["ativo"] = False
print(usuario)
# Saída: {'id': 101, 'nome': 'Alice', 'email': 'alice@exemplo.com', 'ativo': False}
```

### 3\. Fluxo de Controle: Condicionais e Loops

#### A. Condicionais (`if`, `elif`, `else`)

Executa um bloco de código se uma condição for verdadeira. **A indentação define o bloco de código.**

```python
status_code = 404

if status_code == 200:
    print("Sucesso! (OK)")
elif status_code == 404:
    print("Recurso não encontrado. (Not Found)")
else:
    print("Erro desconhecido.")
```

#### B. Loops (`for`)

Itera sobre os itens de uma coleção (como listas ou dicionários).

```python
# Loop em uma Lista
frameworks = ["FastAPI", "Flask", "Django"]
for framework in frameworks:
    print(f"Aprendendo: {framework}")
# Saída:
# Aprendendo: FastAPI
# Aprendendo: Flask
# Aprendendo: Django

# Loop em um Dicionário (para chaves e valores)
for chave, valor in usuario.items():
    print(f"{chave.upper()}: {valor}")
```

-----

## 🛠️ Tarefa da Fase 1

Para solidificar o aprendizado, vamos à tarefa prática:

Crie um script chamado `inventario_idp.py` que faça o seguinte:

1.  Crie um **Dicionário** chamado `componentes_idp` onde as chaves são nomes de componentes e os valores são **Listas** de tecnologias relacionadas.
      * Ex: `"API Service": ["FastAPI", "Pydantic"]`
2.  Crie uma **Função** chamada `adicionar_componente` que aceite o nome de um componente e uma lista de tecnologias e adicione ao dicionário.
3.  Crie uma **Função** chamada `exibir_inventario` que itere sobre o dicionário e imprima cada componente e suas tecnologias associadas.

<!-- end list -->

```python
# Exemplo de Estrutura:
# componentes_idp = {
#     "Base de Dados": ["PostgreSQL", "SQLAlchemy"],
# }

def adicionar_componente(nome, tecnologias):
    # Seu código aqui

def exibir_inventario():
    # Seu código aqui

# Chamadas:
# adicionar_componente("Frontend", ["React", "TypeScript", "Vite"])
# exibir_inventario()
```

## 🐍 Continuação da Fase 1: Funções, Tipagem e Ambiente

### 4\. Funções e Argumentos

Funções são blocos de código reutilizáveis. O Python permite que você defina argumentos de diferentes maneiras.

#### A. Definindo Funções

```python
# Função simples para calcular o total de componentes
def calcular_total(componentes: dict) -> int:
    """Calcula o número total de componentes em nosso IDP."""
    # Retorna a quantidade de chaves (componentes) no dicionário
    return len(componentes)

# Exemplo de uso
meu_idp = {"Frontend": ["React"], "Backend": ["FastAPI"]}
total = calcular_total(meu_idp)
print(f"Total de Componentes: {total}") # Saída: Total de Componentes: 2
```

#### B. Argumentos de Palavra-Chave (`kwargs`)

Você pode aceitar um número arbitrário de argumentos de palavra-chave (keyword arguments) usando `**kwargs`.

```python
# Função que simula a criação de um recurso na nossa IDP
def criar_recurso(**configuracao):
    print("Novo Recurso Criado:")
    for chave, valor in configuracao.items():
        print(f"- {chave}: {valor}")

criar_recurso(
    nome="Projeto Alpha", 
    owner="Time A", 
    ambiente="dev", 
    versao="1.0"
)
```

### 5\. Type Hinting (Análise de Tipos) - **O segredo do FastAPI\!**

O Python é dinamicamente tipado, mas o **Type Hinting** (anotação de tipos) permite que você indique qual tipo de dado é esperado ou retornado por uma função ou variável.

**O FastAPI usa essas dicas de tipo** para validar seus dados, serializar respostas, e **gerar automaticamente a documentação da API (Swagger UI)**.

| Conceito | O que faz | Exemplo |
| :--- | :--- | :--- |
| **Argumentos** | Indica o tipo que a função espera. | `nome: str` |
| **Retorno** | Indica o tipo que a função retorna. | `-> list` |
| **`Optional`** | Importado de `typing`, indica que um valor pode ser do tipo X *ou* `None`. | `depto: Optional[str] = None` |

**Exemplo:**

```python
from typing import List, Optional

# A função espera uma lista de strings e retorna uma string.
def formatar_tecnologias(techs: List[str]) -> str:
    # Retorna uma string unida por vírgulas
    return ", ".join(techs)

# A função espera um float e retorna um float.
# 'desconto' é Optional, ou seja, pode ser float ou None.
def calcular_preco(preco_base: float, desconto: Optional[float] = None) -> float:
    if desconto:
        return preco_base * (1 - desconto)
    return preco_base

# Uso
tecnologias_idp = ["FastAPI", "React", "Docker"]
print(formatar_tecnologias(tecnologias_idp)) 
# Saída: FastAPI, React, Docker

print(calcular_preco(100.0, 0.1)) # 10% de desconto -> 90.0
print(calcular_preco(100.0))       # Sem desconto -> 100.0
```

### 6\. Ambientes Virtuais (`venv`) - **Obrigatório para Projetos\!**

Um ambiente virtual é um diretório isolado que contém uma instalação Python e todas as bibliotecas (`packages`) que o seu projeto precisa.

**Por que usar?**

  * **Isolamento:** Impede conflitos de versões de bibliotecas entre diferentes projetos.
  * **Limpeza:** Mantém as dependências do seu projeto separadas do seu sistema operacional.

#### ⚙️ Comandos Essenciais

1.  **Criar o ambiente (dentro da pasta do seu projeto):**

    ```bash
    python3 -m venv .venv
    ```

    *(Isso cria uma pasta chamada `.venv`)*

2.  **Ativar o ambiente:**

      * **Linux/macOS:**
        ```bash
        source .venv/bin/activate
        ```
      * **Windows (PowerShell):**
        ```bash
        .venv\Scripts\Activate.ps1
        ```
      * **Windows (CMD):**
        ```bash
        .venv\Scripts\activate.bat
        ```

    *(Você saberá que está ativo porque verá `(.venv)` no início da linha de comando.)*

3.  **Instalar dependências (ex: FastAPI):**

    ```bash
    pip install fastapi uvicorn
    ```

4.  **Desativar o ambiente:**

    ```bash
    deactivate
    ```

-----

## 🎯 Tarefa da Fase 1 (Final)

1.  **Crie a Estrutura do Projeto:** Crie uma pasta chamada `idp_backend`.
2.  **Crie o Ambiente Virtual:** Entre na pasta `idp_backend` e crie e ative seu ambiente virtual (`.venv`).
3.  **Instale Dependências:** Instale a biblioteca `typing` (embora já venha com o Python moderno, é bom saber o comando) e qualquer outra que queira testar.
    ```bash
    pip install fastapi # Instale por enquanto, só para testar a instalação.
    ```
4.  **Teste o Type Hinting:** Crie um arquivo `type_test.py` com uma função que use `List` e `Optional` (como nos exemplos acima) e execute-o.

-----
