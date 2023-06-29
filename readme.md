# Data-Science
Area de analise de dados, é utilizada por muitos bancos e hospitais para tratar os dados de forma que tenham valores. 
As anotações a seguir são baseadas no curso de Data Science da Alura.

## Colab google
Para melhor desempenho de processamento e compartilhamento dos dados, voce pode utilizar o colab:
Uma aplicação da google para auxiliar nas anotações e no desenvolvimento de código

```html
https://colab.research.google.com/
```
## Pandas
É uma ferramenta construída em Python para análise e manipulação de dados.

Para importar o pandas para o código é necessario o codigo:

```py
import pd
```
A documentação está em:

```html
https://pandas.pydata.org/
```
Para importar o panda e ler o arquivo que deseja analisar, exibindo o cabeçalho da planilha.
```py
import pandas as pd

notas = pd.read_csv("ratings.csv")
notas.head(5)
```


Exibir o total de entradas em notas.
```py
notas.shape(4)
```


Para alterar o nome das colunas. 
```py
notas.columns = ["usuarioId", "filmeId", "notas", "momento"]
notas.head()
```

Para verificar a quantidade de notas inseridas. 
```py
notas['notas']
```

Quais notas foram dadas em uma lista.
```py
notas['notas'].unique()
```

Quantidade de notas dadas por indice.
```py
notas['notas'].value_counts()
```

Media do total de notas
```py
notas['notas'].mean()
```

## Plotando com o Pandas

Plotagem é uma forma de visualização dos dados. 

Para plotar a coluna notas, lembrando que ele fará riscos de cara usuario, então o gráfico não terá muito sentido.

```py
notas.notas.plot()
```
conforme a imagem:

![](imagens/plotagem.png)

Para que seja mais compreensivel a leitura deste grafico, use o parametro kind, com o hist, de 'histograma' para fixação do termo, a quantidade de numeros existentes em notas conta uma historia, assim o paramatro escolhido da os marcos de cada numero nesta historia, conforme a imagem.

![](imagens/histograma.png)

## Apresentando Medias
Lembrando que a média de um valor é a soma de todos com uma divisão entre eles, não se sabe a quantidade de valores maiores ou menores.

Para exibir uma Media use o mean:

```py
notas.query("filmeId==1").notas.mean()
```
No exemplo acima é listado a media do filme com Id 1.

Para criar um gráfico com as medias dos filmes, crie uma varial com as medias e depois coloque em um gráfico.

Usando o comando para criar a variavel:

```py
medias_por_filme = notas.groupby("filmeId").mean()["notas"]
```
E depois atribuindo a um gráfico.

```py
medias_por_filme.plot(kind='hist')
```
## Seaborn - Gráficos de barras

Esta tambem é uma biblioteca de dados estatiscos que dá para ser utilizada em Python, o Seaborn tem gráficos mais simples em quesitos visuais, ou seja de facil entendimento.

Para importar a biblioteca use o comando:

```py
import seaborn as sns
```
Para usar um gráfico de barras utilize o **barplot**, como parametro do **sns**, abreviação do seaborn:

```py
sns.barplot(x="original_language", y= "total", data = contagem_de_lingua)
```

Quando se quer dar enfâse em um dados é necessario filtrar essa informação em forma de variavel, para este caso crie a variavel que lê a quantidade de filme por lingua de dublagem.

Neste caso foi criado a variavel de todas as linguas a de linguas em ingles e a do resto das linguas.

Todos os filmes separados por idioma 
```py
total_por_lingua = tmdb["original_language"].value_counts()
```
A soma de todos as filmes
```py
total_geral = total_por_lingua.sum()
```
Total de filmes em ingles
```py
total_de_ingles = total_por_lingua.loc["en"]
```
Total do resto dos filmes que não são em ingles
```py
total_do_resto= total_geral - total_de_ingles
```
Agora crie uma base de dados para que seja exibida do forma que desejar no gráfico chamando as variaveis que foram criadas.

```py
dados= {
	'lingua' : ['ingles','outros'],
	'total' : [total_de ingles, total_do_resto]
}
dados = pd.DataFrame(dados)
```

Crie o gráfico barplot, com expecificações da base de dados e qual informação ficará no eixo x e no eixo y.

```py 
sns.barplot(data = dados, x = 'lingua', y = 'total')
```
Conforme a imagem:

![](imagens/graficosen.png)

Agora em pizza:

```py
plt.pie(dados["total"], labels = dados["lingua"])
```
![](imagens/pizza1.png)

Por ultimo gostaria de visualizar um gráfico decrescente e com uma cor que visualmente fosse identificado que isso é do maior para o menor, para isso é necessario criar a variavel que diferencia os idiomas do ingles:

```py
films_sem_lingua_original_em_ingles = tmdb.query("original_language != 'en'")
```

E com esta variavel utilizar o parametro **palette** para definir o modo degradê de cor.

```py 
sns.catplot(x = "original_language", data = filmes_sem_lingua_original_em_ingles, kind="count", aspect=2, palette = "GnBu_d", order = total_por_linguas_de_outros_filmes.index)
```

![](imagens/degrade.png)




