# Genexus
GeneXus é uma ferramenta que constói sistemas de informação, porém, diferentemente de um editor de textos, o objetivo é construir todo o sistema com o menor esforço possível de programação. Parece até um sonho, mas na prática, isso já vem ocorrendo desde os anos 80, e ao longo de todo esse tempo, muitos geradores diferentes foram construidos para entregar os sistemas nas linguagens e bancos de dados atuais.

Se deseja compreender melhor como essa ferramenta funciona, começe pelo básico [Genexus Site](https://www.genexus.com/pt/), quando esse doc foi escrito, a versão que eles estavam trabalhando lá era o Genexus Next, que é a construção dos objetos por meio de IA. Bem atual para os dias de outrora.

## Interfaces Web
Genexus constrói interfaces Windows, Web, SD, e o foco nesta documentação são as interfaces Web.

As interfaces padrões no Genexus são construídas com objetos MasterPage, Webpanel e Component, nas quais são adicionados controles para determinar as funcionalidades. A ferramenta analisa se nos controles são inseridos atributos (de tabelas) ou variáveis, e no caso dos atributos, atua de forma automática para preenchê-los com conteúdos.

Tradicionalmente a construção de interfaces no Genexus são baseadas em controles padrões [Genexus Controls](https://wiki.genexus.com/commwiki/wiki?5925,Category%3AGeneXus+Controls), que permitem fazer o básico em termos de apresentação de informações, obtenção de dados dos usuários, interceptação de eventos. Porém, de certa maneira, este conjunto básico (é muito básico) e limita absurdamente a capacidade da interface, além de agregar informações estruturadas na interface.

A partir da versao Geneus X um novo recurso chamado UserControl passou a oferecer uma ampliação significativa da capacidade da interface, porém sob um custo alto de complexidade para sua produção, permitindo que os meros mortais pudessem também criar controles próprios, e nas  versões mais recentes um novo objeto [UserControl](https://wiki.genexus.com/commwiki/wiki?39356,Category%3AUser+Control+object) foi apresentado como uma forma de reduzir a complexidade.

A ferramenta tem buscado uma forma de gerar uma maior flexibilidade de configuração e uso para os desenvolvedores, e recentemente temos o objeto Unanimo, que agrega elementos de design.

## Pattern

Outra evolução foi significativa foram os [Pattern](https://wiki.genexus.com/commwiki/wiki?2814,Category%3APatterns) que agregou um gerador de objetos dentro do próprio Genexus, atuando de forma orquestrada para montar as interfaces, automaticamente, por meio de certos padrões de operação. 

É muito útil para projetos que seguem o padrão normal de navegação, e muito interessantes para gerenciar a operação de registros em transações.

