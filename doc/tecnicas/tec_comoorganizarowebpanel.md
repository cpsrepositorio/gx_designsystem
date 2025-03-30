# ORGANIZAÇÃO DO WEBPANEL
Na versão Genexus 18 é importante compreender que o modelo de eventos de recarga da interface é completamente diferente.
Não ocorrerá o chamado REFRESH de tela e a sua recarga. Em momento nenhum.

```
Event Start

  /* (1) carga das folhas de estilo */
  form.HeaderRawHTML  = uc_cssLOAD()
  form.Meta.AddItem("viewport",'content="width=device-width, initial-scale=1.0"')

  /* (2) controle de segurança de acesso */
  do 'security'

  /* (3) carga da interface */
  do 'load'	
	
Endevent
```

```
sub 'security'
	
endsub

sub 'load'
	
	/*	DADOS DO ALUNO
	
		-- matricula corrente
		ACD_AlunoId					517122	
		UNI_UnidadeId				311
		ACD_CursoId					164
		ACD_PeriodoId				1
		ACD_EstruturaCurricularId	1085
		ACD_PeriodoOferecimentoId	20251
	
	*/
	
	/* valores default */
	&order = 'ACD_AlunoHistoricoConjuntoId'
	
	/* serviço */
	&ws_siga.parametro  = '471853;175;43;3;894'
	&ws_siga.servico    = 'historico'
	&ws_siga.token		= ''
	
	do 'ws_service'
	do 'ui_grid'
endsub

/* --------------------------------------------------------------------------------
	SERVIÇO EXTERNO (carga de informação para a interface)
   -------------------------------------------------------------------------------- */
sub 'ws_service'
	&texto = serviceGET(&ws_siga)
	ws_limparetorno(&texto)
	&ALU_AlunoHistorico_SDT.FromJson(&texto.Trim())
	if &primeira
		do 'ui_status'
		do 'ui_periodo'
	endif
endsub

/* --------------------------------------------------------------------------------
	UI: montagem do conteúdo da interface
   -------------------------------------------------------------------------------- */
sub 'ui_grid'
	&cards = estatisticaCARDS(&Pgmname, &estatistica, 'uc_card-icone-size16pt')
	&grid  = historicoGRID(&ALU_AlunoHistorico_SDT, &status, &periodo, &order)	
	
	estatistica.Caption  = '<div class="uc_w100">'+UC.uc_carddestaque(&cards.ToJson())+'</div>'
	grid.Caption  = '<div class="uc_w100 uc_p30">'+UC.uc_tabela(&grid.ToJson())+'</div>'
endsub

sub 'ui_status'
	/* situações do aluno */
	for &item in &ALU_AlunoHistorico_SDT
		&isok=true
		/* totaliza as observações para montar o controle de status da tela e apresentar cards estatisticos */
		for &estatisticaSDT in &estatistica
			if &estatisticaSDT.chave = &item.GER_TipoObservacaoHistoricoDescricao
				&estatisticaSDT.total += 1
				&isok=false
				exit	
			endif
		endfor
		/* totalizador estatistico */
		if &isok
			&estatisticaSDT = new()
			&estatisticaSDT.chave = &item.GER_TipoObservacaoHistoricoDescricao
			&estatisticaSDT.total = 1
			&estatisticaSDT.unidade = ''
			&estatisticaSDT.tipo = 1
			&estatistica.add(&estatisticaSDT)			
		endif
	endfor
	
	/* controle para filtrar o status */
	&status.Clear()
	&status.AddItem('','(status)')
	for &estatisticaSDT in &estatistica
		&status.AddItem(&estatisticaSDT.chave,&estatisticaSDT.chave)
	endfor
	&primeira=false
endsub

sub 'ui_periodo'
	for &item in &ALU_AlunoHistorico_SDT
		&isok=true
		for &itemlistan in &listan
			if &itemlistan=&item.ACD_AlunoHistoricoPeriodoOferecimentoId
				&isok=false
				exit	
			endif
		endfor
		if &isok
			&listan.Add(&item.ACD_AlunoHistoricoPeriodoOferecimentoId)
		endif
	endfor
	
	&periodo.Clear()
	&periodo.AddItem(0,'(periodo)')
	for &itemlistan in &listan
		&periodo.AddItem(&itemlistan,&itemlistan.ToString())
	endfor
	&primeira=false
endsub

/* --------------------------------------------------------------------------------
	EVENTO:operaçãoes de click na interface
   -------------------------------------------------------------------------------- */
Event BootstrapClick1.Click
 	alerta.Caption = ''
  	&uc_btclick = Bootstrapclick1.ButtonId
	navDefault_CLICK(&uc_btclick, &uc_btclickparms, &url)
	if not &url.IsEmpty()
		alerta.Caption = '<script>window.location.assign("'+&url.Trim()+'");</script>'
	endif
	
	/* tratamento dos eventos */
	&uc_interface 	= &uc_btclickparms.Item(uc_btitem.interface).ToUpper().Trim()
	&uc_controle 	= &uc_btclickparms.Item(uc_btitem.controle).ToUpper().Trim()
	&uc_acao 		= &uc_btclickparms.Item(uc_btitem.acao).ToUpper().Trim()
	
	do case
		
		/* acoes da interface ----------------------- */	
		case &uc_interface.trim() ='HISTORICOGRID'
			
				
				case &uc_acao='ORDERPERIODO'
					&order = 'ACD_AlunoHistoricoPeriodoOferecimentoId'
					do 'ui_grid'
				case &uc_acao='ORDERPERIODO'
					&order = 'ACD_AlunoHistoricoPeriodoOferecimentoId'
					do 'ui_grid'
				case &uc_acao='ORDEROBSERVACAO'
					&order = 'GER_TipoObservacaoHistoricoDescricao'
					do 'ui_grid'
					
			endcase
	endcase
endevent

Event &status.ControlValueChanged
	do 'ui_grid'
endEvent

Event &periodo.ControlValueChanged
	do 'ui_grid'
endEvent


```
