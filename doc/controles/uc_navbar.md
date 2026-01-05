# uc_navbar
Navbar é a barra de apresentação do sistema, localizada normalmente na parte superior, que contém itens e botões. 

O controle **uc_navbar** foi montado com duas regiões de conteudo, à esquerda com informações sobre o programa, logotipo e itens. E na direita, com informações sobre perfil, alertas, itens e o botão sair.

## Nav
O navbar é uma barra com certas características visuais, e itens que podem ser utilizados para acessar programas no sistema.

A barra possui uma classe específica **uc_nav** e **uc_nav_fixedtop** para posicioná-la no topo do página.

```
&uc_navbarin.classe      = 'uc_nav  uc_nav_fixedtop uc_navblack uc_w100'
```
Também é possível definir a cor da barra.

| Classe  |  Cor |
|---|---|
|uc_navblack | barra com fundo preto |
|uc_navwhite | barra com fundo definido na variável --uc_bs-navbar |
|uc_navgray | barra com fundo cinza |

Os itens da barra são adicionados na coleção **&uc_navbarin.itens** e **&uc_navbarin.rights**
```
&item = new()
&item.titulo ='Item'
&item.evento = 'ITEM:1'
&uc_navbarin.itens.Add(&item)
```

## Logo e Brand
O logo normalmente se refere a um ícone ou imagem que representa a empresa.
O texto enviado para o **uc_navbar.logo** deve conter o img (html), e uma propriedade logolink pode ser utilizada para ligar o logo a uma página externa.

```
&logocps		= '<img src="'+cps.Link()+'">'
&logoestado	= '<img src="'+governo.Link()+'" style="height:36px; width:auto;">'

&uc_navbarin.logolink    = 'https://cps.sp.gov.br'
&uc_navbarin.logo		= &logocps
```
Em Genexus o **cps.Link()** se refere ao caminho URL completo de uma imagem carregada na Kb.

O **uc_navbar.brand** por sua vez, pode ser utilizado para nomear a Empresa ou o Sistema. É um texto simples.

## Botão Sair
A barra possui um recurso para inserir o botão Sair na lateral direita.  Uma única propriedade **&uc_navbarin.sair.bt** definida em true a liga.
O botão gerará um evento SAIR que pode ser interceptado e tratado. 
```
&uc_navbarin.sair.bt	= true
```
## Botão Perfil
A barra também possui um recurso para inserir um botão de Perfil do usuário na lateral direita.

```
&uc_navbarin.perfil.bt	= true
&uc_navbarin.perfil.nome = 'nome'
&uc_navbarin.perfil.foto = '<img....>'
```
## Alerta
A barra permite inserir itens especiais, como um sino para representar a ocorrência de alertas. Na variável &right temos uma propriedade &right.alerta que apresenta o valor em um label vermelho.
```
&right = new()
&right.icone  ='<i class="fas fa-bell"></i>'
&right.evento = 'ALERTA:1'
&right.alerta = '5'
&uc_navbarin.rights.Add(&right)
```

## Exemplo
Abaixo o exemplo completo.
```
&uc_navbarin.id 		= 'NAV'
&uc_navbarin.programa	= &programa.trim()
&uc_navbarin.classe      = 'uc_nav uc_navblack uc_w100'
&uc_navbarin.logo		= 'logo'
&uc_navbarin.logolink		= 'http://...'
&uc_navbarin.brand		= 'brand'

&uc_navbarin.sair.bt	= true

&uc_navbarin.perfil.bt	= true
&uc_navbarin.perfil.nome = 'GX-Design'

&uc_navbarin.itens.Clear()
&uc_navbarin.rights.Clear()

&item = new()
&item.titulo ='Item'
&item.evento = 'ITEM:1'
&uc_navbarin.itens.Add(&item)

&item = new()
&item.titulo ='Item'
&item.evento = 'ITEM:2'
&uc_navbarin.itens.Add(&item)

&item = new()
&item.titulo ='Item'
&item.evento = 'ITEM:3'
&uc_navbarin.itens.Add(&item)

&right = new()
&right.icone  ='<i class="fas fa-bell"></i>'
&right.evento = 'ALERTA:1'
&right.alerta = '5'
&uc_navbarin.rights.Add(&right)

navbar.Caption  = '<h5 class="uc_mt30">uc_navblack</h5>'
navbar.Caption += uc.uc_navbar(&uc_navbarin.ToJson())
```



