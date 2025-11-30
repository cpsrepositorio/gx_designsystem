# uc_chart
Além do conjunto de [gráficos redondos](/doc/controles/uc_chart.md), temos também uma série de outros gráficos de linhas, barras.


## Setup
Diferente dos demais controles para incluir a carga da biblioteca diretamente no Webpanel que utiliza o gráfico.

```
Event Start
 form.HeaderRawHTML = uc_carga()
 form.HeaderRawHTML += '<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>'
 do 'pie'
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

## Informando as coleções
Existem duas maneiras de agregar dados, cores ou rótulos no gráfico.
1) Com o **Add**
```
&linha.dataset.Add('1')
&linha.dataset.Add('9')
&linha.dataset.Add('3')
...
```
2) Com um **Json**
Neste modelo, criamos a definição de uma coleção em Json e adicionamos no dataset. Programa-se menos, mas é um pouco mais complexo em termos de compreensão. As chaves **[** e **]** demarcam a coleção e os itens são separados por virgula.
```
&linha.dataset.FromJson('[1,9,3,5,2,10]')
```
No cenário (2) temos um modo mais compacto e mais simples de ser obtido, caso os dados tenham sido carregados em um SDT previamente.
Podemos utilizar uma variável que já represente a coleção ou uma string, como no exemplo, que forma a coleção.
