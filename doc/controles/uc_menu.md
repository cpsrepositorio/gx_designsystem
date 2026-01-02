# uc_menu
Um menu consiste em uma barra com opções posicionadas na horizontal, normalmente contendo uma imagem e um texto que representam uma certa ação de interesse do usuário. Pressupõe-se que ao clicar sobre a imagem ou texto, o menu causará o efeito de abrir alguma coisa.

O **uc_menu** permite construir menus na horizontal ou vertical.

## uc_menuin
Um objeto **uc_menuin** deve ser utilizado para adicionar itens ao menu. Caso necessite de mais de um menu ao mesmo tempo na mesma interface, utilize um segundo **uc_menuin**.

Para incluir uma lista de itens no menu, uma segunda variável será necessária, do tipo **uc_menuin.item**, e uma ação **uc_menuin.itens.add(&menuitem)** para inserir. 


### Exemplo:
A seguir um exemplo de um menu horizontal.
```
sub 'menu'
 &uc_menuin.id 			= 'MENU'
 &uc_menuin.interface 	= 'interface'
 &uc_menuin.classe       = 'uc_menu-h uc_menu-hc'
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

|var|tipo|
|-----------------|---------------------------|
|&menuitem | uc_menuin.item|
|&uc_menuin | uc_menuin |


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

