# uc_menuapp | uc_appmenu
Um controle do tipo **uc_menuapp** ou **uc_appmenu**, é um modelo de menu baseado em cards com certas caracteristicas como uma imagem ou icone à esquerda, titulo, subtitulo e uma toolbox com botões, para abrir o registro, por exemplo.

Pode ser apresentado 

## uc_menuin
Um controle **uc_menuapp** utiliza o mesmo SDT **uc_menuin** para adicionar itens ao menu.
Para incluir uma lista de itens no menu, uma segunda variável será necessária, do tipo **uc_menuin.item**, e uma ação **uc_menuin.itens.add(&menuitem)** para inserir. 


### Exemplo:
A seguir um exemplo de um menu horizontal.

```
sub 'menu'
	
	&uc_menuin.classe = 'uc_menu-h uc_menu-hc'
	&uc_menuin.itens.Clear()

	&menuitem = new()
	&menuitem.evento = &Pgmname.Trim()+':MENU:HOME:1'
	&menuitem.icone  = '<i class="fas fa-house-damage uc_pointer"></i>'
	&menuitem.titulo = 'relatorio'
	&uc_menuin.itens.Add(&menuitem)

	&menuitem = new()
	&menuitem.evento = &Pgmname.Trim()+':MENU:FOLLOW:1'
	&menuitem.icone  = '<i class="fas fa-running uc_pointer"></i>'
	&menuitem.titulo = 'follow-up'
	&uc_menuin.itens.Add(&menuitem)

	&menuitem = new()
	&menuitem.evento = &Pgmname.Trim()+':MENU:PRODUTO:1'
	&menuitem.icone  = '<i class="fab fa-windows uc_pointer"></i>'
	&menuitem.titulo = 'produto'
	&uc_menuin.itens.Add(&menuitem)

	&menuitem = new()
	&menuitem.evento = &Pgmname.Trim()+':MENU:CVE:1'
	&menuitem.icone  = '<i class="fas fa-shield-alt uc_pointer"></i>'
	&menuitem.titulo = 'cve'
	&uc_menuin.itens.Add(&menuitem)

	&menuitem = new()
	&menuitem.evento = &Pgmname.Trim()+':MENU:UNIDADE:1'
	&menuitem.icone  = '<i class="fas fa-school uc_pointer"></i>'
	&menuitem.titulo = 'unidade'
	&uc_menuin.itens.Add(&menuitem)

	&menuitem = new()
	&menuitem.evento = &Pgmname.Trim()+':MENU:IP:1'
	&menuitem.icone  = '<i class="fas fa-network-wired uc_pointer"></i>'
	&menuitem.titulo = 'ip'
	&uc_menuin.itens.Add(&menuitem)

	html.Caption  = UC.uc_menu(&uc_menuIN.ToJson())
endsub
```

A linha **html.Caption  = UC.uc_menu(&uc_menuIN.ToJson())**, inclui o menu num textblock na interface.


### Estilo
O estilo do menu é definido no arquivo **uc_menu.css**, que contém uma série de classes que permitem configurar o objeto.

A seguir apresentamos uma pequena explicação dessas classes:

| classe   | significado        |
|----------|--------------------|
|uc_menu-h | menu horizontal    |
|uc_menu-hl| alinhado a esquerda|
|uc_menu-hc| alinhado ao centro |
|uc_menu-hr| alinhado a direita |
|uc_menu-v | menu vertical      |
|uc_menu-vl| alinhado a esquerda|
|uc_menu-vc| alinhado ao centro |
|uc_menu-vr| alinhado a direita |

