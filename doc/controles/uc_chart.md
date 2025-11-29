# uc_chart
O pacote inclui um conjunto de controles para gráficos utilizando a biblioteca (chats.js](https://www.chartjs.org/).

## Pie
Os graficos redondos são claros e com muita utilidade, e muito simples de serem construídos, podendo ser cheios (pie) ou com um buraquinho no meio, rs, (doughnut).

| Propriedade | Significado |
|-------|-----|
| width | Define a largura da área do canvas que inclui o grafico, titulo, legenda. Se não definida segue o espaço disponível.|
| height | Define a altura da área do canvas que inclui o grafico, titulo, legenda. Se não definida segue o espaço disponível.|
| Titulo | Opcional, define o nome do gráfico. Se não definido o gráfico ficará maior, pois esta propriedade consumirá um espaço na área do canvas.|
| Tipo | Tipo de gráfico, são vários, neste documento vamos tratar do uc_charttipo.pie e uc_charttipo.doughnut |
| rotulos | São os titulos associado a cada pedaço do grafico |
| datasettitulo |É o titulo do conjunto de dados, para o caso de haver mais de um gráfico no mesmo controle. Em gráficos redondos não faz muito sentido. |
| dataset | É a coleção de dados equivalente a dimensão de cada pedaço da pizza. |
| datasetbgcolor | É a coleção de cores dos diversos pedaços |

**datasetbgcolor**, **dataset** e **rótulos** devem ter a mesma quantidade de itens.

A seguir um exemplo simples.
```
sub 'pie'
 	&pie.id 		= 'pizza1'
	&pie.tipo 		= uc_charttipo.pie
	&pie.titulo  	= 'Grafico Pizza'
	&pie.width		= '300px;'
	&pie.height		= '300px;'
 
	&pie.rotulos.Add("vermeio")
	&pie.rotulos.Add("azur")
	&pie.rotulos.Add("marelo")
	&pie.rotulos.Add("verde palmeiras")
	&pie.rotulos.Add("roxinho")
	&pie.rotulos.Add("laranja")
	
	&pie.datasettitle = 'TITULO'
	&pie.datasetborder = 2
	&pie.dataset.Add('1')
	&pie.dataset.Add('9')
	&pie.dataset.Add('3')
	&pie.dataset.Add('5')
	&pie.dataset.Add('2')
	&pie.dataset.Add('10')
	
	&pie.datasetbgcolor.Add('#FF5733')
	&pie.datasetbgcolor.Add('#FFCA33')
	&pie.datasetbgcolor.Add('#B2FF33')
	&pie.datasetbgcolor.Add('#33F6FF')
	&pie.datasetbgcolor.Add('#3374FF')
	&pie.datasetbgcolor.Add('#4a83bc')

	html.Caption += UC.uc_chart(&pie.ToJson())

endsub
```

## Informando as coleções
Existem duas maneiras de agregar dados, cores ou rótulos no gráfico.
1) Com o **Add**
Este ja vimos no exemplo anterior.
```
&pie.dataset.Add('1')
&pie.dataset.Add('9')
&pie.dataset.Add('3')
&pie.dataset.Add('5')
&pie.dataset.Add('2')
&pie.dataset.Add('10')
```
2) Com um **Json**
Neste modelo, criamos a definição de uma coleção em Json e adicionamos no dataset. Programa-se menos, mas é um pouco mais complexo em termos de compreensão. Os caracteres [ e ] demarcam a coleção e os itens são separados por virgula.
```
&pie.dataset.FromJson('[1,9,3,5,2,10]')
```
No cenário (2) temos um modo mais compacto e mais simples de ser obtido, caso os dados tenham sido carregados em um SDT previamente.
