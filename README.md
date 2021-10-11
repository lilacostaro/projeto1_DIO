# Projeto de ETL - BootCamp DIO
Projeto de ETL desenvolvido para o BootCamp "Cognizant Cloud Data Engineer" da Digital Innovation One em parceria com a Cognizant.

## Materiais e Tecnologias 
A base de dados escolhida para esse projeto foi o dataset de [listings](http://data.insideairbnb.com/brazil/rj/rio-de-janeiro/2021-09-28/data/listings.csv.gz) do Airbnb na Cidade do Rio de Janeiro, obtido no site [insideAirbnb](http://insideairbnb.com/get-the-data.html).

O notebook utilizado para esse projeto foi o [Google Colab](http://data.insideairbnb.com/brazil/rj/rio-de-janeiro/2021-09-28/data/listings.csv.gz).

A linguagem de programação deste projeto é a [Python](https://www.python.org/), importando as seguintes bibliotecas:
- [Pandas](https://pandas.pydata.org/).
- [Pandera](https://pandera.readthedocs.io/).
- [MatPlotLib](https://matplotlib.org/).


## O projeto é dividido em 3 Etapas

- 1ª Etapa - Extração dos Dados
- 2ª Etapa - Transformação dos Dados
- 3ª Etapa - Carregamento dos Dados

### Extração dos Dados

- Os dados foram extraídos utilizando a função '*read_csv*' da biblioteca pandas, e atribuídos a um DataFrame.
- Foi adicionado o parâmetro *parse_dates* no comando de extração dos dados para alterar o tipo de dados das colunas contendo datas que estavam formatadas como *strings*.
- Após uma análise, as colunas que seriam utilizadas foram renomeadas.
- A coluna *price* se encontrava no formato de *string* pois o formato erra $NNN.NN, para alterar o tipo da coluna foi necessária a criação de uma outra coluna que recebeu o nome de 'preço' e o seguinte fatiamento **df['price'].str[1:-3]**, retirando assim o símbolo $, o . e os caracteres dos decimais.
- Ao tentar alterar o tipo da coluna 'preço' de string para inteiro, outro erro surgiu, pois os valores acima de 999 continham virgula para separa as casas de milhar das casas de centena. Então foi aplicado o um tratamento para retirada da virgula.
- Após o tratamento foi possível modificar o tipo de dado da coluna, as colunas 'anfitriao_id' e 'id_anuncio' que estavam com tipo *inteiro* também foram modificadas e passaram a ser *strings* para evitar operações matemáticas ou conflito entre valores, uma vez que esses valores são normalmente utilizados como chaves primarias de identificação. 
- O próximo passo foi validar os dados, para isso a biblioteca pandera foi utilizada. 

### Transformação dos Dados

- Foram criados dois DataFrames principais a partir do DataFrame original,  o primeiro foi o **dflistings**, contendo informações sobre os anúncios, e o **dfhosts** que contém os dados de anfitriões.
- Foram feitos alguns filtros e groupbys com as informações contidas nos DataFrames, com a intenção de explorar os dados. Obs.: Os gráficos plotados nessa etapa não foram tratados por que a ideia era ter uma visão do que posse ser analisado a partir dos dados, não montar um relatório de fato, os dados serão exportados para que possam ser utilizados em uma ferramenta de visualização de dados.
- Com o intuito de criar datasets com uma quantidade menor de dados, foram criados os DataFrames **df_5bairros**, que contem dados dos 5 bairros com maior número de anúncios, e o **df_5bairros_2016**, que apresenta os dados de anúncios nos 5 bairros com mais anúncios e que os anfitriões se cadastraram na plataforma no ano de 2016.
- Outros DataFrames foram criados, mas apenas com o intuito de facilitar a visualização de dados, por isso não foram considerados como datasets.

### Carregamento dos Dados

- Os DataFrames criados foram exportados para  os formatos "CVS" e "json". E podem ser utilizados em ferramentas de visualização de dados, para produção de análises e relatorios. 
