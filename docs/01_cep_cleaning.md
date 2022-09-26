# Script - Limpeza e formatação de CEPs

O script tem como objetivo limpar e formatar os CEPs para um padrão. O padrão adotado é para que o script de [busca de geolocalizações](./02_geo_seach.md) possa ser o mais preciso possível.

A seguir será descrito as seções presentes no script:

## Importando dados

Importa os dados com as informações de CEP a serem formatados.

## Aplicando tratamento nos dados de CEP

Aplica a classe: `FaixaCep`, e as funções: `limpar_cep()`, `formatar_cep()`. Para mais informações, [clique aqui](./funs_cep.md).

### Dicionário de faixas de CEP

Transforma o arquivo *faixacep.txt* em um dicionário para ser consultado.

```python
dict_cep = eval(open("../config/faixacep.txt", "r").read())
faixacep = FaixaCep(dict_cep)
```

### Tratamento

Limpa as strings de CEP, removendo qualquer caracter que não seja número e sinaliza como `None` os CEPs inválidos.

```python
df["cepaluno"] = df["cepaluno"].astype("str")
df["cepaluno_limpo"] = df["cepaluno"].apply(limpar_cep)
df["cepunidade_limpo"] = df["cepunidade"].apply(limpar_cep)
```

O arquivo é filtrado para somente aqueles que contém CEP.

```python
df_notnull = df.dropna(inplace=False)
df_notnull[["cepaluno_limpo", "cepunidade_limpo"]] = df_notnull[
    ["cepaluno_limpo", "cepunidade_limpo"]
].astype("int")
```

O processo é repetido para os alunos e para a unidade de estudo.

### Formatação

Constrói a formatação a ser utilizada para a busca de geolocalização tanto para os alunos quanto para as unidades de estudo.

## Exportando CEPs limpos

Exportando dados limpos para data_cep/

### Para mais informações

Para mais informações, consulte o texto [Funções úteis](./funs_cep.md).
