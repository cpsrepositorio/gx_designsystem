# uc_listapagging (deprecated)

Utilize o controle [uc_listapaginada](/doc/controles/uc_listapaginada.md) ao invés deste controle de paginação.

Este controle realiza a paginação dos registros em uma lista, porém, apresenta uma maior complexidade na navegação das paginas.

## Lista simples

A seguir o exemplo completo.

```
Event Start
	form.HeaderRawHTML = uc_carga()
	html.Caption	= ''	
	alerta.Caption	= ''

	&pg			= 1	
	&pgsize		= 14	
	
	do 'load'
Endevent

sub 'load'
	&registros.Clear()
 	&registros = LIXO_TesteDP(&pgsize, &pg)
	do 'grid'
endsub

Event &search.IsValid
	&registros.Clear()
 	&registros = LIXO_TesteDPSearch(&search)
	do 'grid'
EndEvent

sub 'grid'
	do 'last'
	
	&uc_listIN.id = 'LISTA'
	&uc_listIN.interface = &Pgmname
	&uc_listIN.pagging = true
	&uc_listIN.paggingcolor = 'uc_btblueoutlineclear'
	&uc_listIN.paggingposition = uc_position.bottom
	&uc_listIN.pagginglabel = 'pg: '+&pg.ToString().Trim()+' de: '+&last.ToString()
	&uc_listIN.itens.Clear()
	
	for &reg in &registros

		&uc_botoesIN.id = 'LISTA'
		&uc_botoesIN.interface = &Pgmname.Trim()
		&uc_botoesIN.botoes.Clear()
		
		&uc_botaoIN = new()
		&uc_botaoIN.cor 		= uc_bt.outblue
		&uc_botaoIN.icone		= '<i class="far fa-edit"></i>'
		&uc_botaoIN.evento 		= "EDIT:bt1"
		&uc_botaoIN.tooltip  	= 'tooltip do componente'
		&uc_botaoIN.classe      = 'uc_btspace'
		&uc_botoesIN.botoes.Add(&uc_botaoIN)
		
		&uc_botaoIN = new()
		&uc_botaoIN.cor 		=  uc_bt.outblue
		&uc_botaoIN.icone		= '<i class="fas fa-trash-alt"></i>'
		&uc_botaoIN.evento 		= "DELETE:bt2"
		&uc_botaoIN.tooltip  	= 'tooltip do componente'
		&uc_botaoIN.outline   	= true
		&uc_botaoIN.classe      = 'uc_btspace'
		&uc_botoesIN.botoes.Add(&uc_botaoIN)
		
		
		&item = new()
		&item.titulo 			= &reg.LIXO_TesteNome.ToUpper().Trim()
		&item.tooltip			= &reg.LIXO_TesteNome.ToUpper().Trim()
		&item.evento			= 'ABRIR:'+&reg.LIXO_TesteId.ToString().Trim()
		&item.imagem.classe 	= 'uc_imagemredonda15px'
		&item.imagem.image		= &reg.LIXO_TesteFoto.Trim()
		&item.imagem.tooltip 	= &reg.LIXO_TesteNome.ToUpper().Trim()
		&item.toolbox =  UC.uc_botao(&uc_botoesIN.ToJson())

		&uc_listIN.itens.Add(&item)
	endfor
	html.Caption = UC.uc_listapagging(&uc_listIN.ToJson())
endsub

// ---------- PAGGING ---------------------------------------------------------- //
sub 'PAGGING'
	&search = ''
	do case
		case &uc_btclickparms.Item(uc_btitem.acao) = 'FIRST'
			do '<<'
		case &uc_btclickparms.Item(uc_btitem.acao) = 'BEFORE'
			do '<'
		case &uc_btclickparms.Item(uc_btitem.acao) = 'NEXT'
			do '>'
		case &uc_btclickparms.Item(uc_btitem.acao) = 'LAST'
			do '>>'
	endcase
	do 'load'
endsub

sub '<<'
	&pg=1
endsub

sub '<'
	&pg-=1
	if &pg<=0
		&pg=1
	endif
endsub

sub '>'
	&pg+=1
	do 'last'
	if &pg > &last
		&pg = &last
	endif
	&uc_mensagem = 'proximo '+&pg.ToString()
endsub

sub '>>'
	do 'last'
	&pg = &last
endsub

sub 'last'
	if &pgsize>0
		&total = count(LIXO_TesteId)
		&rs = &total/&pgsize	
		if &rs.Integer()<&rs
			&last = &total/&pgsize + 1
		else
			&last = &total/&pgsize
		endif
	else
		&last=0
	endif
endsub

// ------ CONTROLE DE EVENTOS ---------------------------------------------------- //
Event Bootstrapclick1.Click
	&uc_btclick = Bootstrapclick1.ButtonId
	navEvent2(&uc_btclick, &uc_btclickparms, &url, &isok)
	if &isok
		GlobalEvents.MPHOME(&uc_btclickparms)
	endif
	
	msg(
		' interface:'	+ &uc_btclickparms.Item(uc_btitem.interface)
		+' controle:'	+ &uc_btclickparms.Item(uc_btitem.controle)
		+' acao:'		+ &uc_btclickparms.Item(uc_btitem.acao)
		+' parametro:'	+ &uc_btclickparms.Item(uc_btitem.parm1)
	)

	do case 
		case  &uc_btclickparms.Item(uc_btitem.controle) = 'PAGGING'
			do 'PAGGING'
	endcase
EndEvent

```
