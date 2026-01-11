# uc_botaoicone
Barra de botões são elementos que representam ações que podem ser acionadas pelos usuários.

O pacote apresenta vários tipos distintos de barras de botões, sendo simples de serem construídas. 

A barra **uc_botaoicone** objetiva criar uma linha com diversas imagens que representam ações, com características de um botão, sendo um modelo bem mais simples de programação, pois tudo se limita a definir uma palavra que representa o icone e um evento associado.

Por exemplo, um icone que representa uma lata de lixo, gera um evento APAGAR automaticamente, não sendo necessário ao desenvolvedor incluir detalhes.

### Criando uma barra de botões
Um botão neste controle é formado por uma **palavra**, seguido de um caracter **:** e o **evento** que deverá ser acionado quando ocorrer o click no botão. 

A seguir um exemplo.
```
&uc_botaoiconeIN.id = 'BOTAO'
&uc_botaoiconeIN.interface = 'NOME_DA_INTERFACE'	
&uc_botaoiconeIN.classebar = 'uc_flex-r uc_flex-nowrap uc_mt30'
&uc_botaoiconeIN.classebotao = 'uc_btspace uc_bt-icon uc_pointer'
	
&botoes.add('PLAY:5')
&botoes.add('INFO:5')
&botoes.add('NOVO:1')
&botoes.add('ABRIR:2')
&botoes.add('EDITAR:3')
&botoes.add('APAGAR:4')
&botoes.add('COPIAR:5')
&botoes.add('COLAR:5')
&uc_botaoiconeIN.botoes = &botoes.ToJson()
	
grid.Caption = UC.uc_botaoicone(&uc_botaoiconeIN.ToJson())
```

|var|tipo|
|-----------------|---------------------------|
|&uc_botaoiconeIN | uc_botaoiconein|
|&botoes|varchar(40) collection |

Para produzir a lista de botões, é definida uma variável simples, **&botoes** que é uma collection de Varchar(40), adicionando (add) a lista de botões que se deseja incluir. 

Os numeros que aparecem, por exemplo, PLAY:5, é o ID do registro que será enviado ao controle de eventos para identificar informação adicional para processamento.

Creio que a parte mais importante é a maneira que escrevemos o conteúdo de um botão, pois a palavra APAGAR, do exemplo abaixo, não foi escrita de forma aleatória, pois desejamos de fato que um evento chamado APAGAR seja gerado e uma imagem que represente a ação apagar represente o botão. No exemplo a seguir, um :4 indica que o registro a ser apagado é o de numero quatro (4), o : é apenas o separador.

```&botoes.add('APAGAR:4')```

##### Botões padrões
Os eventos padrões definidos no controle são apresentados a seguir

| Evento        | Tooltip           | icone  |
|------------- |:-------------:| -----:|
|NOVO|Insere novo registro | `<i class="fas fa-plus"></i>`  |
|ABRIR | Abre o registro | `<i class="fas fa-eye"></i>` |
|EDITAR | Atualiza o registro      |   `<i class="fas fa-pen"></i>`  |
|APAGAR | Apaga o registro|    `<i class="fas fa-trash"></i>`  |
|ABRIRPASTA|Abrir a pasta |  `<i class="fas fa-folder-open"></i>` |
|FECHARPASTA| Fechar a pasta ou sair |  `<i class="fas fa-folder"></i>` |
|ANEXAR | Anexar arquivo|  `<i class="fas fa-paperclip"></i>` |
|EXCEL | Exportar em formato Excel| `<i class="fas fa-file-excel"></i>`  |
|PDF |Exportar em formato PDF | `<i class="fas fa-file-pdf"></i>`  |
|IMPRIMIR| Imprimir|  `<i class="fas fa-print"></i>` |
|EMAIL|Enviar email|`<i class="fas fa-envelope"></i>`|
|EMAILENVIADO|Email enviado|`<i class="fas fa-paper-plane"></i>`|
|EMAILENVIAR|Email enviar|`<i class="far fa-paper-plane"></i>`|
|PRIMEIRO | Retorna ao primeiro da lista|  `<i class="fas fa-angle-double-left"></i>` |
|ANTERIOR | Retorna ao anterior|  `<i class="fas fa-angle-left"></i>` |
|PROXIMO| Avança para o proximo|  `<i class="fas fa-angle-right"></i>` |
|ULTIMO |Avança para o último |  `<i class="fas fa-angle-double-right"></i>` |
|PESSOANOVO |Insere pessoa | `<i class="fas fa-user-plus"></i>`  |
|BLOQUEAR|Bloqueia |  `<i class="fas fa-lock"></i>` |
|UNLOCK|Desbloqueia | `<i class="fas fa-unlock"></i>`  |
|CREDENCIAL| Credencial  | `<i class="fas fa-id-card"></i>`  |
|COMENTAR| Comentar |  `<i class="far fa-comment-dots"></i>` |
|COLAR |Colar registro copiado  | `<i class="far fa-paste"></i>`  |
|COPIAR | Copiar registro| `<i class="fas fa-copy"></i>`  |
|TURNON|Ligado|`<i class="fas fa-toggle-on"></i>`|
|TURNOFF|Desigado|`<i class="fas fa-toggle-off"></i>`|
|HISTORICO|Historico de operações|`<i class="fas fa-history"></i>`|
|PIZZA|Estatistica (pizza)|`<i class="fas fa-chart-pie"></i>`|
|BARRA|Estatistica (barra)|`<i class="far fa-chart-bar"></i>`|
|THUMBSUP|Aprovado|`<i class="fas fa-thumbs-up"></i>`|
|THUMBSDOWN|Reprovado|`<i class="fas fa-thumbs-down"></i>`|
|PLAY|Executar|`<i class="fas fa-play"></i>`|
|INFO|Informações|`<i class="fas fa-info"></i>`|
|POWER|Ligar|`<i class="fas fa-power-off"></i>`|
|POSTITCHEIO|Postit (solido)|`<i class="fas fa-sticky-note"></i>`|
|POSTITVAZIO|Postit (vazio) |`<i class="far fa-sticky-note"></i>`|
|CHECKED|Item selecionado |`<i class="far fa-check-square"></i>`|
|UNCHECKED|Item não selecionado |`<i class="far fa-square"></i>`|
			
### Interceptação de eventos
Os eventos gerados pela barra de botão são associados a cada botão individual, sendo formado por uma string separada por dois pontos (:) no seguinte formato:

	&uc_botaoiconeIN.interface : &uc_botaoiconeIN.id : PLAY : 5
	
No exemplo apresentado a sequencia de itens nesse evento seria:

	NOME_DA_INTERFACE:BOTAO:PLAY:5

Para maiores informações a respeito desta operação veja [Eventos](/eventos.md)
