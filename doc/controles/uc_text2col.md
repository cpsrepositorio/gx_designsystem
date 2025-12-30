# uc_text2col

O controle **uc_text2col** é um simples arranjo de texto no formato de uma tabela com duas colunas. Normalmente na coluna da esquerda podemos ter um titulo, e na direita o conteúdo.
O mesmo pode ser utilizado para incluir conteúdo estruturado em um uc_card, ou qualquer outro tipo de controle.

```
	&uc_text2colin.id = ''
	&uc_text2colin.interface = ''
	&uc_text2colin.classe = 'uc_w100'
	&uc_text2colin.tituloclasse = 'uc_w20 uc_textopequeno uc_border-bottom'
	&uc_text2colin.conteudoclasse = 'uc_80 uc_border-bottom'
	
	&linha = new()
	&linha.titulo   = ''
	&linha.conteudo = 'botao'
	&linha.posicao = 'right'
	&uc_text2colin.lines.Add(&linha)
	
	&linha = new()
	&linha.titulo   = 'objetivo'
	&linha.conteudo = 'Mussum Ipsum, cacilds vidis litro abertis. Nullam volutpat risus nec leo commodo, ut interdum diam laoreet. Sed non consequat odio. Detraxit consequat et quo num tendi nada. Em pé sem cair, deitado sem dormir, sentado sem cochilar e fazendo pose. Posuere libero varius. Nullam a nisl ut ante blandit hendrerit. Aenean sit amet nisi.'
	&uc_text2colin.lines.Add(&linha)
	
	&linha = new()
	&linha.titulo   = 'objetivo'
	&linha.conteudo = 'Mussum Ipsum, cacilds vidis litro abertis. Nullam volutpat risus nec leo commodo, ut interdum diam laoreet. Sed non consequat odio. Detraxit consequat et quo num tendi nada. Em pé sem cair, deitado sem dormir, sentado sem cochilar e fazendo pose. Posuere libero varius. Nullam a nisl ut ante blandit hendrerit. Aenean sit amet nisi.'
	&uc_text2colin.lines.Add(&linha)

	html.Caption  = '<h5>uc_text2col</h5>'
	html.Caption += UC.uc_tabelasimples(&uc_text2colin.ToJson())
```

## Classes
Cada &linha deve conter pelo menos duas propriedades, titulo e conteúdo. Titulo à esquerda e conteúdo à direita na tabela.

A largura da coluna da direita e esquerda são definidas pelas classes em **&uc_text2colin.tituloclasse** e **&uc_text2colin.conteudoclasse** que são iguais para todas as linhas.

Uma propriedade **posicao** pode ser utilizada para definir o alinhamento do conteúdo na célula (left, right, center).

As classes são globais e afetam todas as linhas e colunas da 'tabela'.

No exemplo, foram utilizadas classes **uc_w20** e **uc_w80** para definir a largura das colunas em **20%** e **80%**, além de **uc_border-bottom** para definir uma linha somente na parte inferior.
```
	&uc_text2colin.tituloclasse = 'uc_w20 uc_textopequeno uc_border-bottom'
	&uc_text2colin.conteudoclasse = 'uc_80 uc_border-bottom'
```
Maiores informações sobre as classes utilizadas:

| classe | significado |
|--------|-------------|
|.uc_border-bottom {border-bottom: var(--uc_border);}| Borda padrão apenas na parte inferior |
|.uc_border-top {border-top: var(--uc_border);}|Borda padrão apenas na parte superior|
|.uc_border-left {border-left: var(--uc_border);}|Borda padrão apenas na lateral esquerda|
|.uc_border-right {border-right: var(--uc_border);}|Borda padrão apenas na lateral direita|
|.uc_border {border: var(--uc_border);}|Borda padrão em todas as laterais|
|var(--uc_border)|Borda padrão, definida no uc_root.css|


