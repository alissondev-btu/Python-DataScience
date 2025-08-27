# Manipulação de Dados em Banco Não Relacional (TinyDB)

Este projeto demonstra como utilizar **TinyDB** (um banco de dados não
relacional em Python) para armazenar e manipular informações de
monitoramento de temperatura, combinando o uso da biblioteca **Pandas**
para análise de dados.

------------------------------------------------------------------------

## 🚀 Tecnologias Utilizadas

-   [Python 3](https://www.python.org/)
-   [TinyDB](https://tinydb.readthedocs.io/en/latest/)
-   [Pandas](https://pandas.pydata.org/)

------------------------------------------------------------------------

## 📦 Instalação

Clone este repositório e instale as dependências necessárias:

``` bash
pip install tinydb pandas
```

------------------------------------------------------------------------

## 📂 Estrutura do Projeto

-   `manipulacao_nao_relacionais.ipynb` → Notebook principal com o
    código de exemplo.
-   `monitoramento.json` → Arquivo gerado pelo TinyDB para armazenar os
    dados.

------------------------------------------------------------------------

## 📖 Passo a Passo do Código

### 1️⃣ Instalação da biblioteca

``` python
!pip install tinydb
```

Instala o TinyDB, banco de dados não relacional utilizado no projeto.

------------------------------------------------------------------------

### 2️⃣ Importação das bibliotecas

``` python
import pandas as pd
from tinydb import TinyDB, Query
```

-   **pandas** → para manipulação e análise de dados.\
-   **tinydb** → para criação do banco de dados não relacional.

------------------------------------------------------------------------

### 3️⃣ Criação do banco de dados e tabelas

``` python
engine = TinyDB('monitoramento.json')

temperatura = engine.table('temperatura')
resultados = engine.table('resultados')
```

-   Cria um arquivo `monitoramento.json` que servirá como banco de
    dados.\
-   Define as tabelas **temperatura** e **resultados**.

------------------------------------------------------------------------

### 4️⃣ Conjunto de dados simulados

``` python
dados = {
    'codigo': ['M01', 'M02', 'M03', 'M04', 'M05', 'M06', 'M07', 'M08', 'M09', 'M10'],
    'temperatura': [72.5, 68.0, 76.3, 74.0, 78.5, 69.9, 80.1, 73.0, 70.2, 77.5]
}

dados_temperatura = pd.DataFrame(dados)
```

Cria um **DataFrame** com códigos de máquinas e suas temperaturas.

------------------------------------------------------------------------

### 5️⃣ Processamento dos dados

``` python
limite = 75.0

dados_temperatura['status'] = 'Segura'
dados_temperatura.loc[dados_temperatura['temperatura'] > limite, 'status'] = 'Alerta'
```

-   Define um **limite de segurança (75.0)**.\
-   Classifica cada máquina em **"Segura"** ou **"Alerta"** dependendo
    da temperatura.

------------------------------------------------------------------------

### 6️⃣ Armazenando no banco de dados

``` python
temperatura.insert_multiple(dados_temperatura.to_dict(orient="records"))
```

Salva os registros processados na tabela **temperatura** do TinyDB.

------------------------------------------------------------------------

## 📊 Exemplo de Saída

Tabela resultante com os status:

  codigo   temperatura   status
  -------- ------------- --------
  M01      72.5          Segura
  M02      68.0          Segura
  M03      76.3          Alerta
  M04      74.0          Segura
  M05      78.5          Alerta
  M06      69.9          Segura
  M07      80.1          Alerta
  M08      73.0          Segura
  M09      70.2          Segura
  M10      77.5          Alerta

------------------------------------------------------------------------

## 📜 Licença

Este projeto é de uso educacional e livre para estudo.
