# uc_listapaginada
A lista paginada é um controle tipo lista que apresenta páginas de registros ao invés da carga completa da tabela,  cabendo ao usuário a ação de solicitar a próxima página ou a anterior que deseja ser carregada.

O controle é bastante simples, porém necessita de recursos adicionais para a carga dos registros.

## Data provider
O controle precisa de um **DataProvider** que faça a carga dos registros de forma paginada, de forma que ocor
Para simplificar, utilize um SDT que possa ser carregado por etapas.

```
cargaSDT [count=&pgsize][skip=(&pg-1)*&pgsize]
order Id
where Id =&id when &id<>0
{
	Id			
	Nome		
	Foto		
	Endereco	
	Cidade
}

```
O **count=&pgsize** determina o total de registros a ser retornado, e **skip=(&pg-1)*&pgsize** calcula o primeiro registro da lista em função da pagina a ser carrega.

```
sub 'load'
	&registros.Clear()
 	&registros = cargaDP(&id, &pgsize, &pg)
	do 'grid'
endsub
```
A chamada ao **cargaDP** retorna os registros da página carregada.

## Montagem da lista
A lista de registros é carregada para o controle **uc_listapaginada**.

```
sub 'grid'
	/* botão INS */
	&uc_botaoiconein.id			= 'LISTA'
	&uc_botaoiconein.interface	= &Pgmname.ToUpper()
	&botoes.Clear()
	&botoes.Add("NOVO:")
	&uc_botaoiconein.botoes = &botoes.ToJson()

	/* lista de registros */
	&uc_listin.id 						= 'LISTA'
	&uc_listin.interface 				= &Pgmname.ToUpper()
	&uc_listin.pagging 					= true
	&uc_listin.paggingcolor 			= 'uc_btblueoutlineclear'
	&uc_listin.paggingposition 			= uc_position.bottom
	&uc_listIN.paggingpgsize			= &pgsize
	&uc_listIN.paggingpg				= &pg
	&uc_listIN.paggingtrec				= count(nome)
	&uc_listin.toolbox 		 			= UC.uc_botaoicone(&uc_botaoiconein.ToJson())
	&uc_listin.classetoolbox 			= 'uc_flex-r uc_flex-jce uc_mb10'

	/* carga dos registros da lista */
	&uc_listin.itens.Clear()
	for &reg in &registros

		&uc_botaoiconein 				= new()
		&uc_botaoiconein.id				= 'LISTA'
		&uc_botaoiconein.interface		= &Pgmname.ToUpper()
		&uc_botaoiconein.classebar 		= 'uc_flex-r uc_flex-nowrap'
		&uc_botaoiconein.classebotao  	= 'uc_btspace uc_bt-icon uc_pointer'
		&uc_botaoiconein.classeicon   	= ''
		&botoes.Clear()
		&botoes.Add("EDITAR:")
		&botoes.Add("APAGAR:")
		&uc_botaoiconein.botoes = &botoes.ToJson()
		
		&item = new()
		&item.titulo 					= &reg.Nome.ToUpper().Trim()
		&item.tooltip					= &reg.Nome.ToUpper().Trim()
		&item.evento					= 'ABRIR:'+&reg.Id.ToString().Trim()
		&item.imagem.classe 			= 'uc_imagemredonda15px'
		&item.imagem.image				= &reg.Foto.Trim()
		&item.imagem.tooltip 			= &reg.Nome.ToUpper().Trim()
		&item.toolbox 					= UC.uc_botaoicone(&uc_botaoiconein.ToJson())
		&uc_listin.itens.Add(&item)

	endfor
	html.Caption = UC.uc_listapaginada(&uc_listin.ToJson())
endsub
```





* **TRec** = total de registros
* **PGSize** = total de registros por pagina, por exemplo, 20 significa que serão apresentados 20 em 20 
* **PG** = página atualmente carregada na interface

que simplifica completamente a operação de paginação, ficando a cargo da mesma



















O controle **uc.uc_lista** permite criar uma lista de itens em linhas, e na formatação do pacote, é semelhante a uma tabela com uma única coluna.

É util para apresentação de conjuntos de informações, como por exemplo:

* apresentar uma lista de registros
* substituir tabelas mais simples que tenham um texto e botões

## Lista simples

Numa lista simples, o que se precisa definir basicamente as propriedades na variável **&uc_listin**, incluindo o id, interface, classes. E em seguida um laço (for) para definir os registros a serem apresentados

```
	&uc_listin.interface      = &Pgmname
	&uc_listin.id			 = 'LISTA'
	&uc_listin.classe 		 = 'uc_lista'
	&uc_listin.classeitem 	 = 'uc_listaitem'
	
	for &i = 1 to 3
		&item = new()
		&item.titulo 	= 'Titulo '+&i.ToString().Trim()
		&item.tooltip	= 'Tooltip do registro '+&i.ToString().Trim()
		&item.icone		= '<i class="fas fa-user-graduate"></i>'
		&uc_listin.itens.Add(&item)
	endfor

	html.Caption = UC.uc_lista(&uc_listin.ToJson())
```

## Lista com toolbar
Outra possibilidade é incluir na parte superior, em uma área chamada toolbar uma barra de botões, titulos, ou outras coisas de seu interesse.

No exemplo abaixo inserimos em um **&uc_botaoin** um botão para significar a opção do usuário inserir um NOVO registro e o colocamos na propriedade **&uc_listin.toolbox**.

```
sub 'listatoolbar'
	do 'toolbar'
	&uc_listin = new()
	&uc_listin.interface      = &Pgmname
	&uc_listin.id			 = 'LISTA'
	&uc_listin.classe 		 = 'uc_lista'
	&uc_listin.classeitem 	 = 'uc_listaitem'
	&uc_listin.toolbox 		 = UC.uc_botao(&uc_botaoin.ToJson())
	&uc_listin.classetoolbox = 'uc_flex-r uc_flex-jce uc_mb10'
	
	for &i = 1 to 3
		&item = new()
		&item.titulo 	= 'Titulo '+&i.ToString().Trim()
		&item.evento 	= 'SELECIONAR:'+&i.ToString().Trim()
		&item.tooltip	= 'Tooltip do registro '+&i.ToString().Trim()
		&item.icone		= '<i class="fas fa-user-graduate"></i>'
		&uc_listin.itens.Add(&item)
	endfor
	
	html.Caption += '<h5 class="uc_mt40">Toolbar</h5>'
	html.Caption += UC.uc_lista(&uc_listin.ToJson())
endsub

sub 'toolbar'
	&uc_botaoin.interface	= &Pgmname
	&uc_botaoin.id			= 'TOOLBAR'	
	&botao = new()
	&botao.titulo 		= 'novo'
	&botao.evento 		= "NOVO:param0"
	&botao.icone 		= '<i class="fas fa-plus"></i>'
	&botao.tooltip  	= 'Criar novo item na lista'
	&uc_botaoin.botoes.Add(&botao)
endsub	
```
Observe que é possível posicionar o conteúdo desta linha com a propriedade **&uc_listin.classetoolbox**, que nesse exemplo, utilizamos o flex-layout para posicionar o botão à direita **uc_flex-r uc_flex-jce uc_mb10**.

Inicialmente os registros na lista não são 'clicáveis', mas ao se adicionar uma propriedade evento, como por exemplo, **&item.evento = 'SELECIONAR:'+&i.ToString().Trim()**, a linha passa a responder a cliques, assim o exemplo ficou um pouco mais completo, incluindo a operação NOVO e SELECIONAR.

## Lista com botões
Um terceiro uso deste controle é a inclusão de um toolbox diretamente na linha do registro. Nesse caso uma propriedade **&item.toolbox = UC.uc_botao(&uc_botaoin.ToJson())** deverá receber a barra de botões.

Não se esqueça de desligar a propriedade **&item.evento = ''** senão vai sobrepor os eventos dos botões.

```
sub 'listabotoes'
	&uc_listin = new()
	
	&uc_botaoin 			= new()
	&uc_botaoin.interface	= &Pgmname
	&uc_botaoin.id			= 'TOOLBAR'
	&botao = new()
	&botao.classe			='uc_bt-icon'
	&botao.evento 		= "NOVO:param0"
	&botao.icone 		= '<i class="fas fa-plus"></i>'
	&botao.tooltip  	= 'Criar novo item na lista'
	&uc_botaoin.botoes.Add(&botao)
	
	&uc_listin.interface      = &Pgmname
	&uc_listin.id			 = 'LISTA'
	&uc_listin.classe 		 = 'uc_lista'
	&uc_listin.classeitem 	 = 'uc_listaitem'
	&uc_listin.toolbox 		 = UC.uc_botao(&uc_botaoin.ToJson())
	&uc_listin.classetoolbox = 'uc_flex-r uc_flex-jce uc_mb10'
	
	for &i = 1 to 3

    	/* botoes nos registros */
		&uc_botaoin = new()
		&uc_botaoin.interface	= &Pgmname
		&uc_botaoin.id			= 'TOOLBAR'
		
		&botao = new()
		&botao.classe			='uc_bt-icon'
		&botao.evento 			= "EDITAR:"+&i.ToString().Trim()
		&botao.icone 			= '<i class="fas fa-pen"></i>'
		&botao.tooltip  		= 'Criar novo item na lista'
		&uc_botaoin.botoes.Add(&botao)
		
		&botao = new()
		&botao.classe			='uc_bt-icon'
		&botao.evento 			= "APAGAR:"+&i.ToString().Trim()
		&botao.icone 			= '<i class="fas fa-trash"></i>'
		&botao.tooltip  		= 'Criar novo item na lista'
		&uc_botaoin.botoes.Add(&botao)
		
		/* registro */
		&item = new()
		&item.titulo 	= 'Titulo '+&i.ToString().Trim()
		&item.tooltip	= 'Tooltip do registro '+&i.ToString().Trim()
		&item.icone	= '<i class="fas fa-user-graduate"></i>'
		&item.toolbox 	= UC.uc_botao(&uc_botaoin.ToJson())
		&uc_listin.itens.Add(&item)
	endfor
	
	html.Caption += UC.uc_lista(&uc_listin.ToJson())
endsub
```

A barra de botões de EDITAR e APAGAR nas linhas pode ser substituida por algo mais simples, como 
```
		&uc_botaoiconein.id 			= 'LISTA'
		&uc_botaoiconein.interface 		= &Pgmname	
		&uc_botaoiconein.classebar 		= 'uc_flex-r uc_flex-nowrap uc_mt30'
		&uc_botaoiconein.classebotao  	= 'uc_btspace uc_bt-icon uc_pointer'
		&uc_botaoiconein.classeicon   	= ''
		&botoes.add('EDITAR:'+&i.ToString().Trim())
		&botoes.add('APAGAR:'+&i.ToString().Trim())
		&uc_botaoiconein.botoes = &botoes.ToJson()

		&item = new()
		&item.titulo 	= 'Titulo '+&i.ToString().Trim()
		&item.tooltip	= 'Tooltip do registro '+&i.ToString().Trim()
		&item.icone	= '<i class="fas fa-user-graduate"></i>'
		&item.toolbox 	= UC.uc_botaoicone(&uc_botaoiconein.ToJson())
		&uc_listin.itens.Add(&item)
```
