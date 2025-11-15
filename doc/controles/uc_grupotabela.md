# uc_grupotabela

O controle **uc.uc_grupotabela(&uc_grupotabelaIN.ToJson())**, possibilita construir uma ou mais tabelas agrupadas, separadas por um titulo e espaço.
É util para apresentação de informações me bloco, como por exemplo as disciplinas de um semestre, de todo curso.

![alt text](https://github.com/cpsrepositorio/gx_designsystem/blob/main/doc/imagens/uc_grupotabela.PNG "Icone")

O controle foi pensado para simplificar ao máximo a construção de multiplas tabelas.

A primeira cria uma barra e a segunda um botão nesta barra.
1.	Criar um webpanel, com o nome de ex_botao
2.	Criar uma variável do tipo **uc_grupotabelaIN**, e mais duas, **&grupo** (uc_grupotabelaIN.grupo) e **&linha** (uc_grupotabelaIN.grupo.linha)
3.	Em &grupo inclua as definições da tabela, como os titulos de colunas e larguras.
4.	Em &linha inclua as linhas da tabela, respeitando o total de colunas definido.
5.	Adicione na interface um textblock, alterando a propriedade ControlName e Caption para a palavra **html** e Format para **HTML**
6.	Crie um evento Start
7.	Inclua os arquivos de estilo, com a programação de **form.HeaderRawHTML = UC.uc_cssGET_bot523()**
8.	Abaixo um exemplo


```
Event Start
 /* 1 */
 form.HeaderRawHTML = UC.uc_cssGET_bot523()

 /* 2 */
 do 'tabela'
	
  /* 3 */
 html.Caption = UC.uc_grupotabela(&uc_grupotabelaIN.ToJson())
Endevent

Sub 'tabela'
 &uc_grupotabelaIN.interface = &Pgmname
 &uc_grupotabelaIN.id = 'TABELAS'
 &uc_grupotabelaIN.selected_color 	= '#f7e8e8'
 &uc_grupotabelaIN.classebotaobar	= 'uc_flex-r uc_flex-wrap'
 &uc_grupotabelaIN.classebotao		= 'uc_btspace'
 &uc_grupotabelaIN.classeicone		= 'uc_bticon'
	
 for &i = 1 to 2
  &grupo = new()
  &grupo.titulo  = 'Item '+&i.ToString()

  &titulos.clear()
  &titulos.add("id")
  &titulos.add("titulo")
  &grupo.titulos = &titulos.tojson()

  &widths.clear()
  &widths.add("10%")
  &widths.add("80%") 
  &widths.add("10%") 
  &grupo.widths  =  &widths.tojson()
		
  for &n = 1 to 10
   &linhas.clear()
   &linhas.add('#'+&n.ToString().Trim())
   &linhas.add('Nome')
   &linhas.add('10')

   &linha.evento = 'id'+&n.ToString().Trim()
   &linha.toolbar.open 	= true
   &linha.toolbar.update = true
   &linha.toolbar.delete = true
   &grupo.linhas = &linhas.tojson()
  endfor

  &uc_grupotabelaIN.grupos.Add(&grupo)
 endfor
EndSub
```

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
2. **&grupo.widths**, representa o tamanho (width) de cada coluna na tabela, cujo total não pode ser maior que 100%. Por questões de responsividade, é melhor utilizar % ao invés de pixel. Um detalhe importante deve ser levado em conta, porque caso se associe um evento a cada linha de conteúdo, será necessário definir a largura do toolbar, adicionando, neste caso, um item a mais que o titulo. Observe no exemplo que existem dois titulos e três larguras definidas. Utilize uma coleção de Varchar(10) para definir as larguras.
```
  &widths.clear()
  &widths.add("10%")
  &widths.add("80%") 
  &widths.add("10%") 
  &grupo.widths  =  &widths.tojson()
```
3. **&grupo.linhas**, compreende o conteúdo a ser inserido em cada linha da tabela em construção. Como os conteúdos poderão ser obtidos de tabelas, talvez seja necessário um for each, para percorrer cada linha a ser inserida. Dessa forma esta operação será um pouco mais complexa que as anteriores.

Primeiramente deve-se criar a coleção com os conteúdos de cada célula.

```
  for &n = 1 to 10
   &linhas.clear()
   &linhas.add('#'+&n.ToString().Trim())
   &linhas.add('Nome')
   &linhas.add('10')
   ...
```
Em seguida, opcionalmente, o evento associado a linha. Meio estranho, mas bastante otimizado, pois se define o parâmetro que permite identificar em que linha ocorreu a ação, por meio da **&linha.evento = 'id'+&n.ToString().Trim()**, e em seguida os botões de evento com **&linha.toolbar.open = true**. Os botões do toolbar utilizam os mesmos conceitos definidos no controle **[uc_botaoicone](uc_botaoicone.md)**.
```
   ...
   &linha.evento = 'id'+&n.ToString().Trim()
   &linha.toolbar.open 	 = true
   &linha.toolbar.update = true
   &linha.toolbar.delete = true

   &grupo.linhas = &linhas.tojson()
  endfor
```



A variável **&grupo** é do tipo **uc_grupotabelaIN.grupo**, e **&linha** do tipo **uc_grupotabelaIN.grupo.linha**. A primeira representa uma tabela inteira, e a segunda as linhas desta tabela.

**&grupo.titulos** representa um conjunto de TITULO de cabeçalho. Nesse exemplo, **'["SIGLA","DISCIPLINA","TIPO","CH","EXT"]'**, forma uma tabela com 5 colunas.

Caso tenha interesse em definir as larguras das colunas, é possível com **&grupo.widths**, porem, como se deseja incluir uma barra de botões na última coluna, observe que foram definidos, no exemplo, 6 larguras: **'["10%","55%","15%","5%","5%","10%"]'**

Finalmente o controle permite ligar botões de controle na linha a partir de **&linha.toolbar**

O controle ainda permite que certa linha, ou linhas, sejam apresentadas como selecionadas a partir da definição de uma cor de fundo **&uc_grupotabelaIN.selected_color 	= '#f7e8e8'**. Para isso, será necessário apenas incluir um caracter **#** em qualquer célula na linha. Por exemplo:
**&linha.linha =  '["#D'+&n.ToString().Trim()+'","Nome da DI","obrigatoria","10","0"]'**


### Alternativa 
Criar uma coleção para carregar os itens do cabeçalho, widths e células da linha.

 &titulos = new()
 
 &titulos.add("SIGLA")
 
 &titulos.add("DISCIPLINA")
 
 &titulos.add("TIPO")
 
 &titulos.add("CH")
 
 &titulos.add("EXT")
 
 &grupo.titulos = &titulos.ToJson()

Nesse caso &titulos deve ser uma colection de caracteres.
Ou escrever os elementos diretamente na variável.

&grupo.titulos = '["SIGLA","DISCIPLINA","TIPO","CH","EXT"]'
