# uc_carddestacado
Cards destacados são controles que destacam apenas um único valor, levando em consideração cor, unidade, titulo.

Até esse momento, temos tres tipos de cards destacados disponíveis:

* **&card.classe = 'uc_card-destacado-...cor'** coloca a cor no fundo do card.
* **&card.classe = 'uc_card-lborder-...cor'**  coloca a cor na lateral esquerda do card
* **&card.classe = 'uc_card-rborder-...cor'**  coloca a cor na lateral direita do card

As cores possíveis são:

* **blue** azul
* **red** vermelho
* **orange** amarelo
* **green** verde
* **gray** cinza
* **clear** branco

## Tipo destacado
Neste exemplo os cards são mais fortes porque a cor fica no fundo do mesmo. Um icone (opcional) é possível para destacar ainda mais o assunto do cartão.

A classe ainda informa um valor adicional &card.classe = 'uc_card-destacado-blue **uc_card160**' que indica a largura do cartão em 160px.

```
	&uc_carddestacadoin = new()
	&uc_carddestacadoin.id = 'CARDS'
	&uc_carddestacadoin.interface = &Pgmname
	&uc_carddestacadoin.classecontainer = 'uc_cardcontainer'
	&uc_carddestacadoin.classe = 'uc_card-destacado'
	
	&card = new()
	&card.icone  		= '<i class="fas fa-home"></i>'
 	&card.classe 		= 'uc_card-destacado-blue uc_card160'
	&card.titulo 		= 'PROFESSORES'
	&card.tooltip 	= 'TOTAL DE ATRIBUICOES DE AULAS'
	&card.valor  		= '31123'
	&card.unidade 	= 'un'
	&card.evento  	= 'ABRIR:1'
	&uc_carddestacadoin.cards.add(&card)
	
	&card = new()
	&card.icone  	= '<i class="fas fa-user-alt"></i>'
 	&card.classe 	= 'uc_card-destacado-red uc_card160'
	&card.titulo 	= 'PROFESSORES'
	&card.tooltip = 'TOTAL DE ATRIBUICOES DE AULAS'
	&card.valor  	= '31123'
	&card.unidade = 'un'
	&card.evento  = 'ABRIR:2'
	&uc_carddestacadoin.cards.add(&card)
	
	&card = new()
	&card.icone  	= '<i class="fas fa-power-off"></i>'
 	&card.classe 	= 'uc_card-destacado-orange uc_card160'
	&card.titulo 	= 'PROFESSORES'
	&card.tooltip = 'TOTAL DE ATRIBUICOES DE AULAS'
	&card.valor  	= '31123'
	&card.unidade = 'un'
	&card.evento  = 'ABRIR:3'
	&uc_carddestacadoin.cards.add(&card)
	
	&card = new()
	&card.icone  	= '<i class="fas fa-recycle"></i>'
 	&card.classe 	= 'uc_card-destacado-green uc_card160'
	&card.titulo 	= 'PROFESSORES'
	&card.tooltip = 'TOTAL DE ATRIBUICOES DE AULAS'
	&card.valor  	= '31123'
	&card.unidade = 'un'
	&card.evento  = 'ABRIR:4'
	&uc_carddestacadoin.cards.add(&card)
	
	&card = new()
	&card.icone  	= '<i class="fas fa-trash-alt"></i>'
 	&card.classe 	= 'uc_card-destacado-gray uc_card160'
	&card.titulo 	= 'PROFESSORES'
	&card.tooltip 	= 'TOTAL DE ATRIBUICOES DE AULAS'
	&card.valor  	= '31123'
	&card.unidade 	= 'un'
	&card.evento  	= 'ABRIR:5'
	&uc_carddestacadoin.cards.add(&card)
	
	html.Caption  =  '<h5>uc_card-destacado</h5>'
	html.Caption +=  UC.uc_carddestaque(&uc_carddestacadoin.ToJson())
```
## Borda a esquerda ou direita
Trocando para o conjunto de classes lborder na definição da classe, **&card.classe = 'uc_card-lborder-red'**, temos a borda na cor desejada e o fundo do cartão em branco.

```
	&uc_carddestacadoin = new()
	&uc_carddestacadoin.id = 'CARDS'
	&uc_carddestacadoin.interface = &Pgmname
	&uc_carddestacadoin.classecontainer = 'uc_cardcontainer'
	&uc_carddestacadoin.classe = 'uc_card-destacado'
	
	&card = new()
	&card.icone  	= '<i class="fas fa-home"></i>'
 	&card.classe 	= 'uc_card-lborder-blue uc_card160'
	&card.titulo 	= 'PROFESSORES'
	&card.tooltip 	= 'TOTAL DE ATRIBUICOES DE AULAS'
	&card.valor  	= '31123'
	&card.unidade 	= 'un'
	&card.evento  	= 'ABRIR:1'
	&uc_carddestacadoin.cards.add(&card)
	
	&card = new()
	&card.icone  	= '<i class="fas fa-user-alt"></i>'
 	&card.classe 	= 'uc_card-lborder-red uc_card160'
	&card.titulo 	= 'PROFESSORES'
	&card.tooltip 	= 'TOTAL DE ATRIBUICOES DE AULAS'
	&card.valor  	= '31123'
	&card.unidade 	= 'un'
	&card.evento  	= 'ABRIR:2'
	&uc_carddestacadoin.cards.add(&card)
	
	&card = new()
	&card.icone  	= '<i class="fas fa-power-off"></i>'
 	&card.classe 	= 'uc_card-lborder-orange uc_card160'
	&card.titulo 	= 'PROFESSORES'
	&card.tooltip 	= 'TOTAL DE ATRIBUICOES DE AULAS'
	&card.valor  	= '31123'
	&card.unidade 	= 'un'
	&card.evento  	= 'ABRIR:3'
	&uc_carddestacadoin.cards.add(&card)
	
	&card = new()
	&card.icone  	= '<i class="fas fa-recycle"></i>'
 	&card.classe 	= 'uc_card-lborder-green uc_card160'
	&card.titulo 	= 'PROFESSORES'
	&card.tooltip 	= 'TOTAL DE ATRIBUICOES DE AULAS'
	&card.valor  	= '31123'
	&card.unidade 	= 'un'
	&card.evento  	= 'ABRIR:4'
	&uc_carddestacadoin.cards.add(&card)
	
	&card = new()
	&card.icone  	= '<i class="fas fa-trash-alt"></i>'
 	&card.classe 	= 'uc_card-lborder-gray uc_card160'
	&card.titulo 	= 'PROFESSORES'
	&card.tooltip 	= 'TOTAL DE ATRIBUICOES DE AULAS'
	&card.valor  	= '31123'
	&card.unidade 	= 'un'
	&card.evento  	= 'ABRIR:5'
	&uc_carddestacadoin.cards.add(&card)
	
	html.Caption +=  '<h5 class="uc_mt30">uc_card-lborder</h5>'
	html.Caption +=  UC.uc_carddestaque(&uc_carddestacadoin.ToJson())
```

O mesmo pode ser realizado com a borda à direita, com as classes **&card.classe = 'uc_card-rborder-red'**.

```
	&uc_carddestacadoin = new()
	&uc_carddestacadoin.id = 'CARDS'
	&uc_carddestacadoin.interface = &Pgmname
	&uc_carddestacadoin.classecontainer = 'uc_cardcontainer'
	&uc_carddestacadoin.classe = 'uc_card-destacado'
	
	&card = new()
	&card.icone  	= '<i class="fas fa-home"></i>'
 	&card.classe 	= 'uc_card-rborder-blue uc_card160'
	&card.titulo 	= 'PROFESSORES'
	&card.tooltip 	= 'TOTAL DE ATRIBUICOES DE AULAS'
	&card.valor  	= '31123'
	&card.unidade 	= 'un'
	&card.evento  	= 'ABRIR:1'
	&uc_carddestacadoin.cards.add(&card)
	
	&card = new()
	&card.icone  	= '<i class="fas fa-user-alt"></i>'
 	&card.classe 	= 'uc_card-rborder-red uc_card160'
	&card.titulo 	= 'PROFESSORES'
	&card.tooltip 	= 'TOTAL DE ATRIBUICOES DE AULAS'
	&card.valor  	= '31123'
	&card.unidade 	= 'un'
	&card.evento  	= 'ABRIR:2'
	&uc_carddestacadoin.cards.add(&card)
	
	&card = new()
	&card.icone  	= '<i class="fas fa-power-off"></i>'
 	&card.classe 	= 'uc_card-rborder-orange uc_card160'
	&card.titulo 	= 'PROFESSORES'
	&card.tooltip 	= 'TOTAL DE ATRIBUICOES DE AULAS'
	&card.valor  	= '31123'
	&card.unidade 	= 'un'
	&card.evento  	= 'ABRIR:3'
	&uc_carddestacadoin.cards.add(&card)
	
	&card = new()
	&card.icone  	= '<i class="fas fa-recycle"></i>'
 	&card.classe 	= 'uc_card-rborder-green uc_card160'
	&card.titulo 	= 'PROFESSORES'
	&card.tooltip 	= 'TOTAL DE ATRIBUICOES DE AULAS'
	&card.valor  	= '31123'
	&card.unidade 	= 'un'
	&card.evento  	= 'ABRIR:4'
	&uc_carddestacadoin.cards.add(&card)
	
	&card = new()
	&card.icone  	= '<i class="fas fa-trash-alt"></i>'
 	&card.classe 	= 'uc_card-rborder-gray uc_card160'
	&card.titulo 	= 'PROFESSORES'
	&card.tooltip 	= 'TOTAL DE ATRIBUICOES DE AULAS'
	&card.valor  	= '31123'
	&card.unidade 	= 'un'
	&card.evento  	= 'ABRIR:5'
	&uc_carddestacadoin.cards.add(&card)
	
	html.Caption +=  '<h5 class="uc_mt30">uc_card-rborder</h5>'
	html.Caption +=  UC.uc_carddestaque(&uc_carddestacadoin.ToJson())
```

## Sem ícone
Quando não se informa o valor de icone no cartão, o texto de titulo se posiciona à esquerda, produzindo um modelo mais simples ainda.
```
	...

	&card = new()
	&card.titulo 	= 'Titulo'
	// &card.icone  	= '<i class="fas fa-trash-alt"></i>'
	&card.texto 	= 'Mussum Ipsum, cacilds vidis litro abertis. Nullam volutpat risus nec leo commodo, ut interdum diam laoreet. Sed non consequat odio. Detraxit consequat et quo num tendi nada. Em pé sem cair, deitado sem dormir, sentado sem cochilar e fazendo pose. Posuere libero varius. Nullam a nisl ut ante blandit hendrerit. Aenean sit amet nisi.'
	&card.image 	= 'https://www.w3schools.com/howto/img_avatar.png'
	&card.imageclasse = 'uc_card300img'
	
	...
```

## Dimensões
As dimensões definidas nas classes para os cards destacados são:

| Classe   |   Significado |
|----------|---------------|
| .uc_card20      | {width:20%  }  |
| .uc_card25      | {width:25%  }  |
| .uc_card70 	  | {width:70px }  |
| .uc_card110     | {width:110px}  |
| .uc_card160     | {width:160px}  |
| .uc_card200     | {width:200px}  |
| .uc_card220     | {width:220px}  |
| .uc_card300     | {width:300px;}  |
| .uc_cardw100    | {width:100%;}  |
| .uc_cardw99	  | {width:99%;}  |
| .uc_cardw50	  | {width:49%;}  |
| .uc_cardw30	  | {width:32%;}  |
 	
As classes estão definidas em **uc_card.css**.
	
	
	
	
	
	
	
	
	