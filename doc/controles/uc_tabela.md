# UC_TABELA

O controle **uc_tabela** possibilita organizar os dados por meio de linhas e colunas.


```
sub 'matriz'
	&uc_tabelain.id 		= 'TABELA'
	&uc_tabelain.interface 	= &Pgmname.ToUpper()
	&uc_tabelain.class 		= 'minimalistBlack uc_w100'
	
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
		&uc_botaoiconein.classebar 		= 'uc_flex-r uc_flex-nowrap uc_mt30'
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
