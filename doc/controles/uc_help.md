# uc_help
O controle **uc_help** destinado a apresentar informações em duas colunas. Na coluna da esquerda um formato de titulo + texto, e na direita uma lista com links.
Uma propriedade 

## Parágrafos
São compostos por **titulo** e **texto**.
```
&paragrafo = new()
&paragrafo.titulo =  'O que é?'
&paragrafo.texto  = 'Mussum Ipsum, cacilds vidis litro abertis. Suco de cevadiss deixa as pessoas mais interessantis. Interagi no mé, cursus quis, vehicula ac nisi. Si num tem leite então bota uma pinga aí cumpadi! Suco de cevadiss, é um leite divinis, qui tem lupuliz, matis, aguis e fermentis.'
&uc_helpin.paragrafos.Add(&paragrafo)
```

|var|tipo|
|-----------------|---------------------------|
|&paragrafo | &uc_helpin.paragrafo |
|&uc_helpin|uc_helpin|


## Materiais adicionais
Os links são informados em uma variável **&adicional**.
```
 &adicional = new()
 &adicional.icone = '<i class="fab fa-youtube"></i>'
 &adicional.titulo = 'Primeiros passos'
 &adicional.link = 'https://www.youtube.com/watch?v=S1YABU0ssog'
 &uc_helpin.adicionais.Add(&adicional)
```

|var|tipo|
|-----------------|---------------------------|
|&paragrafo | &uc_helpin.adicional |
|&uc_helpin|uc_helpin|


## Exemplo completo
O controle é formado por um texto principal (titulo) e um secundário (subtitulo) apresentado logo abaixo.
```
sub 'textohelp'
 &uc_helpin.classe  = ''	
 &uc_helpin.icone   = '<i class="fas fa-caret-down"></i>'
 &uc_helpin.titulo  = 'Obter ajuda'
 &uc_helpin.tooltip = ''
 &uc_helpin.colapsado = true
	
 &paragrafo = new()
 &paragrafo.titulo =  'O que é?'
 &paragrafo.texto  = 'Mussum Ipsum, cacilds vidis litro abertis. Suco de cevadiss deixa as pessoas mais interessantis. Interagi no mé, cursus quis, vehicula ac nisi. Si num tem leite então bota uma pinga aí cumpadi! Suco de cevadiss, é um leite divinis, qui tem lupuliz, matis, aguis e fermentis.'
 &uc_helpin.paragrafos.Add(&paragrafo)
	
 &paragrafo = new()
 &paragrafo.titulo = 'Onde consigo ajuda?' 
 &paragrafo.texto  = 'Mussum Ipsum, cacilds vidis litro abertis. Suco de cevadiss deixa as pessoas mais interessantis. Interagi no mé, cursus quis, vehicula ac nisi. Si num tem leite então bota uma pinga aí cumpadi! Suco de cevadiss, é um leite divinis, qui tem lupuliz, matis, aguis e fermentis.'
 &uc_helpin.paragrafos.Add(&paragrafo)
	
 &adicional = new()
 &adicional.icone = '<i class="fab fa-youtube"></i>'
 &adicional.titulo = 'Primeiros passos'
 &adicional.link = 'https://www.youtube.com/watch?v=S1YABU0ssog'
 &uc_helpin.adicionais.Add(&adicional)
	
 &adicional = new()
 &adicional.icone = '<i class="fab fa-youtube"></i>'
 &adicional.titulo = 'Designando um docente'
 &adicional.link = 'https://www.bootdey.com/snippets/view/dark-timeline'
 &uc_helpin.adicionais.Add(&adicional)
	
	html.caption = UC.uc_help(&uc_helpin.ToJson())
endsub
```
Na lateral direita, nas informações adicionais, será possível no campo **titulo** incluir qualquer tipo de controle ou mesmo informação.

## Com menu
Por exemplo, poderiamos inserir um **uc_menu** na lateral direita ao invés dos links. Ou ainda os links e o menu.
```
&uc_helpin = new()
&uc_helpin.classe  = ''	
&uc_helpIN.titulodireita = ''
&uc_helpin.tooltip = ''
&uc_helpin.colapsado = false
	
&paragrafo = new()
&paragrafo.titulo =  'O que é?'
&paragrafo.texto  = 'Mussum Ipsum, cacilds vidis litro abertis. Suco de cevadiss deixa as pessoas mais interessantis. Interagi no mé, cursus quis, vehicula ac nisi. Si num tem leite então bota uma pinga aí cumpadi! Suco de cevadiss, é um leite divinis, qui tem lupuliz, matis, aguis e fermentis.'
&uc_helpin.paragrafos.Add(&paragrafo)
	
&paragrafo = new()
&paragrafo.titulo = 'Onde consigo ajuda?'
&paragrafo.texto  = 'Mussum Ipsum, cacilds vidis litro abertis. Suco de cevadiss deixa as pessoas mais interessantis. Interagi no mé, cursus quis, vehicula ac nisi. Si num tem leite então bota uma pinga aí cumpadi! Suco de cevadiss, é um leite divinis, qui tem lupuliz, matis, aguis e fermentis.'
&uc_helpin.paragrafos.Add(&paragrafo)
	
do 'menu'
&adicional = new()
&adicional.titulo =  UC.uc_menu(&uc_menuIN.ToJson())
&uc_helpin.adicionais.Add(&adicional)
	
html.caption += UC.uc_help(&uc_helpin.ToJson())
```
E a carga do menu é programada na sub abaixo.

```
sub 'menu'
	&uc_menuin.id     = 'MENU'
	&uc_menuin.interface  = &Pgmname.Trim()
	&uc_menuin.classe = 'uc_menu-v uc_menu-vl'
	&uc_menuin.itens.Clear()
	
	&menuitem = new()
	&menuitem.icone  = '<i class="fas fa-house-damage uc_pointer"></i>'
	&menuitem.titulo = 'relatorio'
	&uc_menuin.itens.Add(&menuitem)
	
	&menuitem = new()
	&menuitem.icone  = '<i class="fas fa-running uc_pointer"></i>'
	&menuitem.titulo = 'follow-up'
	&uc_menuin.itens.Add(&menuitem)
	
	&menuitem = new()
	&menuitem.icone  = '<i class="fab fa-windows uc_pointer"></i>'
	&menuitem.titulo = 'produto'
	&uc_menuin.itens.Add(&menuitem)
	
	&menuitem = new()
	&menuitem.icone  = '<i class="fas fa-network-wired uc_pointer"></i>'
	&menuitem.titulo = 'ip'
	&uc_menuin.itens.Add(&menuitem)
	
	&menuitem = new()
	&menuitem.icone  = '<i class="fas fa-history uc_pointer"></i>'
	&menuitem.titulo = 'histórico'
	&uc_menuin.itens.Add(&menuitem)
endsub
```

|var|tipo|
|-----------------|---------------------------|
|&menuitem | &uc_menuin.item |
|&uc_menuin|uc_menuin|


## Conteúdo colapsado
Colapsar um conteúdo significa ocultar, sendo assim, podemos esperar a ação do usuário para apresentar o texto.
Serão necessárias tres propriedades para determinar o conteúdo colapsado, **&uc_helpin.colapsado=true**, em seguida o titulo e o icone que convida o usuário a clicar.
```
&uc_helpin.icone   = '<i class="fas fa-caret-down"></i>'
&uc_helpin.titulo  = 'Obter ajuda'
&uc_helpin.colapsado = true
```
