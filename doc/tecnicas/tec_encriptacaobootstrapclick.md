# INTERCEPTAÇÃO DO EVENTO

Não basta ligar o ENCRIPTPARMON no login, é necessário interceptar e tratar todos os parametros enviados ao BootstrapClick.

O UC BootstrapClick inclui um evento Click que permite que todas as ações (de click) sejam direcionadas para o evento Gx.
```
Event BootstrapClick1.Click
 &uc_btclick = Bootstrapclick1.ButtonId
EndEvent
```
&uc_btclick tratá os parametros que foram informados no controle, por exemplo: HISTORICOGRID:GRID:ABRIR:ADM001.

Normalmente quebramos esta string, separada por virgulas e temos:
1) O nome da interface: HISTORICOGRID
2) O controle: GRID
3) O evento: ABRIR
4) O parametro: ADM001

A programação a seguir, é mais completa porque passa para a função [navDefault_CLICK](/doc/tecnicas/navDefault_CLICK.md) a operação de tratamento dos parametros. Envolvendo o tratamento de clicks que podem acontecer no NavBar além dos controles da interface.
```
Event BootstrapClick1.Click
 &uc_btclick = Bootstrapclick1.ButtonId
 navDefault_CLICK(&uc_btclick, &uc_btclickparms, &url)
 if not &url.IsEmpty()
    alerta.Caption = '<script>window.location.assign("'+&url.Trim()+'");</script>'
 endif
EndEvent
```
O retorno deste procedimento será a variável &uc_btclickparms com os valores decriptados e sequencializados para que possamos utilizar.
```
	&uc_interface = &uc_btclickparms.Item(uc_btitem.interface).ToUpper().Trim()
	&uc_controle = &uc_btclickparms.Item(uc_btitem.controle).ToUpper().Trim()
	&uc_acao = &uc_btclickparms.Item(uc_btitem.acao).ToUpper().Trim()
 &uc_parm = &uc_btclickparms.Item(uc_btitem.parm1).ToUpper().Trim() 
```
Em seguida basta testar os valores para entender de onde o click partiu.
```
do case
				case &uc_acao='ORDERSEMESTRE'
					  &order = 'ACD_AlunoHistoricoConjuntoId'
					  do 'ui_grid'
endcase
```
