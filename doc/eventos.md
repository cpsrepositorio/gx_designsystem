# Eventos
O controle de eventos (click) de todo pacote é baseado em um user control chamado BOOTSTRAPCLICK, que deve ser instalado no Genexus.

Todo WEBPANEL deve inserir um único controle deste tipo para que intercepte ações que ocorrem na MASTER PAGE associada e os WEBCOMPONENTs que incluídos neste Webpanel.

Atenção! Não é possível inserir o usercontrol BOOTSTRAPCLICK em MasterPage e WebComponent. Caso isso venha a ser feito, o mesmo não interceptará os eventos. O tratamento de 'onde' partiu o click, quer seja da MasterPage, Component ou Webpanel, deve ser tratada no WebPanel.

A operação que define os eventos em todo pacote segue uma lógica comum, que inclui a informação da interface, controle, ação e paramestros, com os elementos (texto), separados por dois pontos (:)

	NOME_DA_INTERFACE:NOME DO CONTROLE:NOME DA AÇÃO:PARAMETRO1:PARAMETRO2:...

O nome da interface é importante porque em um cenário que envolve MasterPage + Webpanel + Component apresentado ao mesmo tempo no navegador, é necessário para identificar qual foi o controle gerador do click.

