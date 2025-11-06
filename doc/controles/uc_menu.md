# uc_menu
Um menu consiste em uma barra com opções posicionadas na horizontal, normalmente contendo uma imagem e um texto que representam uma certa ação de interesse do usuário. Pressupõe-se que ao clicar sobre a imagem ou texto, o menu causará o efeito de abrir alguma coisa.

![alt text](https://github.com/cpsrepositorio/gx_designsystem/blob/main/doc/imagens/uc_menu.png "Icone")

No pacote de controles, o uc_menu é um controle simples que oferece a construção desta barra horizontal com icones.


## UC_MenuIN
Um SDT é utilizado para adicionar itens ao menu, seguindo o mesmo principio dos demais controles.
Uma parte superior permite identificar o controle na tela (ID e INTERFACE)
E uma lista ITENS é utilizada para inserir os elementos no menu.

### Estilo
O estilo do menu é definido no arquivo uc_menu.css.

Mas otimizações são possíveis por meio da determinação da classe que determina o menu, e sua definição incorporada manualmente na interface.

`
&uc_menuin.classe = 'uc_menu'
`