# uc_botaosimples

Uma variação mais simplificada para criação de uma barra de botões pode ser obtida por meio do controle uc_botaosimples.

Neste ocorre que a informação das propriedades do botao foram simplificadas para apenas uma única propriedade chamada **info**, que representa uma coleção de Varchar(40).

	&botao.info = &info.ToJson()

Esta coleção tem uma sequencia correta para criar a estrutura do botao

	&info = new()
	&info.add('ABRIR:1') 				
	&info.add('<i class="fas fa-eye"></i>') 
	&info.add('Abrir') 					
	&info.add('Abrir o registro') 

* **ABRIR:1** o primeiro parametro representa o evento, que além de uma palavra deve incluir, caso necessário, o codigo do registro após um caracter dois pontos (:)
* **<i class="fas fa-eye"></i>** Em seguida o icone que será apresentado no botão. Em caso de não necessidade, deve ser inserir um texto vazio ''. Os icones são obtidos do FontAwesome versão 5.34
* **Abrir** Em seguida o texto que formará o titulo do botão, e caso não seja necessário, informar um texto vazio ''
* **Abrir o registro** Finalmente o Tooltip para informar ao usuário o que faz o botão.

## Botões redondos
Nesse exemplo o controle é utilizado para produzir uma barra com dois botões arredondados. Isso é obtido devido a classe **classeicon   = 'uc_bt-icon'**
 
```
	&uc_botaosimplesin.id 		= 'id'
	&uc_botaosimplesin.interface 	= 'interface'	
	&uc_botaosimplesin.classebar 	= 'uc_flex-r uc_flex-nowrap'
	&uc_botaosimplesin.classeicon   = 'uc_bt-icon'
	
	&info = new()
	&info.add('EDITAR:1') 				
	&info.add('<i class="fas fa-pen"></i>') 
	&info.add('') 						
	&info.add('Alterar o registro') 		
	&botao = new()
	&botao.info = &info.ToJson()
	&uc_botaosimplesin.botoes.Add(&botao)
	
	&info = new()
	&info.add('APAGAR:1') 					
	&info.add('<i class="fas fa-trash"></i>') 	
	&info.add('') 							
	&info.add('Apagar o registro') 			
	&botao = new()
	&botao.info = &info.ToJson()
	&uc_botaosimplesin.botoes.Add(&botao)
	grid.Caption = UC.uc_botaosimples(&uc_botaosimplesin.ToJson())
```

## Botões comuns
Os botões comuns são os que possuem um icone e texto, e por serem um pouco maior, não é recomendado que sejam totalmente redondos, portanto utilize a classe **classeicon   = 'uc_bt'**

```
	&uc_botaosimplesin.id 		= 'id'
	&uc_botaosimplesin.interface 	= 'interface'	
	&uc_botaosimplesin.classebar 	= 'uc_flex-r uc_flex-nowrap'
	&uc_botaosimplesin.classebotao = 'uc_bt'
	
	&info = new()
	&info.add('ABRIR:1') 				
	&info.add('<i class="fas fa-eye"></i>') 
	&info.add('Abrir') 					
	&info.add('Abrir o registro') 		
	&botao = new()
	&botao.info = &info.ToJson()
	&uc_botaosimplesin.botoes.Add(&botao)
	grid.Caption += '<br>'+UC.uc_botaosimples(&uc_botaosimplesin.ToJson())
```

### Interceptação de eventos

Os eventos gerados pela barra de botão são associados a cada botão individual, sendo formado por uma string separada por dois pontos (:) no seguinte formato:

	&uc_botaoiconeIN.interface : &uc_botaoiconeIN.id : PLAY : 5
	
No exemplo apresentado a sequencia de itens nesse evento seria:

	NOME_DA_INTERFACE:BOTAO:PLAY:5

Para maiores informações a respeito desta operação veja [Eventos](/eventos.md)