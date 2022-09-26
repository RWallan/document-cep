# Cálculo de distância entre duas geolocalizações

O projeto foi feito para calcular a distância entre duas geolocalizações.

As etapas são construídas desde a limpeza e formatação de CEPs, utilização da API Google para buscar as geolocalizações dos CEPs e o cálculo da distância entre as geolocalizações obtidas.

## Estrutura do projeto

    mkdocs.yml          # Configuração do mkdocs.
    requirements.txt    # Bibliotecas python necessárias.
    Makefile            # Arquivo make com comandos úteis.
    .gitignore          # Configuração git.
    README.md           # Descrição do projeto.

    docs/
        index.md                    # Documentação da estrutura do projeto.
        01_cep_cleaning.md          # Documentação do script de limpeza de CEP.
        02_geo_search.md            # Documentação do script de busca das geolocalizações.
        03_distance_calculate.md    # Documentação do script para cálculo das distâncias.
        funs_cep.md                 # Documentação do script com funções úteis.

    config/
        faixacep.txt    # Contém as faixas de CEPs e sua respectiva localidade. Construído a partir dos sites do correios.
        key_google.txt  # Chave de acesso para a API do google. Solicitar ao autor.

    data_cep/ # Diretório com os **data frames** necessários para a execução do projeto. Solicitar ao autor.
    
    sample/
        01_cep_cleaning.py          # Limpeza de CEP.
        02_geo_search.py            # Busca de geolocalizações.
        03_distance_calculate.py    # Cálculo de distâncias.
        funs_cep.py                 # Funções úteis.

## Para o projeto

Para poder atender aos requisitos necessários do projeto, escolha um dos tópicos a seguir que encaixe com as suas ferramentas:

Execute o arquivo *Makefile* com o *GNU Make*. Nele será criado um ambiente virtual e instalará todos os pacotes necessários do projeto. **É necessário ter o virtualenv instalado.**

Para executar via *GNU Make*:

    make install

Caso não tenha o GNU Make. É aconselhável criar um ambiente virtual a partir da sua ferramente de escolha e execute o *requirements.txt* através do PIP.

Algumas ferramentas para a criação de ambientes virtuais:

    virtualenv
    venv
    poetry
    anaconda

Para executar via PIP:

    pip install -r requirements.txt

## Links úteis

Site de consulta de faixas de CEPs: <https://buscacepinter.correios.com.br/app/faixa_cep_uf_localidade/index.php>

GNU Make: <https://www.gnu.org/software/make/>

Anaconda: <https://www.anaconda.com>
