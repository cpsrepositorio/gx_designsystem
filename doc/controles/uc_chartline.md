# uc_chart (linhas e barras)
Além do conjunto de [gráficos redondos](/doc/controles/uc_chart.md), temos também uma série de outros gráficos de linhas, barras.

## Setup
Diferente dos demais controles para incluir a carga da biblioteca diretamente no Webpanel que utiliza o gráfico.

```
Event Start
 form.HeaderRawHTML = uc_carga()
 form.HeaderRawHTML += '<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>'
 do 'line'
EndEvent
```
Mais informações, aqui [getting-started](https://www.chartjs.org/docs/latest/getting-started/)

## Line
Os graficos redondos são claros e com muita utilidade, e muito simples de serem construídos, podendo ser cheios (pie) ou com um buraquinho no meio, rs, (doughnut).

| Propriedade | Significado |
|----------------|---------------------------------------------------------------------------------------------------------------------|
| width          | Define a largura da área do canvas que inclui o grafico, titulo, legenda. Se não definida segue o espaço disponível.|
| height         | Define a altura da área do canvas que inclui o grafico, titulo, legenda. Se não definida segue o espaço disponível.|
| titulo         | Opcional, define o nome do gráfico. Se não definido o gráfico ficará maior, pois esta propriedade consumirá um espaço na área do canvas.|
| tipo           | Tipo de gráfico, são vários, neste documento vamos tratar do uc_charttipo.pie e uc_charttipo.doughnut |
| rotulos        | São os titulos associado a cada pedaço do grafico |
| datasettitulo  |É o titulo do conjunto de dados, para o caso de haver mais de um gráfico no mesmo controle. Em gráficos redondos não faz muito sentido. |
| dataset        | É a coleção de dados equivalente a dimensão de cada pedaço da pizza. |
| datasetbgcolor | É a coleção de cores dos diversos pedaços |

**datasetbgcolor**, **dataset** e **rótulos** devem ter a mesma quantidade de itens.

A seguir um exemplo simples.
```
sub 'line'
 &linha.id = 'linha41'
 &linha.tipo = uc_charttipo.line

 &linha.datasettitle = 'TITULO'
 &linha.datasetborder = 2
 &linha.dataset.FromJson('[1,9,3,2,5,4]')
 &linha.rotulos.FromJson("['a','b','c','d','e','f']")
 &linha.datasetbgcolor.FromJson("['#FF5733','#FFCA33','#B2FF33','#33F6FF','#3374FF','#F933FF']")
 &linha.datasetbordercolor.FromJson("['#FF5733','#FFCA33','#B2FF33','#33F6FF','#3374FF','#F933FF']")

 html.Caption  = '<h3>Line</h3><hr>'
 html.Caption += '<div class="uc_flex-r uc_flex-w">'
 html.Caption +=   UC.uc_chart(&linha.ToJson())
 html.Caption += '</div>'
endsub
```

|var|tipo|
|-----------------|---------------------------|
|&linha | uc_chart|

## Informando as coleções
Existem duas maneiras de agregar dados, cores ou rótulos no gráfico.
* Com o **Add**
```
&linha.dataset.Add('1')
&linha.dataset.Add('9')
&linha.dataset.Add('3')
...
```
* Com um **Json**, sendo que neste modelo, criamos a definição (texto) de uma coleção em Json e adicionamos no dataset. Programa-se menos, mas é um pouco mais complexo em termos de compreensão. As chaves **[** e **]** demarcam a coleção e os itens são separados por virgula.
```
&linha.dataset.FromJson('[1,9,3,5,2,10]')
```
No segundo modelo temos uma forma mais compacta e mais simples de definir. Caso os dados tenham sido carregados em um SDT previamente, poderemos utilizar uma variável que já represente a coleção ou uma string, como no exemplo, que forma a coleção.

## Bar
Os gráficos de barras possuem a mesma estrutura dos gráficos de linhas, inclusive incluindo vários datasets.
```
sub 'bar'
	&bar.id = 'b1'
	&bar.titulo = ''
	&bar.legenda = '' // top, center, bottom
	&bar.width  = '300px'
	&bar.height = '300px'
	&bar.rotulos.Clear()
	&bar.datasets.Clear()
	&bar.dataset.Clear()
	&bar.rotulos.FromJson("['a','b','c','d','e','f']")

	/* (1) serie  ---------------------------------------*/
	&dataset = new()
	&dataset.tipo = uc_charttipo.bar
	&dataset.titulo = 'TITULO1'
	&dataset.border.size = 2	
	&dataset.bordercor = 'rgb(75, 192, 192)'
	&dataset.point = uc_chartpoint.cross
	&dataset.dados.FromJson('[1,9,3,2,5,4]')
	&bar.datasets.Add(&dataset)
	
	/* (2) serie  ---------------------------------------*/
	&dataset = new()
	&dataset.tipo = uc_charttipo.bar
	&dataset.titulo = 'TITULO1'
	&dataset.border.size = 2	
	&dataset.bordercor = 'rgb(75, 192, 192)'
	&dataset.point = uc_chartpoint.cross
	&dataset.dados.FromJson('[11,12,8,7,10,14]')
	&bar.datasets.Add(&dataset)
	
	html.Caption += '<h3 class="uc_mt30">Bar</h3><hr>'
	html.Caption += '<div class="uc_flex-r uc_flex-w">'
	html.Caption +=   UC.uc_chart(&bar.ToJson())
	html.Caption += '</div>'
endsub
```

|var|tipo|
|-----------------|---------------------------|
|&bar | uc_chart|
|&dataset|uc_chart.dataset |

## HorizontalBar
E o gráfico horizontal é a mesma coisa, somente que os datasets são orientados na horizontal.

```
sub 'hbar'
 &hbar.id = 'barh'
	&hbar.titulo = ''
	&hbar.legenda = '' // top, center, bottom
	&hbar.width  = '300px'
	&hbar.height = '300px'
	&hbar.rotulos.Clear()
	&hbar.datasets.Clear()
	&hbar.dataset.Clear()
	&hbar.rotulos.FromJson("['a','b','c','d','e','f']")

	/* (1) barra  ---------------------------------------*/
	&hbards = new()
	&hbards.tipo = uc_charttipo.horizontalbar
	&hbards.titulo = 'TITULO1'
	&hbards.border.size = 2	
	&hbards.bordercor = 'rgb(75, 192, 192)'
	&hbards.point = uc_chartpoint.cross
	&hbards.dados.FromJson('[1,9,3,2,5,4]')
	&hbar.datasets.Add(&hbards)
	
	/* (2) barra  ---------------------------------------*/
	&hbards = new()
	&hbards.tipo = uc_charttipo.horizontalbar
	&hbards.titulo = 'TITULO2 '
	&hbards.border.size = 2	
	&hbards.fill.tipo = ''
	&hbards.fill.acima = ''
	&hbards.fill.abaixo = ''
	&hbards.bordercor = 'rgb(175, 92, 192)'
	&hbards.point = uc_chartpoint.triangle
	&hbards.dados.Clear()
	&hbards.dados.FromJson('[11,12,8,7,10,14]')
	&hbar.datasets.Add(&hbards)

	html.Caption += '<h3 class="uc_mt30">Hbar</h3><hr>'
	html.Caption += '<div class="uc_flex-r uc_flex-w">'
	html.Caption +=   UC.uc_chart(&hbar.ToJson())
	html.Caption += '</div>'
endsub
```

|var|tipo|
|-----------------|---------------------------|
|&hbar | uc_chart|
|&hbards|uc_chart.dataset |

## Multi
São gráficos com multiplas séries, sendo que cada uma pode ser de um tipo diferente, mas da mesma categoria, como linha, barra.
Cada coleção é chamada de **dataset**

```
sub 'multi'
	&multi.id = 'multi'
	&multi.titulo = ''
	&multi.legenda = '' // top, center, bottom
	&multi.rotulos.Clear()
	&multi.datasets.Clear()
	&multi.dataset.Clear()
	&multi.rotulos.FromJson("['a','b','c','d','e','f']")
	&multi.datasetbgcolor.FromJson("['#33ff63','#FFCA33','#FF5733']")
	
	/* (1) serie  ---------------------------------------*/
	&dataset = new()
	&dataset.tipo = uc_charttipo.bar
	&dataset.titulo = 'TITULO1'
	&dataset.border.size = 2	
	&dataset.bordercor = 'rgb(75, 192, 192)'
	&dataset.point = uc_chartpoint.cross
	&dataset.dados.Clear()
	&dataset.dados.FromJson('[1,9,3,2,5,4]')
	&multi.datasets.Add(&dataset)
	
	/* (2) serie  ---------------------------------------*/
	&dataset = new()
	&dataset.tipo = uc_charttipo.line
	&dataset.titulo = 'TITULO2 '
	&dataset.border.size = 2	
	&dataset.bordercor = '#03d65b'
	&dataset.point = uc_chartpoint.triangle
	&dataset.dados.Clear()
	&dataset.dados.FromJson('[11,12,8,7,10,14]')
	&multi.datasets.Add(&dataset)
	
	/* (3) serie  ---------------------------------------*/
	&dataset = new()
	&dataset.tipo = uc_charttipo.line
	&dataset.titulo = 'TITULO222'
	&dataset.border.size = 2	
	&dataset.bordercor = '#d603be'
	&dataset.point = uc_chartpoint.triangle
	&dataset.dados.Clear()
	&dataset.dados.FromJson('[12,2,5,7,12,8]')
	&multi.datasets.Add(&dataset)

	html.Caption += '<h3 class="uc_mt30">Multi</h3><hr>'
	html.Caption += '<div class="uc_flex-r uc_flex-w">'
	html.Caption +=   UC.uc_chart(&multi.ToJson())
	html.Caption += '</div>'
endsub
```
|var|tipo|
|-----------------|---------------------------|
|&multi | uc_chart|
|&dataset|uc_chart.dataset |
