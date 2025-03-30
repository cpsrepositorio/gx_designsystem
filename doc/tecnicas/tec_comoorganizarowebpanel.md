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
Controle de segurança.
```
sub 'security'
	
endsub
```
Carga de registros
```
/* --------------------------------------------------------------------------------
   CARGA
   -------------------------------------------------------------------------------- */
sub 'load'
 /* valores default */
 &order = 'ACD_AlunoHistoricoConjuntoId'

 /* serviço */
 &ws_siga.parametro  = '471853;175;43;3;894'
 &ws_siga.servico    = 'historico'
 &ws_siga.token		= ''
	
 do 'ws_service'
 do 'ui_grid'
endsub

sub 'ws_service'
 &texto = serviceGET(&ws_siga)
 ws_limparetorno(&texto)
 &ALU_AlunoHistorico_SDT.FromJson(&texto.Trim())
 if &primeira
  do 'ui_status'
  do 'ui_periodo'
 endif
endsub
```
Montagem da interface.
```
/* --------------------------------------------------------------------------------
   UI
   -------------------------------------------------------------------------------- */
sub 'ui_grid'
 &grid  = historicoGRID(&ALU_AlunoHistorico_SDT, &status, &periodo, &order)	
 grid.Caption  = '<div class="uc_w100 uc_p30">'+UC.uc_tabela(&grid.ToJson())+'</div>'
endsub
```
Tratamento de eventos 
```
/* --------------------------------------------------------------------------------
   EVENTOS
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
 &uc_aca = &uc_btclickparms.Item(uc_btitem.acao).ToUpper().Trim()
	
 do case
  case &uc_acao='ORDERPERIODO'
   &order = 'ACD_AlunoHistoricoPeriodoOferecimentoId'
   do 'ui_grid'
  endcase
endevent

```
