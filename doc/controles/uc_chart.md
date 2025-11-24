# uc_chart


## Pie
Os graficos redondos são claros e com muita utilidade, e muito simples de serem construídos.
Será necessário uma variável **&pie** do tipo **

```
sub 'pie'
	&pie.id 		= 'pizza1'
	&pie.tipo 		= uc_charttipo.pie
	&pie.titulo  	= 'PIZZA CALABRESA'
	&pie.legenda 	= '' // top, center, bottom, left, chartArea
	
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
endsub
```


