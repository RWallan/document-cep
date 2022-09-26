# Script - Calcular distância das geolocalizações

O script tem como objetivo executar o cálculo de distância entre duas geolocalizações.

A seguir será descrito as seções presentes no script:

## Importando dados

Importa os dados contendo as informações das geolocalizações e os dados contendo os CEPs dos alunos e unidades.

## Dando merge com os CEPs conhecidos

A partir dos dados contendo as geolocalizações e os CEPs únicos, é dado um merge com os CEPs de alunos.

```python
df_aluno_geocode = df_notnull[["DR_CD_MATRICULA", "cepaluno_f"]].merge(
    df_unique_geocode, left_on="cepaluno_f", right_on="cep"
)
```

O mesmo é feito para os CEP de unidade:

```python
df_unidade_geocode = df_notnull[["DR_CD_MATRICULA", "cepunidade_f"]].merge(
    df_unique_geocode, left_on="cepunidade_f", right_on="cep"
)
```

Contendo um banco de dados com as geolocalizações dos alunos e outro com as das unidades, é feito um *merge* com os dois bancos.

```python
df_merged = df_aluno_geocode.merge(
    df_unidade_geocode,
    left_on="DR_CD_MATRICULA",
    right_on="DR_CD_MATRICULA",
    how="inner",
)
df_merged = df_merged.merge(
    df_notnull[["DR", "DR_CD_MATRICULA"]],
    left_on="DR_CD_MATRICULA",
    right_on="DR_CD_MATRICULA",
)
```

## Cálculo de distância

Seção destinada para calcular a distância entre as geolocalizações

### Filtrando para geolocalizações existentes

Remove as linhas que não contém informação da geolocalização do aluno ou da unidade.

### Distância

É feito o cálculo da distância para a métrica de Haversine e para o GeoDesic. Feito os cálculos, um novo *data frame* é salvo com as informações:

* df_distance_full.csv - Possui todas as colunas existentes;
* df_distance.csv - Possui as colunas de DR_CD_MATRICULA, distance_hav e distance_dg.

### Para mais informações

Para mais informações, consulte o texto [Funções úteis](./funs_cep.md).
