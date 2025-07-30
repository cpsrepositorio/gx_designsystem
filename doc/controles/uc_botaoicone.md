# uc_botaoicone
Os botões do tipo icone são elementos em HTML criados a partir do controle **uc.uc_botaoicone(&uc_botaoiconeIN.ToJson())**, que constroem uma barra de icones, permitindo que as classes que definem o formato do botão sejam definidas.
O processo de criação da barra de botões é simplificado, pois segue o conceito de que os eventos foram definidos de forma padrão, e para cada tipo de evento, um icone, também padrão, é associado. Portanto, a unica coisa que precisa ser fornecida para o controle é um array de eventos.

A estrutura possui um cabeçalho simples (id e interface) e uma coleção de botões do tipo uc_botaoIN.botao, que formarão a barra de botões do controle.
É possível criar dois tipos de variáveis a partir deste tipo: uc_botaoIN e uc_botaoIN.botao, e nestas definir o comportamento e o formato dos botões. Vamos testar. A primeira cria uma barra e a segunda um botão nesta barra.
1.	Criar um webpanel, com o nome de ex_botao
2.	Criar duas variáveis do tipo **uc_botaoiconeIN**.
3.	Adicione na interface um textblock, alterando a propriedade ControlName e Caption para a palavra **html** e Format para **HTML**
4.	Crie um evento Start
5.	Inclua os arquivos de estilo, com a programação de **form.HeaderRawHTML = UC.uc_cssGET_bot523()**
6.	E a definição da barra e do botão, conforme o exemplo abaixo:	

```Genexus
Event Start
	/* 1 */
	form.HeaderRawHTML = UC.uc_cssGET_bot523()

	/* 2 */
	do 'iconebar'
	
  /* 3 */
	html.Caption = UC.uc_botaoicone(&uc_botaoiconeIN.ToJson())
Endevent

sub 'iconebar'
	&uc_botaoiconeIN.id 			    = 'id'
	&uc_botaoiconeIN.interface 		= 'interface'	
	&uc_botaoiconeIN.classebar 		= 'uc_flex-r uc_flex-nowrap'
	&uc_botaoiconeIN.classebotao  = 'uc_btspace'
	&uc_botaoiconeIN.classeicon   = 'uc_bticon'
	
	&botoes.add('[ABRIR:1]')
	&botoes.add('[EDITAR:1]')
	&botoes.add('[APAGAR:1]')
	&uc_botaoiconeIN.botoes = &botoes.ToJson()
endsub
```

A variável &botoes é uma varchar(40) do tipo collection. Observe que ao se carregar no SDT &uc_botaoiconeIN.botoes a mesma é convertida para Json, &botoes.ToJson()
Fique atento aos eventos, pois o controle segue de forma rígida as palavras previamente programadas e para cada palavra, se tem um icone e tooltip associado.
O controle é preparado para montar uma barra de botões, para isso adicione vários eventos na variável &botoes. Se desejar apenas um único botão, execute o &botoes.add, apenas uma vez.

