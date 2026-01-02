# uc_sidebar
Sidebar é um tipo de menu lateral que é apresentado em formato de ícones que é expandido assim que o mouse passa sobre o item. Sua utilização é ampla, porém, no padrão dos sistemas temos uma lista de programas.

## Exemplo
Os itens do sidebar possuem apenas um titulo, icone e evento, e são inseridos no **uc_sidebarin**. 
```
&item = new()
&item.titulo = 'Mapeamento'
&item.evento = 'MAPEAMENTO'
&item.icone = '<i class="far fa-map"></i>'
&uc_sidebarin.itens.Add(&item)
```
O controle **uc_sidebar** pode incluir id, interface e uma classe que determina 
```
sub  'sidebar'
 &uc_sidebarin.id = 'SIDEBAR'
 &uc_sidebarin.interface = &Pgmname.ToUpper()
 &uc_sidebarin.classe = 'uc_sidebar'

 &item = new()
 &item.titulo	= 'Mapeamento'
 &item.evento	= 'MAPEAMENTO'
 &item.icone 	= '<i class="far fa-map"></i>'
 &uc_sidebarin.itens.Add(&item)

 &item = new()
 &item.titulo	= 'Incluir'
 &item.evento	= 'DEFINIR'
 &item.icone 	= '<i class="fas fa-plus-square"></i>'
 &uc_sidebarin.itens.Add(&item)

 &item = new()
 &item.titulo	= 'Voltar'
 &item.evento	= 'VOLTAR'
 &item.icone 	= '<i class="fas fa-angle-right"></i>'
 &uc_sidebarin.itens.Add(&item)

 &item = new()
 &item.titulo	= 'Tabela'
 &item.link	= 'uc_tabela'
 &item.icone 	= '<i class="fas fa-table"></i>'
 &uc_sidebarin.itens.Add(&item)

 sidebar.Caption = UC.uc_sidebar(&uc_sidebarin.ToJson())
endsub
```

|var|tipo|
|-----------------|---------------------------|
|&item | uc_sidebarin.item|
|&uc_sidebarin | uc_sidebarin |

## Classes
A classe **uc_sidebar** define o formato, dimensões e a expansão dos itens com o posicionamento do mouse, porém, é possível incluir outras classes, como por exemplo, cores.

| classe   | cor      |
|----------|----------|
| uc_white | branco   |
| uc_black | preto    |
| uc_gray  | cinza    |
| uc_blue  | azul     |
| uc_red   | vermelho |
| uc_orange| laranja  |
| uc_green | verde    |

Para incluir outras definições, insira a classe na mesma propriedade **&uc_sidebarin.classe = 'uc_sidebar uc_green'**
  



