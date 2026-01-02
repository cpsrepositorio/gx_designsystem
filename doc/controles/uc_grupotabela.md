# uc_grupotabela (deprecated)

O controle **uc.uc_grupotabela(&uc_grupotabelaIN.ToJson())**, possibilita construir um agrupamento de tabelas separadas por um titulo e espaço.
É util para apresentação de informações me bloco, como por exemplo as disciplinas de um semestre, de todo curso.

![alt text](https://github.com/cpsrepositorio/gx_designsystem/blob/main/doc/imagens/uc_grupotabela.PNG "Icone")

O controle foi pensado para simplificar ao máximo a construção de multiplas tabelas.

Cada tabela no controle é representada por um **Grupo**.

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

|var|tipo|
|-----------------|---------------------------|
|&titulos | uc_chart|
|&grupo|uc_grupotabelasIN.grupo| 

2. **&grupo.widths**, representa o tamanho (width) de cada coluna na tabela, cujo total não pode ser maior que 100%. Por questões de responsividade, é melhor utilizar % ao invés de pixel. Um detalhe importante deve ser levado em conta, porque caso se associe um evento a cada linha de conteúdo, será necessário definir a largura do toolbar, adicionando, neste caso, um item a mais que o titulo. Observe no exemplo que existem dois titulos e três larguras definidas. Utilize uma coleção de Varchar(10) para definir as larguras.
```
&widths.clear()
&widths.add("10%")
&widths.add("80%") 
&widths.add("10%") 
&grupo.widths  =  &widths.tojson()
```

|var|tipo|
|-----------------|---------------------------|
|&widths | varchar(40) collection |

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

|var|tipo|
|-----------------|---------------------------|
|&linhas | varchar(40) collection |

Em seguida, opcionalmente, o evento associado a linha. Meio estranho, mas bastante otimizado, pois se define o parâmetro que permite identificar em que linha ocorreu a ação, por meio da **&linha.evento = 'id'+&n.ToString().Trim()**, e em seguida os botões de evento com **&linha.toolbar.open = true**. Os botões do toolbar podem ser três, até aqui, OPEN, UPDATE e DELETE, mas poderão ser expandidos conforme necessidade.
```
  ...
  &linha.evento = 'id'+&n.ToString().Trim()
  &linha.toolbar.open 	 = true
  &linha.toolbar.update = true
  &linha.toolbar.delete = true
  &grupo.linhas = &linhas.tojson()
endfor
```
## Exemplo completo
Uma vez definido o conceito fundamental, a proxima etapa é montar o controle com todos os recursos.

1.	Criar um webpanel
2.	Criar uma variável do tipo **uc_grupotabelaIN**, e mais duas, **&grupo** (uc_grupotabelaIN.grupo) e **&linha** (uc_grupotabelaIN.grupo.linha)
3.	Em seguida uma coleção chamada **&widths**, do tipo Varchar(10), para adicionar as larguras das colunas.
4.	E outra **&titulos**, também coleção do tipo Varchar(40) para o texto das colunas.
5.  E mais outra, &linha, também coleção, mas a largura pode ser maior que as anteriores, para conter o conteúdo de cada céluna em cada linha.
6.	Adicione na interface um **textblock**, alterando a propriedade ControlName e Caption para a palavra **html** e Format para **HTML**
6.	Crie um evento Start, faça a carga do CSS e monte a tabela, veja o exemplo abaixo.

```
Event Start
 form.HeaderRawHTML = UC.uc_cssGET_bot523()
 do 'tabela'
 html.Caption = UC.uc_grupotabela(&uc_grupotabelain.ToJson())
Endevent

Sub 'tabela'
 &uc_grupotabelain.interface   = &Pgmname
 &uc_grupotabelain.id    = 'TABELAS'
 &uc_grupotabelain.selected_color 	= '#f7e8e8'
 &uc_grupotabelain.classebotaobar	= 'uc_flex-r uc_flex-wrap'
 &uc_grupotabelain.classebotao		= 'uc_btspace'
 &uc_grupotabelain.classeicone		= 'uc_bticon'
	
 for &i = 1 to 2
  &grupo = new()
  &grupo.titulo  = 'GRUPO '+&i.ToString()

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

  &uc_grupotabelain.grupos.Add(&grupo)
 endfor
EndSub
```
## SELECTED
O controle ainda permite que certa linha, ou linhas, sejam apresentadas de forma destacada, como se estivessem selecionadas a partir da definição de uma cor de fundo **&uc_grupotabelaIN.selected_color = '#f7e8e8'**. 

Para 'selecionar' a linha necessário apenas incluir um caracter **#** em qualquer célula na linha. Por exemplo:
**&linha.linha = '["#D'+&n.ToString().Trim()+'","Nome da DI","obrigatoria","10","0"]'**
