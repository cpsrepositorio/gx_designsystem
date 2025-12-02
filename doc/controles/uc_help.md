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

## Materiais adicionais
Os links são informados em uma variável **&adicional**.
```
 &adicional = new()
 &adicional.icone = '<i class="fab fa-youtube"></i>'
 &adicional.titulo = 'Primeiros passos'
 &adicional.link = 'https://www.youtube.com/watch?v=S1YABU0ssog'
 &uc_helpin.adicionais.Add(&adicional)
```

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
