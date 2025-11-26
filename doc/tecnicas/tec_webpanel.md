# Criando um webpanel
Tudo começa com uma interface Web, que em Genexus é definida a partir de um objeto WebPanel, mas não é muito simples de se compreender a principio.

Primeiramente, é necessário compreender que o Genexus é um gerador de código e ele sempre vai querer incluir um monte de coisas a mais, que consideramos desnecessárias e o pior, que atrapalham no design da tela.

## Layout control
O [Abstract Editor](https://docs.genexus.com/en/wiki?25250,How+to+use+the+Abstract+Editor%3A+designing+a+Web+Transaction+Form) do Genexus possibilita criar alguns tipos de layouts para controlar os objetos na interface:
* **Responsive Table**, é o design que segue as regras de estrutura do Bootstrap com suas 12 colunas, e que permite criar [design responsivo(https://docs.genexus.com/en/wiki?29134,Table+of+contents%3AResponsive+Web+Design+in+GeneXus)
* **Flex layout**, é o layout mais flexível (e simples) que permite organizar os objetos em linhas e colunas, aqui temos um artigo de um dos desenvolvedores do Genexus: [galeria de fotos com flex layout](https://genexus.blog/es_ES/design/photosgallery-a-genexus-flex-and-flex-grid-sample/). Aqui um guia completo [A guide to flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
* **Canvas**, é um layout que permite posicionar os objetos por coordenadas absolutas e mais dedicado a aplicações Smartdevices. [Canvas control](https://docs.genexus.com/en/wiki?22452,Canvas+control)
* **Smart table**, é um layout que permite construir áreas na interface como uma tabela. [Smart tables](https://docs.genexus.com/en/wiki?45577,Smart+Table+control)
* **Tabular table**, é o design mais simples que define layout por tabelas tradicionais (<table>)

Utilizamos com maior frequencia o **flex layout** em nossos sistemas.
