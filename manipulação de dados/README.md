# Manipulação de Dados com Pandas e SQLite

Este projeto demonstra como manipular dados utilizando **Python**, **Pandas** e **SQLite**, integrando análise de dados e armazenamento em banco relacional.

## 📌 Objetivo

Criar um fluxo de trabalho simples para:

1. Criar e armazenar dados em um banco de dados SQLite.
2. Processar e validar informações de qualidade de produtos.
3. Consultar e analisar resultados usando SQL e Pandas.

## 🚀 Tecnologias Utilizadas

* **Python 3**
* **Pandas** – para manipulação de dados
* **SQLite** – banco de dados relacional local
* **SQLAlchemy** – integração entre Pandas e SQLite

## 📂 Estrutura do Notebook

### 1. Instalação das bibliotecas

```python
!pip install sqlite3
!pip install sqlalchemy
```

### 2. Importação das bibliotecas

```python
import pandas as pd
from sqlalchemy import create_engine
```

### 3. Criação do banco de dados

```python
engine = create_engine('sqlite:///qualidade-automotiva.db')
```

### 4. Criação do conjunto de dados

Um dicionário é convertido em **DataFrame**:

```python
dados = {
    'codigo': ['P01','P02','P03','P04','P05','P06','P07','P08','P09','P10'],
    'altura': [10.0, 9.8, 10.2, 10.1, 9.7, 10.0, 10.3, 9.9, 10.0, 10.1],
    'largura': [5.0, 5.1, 5.0, 4.9, 5.2, 5.0, 4.8, 5.0, 5.0, 5.3]
}

dados_produtos = pd.DataFrame(dados)

dados_produtos.to_sql('produtos', con=engine, index=False, if_exists='replace')
```

### 5. Processamento dos dados

Validação de qualidade dos produtos:

```python
dados_produtos['aprovados'] = (
    (dados_produtos['altura'].between(9.9, 10.1)) &
    (dados_produtos['largura'].between(4.9, 5.1))
)

dados_produtos.to_sql('produtos', con=engine, index=False, if_exists='replace')
```

### 6. Consultas no banco de dados

Comandos SQL podem ser usados para verificar os produtos aprovados ou reprovados:

```python
pd.read_sql('SELECT * FROM produtos WHERE aprovados = 1', con=engine)
```

## ✅ Resultados

O notebook gera:

* Um banco de dados `qualidade-automotiva.db`.
* Uma tabela `produtos` contendo colunas de **código, altura, largura e aprovação**.
* Relatórios de quais produtos foram aprovados/reprovados de acordo com os critérios.

## 📖 Como executar

1. Abra o notebook `manipulacao_de_dados.ipynb` no **Jupyter Notebook** ou **JupyterLab**.
2. Execute as células em ordem.
3. Verifique os resultados impressos e as tabelas salvas no SQLite.

---

✍️ Desenvolvido como exemplo de integração entre **Pandas** e **SQLite** para manipulação e análise de dados.
