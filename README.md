# Analyzing_Spreadsheet
# Documentação do Código Python

Este é um exemplo de código Python que faz o download de um arquivo Excel contendo dados de aeroportos, lê esses dados usando a biblioteca Pandas e executa algumas operações básicas. Vamos detalhar cada parte do código e explicar como funciona.

## Instalação de Dependências

```python
!pip install openpyxl
```

Esta linha de código instala a biblioteca `openpyxl` se ainda não estiver instalada. Ela é usada posteriormente para trabalhar com arquivos Excel.

## Download do Arquivo Excel

```python
import requests
import os

if not os.path.isfile("./Airport_Data.xlsx"):
    r = requests.get("https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/analysing-spreadsheet-data-with-python/Airport_Data.xlsx")
    f = open("./Airport_Data.xlsx", mode="wb+")
    f.write(r.content)
    f.close()
```

Este trecho de código faz o seguinte:
- Importa as bibliotecas `requests` e `os`.
- Verifica se o arquivo `"./Airport_Data.xlsx"` já existe no sistema de arquivos.
- Se o arquivo não existe, faz o download do arquivo Excel a partir de uma URL especificada.
- Salva o arquivo Excel no sistema de arquivos local com o nome `"Airport_Data.xlsx"`.

## Leitura do Arquivo Excel usando Pandas

```python
import pandas as pd

df_facilities = pd.read_excel("./Airport_Data.xlsx", sheet_name="Facilities")
```

Aqui, estamos usando a biblioteca Pandas para ler o arquivo Excel recém-baixado. O DataFrame resultante é armazenado na variável `df_facilities`. O parâmetro `sheet_name` especifica a aba do Excel que será lida.

## Análise dos Dados

Aqui, realizamos algumas operações simples para analisar os dados no DataFrame `df_facilities`.

```python
# Exibe o DataFrame df_facilities
df_facilities

# Seleciona a coluna "Type" do DataFrame
df_facilities["Type"]

# Obtém valores únicos da coluna "Type"
df_facilities["Type"].unique()

# Filtra o DataFrame para obter apenas linhas onde a coluna "Type" é igual a "SEAPLANE BASE"
df_facilities[df_facilities["Type"] == "SEAPLANE BASE"]

# Ordena o DataFrame pelo valor da coluna "ARPElevation" em ordem decrescente
df_facilities.sort_values(by="ARPElevation", ascending=False)

# Obtém as 5 primeiras linhas do DataFrame ordenado
df_facilities.sort_values(by="ARPElevation", ascending=False).head(5)

# Calcula a média da coluna "ARPElevation"
df_facilities["ARPElevation"].mean()

# Encontra o valor máximo da coluna "ARPElevation"
df_facilities["ARPElevation"].max()

# Encontra o valor mínimo da coluna "ARPElevation"
df_facilities["ARPElevation"].min()

# Filtra o DataFrame para obter apenas linhas onde a coluna "Type" é igual a "SEAPLANE BASE"
df_seaplane = df_facilities[df_facilities["Type"] == "SEAPLANE BASE"]

# Salva o DataFrame filtrado em um novo arquivo Excel
df_seaplane.to_excel("./seaplane.xlsx")
```

Essas operações demonstram como você pode manipular e analisar os dados em um DataFrame Pandas. As saídas e resultados são exibidos diretamente no ambiente de programação Python.

Este é um exemplo básico de análise de dados usando Python, Pandas e a manipulação de arquivos Excel. Você pode adaptar e expandir esse código para atender às suas necessidades específicas de análise de dados.
