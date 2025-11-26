# alo mamãe
Comecemos de forma simples, apresentando os fundamentos de uso do pacote UC.
Se você ainda não está familiarizado com Genexus sugerimos que estude, pois aqui não estaremos detalhando a funcionalidade dos objetos.

Voce vai precisar de um Webpanel.

1) Na kb recém-criada, crie um webpanel.
2) Altere a propriedade do objeto colocando em Master Page o valor nulo (em branco)
3) Selecione Toolbox e inclua um controle Textblock na aba WebLayout.
4) Em seguida clique sobre este e pressione F4 para alterar a propriedade para Format: HTML
5) Na área Events do objeto, crie um Event Start.

```
Event Start
   form.HeaderRawHTML = uc_cssLOAD()
	form.Meta.AddItem("mobile-web-app-capable",'content="yes"')
  
   textblock1.caption = '<div style="border:1px solid red;">teste</div>'
Endevent
```
6) Salve o objeto
7) Execute o Genexus

Voce deve ter observado que é possivel a partir de um Textblock simples apresentar comandos HTML na interface. Pois o pacote UC é baseado nesta capacidade.

Parece ser um modelo tão elementar, mas na prática, todo conteúdo baseado na internet parte da estrutura HTML incluido informações texto. O pacote UC utiliza desta capacidade para inserir na interface padrão Genexus as tags HTML que apresentarão recursos complexos.

Não se esqueça de ver a explicação sobre o procedimento [uc_cssLOAD()](/docs/classes.md), que é uma procedure que precisa ser criada no projeto.

## Inserindo um botão
Após a execução do exemplo, podemos então utilizar esse painel para criar um Botão AloMamãe!!

```
Event Start
   form.HeaderRawHTML = uc_cssLOAD()
	form.Meta.AddItem("mobile-web-app-capable",'content="yes"')
  
   // textblock1.caption = '<div style="border:1px solid red;">teste</div>'

   &uc_botaoin.id 		   = 'id'
	&uc_botaoin.interface 	= 'interface'	

	&botao = new()
	&botao.evento = 'ALO'
	&botao.icone = '<i class="fas fa-female"></i>'
	&botao.titulo = 'Alô Mamãe!'
	&uc_botaoin.botoes.Add(&botao)
	
	textblock1.caption = UC.uc_botao(&uc_botaoin.ToJson())
Endevent
```
Crie duas variáveis, uma **&uc_botaoin** do tipo uc_botaoIN e outra **&botao** do tipo uc_botaoIN.botao.

## Evento
Para finalizar este primeiro exemplo, vamos adicionar um evento, mas somente se você instalou o User Control **BootstrapClick**.

No toolbox do Genexus arraste o controle Click para a interface (Weblayout), pode ser no final da mesma. Em seguida em Events copie o seguinte trecho de código:

```
Event BootstrapClick1.Click	
   	&uc_btclick = Bootstrapclick1.ButtonId
	msg('Clicou '+&uc_btclick)
EndEvent
```

Aqui o exemplo completo

```
Event Start
   form.HeaderRawHTML = uc_carga()
	form.Meta.AddItem("mobile-web-app-capable",'content="yes"')
   
   &uc_botaoin.id 		   = 'id'
	&uc_botaoin.interface 	= 'interface'	
	
	&botao = new()
	&botao.evento = 'ALO'
	&botao.icone = '<i class="fas fa-female"></i>'
	&botao.titulo = 'Alô Mamãe!'
	&uc_botaoin.botoes.Add(&botao)
	
	textblock1.caption = UC.uc_botao(&uc_botaoin.ToJson())
Endevent

Event BootstrapClick1.Click	
   &uc_btclick = Bootstrapclick1.ButtonId
	msg('Clicou '+&uc_btclick)
EndEvent

```

A variável **&uc_btclick** é do tipo Varchar(100)

Basicamente essa estrutura permite criar qualquer interface com o pacote.
