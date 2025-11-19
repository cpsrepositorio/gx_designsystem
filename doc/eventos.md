# Eventos
O controle de eventos (click) de todo pacote é baseado em um user control chamado BOOTSTRAPCLICK, que deve ser instalado no Genexus.

Todo WEBPANEL deve inserir um único controle deste tipo para que intercepte ações que ocorrem na MASTER PAGE associada e os WEBCOMPONENTs que incluídos neste Webpanel.

Atenção! Não é possível inserir o usercontrol BOOTSTRAPCLICK em MasterPage e WebComponent. Caso isso venha a ser feito, o mesmo não interceptará os eventos. O tratamento de 'onde' partiu o click, quer seja da MasterPage, Component ou Webpanel, deve ser tratada no WebPanel.

A operação que define os eventos em todo pacote segue uma lógica comum, que inclui a informação da interface, controle, ação e paramestros, com os elementos (texto), separados por dois pontos (:). Todas as palavras utilizadas na construção da string são livres e podem ser escolhidas pelo próprio desenvolvedor, apenas a sequencia deve ser respeitada.

	NOME_DA_INTERFACE:NOME DO CONTROLE:NOME DA AÇÃO:PARAMETRO1:PARAMETRO2:...

O nome da interface é importante porque em um cenário que envolve MasterPage + Webpanel + Component apresentado ao mesmo tempo no navegador, é necessário para identificar qual foi o controle gerador do click.

## Interceptando evento
Assim que ocorre um CLICK na interface, um evento é enviado ao User Control, que o recebe de forma integral, com o mesmo formato da string apresentada acima.

```
Event BootstrapClick1.Click

 &uc_btclick = Bootstrapclick1.ButtonId

 /* quebrar o &uc_btclick pelo (:) */
 &uc_btclickparms = &uc_btclick.SplitRegEx(':')

 /* isso gera uma coleção onde os itens representam as palavras passadas no evento:
  &uc_btclickparms.item(1) = NOME_DA_INTERFACE
  &uc_btclickparms.item(2) = NOME_DO_CONTROLE
  &uc_btclickparms.item(3) = NOME_DA_ACAO
  &uc_btclickparms.item(4) = PARAMETRO 1
  &uc_btclickparms.item(5) = PARAMETRO 2
  &uc_btclickparms.item(6) = ...
 
 */

 if &uc_btclickparms.item(1)='NOME_DA_INTERFACE' and &uc_btclickparms.item(2)="NOME_DO_CONTROLE" and &uc_btclickparms.item(3)="NOME_DA_ACAO"
   
   // faça alguma coisa

 endif

EndEvent
```

Essa estrutura é utilizada para tratar todos os eventos que ocorrem nos controles.

Porém, a operação vai um pouco além desta simples explicação, pois o controle envolve mais recursos relacionados a encriptação dos valores. Consulte os documentos a seguir para maiores informações:

* [interceptação na NavBar](/tecnicas/tec_navevent.md)
* [encriptação manual de parametros](/tecnicas/tec_encriptacaomanual.md).
* [encriptação de parametros](/tecnicas/tec_encriptacaoparm.md).
* [interceptação de eventos](/tecnicas/tec_encriptacaobootstrapclick.md).

