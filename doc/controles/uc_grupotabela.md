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
  &grupo.titulo  = 'SEMESTRE '+&i.ToString()
  &grupo.titulos = '["SIGLA","DISCIPLINA","TIPO","CH","EXT"]'
  &grupo.widths  =  '["10%","55%","15%","5%","5%","10%"]'
		
  for &n = 1 to 2
   &linha = new()
   if &n=1
    &linha.linha = 	'["#D'+&n.ToString().Trim()+'","Nome da DI","obrigatoria","10","0"]'
   else
    &linha.linha = 	'["D'+&n.ToString().Trim()+'","Nome da DI","obrigatoria","10","0"]'
   endif

   /* toolbar */
   &linha.evento = 'id'+&n.ToString().Trim()
   &linha.toolbar.open 	= true
   &linha.toolbar.update = true
   &linha.toolbar.delete = true
   &grupo.linhas.Add(&linha)
  endfor

  &uc_grupotabelaIN.grupos.Add(&grupo)
 endfor
EndSub
```
A variável **&grupo** é do tipo **uc_grupotabelaIN.grupo**, e **&linha** do tipo **uc_grupotabelaIN.grupo.linha**. A primeira representa uma tabela inteira, e a segunda as linhas desta tabela.

**&grupo.titulos** representa um conjunto de TITULO de cabeçalho. Nesse exemplo, **'["SIGLA","DISCIPLINA","TIPO","CH","EXT"]'**, forma uma tabela com 5 colunas.

Caso tenha interesse em definir as larguras das colunas, é possível com **&grupo.widths**, porem, como se deseja incluir uma barra de botões na última coluna, observe que foram definidos, no exemplo, 6 larguras: **'["10%","55%","15%","5%","5%","10%"]'**

Finalmente o controle permite ligar botões de controle na linha a partir de **&linha.toolbar**

O controle ainda permite que certa linha, ou linhas, sejam apresentadas como selecionadas a partir da definição de uma cor de fundo **&uc_grupotabelaIN.selected_color 	= '#f7e8e8'**. Para isso, será necessário apenas incluir um caracter **#** em qualquer célula na linha. Por exemplo:
**&linha.linha =  '["#D'+&n.ToString().Trim()+'","Nome da DI","obrigatoria","10","0"]'**


### Alternativa 
["1","2","3","4","5"]
