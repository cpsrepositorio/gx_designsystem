# home
A webpanel **home** é bem simples, contendo apenas um TEXTBLOCK e o controle de eventos.

![estrutura da tela](/doc/imagens/tec_home.png)

No TEXTBLOCK (grid) apresentamos informações a respeito do módulo que está sendo aberto e o controle de eventos é utilizado para interceptar as ações que ocorrem na tela enquanto a página esta aberta.

```
event Start
	form.HeaderRawHTML = uc_carga()
	form.Meta.AddItem("viewport", "width=device-width,initial-scale=1")
	do 'ui_grid'
endevent

sub 'ui_grid'
	&modulo = &websession.get('MODULO')
	do 'modulo'
endsub

sub 'modulo'
	for each
	where ModuloNome = &modulo.ToLower()
		&uc_cardin.classe			= 'uc_card_clear '
		&uc_cardin.classesize		= 'uc_card300'
		&uc_cardin.classecontainer 	= 'uc_cardcontainer_clear'
		&carditem = new()
		&carditem.titulo 			= ModuloNome.Trim()
		&carditem.texto 			= ModuloDescricao.Trim()
		&carditem.image 			= ModuloImagem.Trim()
		&carditem.imageclasse 		= 'uc_card300img'
		&uc_cardin.cards.add(&carditem)
		grid.Caption = UC.uc_card(&uc_cardin.ToJson())
		
	/* modulo nao localizado */
	when none
	 grid.Caption = ''
	endfor		
endsub

event BootstrapClick1.Click	
   	&uc_btclick = Bootstrapclick1.ButtonId
	navEvent(&uc_btclick, &uc_btclickparms, &url, &isok)
	if &isok
		GlobalEvents.MPHOME(&uc_btclickparms)
	endif
endevent

```
Na rotina **modulo** o programa obtém os dados do módulo selecionado (armazenado na &websession) e apresenta um card com as informações.

![card](/doc/imagens/tec_homecard.png)

Nesse cartão pode ser adicionado imagem e também sua apresentação pode ocupar toda largura da tela.

![card](/doc/imagens/tec_homecardlong.png)


## event BootstrapClick1.Click	
Esse é o evento importante no home, pois intercepta todos os clicks que estão acontecendo na interface. E uma vez que a home sempre vai direcionar o controle da operação para a masterpage, o evento global **GlobalEvents.MPHOME(&uc_btclickparms)** é acionado.

```
event BootstrapClick1.Click	
   	&uc_btclick = Bootstrapclick1.ButtonId
	navEvent(&uc_btclick, &uc_btclickparms, &url, &isok)
	if &isok
		GlobalEvents.MPHOME(&uc_btclickparms)
	endif
endevent
```

O evento é tratado na própria [master page](/doc/tecnicas/tec_masterpage.md) 
