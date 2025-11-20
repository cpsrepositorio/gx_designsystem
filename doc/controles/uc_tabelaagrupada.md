# uc_tabelaagrupada

O controle **uc.uc_tabelaagrupada**, possibilita construir um conjunto de tabelas agrupadas, em sequencia e com um titulo.

É util para apresentação de informações em bloco, como por exemplo:

* disciplinas por semestre
* eventos em um dia/mes/ano
* atividades em uma semana 

O controle foi planejado para simplificar ao máximo a construção de multiplas tabelas.

Cada tabela no controle é representada por uma variavel **grupo**, do tipo **uc_tabelaagrupada.grupo**.

## Grupo
Grupo representa um titulo na parte superior e uma tabela completa. Um conjunto de grupos fornece o aspecto de várias tabelas completas agrupadas, com a separação de um espaço.

Cada **&grupo** possui três coleções com a finalidade de definir a estrutura e o conteúdo da tabela.

1. **&grupo.titulos**, pode ser criado por meio de uma variável coleção do tipo Varchar(40), por exemplo, e add() para adicionar cada coluna à tabela.
```
  &titulos.clear()
  &titulos.add("id")
  &titulos.add("titulo")
  &grupo.titulos = &titulos.tojson()
```
2. **&grupo.widths**, representa o tamanho (width) de cada coluna na tabela, cujo total não pode ser maior que 100%. Por questões de responsividade, é melhor utilizar % ao invés de pixel. Caso inclua botões no final, será necessário adicionar um Width a mais na lista, com a largura da barra de botões.  Observe no exemplo que existem dois titulos e três larguras definidas. Utilize uma coleção de Varchar(10) para definir as larguras.
```
  &widths.clear()
  &widths.add("10%")
  &widths.add("70%") 
  &widths.add("30%") // para o toolbar
  &grupo.widths  =  &widths.tojson()
```
3. **&grupo.linhas**, compreende o conteúdo a ser inserido em cada linha da tabela em construção. Como os conteúdos poderão ser obtidos de tabelas, talvez seja necessário um for each, para percorrer cada linha a ser inserida. Dessa forma esta operação será um pouco mais complexa que as anteriores.
Primeiramente deve-se criar a coleção com os conteúdos de cada célula da linha. Essa coleção de células deve ser inserida na linha ao final **&linha.linha = &celulas.ToJson()**

```
for &n = 1 to 10

  &linha = new()

  &celulas.clear()
  &celulas.add(&n.ToString().Trim())
  &celulas.Add("Nome "+&i.ToString().Trim()+'/'+&n.ToString().Trim())
  &linha.linha = &celulas.ToJson()

```
Em seguida associamos um evento linha, definindo o valor da Ação e em seguida chave do evento que será retornada. Os botões são ligados por meio de true em (Open, Update, Delete). 
```
   ...
   &linha.evento = 'ID:'+&n.ToString().Trim()
   &linha.toolbar.open 	 = true
   &linha.toolbar.update = true
   &linha.toolbar.delete = true
  ...
```
E finalmente se insere a linha construída pela coleção de células e o evento no grupo: **&grupo.linhas.Add(&linha)**
```
   &grupo.linhas.Add(&linha)
  endfor
```

## Exemplo simples
A seguir o código completo do exemplo, caso queira copiar de uma única vez. Neste é possível observar como um novo **&grupo** é criado no **for &i = 1 to 2**.

```
sub 'ex'
	&uc_tabelaagrupadain.interface   		= &Pgmname
	&uc_tabelaagrupadain.id    			= 'TABELAS'
	&uc_tabelaagrupadain.classebotaobar	= 'uc_flex-r uc_flex-wrap'
	&uc_tabelaagrupadain.classebotao		= 'uc_btspace'
	&uc_tabelaagrupadain.classeicone		= 'uc_bticon'
		
	for &i = 1 to 2
		&grupo = new()
		&grupo.titulo  = 'GRUPO '+&i.ToString()
			
		&titulos.clear()
		&titulos.add("id")
		&titulos.add("titulo")
		&grupo.titulos = &titulos.tojson()
			
		&widths.clear()
		&widths.add("10%")
		&widths.add("70%") 
		&widths.add("30%") 
		&grupo.widths  =  &widths.tojson()
			
		for &n = 1 to 4
			&linha = new()
			
			&celulas.Clear()
			&celulas = new()
			&celulas.Add(&n.ToString().Trim())
			&celulas.Add("Nome "+&i.ToString().Trim()+'/'+&n.ToString().Trim())
			&linha.linha = &celulas.ToJson()
		
			/* toolbar */
			&linha.evento 			= 'id'+&n.ToString().Trim()
			&linha.toolbar.open 	= true
			&linha.toolbar.update 	= true
			&linha.toolbar.delete 	= true

			&grupo.linhas.Add(&linha)
		endfor
			
		&uc_tabelaagrupadain.grupos.Add(&grupo)
	endfor
  
	grid.Caption  = '<h5>Exemplo Simples</h5>'
	grid.Caption += UC.uc_tabelaagrupada(&uc_tabelaagrupadain.ToJson())
endsub
```

## SELECTED
O controle ainda permite que certa linha, ou linhas, sejam apresentadas de forma destacada, como se estivessem selecionadas a partir da definição de uma cor de fundo **&uc_tabelaagrupadain.selected_color = '#f7e8e8'**. 

Para 'selecionar' a linha necessário apenas incluir um caracter **#** em qualquer célula na linha. Por exemplo:
**&linha.linha = '["#D'+&n.ToString().Trim()+'","Nome da DI","obrigatoria","10","0"]'**
