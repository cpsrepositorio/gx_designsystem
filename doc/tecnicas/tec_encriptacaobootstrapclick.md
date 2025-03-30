# INTERCEPTAÇÃO DO EVENTO

Não basta ligar o ENCRIPTPARMON no login, é necessário interceptar e tratar todos os parametros enviados ao BootstrapClick.

O UC BootstrapClick inclui um evento Click que permite que todas as ações (de click) sejam direcionadas para o evento Gx.

```
Event BootstrapClick1.Click
 &uc_btclick = Bootstrapclick1.ButtonId
EndEvent
```
&uc_btclick tratá os parametros que foram informados no controle, por exemplo: 
 
	navDefault_CLICK(&uc_btclick, &uc_btclickparms, &url)
	if not &url.IsEmpty()
		alerta.Caption = '<script>window.location.assign("'+&url.Trim()+'");</script>'
	endif
