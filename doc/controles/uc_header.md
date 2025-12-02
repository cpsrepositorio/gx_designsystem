# uc_header
O header é um controle semelhante ao **uc_titulo** exceto pela estrutura e classes. O objetivo é apresentar um titulo e texto no topo de uma página.

## Exemplo
O controle é formado por um texto principal (titulo) e um secundário (subtitulo) apresentado logo abaixo.
```
sub 'header'
 &uc_headerIN.classe = 'uc_header'
 &uc_headerIN.titulo = 'Conteúdo'
 &uc_headerIN.texto = 'Mussum Ipsum, cacilds vidis litro abertis. Casamentiss faiz malandris se pirulitá. Nec orci ornare consequat. Praesent lacinia ultrices consectetur. Sed non ipsum felis. Todo mundo vê os porris que eu tomo, mas ninguém vê os tombis que eu levo! Sapien in monti palavris qui num significa nadis i pareci latim.'
 html.Caption = UC.uc_header(&uc_headerIN.ToJson())
endsub
```
No caso do **uc_header** as classes estão padronizadas no próprio código, diferente do **uc_titulo** que permite a personalização.
