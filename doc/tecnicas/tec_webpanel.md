# Criando webpanel´s
Tudo começa com uma interface Web, que em Genexus é definida a partir de um objeto WebPanel, mas não é muito simples de se compreender a principio.

Primeiramente, é necessário compreender que o Genexus é um gerador de código e ele sempre vai querer incluir um monte de coisas a mais, que consideramos desnecessárias e o pior, que atrapalham no design da tela.

## Layout control
O [Abstract Editor](https://docs.genexus.com/en/wiki?25250,How+to+use+the+Abstract+Editor%3A+designing+a+Web+Transaction+Form) do Genexus possibilita criar alguns tipos de layouts para controlar os objetos na interface:
* **Responsive Table**, é o design que segue as regras de estrutura do Bootstrap com suas 12 colunas, e que permite criar [design responsivo(https://docs.genexus.com/en/wiki?29134,Table+of+contents%3AResponsive+Web+Design+in+GeneXus)
* **Flex layout**, é o layout mais flexível (e simples) que permite organizar os objetos em linhas e colunas, aqui temos um artigo de um dos desenvolvedores do Genexus: [galeria de fotos com flex layout](https://genexus.blog/es_ES/design/photosgallery-a-genexus-flex-and-flex-grid-sample/). Aqui um guia completo [A guide to flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
* **Canvas**, é um layout que permite posicionar os objetos por coordenadas absolutas e mais dedicado a aplicações Smartdevices. [Canvas control](https://docs.genexus.com/en/wiki?22452,Canvas+control)
* **Smart table**, é um layout que permite construir áreas na interface como uma tabela. [Smart tables](https://docs.genexus.com/en/wiki?45577,Smart+Table+control)
* **Tabular table**, é o design mais simples que define layout por tabelas tradicionais (<table>)

Utilizamos com maior frequencia o **flex layout** em nossos sistemas.

## Stencil
Não utilize stencil nas interfaces com o gxdesignsystem, simplesmente não funcionam.

## Section
Outro objeto importante para adicionar em nosso projeto de interface são os controles **Section** do Genexus, que produzem **<div>...</div>** na interface.
São úteis para organizar agrupamentos de controles na interface.

## Textblock
É o controle principal que utilizaremos para apresentar nossos controles.

## Exemplo completo
Nesse exemplo, que temos como padrão para interfaces com o controle de lista temos



```
Event Start
	form.HeaderRawHTML = uc_carga()
	
	/* estrutura da informação */
	&pg = 1
	&pgsize = 5
	
	/* controles em modo default */
	do 'seguranca'
	do 'load'
Endevent

/* ------------------------ ESTRUTURA DA INTERFACE -------------------------- */
sub 'seguranca'
//	segurancaGET(&Pgmname)
	
	/* detalhes do programa */
	&HelpSDT= HelpGET(&Pgmname)
	&uc_tituloin.titulo = &HelpSDT.HelpTitle
	&uc_tituloin.tituloclasse = 'uc_title'
	&uc_tituloin.texto = &HelpSDT.HelpText.Trim()
	&uc_tituloin.textoclasse = 'uc_titletext'
	&uc_tituloin.textovisible = false
	titulo.Caption = UC.uc_titulo(&uc_tituloin.ToJson())
endsub

sub 'ui_modo_default'
	alerta.Caption = ''
	grid.Caption 	= ''
	icone.Caption 	= '<i class="fas fa-filter uc_pr10"></i>'
	&search.Visible = 1
	tb_detail.Visible = 0
	
	&ButtonBarSDT.programa  	= &Pgmname
	&ButtonBarSDT.inserir	= true
	&ButtonBarSDT.fechar	= false
	&ButtonBarSDT.detalhe	= false
	&ButtonBarSDT.doc      	= false
	do 'ui_buttonbar'
endsub

sub 'ui_modo_detail'
	alerta.Caption = ''
	grid.Caption = ''
	icone.Caption 	= ''
	&search.Visible	= 0
	tb_detail.Visible 	= 1
	
	&ButtonBarSDT.programa  	= &Pgmname
	&ButtonBarSDT.inserir	= false
	&ButtonBarSDT.fechar	= true
	&ButtonBarSDT.detalhe	= false
	&ButtonBarSDT.doc      	= false
	do 'ui_buttonbar'
endsub

sub 'ui_buttonbar'
	&uc_botaoin = ButtonBarGET(&ButtonBarSDT)
	buttonbar.Caption = '<div class="uc_flex-r uc_flex-jce">'+UC.uc_botao(&uc_botaoin.ToJson())+'</div>'
endsub

/* ------------------------ CARGA DE DADOS ----------------------------- */
sub 'load'
	do 'ui_modo_default'
	&rows.Clear()
	&rows = exemploDP(&id, &pgsize, &pg)
	&rows.Sort('Descricao')
	do 'ui_grid'
endsub

sub 'ui_grid'
	&GridViewSDT.id = 'LISTA'
	&GridViewSDT.programa = &Pgmname
	&GridViewSDT.pagging = true
	&GridViewSDT.pg = &pg
	&GridViewSDT.pgsize = 5
	&GridViewSDT.totalrec = count(LIXO_TesteNome)
	&GridViewSDT.typeid = typeid.Numero
	&GridViewSDT.toolbar.inserir = false
	&GridViewSDT.toolbar.abrir  = false
	&GridViewSDT.toolbar.editar = true
	&GridViewSDT.toolbar.apagar = true

	/* apresenta */
	&uc_listin = GridGET(&rows, &GridViewSDT)
	grid.Caption = UC.uc_listapaginada(&uc_listin.ToJson())
endsub

/* ----------------------- CONTROLE DE EVENTOS ---------------------------- */
Event Bootstrapclick1.Click

	&uc_btclick = Bootstrapclick1.ButtonId
	navEvent2(&uc_btclick, &uc_btclickparms, &url, &isok)
	if &isok
		GlobalEvents.MPHOME(&uc_btclickparms)
	endif

	/* eventos */
	do case
		case &uc_btclickparms.Item(uc_btitem.interface)=&Pgmname.toupper()
			do case
				case &uc_btclickparms.Item(uc_btitem.acao)='INSERIR'
					do 'ui_modo_detail'
					&id = 0
					component1.Object = LIXO_Teste.Create(trnmode.Insert, &id)
				case &uc_btclickparms.Item(uc_btitem.acao)='EDITAR'
					do 'ui_modo_detail'
					&id = &uc_btclickparms.Item(uc_btitem.parm1).ToNumeric()
					component1.Object = LIXO_Teste.Create(trnmode.Update, &id)
				case &uc_btclickparms.Item(uc_btitem.acao)='APAGAR'
					&id = &uc_btclickparms.Item(uc_btitem.parm1).ToNumeric()
					&LIXO_Teste.Load(&id)
					&LIXO_Teste.Delete()
					if &LIXO_Teste.Success()
						commit
						do 'load'
					else
						msg('Erro '+&LIXO_Teste.GetMessages().Item(1).Description)
					endif
				case &uc_btclickparms.Item(uc_btitem.controle)='PAGGING'
					&pg = &uc_btclickparms.Item(uc_btitem.parm1).ToNumeric()
					do 'ui_modo_default'
					do 'load'
			endcase
		otherwise
	endcase
EndEvent

Event Enter
	do 'load'
Endevent

```
