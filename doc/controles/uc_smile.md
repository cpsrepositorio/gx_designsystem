# uc_smile
Temos aqui um controle com sentido de avaliação, que coloca várias faces com diversos sentimentos, permitindo que o usuário expresse sua avaliação pela escolha do rosto que lhe pareça adequado.

## Exemplo
O controle é simples, e muito semelhante ao [**uc_rating**](/doc/controles/uc_rating.md) segue o padrão tradicional, e um conjunto de **itens** que inclui um icone e evento.

```
&smile=new()
&smile.icone = '<i class="fa-2x far fa-sad-cry"></i>'
&smile.evento = 'SMILE:1'
&uc_smileIN.itens.Add(&smile)
```
|var|tipo|
|-----------------|---------------------------|
|&smile | uc_smilein.item|
|&uc_smileIN | uc_smilein |

Na montagem do objeto temos mais duas informações importantes: 1) o item selecionado **&uc_smileIN.selected** que é utilizado para aplicar uma classe de seleção, definida em  **&uc_smileIN.selectedclass**, para destacar a imagem das demais da lista. Caso opte por um icone distinto forneça-o em **&uc_smileIN.selectedicone**

```
sub 'smile'	
 &uc_smileIN.id        		= 'SMILE'
 &uc_smileIN.interface 		= &Pgmname.Trim()
 &uc_smileIN.selected		= &s
 &uc_smileIN.selectedicone 	= ''
 &uc_smileIN.selectedclass	= 'uc_smileselected'
 &uc_smileIN.itens.Clear()

 &smile=new()
 &smile.icone = '<i class="fa-2x far fa-sad-cry"></i>'
 &smile.evento = 'SMILE:1'
 &uc_smileIN.itens.Add(&smile)
	
 &smile=new()
 &smile.icone = '<i class="fa-2x far fa-frown"></i>'
 &smile.evento = 'SMILE:2'
 &uc_smileIN.itens.Add(&smile)
	
 &smile=new()
 &smile.icone = '<i class="fa-2x far fa-meh"></i>'
 &smile.evento = 'SMILE:3'
 &uc_smileIN.itens.Add(&smile)

 &smile=new()
 &smile.icone = '<i class="fa-2x far fa-smile"></i>'
 &smile.evento = 'SMILE:4'
 &uc_smileIN.itens.Add(&smile)
	
 &smile=new()
 &smile.icone = '<i class="fa-2x far fa-smile-beam"></i>'
 &smile.evento = 'SMILE:5'
 &uc_smileIN.itens.Add(&smile)
	
 grid.caption = UC.uc_smiles(&uc_smileIN.ToJson())
endsub
```


