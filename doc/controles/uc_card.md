# uc_card
Cards são elementos que incluem imagens, titulos e textos em um cartão.

## Simples
No exemplo abaixo temos um titulo, texto e imagem, com a classe **uc_card** que inclui uma borda.
```
	&uc_cardin.classe	  = 'uc_card'
	&uc_cardin.classesize = 'uc_card300'
	
	&card = new()
	&card = new()
	&card.titulo 	= 'Titulo'
	&card.texto 	= 'Mussum Ipsum, cacilds vidis litro abertis. Nullam volutpat risus nec leo commodo, ut interdum diam laoreet. Sed non consequat odio. Detraxit consequat et quo num tendi nada. Em pé sem cair, deitado sem dormir, sentado sem cochilar e fazendo pose. Posuere libero varius. Nullam a nisl ut ante blandit hendrerit. Aenean sit amet nisi.'
	&card.image 	= 'https://www.w3schools.com/howto/img_avatar.png'
	&card.imageclasse = 'uc_card300img uc_card-img'
	
	&uc_cardin.cards.add(&card)
	
	html.Caption  = '<h5>uc_card</h5>'
	html.Caption += UC.uc_card(&uc_cardin.ToJson())
```

## Cinza
Um pequeno ajuste da classe, desta vez para **uc_card_gray**.
```
&uc_cardin = new()
	&uc_cardin.classe	  = 'uc_card_gray'
	&uc_cardin.classesize = 'uc_card300'
	
	&card = new()
	&card.titulo 	= 'Titulo'
	&card.texto 	= 'Mussum Ipsum, cacilds vidis litro abertis. Nullam volutpat risus nec leo commodo, ut interdum diam laoreet. Sed non consequat odio. Detraxit consequat et quo num tendi nada. Em pé sem cair, deitado sem dormir, sentado sem cochilar e fazendo pose. Posuere libero varius. Nullam a nisl ut ante blandit hendrerit. Aenean sit amet nisi.'
	&card.image 	= 'https://www.w3schools.com/howto/img_avatar.png'
	&card.imageclasse = 'uc_card300img uc_card-img'
	
	&uc_cardin.cards.add(&card)
	
	html.Caption += '<h5 class="uc_mt30">uc_card_gray</h5>'
	html.Caption += UC.uc_card(&uc_cardin.ToJson())
```

## Clear
Um outro conjunto de classes apresenta o cartão sem as bordas num padrão mais claro,  **uc_card_clear**.
```
	&uc_cardin = new()
	&uc_cardin.classe	  = 'uc_card_clear'
	&uc_cardin.classesize = 'uc_card300'
	
	&card = new()
	&card.titulo 	= 'Titulo'
	&card.texto 	= 'Mussum Ipsum, cacilds vidis litro abertis. Nullam volutpat risus nec leo commodo, ut interdum diam laoreet. Sed non consequat odio. Detraxit consequat et quo num tendi nada. Em pé sem cair, deitado sem dormir, sentado sem cochilar e fazendo pose. Posuere libero varius. Nullam a nisl ut ante blandit hendrerit. Aenean sit amet nisi.'
	&card.image 	= 'https://www.w3schools.com/howto/img_avatar.png'
	&card.imageclasse = 'uc_card300img uc_card-img'
	
	&uc_cardin.cards.add(&card)
	
	html.Caption += '<h5 class="uc_mt30">uc_card_clear</h5>'
	html.Caption += UC.uc_card(&uc_cardin.ToJson())
```

## Botões
Um toolbox também pode ser inserido, incluindo botões.

* **&card.toolboxclasse = 'uc_flex-r uc_flex-jcc uc_pt10 uc_pb10'** Define a classe da linha onde se inclui o toolbox, com a centralização e espaçamentos.
* **&card.toolbox  = UC.uc_botao(&uc_botaoin.ToJson())** Inclui a barra de botões.
```
	&uc_cardin = new()
	&uc_cardin.classe			= 'uc_card_clear'
	&uc_cardin.classecontainer 	= 'uc_cardcontainer_clear'
	&uc_cardin.classesize		= 'uc_card300'
	
	&card = new()
	&card.titulo 	= 'Titulo'
	&card.texto 	= 'Mussum Ipsum, cacilds vidis litro abertis. Nullam volutpat risus nec leo commodo, ut interdum diam laoreet. Sed non consequat odio. Detraxit consequat et quo num tendi nada. Em pé sem cair, deitado sem dormir, sentado sem cochilar e fazendo pose. Posuere libero varius. Nullam a nisl ut ante blandit hendrerit. Aenean sit amet nisi.'
	&card.image 	= 'https://www.w3schools.com/howto/img_avatar.png'
	&card.imageclasse = 'uc_card300img'
	
	&uc_botaoin = new()
	&botao.cor 		= uc_botaocor.primary
	&botao.titulo 	= 'Salvar'
	&botao.evento 	= "SALVAR"
	&botao.icone	= '<i class="far fa-save"></i>'
	&botao.tooltip  = 'tooltip do componente'
	&botao.outline  = false
	&uc_botaoin.botoes.Add(&botao)

	&card.toolboxclasse = 'uc_flex-r uc_flex-jcc uc_pt10 uc_pb10'
	&card.toolbox  = UC.uc_botao(&uc_botaoin.ToJson())
	
	&uc_cardin.cards.add(&card)
	
	html.Caption += '<h5 class="uc_mt30">Clear com botões</h5>'
	html.Caption += UC.uc_card(&uc_cardin.ToJson())
```

## Footer
O controle também permite incluir um rodapé, que pode ser utilizado para incluir o toolbox, por exemplo.
```
	&uc_cardin = new()
	&uc_cardin.classe			= 'uc_card_clear '
	&uc_cardin.classecontainer 	= 'uc_cardcontainer_clear'
	&uc_cardin.classesize		= 'uc_card300'
	
	&card = new()
	&card.titulo 	= 'Titulo'
	&card.texto 	= 'Mussum Ipsum, cacilds vidis litro abertis. Nullam volutpat risus nec leo commodo, ut interdum diam laoreet. Sed non consequat odio. Detraxit consequat et quo num tendi nada. Em pé sem cair, deitado sem dormir, sentado sem cochilar e fazendo pose. Posuere libero varius. Nullam a nisl ut ante blandit hendrerit. Aenean sit amet nisi.'
	&card.image 	= 'https://www.w3schools.com/howto/img_avatar.png'
	&card.imageclasse = 'uc_card300img'
	
	&uc_botaoin = new()
	&botao.cor 		= uc_botaocor.primary
	&botao.titulo 		= 'Salvar'
	&botao.evento 		= "SALVAR"
	&botao.icone	 	= '<i class="far fa-save"></i>'
	&botao.tooltip  	= 'tooltip do componente'
	&botao.outline   	= false
	&uc_botaoin.botoes.Add(&botao)
		
	&card.footerclasse = 'uc_flex-r uc_flex-jcc uc_blue uc_p10 uc_borderradius-bottom'
	&card.footertexto  = UC.uc_botao(&uc_botaoin.ToJson())
	
	&uc_cardin.cards.add(&card)
	
	html.Caption += '<h5 class="uc_mt30">Footer</h5>'
	html.Caption += UC.uc_card(&uc_cardin.ToJson())
```

