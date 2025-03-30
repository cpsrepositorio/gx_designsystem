# O QUE É UM COMPONENTE
Um componente no pacote UC é simplesmente uma PROCEDURE, que possui um nome padrão que inicia com uc_..., como por exemplo, **uc_tabela**.

Esta procedure tem a finalidade de construir o objeto HTML + CSS + EVENTO necessário para dar forma, sustentação e operacionalidade para o componente. Produzindo ao final um conteúdo HTML que será apresentado em um Textblock em formato HTML.

Por esta característica, é possível alterar esta procedure a qualquer momento incluindo funcionalidades, ajustes e melhorias que tornam o componente melhor em termos visuais e operacionais, com grande simplicidade. Sem a necessidade de se executar instalações constantes no Genexus, como e o caso dos tradicionais User Controls.

O agrupamento destas procedures em um Package (OPC) também permite que as mesmas não sejam alteradas de forma indiscriminada nas Kbs que os utilizam, mantendo um padrão regular. Pois, caso seja necessário, altera-se a procedure equivalente e se gera uma nova versão do Package para todas as kbs.

## SDT
Cada componente é configurado de acordo com um SDT que por convenção, possui a denominação do componente seguido de um IN no final, para indicar o input de dados necessário para configurar o controle.

Exemplo, para a **uc_tabela** temos um **uc_tabelaIN** que apresentará todas as propriedades que permitirão criar uma tabela.
