# uc_tabela

O controle **uc_tabela** possibilita organizar os dados de forma estruturada por meio de linhas e colunas.

Cada linha representa um certo registro e as colunas as propriedades que se deseja exibir, deste mesmo registro.

A tabela é um controle um pouco mais complexo, uma vez que exige a definição de um cabeçalho, com propriedades e em seguida adiconar as células de cada linha.

## Header
O cabeçalho é inserido em uma coleção, do tipo **uc_tabelain.cell**, no exemplo a seguir, a variavel **&tabhead** é desse tipo. Observe que cada coluna da tabela pode conter um **width** para determinar sua largura.

```
&uc_tabelain.header.Clear()
		
&tabhead = new()
&tabhead.text = 'Titulo'
&tabhead.width = '50%'
&uc_tabelain.header.Add(&tabhead)
	
&tabhead = new()
&tabhead.text = 'Conteudo'
&tabhead.width = '40%'
&uc_tabelain.header.Add(&tabhead)

&tabhead = new()
&tabhead.text = ''
&tabhead.width = '10%'
&uc_tabelain.header.Add(&tabhead)
```

|var |tipo|
|----|-----|
|&uc_tabelain|uc_tabelain|
|&tabhead|uc_tabelain.cell|

As linhas normalmente são extraidas de uma tabela, portanto, um **for each** ou **for in** deve ser programado para percorrer a coleção.

## Lines
```
&uc_tabelaIN.lines.Clear()
for &i = 1 to 5	
 &tablin = new()
	
 &tabcel = new()
 &tabcel.text = 'Titulo'+&i.ToString()
 &tablin.cells.Add(&tabcel)
	
 &tabcel = new()
 &tabcel.text = 'Conteudo'+&i.ToString()
 &tablin.cells.Add(&tabcel)

 &uc_botaoiconein.id = 'id'
 &uc_botaoiconein.interface = 'interface'	
 &uc_botaoiconein.classebar = 'uc_flex-r uc_flex-nowrap'
 &uc_botaoiconein.classebotao = 'uc_btspace uc_bt-icon uc_pointer'
 &uc_botaoiconein.classeicon = ''
 &botoes.Clear()
 &botoes.add('ABRIR:'+&i.ToString())
 &uc_botaoiconein.botoes = &botoes.ToJson()
	
 &tabcel = new()
 &tabcel.text = UC.uc_botaoicone(&uc_botaoiconein.ToJson())
 &tablin.cells.Add(&tabcel)
	
 &uc_tabelain.lines.Add(&tablin)	
endfor
```
|var |tipo|
|----|-----|
|&uc_tabelain|uc_tabelain|
|&tablin|uc_tabelain.line|
|&tabcel|uc_tabelain.line.cell|

O codigo inclui uma barra de botões em cada registro.

## Cores
A cor da tabela é definida na classe **&uc_tabelain.class = 'minimalistBlack'**, sendo que temos duas cores minimalistBlack e minimalistGray.
```
&uc_tabelain.id = 'TABELA'
&uc_tabelain.interface = &Pgmname.ToUpper()
&uc_tabelain.class = 'minimalistBlack'
...
```
## Card
O controle **uc_tabela** possui um ajuste que permite mostrar os registros como cards. Algumas propriedades permitem definir o modo de apresentação em formato Card.

| classe							| funcionamento						|
|-----------------------------------|-----------------------------------|
| **&uc_tabelaIN.card** 			| true. modo card                 	|
| **&uc_tabelaIN.cardcontainer** 	| define a disposição dos cartões 	|
| **&uc_tabelaIN.cardclass**     	| define o formato do cartão      	| 

Eventualmente, será necessário reposicionar a barra de botões **&tabcel.classe = 'uc_flex-r uc_flex-jce'** utilizando as classes uc_flex para colocar os botões no centro **uc_flex-jcc**, na esquerda **uc_flex-jcs** ou direita **uc_flex-jce**.

```
sub 'card'
...
&uc_tabelain.card = true
&uc_tabelaIN.cardcontainer = 'uc_flex-r uc_flex-w uc_flex-jcc'
&uc_tabelaIN.cardclass = 'uc_card uc_card300'
...
&uc_tabelaIN.lines.Clear()
for &i = 1 to 4		
  ...		
  &tabcel = new()
  &tabcel.text = UC.uc_botaoicone(&uc_botaoiconein.ToJson())
  &tabcel.classe = 'uc_flex-r uc_flex-jce'
  &tablin.cells.Add(&tabcel)		
  &uc_tabelain.lines.Add(&tablin)	
 endfor
 grid.Caption += '<h5 class="uc_mt30">Card</h5>'
 grid.Caption += UC.uc_tabela(&uc_tabelain.ToJson())
endsub
```
## Botões
O controle **uc_tabela** também inclui uma barra de botões na parte superior.

| classe							| opção						|
|-----------------------------------|-----------------------------------|
| **&uc_tabelaIN.toolbar.__** 	| new,close, refresh, export, filter, config, filteredit, save, view, por exemplo: **&uc_tabelaIN.toolbar.new**  | 
| **&uc_tabelaIN.toolbar.___title** | titulos nos botões, por exemplo: **&uc_tabelaIN.toolbar.newtitle** |
| **&uc_tabelaIN.toolbar.notitle** 	| não inclui titulos nos botões |

```
...
&uc_tabelain.toolbar.notitle = true
&uc_tabelain.toolbar.new = true
&uc_tabelain.toolbar.export = true
...
```
## DivTable
Este controle foi construído tendo como base o site [divtable.com](https://divtable.com/table-styler/), que possui um editor de estilo interessante, caso se deseje configurar tabelas com cores diferentes.
