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

-----

**Próximo Passo:**

Assim que terminar ou se sentir confortável com essa base (Listas, Dicionários, Condicionais e Loops), podemos avançar para o próximo bloco da **Fase 1**: **Funções, Type Hinting e Ambientes Virtuais**.

Me avise quando estiver pronto para a próxima etapa\!