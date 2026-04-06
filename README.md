# AtividadeAED - Análise de Logs de Sistema com Python

## Descrição

Este projeto realiza uma análise exploratória de logs de sistema utilizando Python, Pandas e Matplotlib.

O objetivo é identificar:

- Frequência dos tipos de log
- Serviços mais afetados
- Quantidade de erros críticos
- Distribuição do tempo de resposta
- Eventos mais lentos do sistema

---

## Bibliotecas Utilizadas

```python
import pandas as pd
import matplotlib.pyplot as plt
```

---

## Base de Dados

O projeto utiliza um arquivo CSV chamado:

```python
logs_sistema.csv
```

As principais colunas analisadas são:

- `ID_Evento`
- `Timestamp_UTC`
- `Nivel_Log`
- `Servico_Afetado`
- `Codigo_Erro`
- `Tempo_Resposta_MS`

---

## Etapas da Análise

### 1. Leitura dos Dados

```python
df = pd.read_csv('logs_sistema.csv')
```

Também foram utilizadas funções como:

```python
df.head()
df.info()
```

---

### 2. Tratamento dos Dados

Preenchimento de valores ausentes:

```python
df['Codigo_Erro'] = df['Codigo_Erro'].fillna('N/A')
```

Conversão da coluna de data:

```python
df['Timestamp_UTC'] = pd.to_datetime(df['Timestamp_UTC'], utc=True)
```

---

### 3. Frequência dos Logs

```python
dataLogs = df['Nivel_Log'].value_counts()
```

Foi criado um gráfico de barras para mostrar os tipos de log mais frequentes.

---

### 4. Serviços Mais Afetados

```python
dataServicos = df['Servico_Afetado'].value_counts()
```

Essa análise permite identificar quais serviços apresentam mais ocorrências de logs.

---

### 5. Análise de Erros

Filtragem de logs `ERROR` e `CRITICAL`:

```python
dfLogsErros = df[df['Nivel_Log'].isin(['ERROR', 'CRITICAL'])]
```

Agrupamento por serviço:

```python
dfLogsErros.groupby('Servico_Afetado').size().sort_values(ascending=False)
```

---

### 6. Tempo de Resposta

```python
plt.hist(df['Tempo_Resposta_MS'])
```

O histograma mostra a distribuição dos tempos de resposta e ajuda a identificar possíveis lentidões.

---

### 7. Evento Mais Lento

```python
idx_max = df['Tempo_Resposta_MS'].idxmax()
evento_mais_lento = df.loc[idx_max]
```

Essa etapa identifica o evento com maior tempo de resposta.

---

## Conclusões

- Serviços de autenticação e pagamentos apresentaram mais erros
- Logs críticos possuem maiores tempos de resposta
- A maioria dos eventos é rápida, mas existem casos de lentidão
- Eventos críticos podem indicar gargalos no sistema

---

## Métodos Utilizados

### Pandas

- `read_csv()`
- `head()`
- `info()`
- `fillna()`
- `to_datetime()`
- `value_counts()`
- `groupby()`
- `sort_values()`
- `idxmax()`
- `loc()`

### Matplotlib

- `plot(kind='bar')`
- `hist()`
- `show()`

---

## Como Executar

1. Instale as dependências:

```bash
pip install pandas matplotlib
```

2. Coloque o arquivo `logs_sistema.csv` na mesma pasta do projeto.

3. Execute o notebook ou script Python.
