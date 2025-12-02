# uc_word
O controle **uc_word** é uma coleção de palavras que se comportam como botões, aceitando eventos e interceptações. Pode ser util para representar um conjunto de palavras selecionadas pelo usuário, talvez para filtro.
O controle não opera o filtro em si, apenas guarda uma lista de palavras.

## Exemplo
A inclusão de palavras na lista é muito simples, veja o exemplo abaixo. 
```
&word = new()
&word.text = 'Palavra1'
&word.classe = 'uc_worditem'
&word.event = 'Palavra1'
&uc_wordin.words.Add(&word)
```
A seguir o exemplo completo.
```
sub 'word'
 &uc_wordin.interface = &Pgmname
 &uc_wordin.id = 'WORDS'
 &uc_wordin.classe = 'uc_wordcontainer'

 &word = new()
 &word.text = 'Palavra1'
 &word.classe = 'uc_worditem'
 &word.event = 'Palavra1'
 &uc_wordin.words.Add(&word)
	
 &word = new()
 &word.text = 'Palavra2'
 &word.classe = 'uc_worditem'
 &word.event = 'Palavra2'
 &uc_wordin.words.Add(&word)

 grid.Caption  = UC.uc_words(&uc_wordin.ToJson())
 endsub
```
## Carregando palavras
O exemplo, ainda apresenta uma caixa de textos que utilizamos para colar um texto e em seguida criar a lista.
Desta forma para criar dinamicamente a lista de palavras poderiamos quebrar um parágrafo, pelo espaço em branco, gerando uma coleção de palavras, e em seguida inserí-las no controle.
```
&palavras = &texto.SplitRegEx(" ")
for &palavra in &palavras
 &word = new()
 &word.text = &palavra
 &word.classe = 'uc_worditem'
 &word.event = &palavra
 &word.close = true
 &uc_wordin.words.Add(&word)
endfor
```
Uma propriedade adicional, **&word.close = true**, pode ser utilizada para inserir uma imagem (um X) que representa o evento remover a palavra da lista.
Abaixo a rotina completa.

```
Event Enter
 &uc_wordin.interface = &Pgmname
 &uc_wordin.id = 'WORDS'
 &uc_wordin.classe = 'uc_wordcontainer'
 &uc_wordin.words.Clear()
	
 &palavras = &texto.SplitRegEx(" ")
 for &palavra in &palavras
  &word = new()
  &word.text = &palavra
  &word.classe = 'uc_worditem'
  &word.event = &palavra
  &word.close = true
  &uc_wordin.words.Add(&word)
 endfor

 grid.Caption = UC.uc_words(&uc_wordin.ToJson())
Endevent
```
## Interceptando ações
A lista também faz sentido se um click sobre uma das palavras permitir algum tipo de ação (abrir ou fechar) alguma coisa, por exemplo.
Nesse caso precisaremos do BootstrapClick para obter a palavra que foi clicada.
```
Event Bootstrapclick1.Click
 &uc_btclick = Bootstrapclick1.ButtonId
 navEvent2(&uc_btclick, &uc_btclickparms, &url, &isok)
 if &isok
  GlobalEvents.MPHOME(&uc_btclickparms)
 endif
	
 alerta.caption =  
 ' I:'	+ &uc_btclickparms.Item(uc_btitem.interface)
 +'<br>C:'	+ &uc_btclickparms.Item(uc_btitem.controle)
 +'<br>A:'	+ &uc_btclickparms.Item(uc_btitem.acao)
	
 do 'remover'	
EndEvent
```
Uma subrotina **'remover'** é chamada para retirar a palavra da lista e em seguida para reconstruir o controle na interface. Esse método precisa de aprimoramento, principalmente para eliminar as palavras iguais na lista.
```
sub 'remover'
 &i = 1
 for &palavra in &palavras
  if &palavra = &uc_btclickparms.Item(uc_btitem.acao)
   msg('removendo palavra '+&palavra)
   &uc_wordin.words.Remove(&i)
   exit
  endif
 &i += 1	
 endfor
 grid.Caption = UC.uc_words(&uc_wordin.ToJson())
endsub
```


