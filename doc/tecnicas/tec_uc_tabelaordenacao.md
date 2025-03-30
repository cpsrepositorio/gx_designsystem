# COLUNAS ORDENADAS
As pessoas estão acostumadas a encontrar as coisas em uma tabela lendo o conteúdo apresentado linha-a-linha, e a ordenação da coluna é importante para facilitar a localização.

[ordenação](uc_tabela_ordenacao.PNG)
A imagem apresenta um simbolo ao lado do titulo, para indicar que a coluna pode ser ordenada.

## Como fazer?
Ordenar as colunas pode ser mais simples, como apresentado aqui neste documento, para um conjunto pequeno de registros, ou muito dificil, caso se tenha que recorrer a leitura ordenada dos registros no banco de dados.

Nesse modelo os dados serão carregados uma única vez, e sobre esses ocorrerá a ordenação.

1) Esta tecnica vai necessitar que os dados sejam carregados em um SDT
2) A operação vai utilizar uma ação Sort('<nome da coluna>') para ordenar
3) Não será necessário recarregar a página
4) Vai necessitar interceptar o evento indicando a coluna a ser ordenada.

## Estrutura do programa
O programa deve ser construido em um webpanel com um Textblock e o [BootstrapClick](recursos/bootstrapclick.md).

A programação será simples.

Em primeiro lugar é necessário proceder a carga dos dados no SDT, que pode ser feito por um Data Provider ou for each... Utilizamos uma sub 'load' para realizar a operação.

```
Event Start
   &order = ''
   do 'load'
EndEvent

sub 'load'
   &sdt = CargaDP()
   do 'ui_grid'
endsub

```
Uma variável texto &order é utilizada para indicar o nome da coluna a ordenar a tabela.

Uma vez carregado o SDT a partir do Start o próximo passo será montar a interface. Uma operação do 'ui_grid' foi inserida para esta finalidade.

A variável &order é fornecida à procedure responsavel pela carga da tabela.

```
sub 'ui_grid'
   &grid = InterfaceGRID(&sdt, &order)
   textblock.caption = '<div>'+uc.uc_tabela(&grid.tojson())+'</div>'
endsub
```
A operação ficara concentrada na procedure que cria o Grid.

## SDT do exemplo

```
sdt{
    colunaA   
    colunaB
    colunaC
    colunaD    
}
```
## CargaDP()
O objeto de carga é comum, apontando para uma tabela e carregando o SDT. A operação de filtro acontece posteriormente.

```
output: collection
sdt
where colunaA...
{
   colunaA = colunaA
   colunaB = colunaB
   colunaC = colunaC

}
```

## Criando a Tabela

A procedure primeiro trata se a ordenação foi informada ou não. Neste caso, se não informada, elege uma ordenação default.

```
    parm(in:&sdt, in:&order, out:&tabela);

    source:

	/* 1) ordenacao da coluna */
	if &order.IsEmpty()
		&order='colunaA'
	endif

	/* 2) ordena o sdt */
	&sdt.Sort(&order.Trim())

    /* 3) cria a tabela */

	&tabela  = new()
	&tabela.interface = &Pgmname
	&tabela.id = 'GRID'
	&tabela.class = 'minimalistBlack'
	&tabela.buttonclass = 'uc_bt uc_btdefault uc_btspace'
	&tabela.pagging  = false
	&tabela.card = false
	&tabela.header.Clear()
	&tabela.lines.Clear()
		
	// header   	
	&tbcab 			= new()
	&tbcab.text 	= 'ColunaA'
	&tbcab.event    = 'ORDER_COLUNAA'
	&tabela.header.Add(&tbcab)
		
	&tbcab 			= new()
	&tbcab.text 	= 'ColunaA'
	&tbcab.event    = 'ORDER_COLUNAA'
	&tabela.header.Add(&tbcab)

	&tbcab 			= new()
	&tbcab.text 	= 'ColunaB'
	&tbcab.event    = 'ORDER_COLUNAB'
	&tabela.header.Add(&tbcab)

	&tbcab 			= new()
	&tbcab.text 	= 'ColunaC'
	&tbcab.event    = 'ORDER_COLUNAC'
	&tabela.header.Add(&tbcab)

	for &item in &sdt
		&tblin = new()		
				
		&tbcel 			= new()
		&tbcel.text 	= &item.colunaA
		&tblin.cells.Add(&tbcel)	

		&tbcel 			= new()
		&tbcel.text 	= &item.colunaB
		&tblin.cells.Add(&tbcel)

		&tbcel 			= new()
		&tbcel.text 	= &item.colunaC
		&tblin.cells.Add(&tbcel)

		&tbcel 			= new()
		&tbcel.text 	= &item.colunaD
		&tblin.cells.Add(&tbcel)	

				
		&tabela.lines.Add(&tblin)

	endfor

```
Observe que nas colunas que se deseja ordenar é incluido um evento: ORDER_COLUNA...

```
	&tbcab 			= new()
	&tbcab.text 	= 'ColunaA'
	&tbcab.event    = 'ORDER_COLUNAA'
	&grid.header.Add(&tbcab)
``` 
## Evento de ordenação

A parte mais simples fica aqui, apenas intercepta o click e em caso ocorra em um cabecalho, chama novamente a criação da tabela passando a ordenação. 

```
Event BootstrapClick1.Click
 	alerta.Caption = ''
  	&uc_btclick = Bootstrapclick1.ButtonId
	navDefault_CLICK(&uc_btclick, &uc_btclickparms, &url)
	if not &url.IsEmpty()
		alerta.Caption = '<script>window.location.assign("'+&url.Trim()+'");</script>'
	endif
	
	/* tratamento dos eventos */
	&uc_interface 	= &uc_btclickparms.Item(uc_btitem.interface).ToUpper().Trim()
	&uc_controle 	= &uc_btclickparms.Item(uc_btitem.controle).ToUpper().Trim()
	&uc_acao 		= &uc_btclickparms.Item(uc_btitem.acao).ToUpper().Trim()
	
	do case
		
		case &uc_acao='ORDER_COLUNAA'
			&order = 'colunaA'
			do 'ui_grid'

		case &uc_acao='ORDER_COLUNAB'
			&order = 'colunaAB'
			do 'ui_grid'

		case &uc_acao='ORDER_COLUNAC'
			&order = 'colunaC'
			do 'ui_grid'

		case &uc_acao='ORDER_COLUNAD'
			&order = 'colunaD'
			do 'ui_grid'
            
	endcase
endevent
```
>[!NOTA]
>Observação importante: nesse modelo o dado fica armazenado no &sdt e não é recarregado o tempo todo do banco de dados. O que se usa é um sort no SDT para gerar a ordenação. Como resultado, temos uma operação muito rápida, porém somente é indicado para um conjunto pequeno de registros.

## Ordenação descrescente

Para obter ordenação decrescente é necessário agregar [ e ] ao nome da coluna.

* sort("colunaA") = ordenação crescente
* sort("[colunaA]")  = ordenação decrescente
