# Script - Busca de geolocalização

O script tem como objetivo buscar a geolocalização dos dados de Estado - CEP.

A seguir está descrito as seções presentes no script.

## Importando dados limpos

Import os dados limpos obtidos do script de [limpeza de CEPs](./01_cep_cleaning.md).

## Criando array apenas com CEPs distintos

Cria uma lista de CEPs únicos tanto de alunos quanto das unidades.

## Buscando geolocalização

Primeiramente faz uma verificação para encontrar a base *geocode.csv* existente de geolocalizações para CEPs conhecidos.

```python
if os.path.isfile(PATH):
    df_verify = pd.read_csv(PATH)
else:
    df_verify = pd.DataFrame(columns=column_name)
```

 Faz um filtro para executar a API para os CEPs que não constam na base de dados. Caso não haja esse arquivo, é criado uma lista vazia e é feito a busca para todos os CEPs.

```python
cep_distinct = [cep for cep in cep_distinct if cep not in df_verify["cep"].values]
```

Feito a lista de CEPs definitiva, uma lógica de lotes é executada. A API é executada em uma sequência de 100 CEPs. E após finalizado a sequência é salvo no arquivo *geocode.csv* as informações coletadas. Esse passo é executado até percorrer a lista de todos os CEPs.

```python
BUFFER_SIZE = 100
for i in range(0, n_distinct, BUFFER_SIZE):
    start_at = i
    end_at = min(start_at + BUFFER_SIZE, n_distinct)
    temp = []
    print(f"Buscando CEPs {start_at} - {end_at}")
    for cep in cep_distinct[start_at:end_at]:
        geocode = geo.locate_geocode(cep)
        temp.append([cep, geocode])
    df_geocode = pd.DataFrame(temp, columns=column_name)

    if not os.path.isfile(PATH):
        df_geocode.to_csv(PATH, index=False)
    else:
        df_geocode.to_csv(PATH, mode="a", header=False, index=False)
```

### Para mais informações

Para mais informações, consulte o texto [Funções úteis](./funs_cep.md).
