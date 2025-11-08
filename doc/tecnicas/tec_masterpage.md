# MasterPage

Este documento trata da construção de uma estratégia de uma única master page que controla todos os módulos do sistema.
O objetivo é que uma única pagina **home** possa ser utilizada como elemento raiz para todos os módulos do sistema, apresentando conteúdo personalizado assim que se abre o módulo.

Modulo é um conceito de agrupamento de programas.

## estrutura
A estrutura da masterpage está sendo apresentada no documento [Estratégias de interface](/doc/tecnicas/tec_estrategiasinterface.md). Neste estaremos apresentando a construção da lógica da masterpage e do home.

![estrutura da tela](/doc/imagens/tec_estruturatela.png)

Precisaremos definir como serão carregados os conteúdos das seções e também o tratamento de eventos necessário para a operacionalização do sistema.

Queremos produzir algo semelhante a imagem a seguir.

![estrutura da tela](/doc/imagens/tec_sidebar.png).

Onde teremos um menu na lateral com os Modulos, em caso de seleção de algum modulo (click) o sidebar deve apresentar os programas associados a este modulo, e uma área central com o conteúdo selecionado no sidebar.

## codigo da masterpage

```
Event Start
	form.HeaderRawHTML = uc_carga()
	
	do 'ui_menu'
	do 'ui_navbar'
	do 'ui_sidebar'
Endevent

// 1
sub 'ui_menu'
	&uc_menuin 	    = navMenuGET(&Pgmname.ToUpper().Trim())
	menu.Caption  	= UC.uc_menu(&uc_menuIN.ToJson())	
endsub

// 2
sub 'ui_navbar'
	&uc_navbarin    = navGET(&Pgmname.ToUpper().Trim())
	navbar.Caption  = UC.uc_navbar(&uc_navbarin.ToJson())
endsub

// 3
sub 'ui_sidebar'
	sidebar.Caption = ''
	&modulo = &websession.get('MODULO')
	if not &modulo.IsEmpty()
		&uc_sidebarIN = sidebarGET(&Pgmname.ToUpper())
		if &uc_sidebarIN.itens.Count>0
			sidebar.Caption = uc.uc_sidebar(&uc_sidebarIN.ToJson())
		endif
	endif
endsub

// 4
Event GlobalEvents.MPHOME(&uc_btclickparms)
	do 'ui_navbar'
	do 'ui_sidebar'
	if &uc_btclickparms.Item(2)='NAV'
		home()
	endif
EndEvent
```
(1) Temos a chamada a um procedimento que cria o menu lateral **navMenuGET**
(2) Temos a chamada ao navbar que cria a imagem na parte superior da interface
(3) Temos a chamada ao procedimento que cria o sidebar, **sidebarGET**, mas somente se existe algum módulo previamente selecionado que se encontra na &websession.
(4) Temos o tratamento de eventos, sendo que neste caso, já aciona a reconstrução do navbar (para se incluir o nome do módulo) e do sidebar para se recriar os itens do sidebar que foram perdidos no refresh. Se o evento foi oriundo de NAV se recarrega a página home, e aqui tem uma pegadinha, porque utilizamos o nome NAV para referir aos objetos do menu.


