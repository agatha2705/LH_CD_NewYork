# Airbnb Nova York Price Prediction & EDA
### Projeto para o programa Lighthouse - Processo de criação de um sistema de preditivo de aluguéis temporários na cidade de Nova York.

#### Objetivo:
- Desenvolver uma estratégia de precificação.

## Etapa 1: Importando bibliotecas e a nossa base de dados
Nessa etapa importamos as bibliotecas inicias e a nossa base de dados. Foi feita uma análise rápida para conhecer melhor as variáveis e as colunas com que vamos trabalhar, quais são os bairros, os tipos de quartos... Verificamos também a presença de valores vazios(NaN) substituindo e excluindo o que fosse necessário.

## Etapa 2: EDA (Exploratory Data Analysis)
Aqui entra uma análise mais aprofundada e mais visual dos dados. Nessa etapa focamos mais em entender como essas variáveis estão distribuídas, a média dos preços dos imóveis em Nova York, valores mínimos, máximos, e desvio padrão. Mas também usando o "groupby" para sabermos a média dos preços por bairro ou por tipo de quarto ou por bairro e tipo de quarto. Usando o scatterplot da biblioteca seaborn para sabermos a localização dos bairro e a distribuição dos tipos de quartos em Nova York.

## Etapa 3: Respondendo as perguntas propostas
1. Supondo que uma pessoa esteja pensando em investir em um apartamento para alugar na plataforma, onde seria mais indicada a compra?
     - Primeiro foi feito um gráfico da distribuição dos bairros. O resultado mostra que Manhattan e Brooklyn são os que mais aparecem. Então, depois verificamos o TOP 5 bairros em Manhatten e em Brooklyn, e o top 10 de bairros ao todo. Três predominaram: Em Manhattan, o bairro que predominou foi Harlem. Em Brooklyn, os bairros que predominaram foram Williamsburg e Bedford-Stuyvesant. No TOP 10 Williamsburg em primeiro, Bedford-Stuyvesant em segundo, e Harlem em terceiro.
     - Segundo comparamos o preço médio de aluguel nesses três bairros --> Bedford-Stuyvesant é o TOP 2 de bairros e o preço médio na região é melhor que no Williamsburg e em Harlem.
     - Terceiro, o que justificaria Manhattan mesmo com o preço muito mais elevado possuir mais impressões? Seria por exemplo, um único host possuir muitos imóveis. Gerando um gráfico do TOP 5 hosts que mais aparecem e filtrando para saber onde esse host possui mais imóveis vemos que o total de 327 imóveis é só de Manhattan. Assim como o segundo host, que de 232, 230 são só de Manhattan.

- Então com base nos resultados, Brooklyn - Bedford_Stuyvesant seria o mais indicado considerando o preço e a preferência das pessoas ao escolherem esse lugar.

2. O número mínimo de noites e a disponibilidade ao longo do ano interferem no preço?
     - Fazendo a correlação das colunas com a nossa coluna target("price"), embora a correlação das colunas "minimo_noites" e "disponibilidade_365" sejam altas em comparação ao restante, essa correlação ainda é baixa, portanto, não interfere muito no preço dos imóveis em Nova York.
       
3. Existe algum padrão no texto do nome do local para lugares de mais alto valor?
     - Primeiro conferimos se não havia correlação com o nome dos bairros, vimos que não há correlação. Então vimos o nome dos locais.
     - Retirando palavras comuns como "the", "in", "at", "is", "to", "with". Retirando pontuações como ".", ",", "/". E por fim retirando números. A conclusão é que existe sim um padrão no texto do nome do local para lugares de mais alto valor. Palavras como "luxury", "townhouse" que seria um estilo que une uma ou mais casas de forma proporcional e simetrica, "penthouse" que seria a famosa cobertura, e localizações como "nyc", "manhattan", "brooklyn", o que faz sentido com a análise na primeira pergunta.
      
4. Supondo um apartamento com as seguintes características, qual seria a sugestão de preço? (Antes de responder essa pergunta precisamos do nosso modelo de machine learning).

## Etapa 4: Tratando Outliers
Tratamos os outliers de acordo com o perfil da pessoa com base na pergunta 4, e nas características fornecidas. Optamos por retirar os outliers porque primeiro, o perfil da pessoa de acordo com as caracteísticas fornecidas é mais comum, e segundo que, se formos ver na etapa do EDA, a diferença do preço mínimo e máximo dos imóveis é discrepante variando de 0 a 10.000, o que pode atrapalhar o nosso modelo de previsão.

## Etapa 5: Enconding dos dados
- Nessa etapa retiramos as colunas desnecessárias para o nosso modelo de machine learning, como ID, nome, host name e ultima review. 
- Tratamos os valores de texto transformando-os em valores numéricos usando o Label Encondig na coluna "bairro", e de forma manual atribuindo valores para as colunas "bairro_group" e "room_type" de acordo com a média dos preços. Atribuindo 1 para o grupo de bairro e o tipo de quarto mais caro, e assim por diante.

## Etapa 6: Modelo de Previsão - Padronizando os dados e escolhendo o nosso modelo
- Padronizamos os dados com o StandardScaler e testamos os modelos Random Forest Regressor, Linear Regression, Extra Trees Regressor.
