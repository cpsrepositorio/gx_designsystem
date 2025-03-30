# navDefault_CLICK

Esta procedure pode ser programada livremente para tratar dos eventos no navegador pelo desenvolvedor.

Temos a seguir um modelo, que programa tres ações principais:
1) Controle de encriptação dos parametros, decriptando caso o mesmo esteja ligado. Observe que utiliza as variáveis de sessão que foram definidas no login do sistema.
2) Quebra das informações do parametro nas partes definidas como Interface, Controle, Evento, Parametro 1, Parametro 2, ...
3) Tratamenteo de eventos que tenham ocorrido da navbar (opcional)

```
 /* 1) controle de encriptação */
 &encrypt  = iif(&websession.Get("SECURITYPARMON")="1", true, false)
 &encryptkey = &websession.Get("SECURITYPARMKEY")
 if &encrypt
  &uc_btclick = uc_clickDEC(&uc_btclick, &encryptkey)
 endif

/* 2) quebra do parametro em partes */
 &uc_btclickparms = &uc_btclick.SplitRegEx(':')

 /* 3) trata os eventos no NAVBAR */
 &modulo = &uc_btclickparms.Item(&uc_btclickparms.Count)
 do case
 case &uc_btclick like '%:NAV:PORTFOLIO%'  
  &websession.set('&modulo', &modulo)
  &url='home_portfolio.aspx'
  case &uc_btclick like '%:NAV:SAIR%'
   sair() 
 endcase
```
