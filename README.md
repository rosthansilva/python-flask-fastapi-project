## 🚀 Fases do Aprendizado e Projeto

Dividiremos o seu aprendizado e o projeto IDP em fases claras.

| Fase | Foco Principal | Ferramentas |
| :--- | :--- | :--- |
| **1: Fundamentos Python & Backend** | Estruturas de Dados, Funções, Classes, Ambiente Virtual. | Python 3, `venv` |
| **2: Introdução ao FastAPI** | Configuração do projeto, Rotas, Modelos Pydantic, CRUD Básico. | FastAPI, Uvicorn, Pydantic |
| **3: Fundamentos React & Frontend** | JSX, Componentes, Props, State, Hooks básicos. | React, Vite |
| **4: Tipagem com TypeScript** | Tipos básicos, Interfaces, Tipagem de Componentes e Hooks. | TypeScript |
| **5: Integração (IDP Básico)** | Fazer o Frontend comunicar com o Backend (Fetch/Axios), Configurar o CORS. | FastAPI, React, TypeScript |
| **6: Melhores Práticas & Refatoração** | Segurança (Autenticação JWT), Testes, Padrões de API. | (Todos) |

---

## 📚 Fase 1: Fundamentos Python Essenciais

Antes de mergulhar no FastAPI, precisamos de uma base sólida em **Python**.

### Tópicos para Estudar (Python Básico)

1.  **Variáveis e Tipos de Dados:** Inteiros (`int`), Floats (`float`), Strings (`str`), Booleanos (`bool`).
2.  **Estruturas de Dados Fundamentais:**
    * **Listas:** Onde e como usar (mutabilidade, indexação).
    * **Tuplas:** Onde e como usar (imutabilidade).
    * **Dicionários:** Chaves e Valores (essencial para JSON e APIs).
    * **Sets:** Coleções de itens únicos.
3.  **Fluxo de Controle:**
    * **Condicionais:** `if`, `elif`, `else`.
    * **Loops:** `for` (com `range`, listas e dicionários), `while`.
4.  **Funções:**
    * Definindo funções (`def`).
    * Argumentos posicionais e de palavra-chave (`*args`, `**kwargs`).
    * **Type Hinting:** Comece a usar a anotação de tipos (ex: `def soma(a: int, b: int) -> int:`). **Isso é crucial para o FastAPI!**
5.  **Ambientes Virtuais (`venv`):** Como criar, ativar e desativar um ambiente virtual. (Isto isola as dependências do seu projeto).

> **Tarefa Prática:** Crie um script Python simples que gerencia um inventário (usando um **dicionário** para o inventário, **listas** para itens, e **funções** para adicionar/remover/exibir).# python-flask-fastapi-project
