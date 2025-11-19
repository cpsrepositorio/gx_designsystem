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

* **'ABRIR:1'** Primeiro o evento com os parametros
* **<i class="fas fa-eye"></i>'** Em seguida o icone que será apresentado no botão. Em caso de não necessidade, deve ser inserir um texto vazio ''.
* **'Abrir'** Em seguida o texto que formará o rótulo do botão, e caso não seja necessário, informar um texto vazio ''
* **'Abrir o registro'** Finalmente o Tooltip para informar ao usuário o que faz o botão.

A seguir um exemplo.
```
	
    &uc_botaosimplesin.id 		= 'id'
	&uc_botaosimplesin.interface 	= 'interface'	
	&uc_botaosimplesin.classebar 	= 'uc_flex-r uc_flex-nw's
	&uc_botaosimplesin.classebotao  = 'uc_bt uc_btspace'
	&uc_botaosimplesin.classeicon   = 'uc_bticon'
	
	&info = new()
	&info.add('ABRIR:1') 				
	&info.add('<i class="fas fa-eye"></i>') 
	&info.add('Abrir') 					
	&info.add('Abrir o registro') 
	&botao = new()
	&botao.info = &info.ToJson()
	&uc_botaosimplesin.botoes.Add(&botao)
	
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
	
	grid.Caption = UC.uc_botaosimples(&uc_botaoin.ToJson())
```