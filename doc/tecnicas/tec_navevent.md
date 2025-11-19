# NavEvent
Ao longo do tempo certas estratégias com o modulo foram sendo aprimoradas de forma a centralziarem todo processo de encriptação, controle de localização do evento em um único procedimento.

Esse procedimento avalia se a variavel de sessão pede encriptação ou não de parametros e trata da decriptação dos parametros, caso esta esteja ligado (uc_clickDEC). Isso retorna uma string sempre decriptada que em seguida é quebrada com &uc_btclickparms = &uc_btclick.SplitRegEx(':').


### NavEvent(&uc_btclick, &uc_btclickparms, &url, &isok)
É uma procedure que centraliza a encriptação e trata dos eventos que ocorrem no NAVBAR e SIDEBAR.

* **&uc_btclick** string original do evento que pode estar encriptada. Ao término do processamento retorna para o chamador no formato decriptado.
* **&uc_btclickparms** coleção de parametros do evento
* **&url** é a URL do módulo em que ocorreu o evento
* **&isok** informa, se true, que o evento de fato é da NAVBAR ou SIDEBAR.

```
	&encrypt 	= iif(&websession.Get("SECURITYPARMON")="1", true, false)
	&encryptkey = &websession.Get("SECURITYPARMKEY")
	if &encrypt
		&uc_btclick = uc_clickDEC(&uc_btclick, &encryptkey)
	endif
	&uc_btclickparms = &uc_btclick.SplitRegEx(':')
	
	&isok = false
	do case
		
		/* saida do sistema ------------------------------------------------------ */
		case &uc_btclick.IndexOf('NAV:SAIR')>0
			sair()
			
		/* itens do menu --------------------------------------------------------- */
		case &uc_btclickparms.Item(2)='NAV' 
			&isok   = true
			&websession.set('MODULO', &uc_btclickparms.Item(3).Trim())

	endcase

```

Esta procedure deve sempre ser chamada, em todos os WebPanels.
```
Event Bootstrapclick1.Click
	&uc_btclick = Bootstrapclick1.ButtonId
	navEvent2(&uc_btclick, &uc_btclickparms, &url, &isok)
	if &isok
        // chama a pagina home do modulo quando trocado 
		/// GlobalEvents.MPHOME(&uc_btclickparms)
	
    else
    
    /* tratar o evento da interface */
	alerta.Caption =  
		' I:'	+ &uc_btclickparms.Item(uc_btitem.interface)
		+'<br>C:'	+ &uc_btclickparms.Item(uc_btitem.controle)
		+'<br>A:'	+ &uc_btclickparms.Item(uc_btitem.acao)
		+'<br>P:'	+ &uc_btclickparms.Item(uc_btitem.parm1)

    endif
	
endEvent
```

Quando a mesma retorna &isok=true, significa que ocorreu um evento na MASTERPAGE, indicando que o usuário trocou o MÓDULO para outro, exigindo que se altere o SIDEBAR e as opções de programas.

Fazemos a troca da MASTERPAGE por meio de um evento Global.

