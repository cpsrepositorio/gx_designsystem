# GridGET
Depois de muito tempo montando o mesmo uc_list, cheguei a conclusão que uma procedure seria ideal para criar qualquer lista que fosse necessária, desde que seguisse o conceito de uma única coluna.

Um SDT foi criado para representar as propriedades desta 'lista padrão', e a partir daí, a programação se resumiu a criar o Dataprovider de carga e em seguida a definição do formato da lista, o resto a procedure fazia.

## GridViewSDT
Essa 'lista padrão' chamada **GridGET** utiliza um SDT que define suas propriedades.
```
GridViewSDT
{
 id
 viewcard
 pagging
 pg
 pgsize
 last
 programa
 typeid
 toolbar
   editar
   apagar
   abrir
   inserir
}
```
## Como utilizar
Para se criar uma lista, será necessário criar uma variável desse tipo SDT, **GridViewSDT**, e definir suas propriedades.
```
sub 'grid'
 /* propriedades do grid */
 &GridViewSDT.id = 'LISTA'
 &GridViewSDT.programa = &Pgmname
 &GridViewSDT.pagging = true
 &GridViewSDT.pg = &pg
 &GridViewSDT.pgsize = &pgsize
 &GridViewSDT.totalrec = count(ModuloNome)
 &GridViewSDT.typeid = typeid.Numero
 &GridViewSDT.toolbar.inserir = false
 &GridViewSDT.toolbar.abrir = false
 &GridViewSDT.toolbar.editar = true
 &GridViewSDT.toolbar.apagar = true
	
 /* monta o grid */
 &rows.Sort('Descricao')
 &grid = GridGET(&rows, &GridViewSDT)
	
 /* apresenta */
 if &GridViewSDT.pagging
 	grid.Caption  = UC.uc_listapaginada(&grid.ToJson())
 else
	grid.Caption  = UC.uc_lista(&grid.ToJson())
 endif
endsub
```
A chamada a procedure temos o **&rows** que foram carregados do DataProvider (veja maiores detalhes em [Row](tec_row.md)). A variável &grid deve ser definida como **uc_listin**
```
&grid = GridGET(&rows, &GridViewSDT)
```
Os controles de paginação são ligados com as propriedades **pagging**, **pg**, **pgsize**, **totalrec**. A última representa o total de registros da tabela que fornece os registros para o controle, que é facilmente obtido com um **count(<nome_do_atributo>)**
```
 &GridViewSDT.pagging = true
 &GridViewSDT.pg = &pg
 &GridViewSDT.pgsize = &pgsize
 &GridViewSDT.totalrec = count(OpcaoTitulo)
 ```
Uma definição importante é o tipo do Id da tabela, visto que essa procedure funciona para todas as tabelas que podem ser do tipo Numeric, Texto ou GUID. No caso deste exemplo, temos uma definição de chave numérica **typeid.Numero**.
```
&GridViewSDT.typeid = typeid.Numero
```

## GridGET
O código do GridGET é apresentado abaixo, e para sua utilização necessita dos parametros **&rows** e **&GridViewSDT**, e o retorno é um tipo **&uc_listin**.

**GridGET**
```
&uc_listin.id = &GridViewSDT.id.trim()
&uc_listin.interface = &GridViewSDT.programa.ToUpper().Trim()
&uc_listin.pagging = &GridViewSDT.pagging
&uc_listin.paggingpg = &GridViewSDT.pg
&uc_listin.paggingpgsize = &GridViewSDT.pgsize
&uc_listin.paggingtrec = &GridViewSDT.totalrec
&uc_listin.paggingposition = uc_position.bottom
	
for &row in &rows
	/* tipo de id */
	do case
		case &GridViewSDT.typeid=typeid.Numero
			&id = &row.Id.ToString()
		case &GridViewSDT.typeid=typeid.Texto
			&id = &row.IdText
		case &GridViewSDT.typeid=typeid.GUID
			&id = &row.Guid.ToString()
	endcase

	/* toolbox */
	&uc_botaoiconein.id = &GridViewSDT.id.trim()
	&uc_botaoiconein.interface = &GridViewSDT.programa.ToUpper().Trim()
	&uc_botaoiconein.classebar = 'uc_flex-r'
	&uc_botaoiconein.classebotao = 'uc_bt-icon uc_btspace'
	&botoes.clear()
	if &GridViewSDT.toolbar.inserir
		&botoes.Add('NOVO:'+&id.Trim())
	endif
	if &GridViewSDT.toolbar.abrir
		&botoes.Add('ABRIR:'+&id.Trim())
	endif
	if &GridViewSDT.toolbar.editar
		&botoes.Add('EDITAR:'+&id.Trim())
	endif
	if &GridViewSDT.toolbar.apagar
		&botoes.Add('APAGAR:'+&id.Trim())
	endif
	&uc_botaoiconein.botoes = &botoes.ToJson()

	/* linha */
	&item = new()
	&item.titulo = &row.descricao.Trim()
	&item.strikethrough = &row.Flag
	&item.toolbox = UC.uc_botaoICONE(&uc_botaoiconein.ToJson())
	&uc_listin.itens.Add(&item)
endfor
```

