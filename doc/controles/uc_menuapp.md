# uc_menuapp | uc_appmenu
Um controle do tipo **uc_menuapp** ou **uc_appmenu**, apresenta um menu em estilo cards, com um titulo, subtitulo e toolbox com botões.

## uc_menuin
Um controle **uc_menuapp** utiliza o mesmo SDT **uc_menuin** para adicionar itens ao menu.
Para incluir uma lista de itens no menu, uma segunda variável será necessária, do tipo **uc_menuin.item**, e uma ação **uc_menuin.itens.add(&menuitem)** para inserir. 


### Exemplo:
A seguir um exemplo de um menu horizontal.

```
	&uc_menuIN.id = 'MENU'
	&uc_menuIN.interface = &Pgmname.Trim()
	&uc_menuIN.classe = 'uc_mt30'
	&uc_menuIN.itens.Clear()
	&uc_menuIN.toolbarclass = 'uc_flex-c'
	
	&uc_botaoiconeIN.id 			= 'id'
	&uc_botaoiconeIN.interface 		= 'interface'	
	&uc_botaoiconeIN.classebar 		= 'uc_flex-r uc_flex-nowrap'
	&uc_botaoiconeIN.classebotao  	= 'uc_btspace uc_appmenu-toolbar-icon'
	&uc_botaoiconeIN.classeicon   	= 'uc_bticon'
	&botoes.add('PLAY:1')
	&botoes.add('INFO:1')
	&uc_botaoiconeIN.botoes = &botoes.ToJson()
	
	&item = new()
	&item.evento = ''//ABRIR:1'
	&item.icone = '<i class="fas fa-user-cog"></i>'
	&item.titulo = 'Configuração'
	&item.subtitulo = 'infraestrutura'
	&item.toolbar = UC.uc_botaoicone(&uc_botaoiconeIN.ToJson())
	&uc_menuIN.itens.Add(&item)
	
	&item = new()
	&item.evento = 'ABRIR:1'
	&item.icone = '<i class="fas fa-copy"></i>'
	&item.titulo = 'Projeto Um'
	&item.subtitulo = 'academico'
	&uc_menuIN.itens.Add(&item)
		
	&item = new()
	&item.evento = 'ABRIR:1'
	&item.icone = '<i class="fas fa-eye"></i>'
	&item.titulo = 'Projeto Principal'
	&item.subtitulo = 'academico'
	&uc_menuIN.itens.Add(&item)

	grid.Caption  = '<div>'+UC.uc_appmenu(&uc_menuIN.ToJson()) + '</div>'
```
Observe que quando **&item.evento** é definido passa a gerar o evento de todo card, independente se houver algum botão na toolbox.

