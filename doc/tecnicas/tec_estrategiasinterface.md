# estratégia de interface

Temos três objetos para construir uma interface:

* **Master page** definem o formato e a navegação do sistema como um todo. Este objeto forma um entorno sobre o Webpanel, padronizando e determinando sua identidade visual.
* **Webpanel** ponto de entrada de um programa, sendo a interface do usuário em si, com o conteúdo referente ao processo que resolve.
* **Webcomponent** recurso complementar para a execução de certo programa, que inclui funcionalidades a um webpanel.

Utilizaremos a **Master page** para definir a navegação, com o navbar na parte superior, menu e lista de programas na parte esquerda. 

O **Webpanel** será livre para que o desenvolvedor monte a interface para o usuário. E os **Webcomponents** poderão ser utilizados para complementar a operação dos webpanels.


## estrutura da interface
A estrutura não é muito simples, são diversas Sections estruturadas. A MainTable deve ser do tipo Flex com direction=row.

![padrao](https://raw.githubusercontent.com/cpsrepositorio/gx_designsystem/refs/heads/main/doc/imagens/tec_estrutura.png)

A seguir uma tabela com as Sections e TextBlocks necessários.

| Seção        | Classe seção         | Objeto                     |
|--------------|----------------------|----------------------------|
| secnavbar    | uc_w100              | navbar (*)                 |
| seclinha     | uc_flex-row uc_w100  | secnavegacao, secconteudo  |
| secnavegacao | uc_flex-r uc_mt60    | secmenu, secsidebar        |
| secconteudo  | uc_w100 uc_mt60      | contentplaceholder         |
| secmenu      | uc_flex-c            | menu (*)                   |
| secsidebar   | uc_flex-c            | sidebar (*)                |

(*) Textblock

No objeto contentplaceholder teremos a apresentação do **Webpanel**.

A estrutura na interface Abstract Editor não fica tão clara.
![estrutura da tela](/doc/imagens/tec_estruturatela.png)

## masterpage
A master page deve ser criada com duas linhas (seções), sendo que na primeira deverá ser apresentada a navbar e na segunda uma linha com duas colunas, esquerda para os menus de navegação e direita para conteúdo.

![navbar](/doc/imagens/tec_navbar.png)

A maintable deve ser definida como Flex Layout do tipo Column.

Para que funcio
ne adequadamente, a masterpage deve, além das seções apresentadas,apresentar o navbar e menu padrão.

```
Event Start
	form.HeaderRawHTML = uc_carga()
	
	navbar.Caption		= 'navbar'
	sidebar.Caption	    = ''
	
	do 'ui_navbar'
	do 'ui_menu'
EndEvent

```

E controlar os eventos da interface, que são recebidos de todos os Webpanels que utilizam essa master page.
A programação é apenas orientativa pois não trata otimizações para reduzir o código programado.

```
Event GlobalEvents.MPHOME(&uc_btclickparms)
//	msg(&uc_btclickparms.ToJson())
	do case
		case &uc_btclickparms.Item(2)='MENU'
			&uc_sidebarIN.itens.Clear()
			do case
				case &uc_btclickparms.Item(3)='HOME'
//					do 'ui_sidebarHOME'
				case &uc_btclickparms.Item(3)='FOLLOW'
//					do 'ui_sidebarFOLLOW'
				case &uc_btclickparms.Item(3)='PRODUTO'
//					do 'ui_sidebarPRODUTO'
				case &uc_btclickparms.Item(3)='UNIDADE'
//					do 'ui_sidebarUNIDADE'
				case &uc_btclickparms.Item(3)='HISTORICO'
					do 'ui_sidebarHISTORICO'
			endcase
		
		case &uc_btclickparms.Item(2)='SIDEBAR'
			do case
				case &uc_btclickparms.Item(3)='MAPEAMENTO'
					msg('ABRIR MAPEAMENTO')
				case &uc_btclickparms.Item(3)='DEFINIR'
					msg('ABRIR DEFINIR')
			endcase
	endcase
EndEvent
```

### navbar
Contém a identificação da instituição, sistema e botões.

A seguir um exemplo, que inclui o logotipo da empresa, botão na direita para o usuário sair do sistema.

Em caso de interesse em colocar os itens do menu na barra superiora, um trecho do código está comentado que realiza exatamente esta operação: navModulo(&uc_navbarin)

```
sub 'ui_navbar'
	
	&logocps		= '<img src="'+cps.Link()+'">'
	&logoestado	= '<img src="'+governo.Link()+'" style="height:36px; width:auto;">'
	
	&uc_navbarin.id 		= 'NAV'
	&uc_navbarin.programa	= &Pgmname.ToUpper()
	&uc_navbarin.classe     = 'uc_nav uc_nav_fixedtop uc_navwhite'
	&uc_navbarin.logolink   = 'https://cps.sp.gov.br'
	&uc_navbarin.logo		= &logocps
	&uc_navbarin.brand		= '<STRONG class="uc_ml5">sistema</STRONG>'
	&uc_navbarin.itens.Clear()
	&uc_navbarin.rights.Clear()
	
//	/* menu de modulos */
//	navModulo(&uc_navbarin)
	
	/* botoes à direita */	
	&uc_botaoin.interface 	= &Pgmname.ToUpper()
	&uc_botaoin.id 		= "NAV"
	&uc_botaoin.botoes.Clear()
	
	&botaoitem.cor 		= 'uc_btblueoutlineclear'
	&botaoitem.titulo 		= 'Sair'
	&botaoitem.evento 		= "SAIR"
	&botaoitem.icone	 	= '<i class="fas fa-sign-out-alt"></i>&nbsp;'
	&botaoitem.tooltip  	= 'Sair do sistema'
	&botaoitem.outline   	= true
	&uc_botaoin.botoes.Add(&botaoitem)
	
	&right = new()
	&right.titulo = '<div class="uc_mr10">'+UC.uc_botao(&uc_botaoin.ToJson())+'</div>'
	&uc_navbarin.rights.Add(&right)
	
	navbar.Caption  = UC.uc_navbar(&uc_navbarin.ToJson())
endsub
```

### menu
Deve apresentar os módulos que a pessoa possui acesso.

![menu](/doc/imagens/tec_menu.png "")

O exemplo é apenas orientativo, uma vez que os itens devem ser definidos com base em analise de segurança e privilégio do usuário.

```
sub 'ui_menu'
	&uc_menuin.id			= 'MASTERMENU'
	&uc_menuin.interface	= &Pgmname.ToUpper()
	&uc_menuin.classe 		= 'uc_menu-v uc_menu-vl uc_menu-v-mp'
	&uc_menuin.itens.Clear()

	&menuitem = new()
	&menuitem.evento = &Pgmname.Trim()+':MENU:HOME'
	&menuitem.icone  = '<i class="fas fa-house-damage uc_pointer"></i>'
	&menuitem.titulo = 'home'
	&uc_menuin.itens.Add(&menuitem)

	&menuitem = new()
	&menuitem.evento = &Pgmname.Trim()+':MENU:FOLLOW'
	&menuitem.icone  = '<i class="fas fa-running uc_pointer"></i>'
	&menuitem.titulo = 'follow-up'
	&uc_menuin.itens.Add(&menuitem)

	&menuitem = new()
	&menuitem.evento = &Pgmname.Trim()+':MENU:PRODUTO'
	&menuitem.icone  = '<i class="fab fa-windows uc_pointer"></i>'
	&menuitem.titulo = 'produto'
	&uc_menuin.itens.Add(&menuitem)

	&menuitem = new()
	&menuitem.evento = &Pgmname.Trim()+':MENU:UNIDADE'
	&menuitem.icone  = '<i class="fas fa-school uc_pointer"></i>'
	&menuitem.titulo = 'unidade'
	&uc_menuin.itens.Add(&menuitem)

	&menuitem = new()
	&menuitem.evento = &Pgmname.Trim()+':MENU:HISTORICO'
	&menuitem.icone  = '<i class="fas fa-history uc_pointer"></i>'
	&menuitem.titulo = 'histórico'
	&uc_menuin.itens.Add(&menuitem)

	menu.Caption  = UC.uc_menu(&uc_menuIN.ToJson())	
endsub
```

### sidebar
Deve apresentar os programas associados ao módulo selecionado pelo usuário.

![sidebar](/doc/imagens/tec_sidebar.png)

A seguir um exemplo.

```

sub 'ui_sidebarHISTORICO'
	
	&uc_sidebarin.id = 'SIDEBAR'
	&uc_sidebarin.programa = &Pgmname.ToUpper()
	&uc_sidebarin.classe = 'uc_sidebar uc_sidebarwhite uc_pt10'
	
	&sidebaritem = new()
	&sidebaritem.titulo	= 'Mapeamento'
	&sidebaritem.evento	= 'MAPEAMENTO'
	&sidebaritem.icone 	= '<i class="far fa-map"></i>'
	&uc_sidebarIN.itens.Add(&sidebaritem)
	
	&sidebaritem = new()
	&sidebaritem.titulo	= 'Incluir'
	&sidebaritem.evento	= 'DEFINIR'
	&sidebaritem.icone 	= '<i class="fas fa-plus-square"></i>'
	&uc_sidebarIN.itens.Add(&sidebaritem)
	
	sidebar.Caption	= UC.uc_sidebar(&uc_sidebarIN.ToJson())
endsub
```

### conteúdo
Apresenta o resultado do programa selecionado no sidebar, em um controle ContentPlaceHolder do Genexus.
Toda interface deve ser construída associando a master page HOME.

```
```

## home
O painel home é o que abre o sistema após o login e o redirecionamento do usuário.
É um webpanel completo e poderá ser utilizado para multiplas funcionalidades, como apresentar conteúdos específicos do modulo selecionado. Sendo que o conceito de módulo se refere ao item do menu selecionado.

```
Event Start
	form.HeaderRawHTML = uc_carga()
	form.Meta.AddItem("viewport", "width=device-width,initial-scale=1")
	grid.Caption = ''
Endevent

/* tratamento dos eventos no navbar */
Event BootstrapClick1.Click	
   	&uc_btclick = Bootstrapclick1.ButtonId
	navEvent(&uc_btclick,&uc_btclickparms, &url, &isok)
	if &isok and not &url.IsEmpty()
		grid.Caption = '<script>'+&url.Trim()+'</script>'
	endif
	
	GlobalEvents.MPHOME(&uc_btclickparms)
Endevent

```
Para funcionar adequadamente, o programa deverá incluir uma ação de evento Global a ser interceptada no objeto MasterPage. **GlobalEvents.MPHOME(&uc_btclickparms)**


Este programa encontra-se na kb do CEETEPS_DESIGNSYSTEM18, e se chama home.aspx.
