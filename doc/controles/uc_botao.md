# uc_botao
É um controle que apresenta um formato e comportamento que leva o usuário a interpretar que se trata de uma ação a ser executada pelo sistema.

## Botão simples
Um botão simples pode ser obtido pela definição das classes Titulo, Icone, Evento. Sem o fornecimento de nenhuma classe ele adotará a classe uc_btn.

```
	&uc_botaoin.id 		= 'id'
	&uc_botaoin.interface 	= 'interface'	

	&botao = new()
	&botao.evento = 'ABRIR:1'
	&botao.icone = '<i class="fas fa-eye"></i>'
	&botao.titulo = 'Abrir'
	&botao.tooltip = 'Abrir o registro'
	&uc_botaoin.botoes.Add(&botao)
	
	grid.Caption = UC.uc_botao(&uc_botaoin.ToJson())
```

## Botão colorido
Os botões podem também ser coloridos.

```
	&uc_botaoin.id 		= 'id'
	&uc_botaoin.interface 	= 'interface'	

	&botao = new()
	&botao.evento = 'ABRIR:0'
	&botao.classe = 'uc_white'
	&botao.titulo = 'White'
	&botao.tooltip = 'Abrir o registro'
	&uc_botaoin.botoes.Add(&botao)

	&botao = new()
	&botao.evento = 'ABRIR:1'
	&botao.classe = 'uc_green'
	&botao.titulo = 'Green'
	&botao.tooltip = 'Abrir o registro'
	&uc_botaoin.botoes.Add(&botao)
	
	&botao = new()
	&botao.evento = 'ABRIR:2'
	&botao.classe = 'uc_red'
	&botao.titulo = 'Red'
	&botao.tooltip = 'Abrir o registro'
	&uc_botaoin.botoes.Add(&botao)
	
	&botao = new()
	&botao.evento = 'ABRIR:3'
	&botao.classe = 'uc_blue'
	&botao.titulo = 'Blue'
	&botao.tooltip = 'Abrir o registro'
	&uc_botaoin.botoes.Add(&botao)
	
	&botao = new()
	&botao.evento = 'ABRIR:4'
	&botao.classe = 'uc_orange'
	&botao.titulo = 'Orange'
	&botao.tooltip = 'Abrir o registro'
	&uc_botaoin.botoes.Add(&botao)
	
	&botao = new()
	&botao.evento = 'ABRIR:5'
	&botao.classe = 'uc_gray'
	&botao.titulo = 'Gray'
	&botao.tooltip = 'Abrir o registro'
	&uc_botaoin.botoes.Add(&botao)
	
	&botao = new()
	&botao.evento = 'ABRIR:6'
	&botao.classe = 'uc_black'
	&botao.titulo = 'Black'
	&botao.tooltip = 'Abrir o registro'
	&uc_botaoin.botoes.Add(&botao)
	
	grid.Caption = UC.uc_botao(&uc_botaoin.ToJson())
```

## Icones
O controle permite que se crie botões que sejam simples e apenas representados por um ícone.  
```
	&uc_botaoin.id 		= 'id'
	&uc_botaoin.interface 	= 'interface'	

	&botao = new()
	&botao.classe = 'uc_bt-icon'
	&botao.evento = 'ABRIR:7'
	&botao.icone = '<i class="fas fa-paperclip"></i>'
	&uc_botaoin.botoes.Add(&botao)
	
	&botao = new()
	&botao.classe = 'uc_bt-icon'
	&botao.evento = 'EDITAR:1'
	&botao.icone = '<i class="fas fa-pen"></i>'
	&uc_botaoin.botoes.Add(&botao)
	
	&botao = new()
	&botao.classe = 'uc_bt-icon'
	&botao.evento = 'APAGAR:1'
	&botao.icone = '<i class="fas fa-trash"></i>'
	&uc_botaoin.botoes.Add(&botao)

	grid.Caption = UC.uc_botao(&uc_botaoin.ToJson())
```
Temos uma forma mais simples de fazer isso com o controle [uc_botaoicone](/doc/controles/uc_botaoicone.md)

## Links
O controle permite que links tenham o mesmo formato de um botão tradicional, inclusive, com o linktarget indicando onde o navegador deverá executar a ação.

```
	&uc_botaoin.id 		= 'id'
	&uc_botaoin.interface 	= 'interface'	

	&botao = new()
	&botao.icone = '<i class="fas fa-eye"></i>'
 	&botao.link = 'https://google.com'
	&botao.linktarget = '_blank'
	&botao.titulo = 'Google'
	&botao.tooltip = 'Abrir o registro'
	&uc_botaoin.botoes.Add(&botao)

	grid.Caption = UC.uc_botao(&uc_botaoin.ToJson())
```

## Eventos
O controle de eventos é o mesmo que nos demais controles, com a criação da string com Interface:Controle:Acao:Parametro.

Para maiores informações a respeito desta operação veja [Eventos](/eventos.md)


## Classes
Os botões são definidos nas classes do arquivo **uc_button.css**

