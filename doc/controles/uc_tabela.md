# uc_tabela

O controle **uc_tabela** possibilita organizar os dados de forma estruturada por meio de linhas e colunas.

Cada linha representa um certo registro e as colunas as propriedades que se deseja exibir, deste mesmo registro.

A tabela é um controle um pouco mais complexo, uma vez que exige a definição de um cabeçalho, com propriedades e em seguida adiconar as células de cada linha.

## Header
O cabeçalho é inserido em uma coleção, do tipo **uc_tabelain.cell**, no exemplo a seguir, a variavel **&tabhead** é desse tipo. Observe que cada coluna da tabela pode conter um **width** para determinar sua largura.

```
&uc_tabelain.header.Clear()
		
&tabhead = new()
&tabhead.text  = 'Titulo'
&tabhead.width = '50%'
&uc_tabelain.header.Add(&tabhead)
	
&tabhead = new()
&tabhead.text  = 'Conteudo'
&tabhead.width = '40%'
&uc_tabelain.header.Add(&tabhead)

&tabhead = new()
&tabhead.text  = ''
&tabhead.width = '10%'
&uc_tabelain.header.Add(&tabhead)
```
As linhas normalmente são extraidas de uma tabela, portanto, um **for each** ou **for in** deve ser programado para percorrer a coleção.

## Lines
```
&uc_tabelaIN.lines.Clear()
for &i = 1 to 10
	
	&tablin = new()
	
	&tabcel = new()
	&tabcel.text = 'Titulo'+&i.ToString()
	&tablin.cells.Add(&tabcel)
	
	&tabcel = new()
	&tabcel.text = 'Conteudo'+&i.ToString()
	&tablin.cells.Add(&tabcel)
	
	&uc_botaoiconein.id 			= 'id'
	&uc_botaoiconein.interface 		= 'interface'	
	&uc_botaoiconein.classebar 		= 'uc_flex-r uc_flex-nowrap'
	&uc_botaoiconein.classebotao  	= 'uc_btspace uc_bt-icon uc_pointer'
	&uc_botaoiconein.classeicon   	= ''
   	&botoes.Clear()
	&botoes.add('ABRIR:'+&i.ToString())
	&uc_botaoiconein.botoes = &botoes.ToJson()
	
	&tabcel = new()
	&tabcel.text = UC.uc_botaoicone(&uc_botaoiconein.ToJson())
	&tablin.cells.Add(&tabcel)
	
	&uc_tabelain.lines.Add(&tablin)
	
endfor
```
O codigo inclui uma barra de botões em cada registro.

## Cores
A cor da tabela é definida na classe **&uc_tabelain.class = 'minimalistBlack'**, sendo que temos duas cores minimalistBlack e minimalistGray.

```
sub 'matriz'
	&uc_tabelain.id 		= 'TABELA'
	&uc_tabelain.interface 	= &Pgmname.ToUpper()
	&uc_tabelain.class = 'minimalistBlack'
	
	&uc_tabelain.header.Clear()
	&uc_tabelain.lines.Clear()
	&uc_tabelain.footer.Clear()
			
	&tabhead = new()
	&tabhead.text  = 'Matriz'
	&tabhead.width = '80%'
	&uc_tabelain.header.Add(&tabhead)

	&tabhead = new()
	&tabhead.text  = 'Status'
	&tabhead.width = '10%'
	&uc_tabelain.header.Add(&tabhead)

	&tabhead = new()
	&tabhead.text  = ''
	&tabhead.width = '10%'
	&uc_tabelain.header.Add(&tabhead)
	
	for each

		&tablin = new()
		
		&tabcel = new()
		&tabcel.text = 'titulo'
		&tablin.cells.Add(&tabcel)
		
		&uc_botaoiconein.id 			= 'id'
		&uc_botaoiconein.interface 		= 'interface'	
		&uc_botaoiconein.classebar 		= 'uc_flex-r uc_flex-nowrap'
		&uc_botaoiconein.classebotao  	= 'uc_btspace uc_bt-icon uc_pointer'
		&uc_botaoiconein.classeicon   	= ''
        &botoes.Clear()
		&botoes.add('ABRIR:'+id)
		&uc_botaoiconein.botoes = &botoes.ToJson()
		
		&tabcel = new()
		&tabcel.text = UC.uc_botaoicone(&uc_botaoiconein.ToJson())
		&tablin.cells.Add(&tabcel)
		
		&uc_tabelain.lines.Add(&tablin)

	endfor
	matriz.Caption = uc.uc_tabela(&uc_tabelain.ToJson())
endsub
```

## DivTable
Este controle foi construído tendo como base o site [divtable.com](https://divtable.com/table-styler/), que possui um editor de estilo interessante, caso se deseje configurar tabelas com cores diferentes.
