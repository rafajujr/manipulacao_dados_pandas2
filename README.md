# Manipulação de Dados com Pandas

Projeto desenvolvido para praticar **manipulação, transformação e limpeza de dados utilizando Python e Pandas**.

O projeto utiliza uma base de dados de hospedagens e demonstra, de forma prática, algumas das principais técnicas utilizadas no tratamento de dados tabulares.

## 📌 Sobre o projeto

O notebook principal do projeto é o [`manipula_dados.ipynb`](./manipula_dados.ipynb).

Nele, os dados são carregados a partir de um arquivo JSON e posteriormente passam por diferentes etapas de exploração e transformação.

A base utilizada contém informações sobre hospedagens, incluindo avaliação, quantidade de hóspedes, quartos, camas, comodidades, taxas e preço.

O dataset possui **3.818 registros e 13 colunas** após o processo de transformação inicial.

## 🎯 Objetivos

Este projeto tem como principais objetivos:

* Praticar a utilização da biblioteca Pandas;
* Carregar dados armazenados em arquivos JSON;
* Explorar a estrutura de um DataFrame;
* Verificar e alterar tipos de dados;
* Converter dados textuais em dados numéricos;
* Limpar informações monetárias;
* Trabalhar com valores ausentes;
* Manipular informações armazenadas em strings;
* Realizar limpeza e tratamento de textos;
* Aplicar técnicas de tokenização;
* Organizar os dados para utilização em análises posteriores.

## 🛠️ Tecnologias utilizadas

* **Python**
* **Pandas**
* **NumPy**
* **Jupyter Notebook**

## 📂 Estrutura do projeto

```text
manipulacao_dados_pandas2/
│
├── files/
│   └── dados_hospedagem.json
│
├── manipula_dados.ipynb
│
└── README.md
```

## 📊 Dados utilizados

O arquivo `dados_hospedagem.json` contém informações relacionadas a imóveis e hospedagens.

Entre as principais variáveis trabalhadas estão:

| Coluna                 | Descrição                             |
| ---------------------- | ------------------------------------- |
| `avaliacao_geral`      | Avaliação geral da hospedagem         |
| `experiencia_local`    | Informações sobre a experiência local |
| `max_hospedes`         | Quantidade máxima de hóspedes         |
| `descricao_local`      | Descrição do imóvel/local             |
| `descricao_vizinhanca` | Descrição da vizinhança               |
| `quantidade_banheiros` | Quantidade de banheiros               |
| `quantidade_quartos`   | Quantidade de quartos                 |
| `quantidade_camas`     | Quantidade de camas                   |
| `modelo_cama`          | Modelo/tipo de cama                   |
| `comodidades`          | Comodidades disponíveis               |
| `taxa_deposito`        | Valor da taxa de depósito             |
| `taxa_limpeza`         | Valor da taxa de limpeza              |
| `preco`                | Preço da hospedagem                   |

## 🔎 Etapas realizadas

### 1. Importação dos dados

Inicialmente, a biblioteca Pandas é utilizada para carregar o arquivo JSON:

```python
import pandas as pd

df = pd.read_json('files/dados_hospedagem.json')
```

### 2. Exploração inicial

O DataFrame é explorado utilizando métodos como:

```python
df.head()
```

Também é realizada a verificação dos tipos de dados com:

```python
df.dtypes
```

### 3. Conversão de dados numéricos

Algumas colunas originalmente armazenadas como texto são convertidas para tipos numéricos.

Entre elas:

* `max_hospedes`
* `quantidade_banheiros`
* `quantidade_quartos`
* `quantidade_camas`
* `avaliacao_geral`
* `preco`
* `taxa_deposito`
* `taxa_limpeza`

Exemplo:

```python
df["max_hospedes"] = df["max_hospedes"].astype(int)
```

Para algumas colunas, a conversão é realizada em conjunto:

```python
columns_numerics = [
    "quantidade_banheiros",
    "quantidade_quartos",
    "quantidade_camas"
]

df[columns_numerics] = df[columns_numerics].astype(float)
```

### 4. Tratamento de valores monetários

Os valores financeiros inicialmente estão armazenados como strings, contendo símbolos como `$` e separadores de milhares.

O projeto realiza a limpeza dessas informações antes da conversão para `float`.

Exemplo:

```python
df["preco"] = df["preco"].apply(
    lambda x: x.replace("$", "").replace(",", "").strip()
)

df["preco"] = df["preco"].astype(float)
```

O mesmo processo é aplicado às colunas de depósito e taxa de limpeza.

### 5. Limpeza de textos

A coluna `descricao_local` passa por uma etapa de limpeza utilizando expressões regulares:

```python
df["descricao_local"] = df["descricao_local"].str.replace(
    "[^a-zA-Z0-9]",
    " ",
    regex=True
)
```

Essa etapa remove caracteres que não correspondem a letras ou números.

### 6. Tokenização

Após a limpeza, a descrição do local é dividida em palavras:

```python
df["descricao_local"] = df["descricao_local"].str.split()
```

Também é realizada a separação das comodidades:

```python
df["comodidades"] = df["comodidades"].str.split(",")
```

Essas transformações tornam determinadas informações mais estruturadas e facilitam tratamentos posteriores.

## 🚀 Como executar o projeto

### Pré-requisitos

É necessário ter o Python instalado na máquina.

Recomenda-se utilizar um ambiente virtual.

### 1. Clone o repositório

```bash
git clone https://github.com/rafajujr/manipulacao_dados_pandas2.git
```

### 2. Acesse a pasta do projeto

```bash
cd manipulacao_dados_pandas2
```

### 3. Instale as dependências

```bash
pip install pandas numpy jupyter
```

### 4. Inicie o Jupyter Notebook

```bash
jupyter notebook
```

Em seguida, abra o arquivo:

```text
manipula_dados.ipynb
```

## 📚 Principais conceitos praticados

Durante o desenvolvimento do projeto são praticados conceitos importantes de tratamento de dados:

* DataFrames;
* Leitura de arquivos JSON;
* Inspeção de dados;
* Tipagem de colunas;
* Conversão com `astype()`;
* Manipulação de strings;
* Expressões regulares;
* Tokenização;
* Tratamento de valores ausentes;
* Limpeza de dados financeiros;
* Manipulação de múltiplas colunas;
* Organização de dados para análise.

## 💡 Aprendizados

O projeto demonstra uma etapa fundamental de qualquer processo de análise de dados: **transformar dados brutos em dados estruturados e adequados para análise**.

A utilização do Pandas permite realizar essas transformações de maneira eficiente, enquanto o NumPy complementa o trabalho com operações e estruturas numéricas.

## 📌 Próximos passos

Como evolução do projeto, algumas melhorias possíveis seriam:

* Adicionar análises exploratórias dos dados;
* Criar gráficos para visualizar os resultados;
* Identificar e tratar de forma mais detalhada os valores ausentes;
* Criar novas variáveis derivadas;
* Realizar análises estatísticas;
* Documentar as principais descobertas obtidas a partir dos dados;
* Adicionar um arquivo `requirements.txt` para facilitar a instalação das dependências.

## 👨‍💻 Autor

**Rafael Júnior**

GitHub: [`@rafajujr`](https://github.com/rafajujr)

## 🔗 Repositório

Este projeto está disponível no GitHub:

https://github.com/rafajujr/manipulacao_dados_pandas2
