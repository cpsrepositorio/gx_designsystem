# uc_botao
Os botões são elementos em HTML criados a partir do controle **uc.uc_botao(&uc_botaoIN.ToJson())**.
Portanto é necessário ter uma variável **&uc_botaoIN** para carregar.

A estrutura possui um cabeçalho simples (id e interface) e uma coleção de botões do tipo uc_botaoIN.botao, que formarão a barra de botões do controle.
É possível criar dois tipos de variáveis a partir deste tipo: uc_botaoIN e uc_botaoIN.botao, e nestas definir o comportamento e o formato dos botões. Vamos testar. A primeira cria uma barra e a segunda um botão nesta barra.
1.	Criar um webpanel, com o nome de ex_botao
2.	Criar duas variáveis do tipo uc_botaoIN, uma chamada barra e outra botão, veja os tipos exatos a seguir.
3.	Adicione na interface um textblock, alterando a propriedade ControlName e Caption para a palavra html e Format para HTML
4.	Crie um evento Start
5.	Inclua os arquivos de estilo, com a programação de form.HeaderRawHTML = UC.uc_cssGET_bot523()
6.	E a definição da barra e do botão, conforme o exemplo abaixo:	
Event Start
	/* 1 */
	form.HeaderRawHTML = UC.uc_cssGET_bot523()
	/* 2 */
	&barra.id = 'BAR1'
	&barra.interface = &Pgmname.Trim()
	/* 3 */
	&botao.titulo = 'Teste'
	&barra.botoes.Add(&botao)
	/* 4 */
	html.Caption = uc.uc_botao(&barra.ToJson())
Endevent

Ao executar o exemplo será possível visualizar o botão criado.


