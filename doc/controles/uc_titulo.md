# uc_titulo
Existem alguns controles bem simples, apenas para evitar a programação de HTML no sistema, **uc_titulo** é um exemplo.

## Exemplo
O controle é formado por um texto principal (titulo) e um secundário (subtitulo) apresentado logo abaixo.
```
sub 'titulo'
 &uc_tituloIN.titulo = 'Titulo'
 &uc_tituloIN.tituloclasse = 'uc_title' 
 &uc_tituloIN.texto = 'Mussum Ipsum, cacilds vidis litro abertis. Suco de cevadiss, é um leite divinis, qui tem lupuliz, matis, aguis e fermentis.Todo mundo vê os porris que eu tomo, mas ninguém vê os tombis que eu levo!Nec orci ornare consequat. Praesent lacinia ultrices consectetur. Sed non ipsum felis.Nullam volutpat risus nec leo commodo, ut interdum diam laoreet. Sed non consequat odio. Paisis, filhis, espiritis santis.Atirei o pau no gatis, per gatis num morreus.Pra lá , depois divoltis porris, paradis.Diuretics paradis num copo é motivis de denguis.'
 &uc_tituloIN.textoclasse = 'uc_titletext' 
 &uc_tituloIN.textovisible = true

 html.Caption = UC.uc_titulo(&uc_tituloIN.ToJson())
endsub
```
|var |tipo|
|----|-----|
|&uc_tituloIN|uc_tituloIN|

Observe que tanto em  **&uc_tituloIN.titulo** quanto em **&uc_tituloIN.texto** podemos inserir qualquer coisa, inclusive outro controle, como uma barra de botões por exemplo.

## Barra ao invés de texto
A seguir utilizamos o espaço do texto para inserir uma barra de botões.

```
sub 'barra'
 &uc_botaoiconeIN.id 			= 'id'
 &uc_botaoiconeIN.interface 		= 'interface'	
 &uc_botaoiconeIN.classebar 		= 'uc_flex-r uc_flex-nowrap'
 &uc_botaoiconeIN.classebotao  	= 'uc_btspace uc_bt-icon uc_pointer'
 &uc_botaoiconeIN.classeicon   	= ''
	
 &botoes.add('PLAY:5')
 &botoes.add('INFO:5')
 &botoes.add('NOVO:1')
 &botoes.add('ABRIR:2')
 &botoes.add('EDITAR:3')
 &botoes.add('APAGAR:4')
 &botoes.add('COPIAR:5')
 &botoes.add('COLAR:5')
 &uc_botaoiconeIN.botoes = &botoes.ToJson()
	
 &uc_tituloIN.titulo = 'Titulo'
 &uc_tituloIN.tituloclasse = 'uc_title' 
 &uc_tituloIN.texto = UC.uc_botaoicone(&uc_botaoiconeIN.ToJson())
 &uc_tituloIN.textoclasse = 'uc_titletext'
 &uc_tituloIN.textovisible = true

 html.Caption += UC.uc_titulo(&uc_tituloIN.ToJson())
endsub
```
|var |tipo|
|----|-----|
|&uc_tituloIN|uc_tituloIN|
|&uc_botaoiconeIN|uc_botaoiconein|
|&botoes|varchar(40) collection|


