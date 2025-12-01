# uc_rating
Temos aqui um controle bastante simples, que coloca várias estrelas vazias em uma linha e permite que o usuário clique sobre alguma delas, gerando um evento e o preenchimento das que se encontram à esquerda.
Pode ser utilizada para criar uma avaliação baseada na seleção da quantidade de estrelas.

## Exemplo
O controle é simples, segue o padrão tradicional, e um conjunto de **itens** que inclui um icone e evento.

```
&rating=new()
&rating.icone = '<i class="far fa-star"></i>'
&rating.evento = 'STAR:1'
&uc_ratingIN.itens.Add(&rating)
```

Na montagem do objeto temos mais duas informações importantes: 1) o item selecionado **&uc_ratingIN.selected** que é utilizado para preencher as imagens à esquerda e a **&uc_ratingIN.selectedicone** que indica a imagem a ser substituida para indicar o preenchimento.
O valor inicial de **&s** deve ser zero.

```
sub 'rating'	
 &uc_ratingIN.id = 'SMILE'
 &uc_ratingIN.interface = &Pgmname.Trim()
 &uc_ratingIN.selected = &s
 &uc_ratingIN.selectedicone = '<i class="fas fa-star"></i>'
 &uc_ratingIN.itens.Clear()
	
&rating=new()
&rating.icone = '<i class="far fa-star"></i>'
&rating.evento = 'STAR:1'
&uc_ratingIN.itens.Add(&rating)

 &rating=new()
 &rating.icone = '<i class="far fa-star"></i>'
 &rating.evento = 'STAR:2'
 &uc_ratingIN.itens.Add(&rating)
	
 &rating=new()
 &rating.icone = '<i class="far fa-star"></i>'
 &rating.evento = 'STAR:3'
 &uc_ratingIN.itens.Add(&rating)
	
 &rating=new()
 &rating.icone = '<i class="far fa-star"></i>'
 &rating.evento = 'STAR:4'
 &uc_ratingIN.itens.Add(&rating)
	
 &rating=new()
 &rating.icone = '<i class="far fa-star"></i>'
 &rating.evento = 'STAR:5'
 &uc_ratingIN.itens.Add(&rating)
	
 grid.caption = UC.uc_ratings(&uc_ratingIN.ToJson())
endsub
```


