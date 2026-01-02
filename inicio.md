# gx_designsystem

O **gx_designsystem** é um recurso para construção de interfaces Web que pode ser utilizado em Kbs Genexus (18). O pacote inclui um Package, Classes CSS, SDTs, documentação técnica e exemplos, que auxilia na construção de interfaces em Genexus de forma mais simples. 

## Começando
 A seguir apresentamos uma trilha básica para iniciar na utilização do pacote de componentes:
 
1. Começe entendendo [o que é](/doc/oquee.md) o gxdesignsystem
2. Instale os recursos necessários na sua kb Genexus [instalacao](/doc/instalacao.md)
3. Vamos para o importante [alomamae](/doc/alomamae.md) para ver como tudo funciona
4. Planeje e construa sua interface [webpanel](/doc/tecnicas/tec_webpanel.md)
5. Entenda sobre Flex layout, Sections e classes de dimensionamento e margens, [Sections e Classes](doc/tecnicas/tec_sectionseclasses.md).
6. Voce também precisa entender sobre a carga das classes de estilo [Carga das classes](doc/classes.md)
7. Estude e utilize os controles, aqui tem uma lista: [indice de controles](/doc/indexcontrole.md)
8. Infelizmente tem coisas esquisitas para aprender, [eventos](/doc/eventos.md), por exemplo.
9. Depois que ficar craque no assunto vamos ao checklist para os herois que desejam contribuir no projeto [o que falta fazer](/doc/oquefalta.md)

Temos uma trilha em formato de vídeo.

| Assunto        |  Link                                      | Conteúdo                                                                          |
|----------------|--------------------------------------------|-----------------------------------------------------------------------------------|
| Botão icone    | [**Aula 1**](https://youtu.be/54zNXZInaas) | Apresentação da construção de uma interface simples com botão em formato de ícone|
| Card           | [**Aula 2**](https://youtu.be/LTCTCcN7U1w) | Apresentação da construção de um simples card|
| Card (toolbox) | [**Aula 2**](https://youtu.be/NwLOJCMSus4) | Finalização da apresentação dos cards, incluindo um toolbox com alinhamento centralizado|
| Card destaque  | [**Aula 3**](https://youtu.be/fhbMoOUoC4E) | Apresentação de cards para apresentação de valores destacados|
| Lista          | [**Aula 4**](https://youtu.be/KFRgNyHNNAk) | Apresentação de conteúdo em formato de lista|
| Tabela         | [**Aula 5**]() | Apresentação de conteúdo em formato de tabela|


Temos também alguns exemplos que podem te ajudar a planejar sua interface:
1. [Estratégias de interface](/doc/tecnicas/tec_estrategiasinterface.md), sobre Master page, Webnel, Webcomponent, sidebar, navbar
2. [Como organizar o webpanel](gx_designsystem/doc/tecnicas/tec_comoorganizarowebpanel.md), sobre estrutura principal do sistema, evento start, load, grid, eventos.

Depois das devidas apresentações, vamos evoluir para um nivel superior, tratando carga de registros, estratégias de interface, estratégias de encriptação.

*  [Estratégias](/doc/tecnicas/tec_estrategias.md)
*  [Estratégias de carga de registros](/doc/tecnicas/tec_estrategiascarga.md)
*  [Estratégias de controle de eventos](/doc/tecnicas/tec_estrategiaseventos.md)

## Interfaces com Genexus
Com um olhar excessivamente simplista, a construção de uma interface em Genexus segue um ritual de inserir controles em um editor estranho, e em seguida configurar suas propriedades. O conteúdo, as ações, formas, são, de certa maneira, limitados pelas caracteristicas do proprio controle. O editor é meio esquisito porque é conceitual e não reflete exatamente como será a interface final, é usado mais ou menos para definir os controles que precisamos para montar nossa interface e só isso. É chamado de Abstract Editor, portanto, precisamos abstrair bastante para imaginar como será a interface. Alguns controles nesse editor, como Grid, são até mesmo visiveis, mas nem todos tem um comportamento mais visual.

Para se obter interfaces diferentes, é necessário produzir novos 'controles', que nesse caso se chamam 'user controls'. Mas este é um cenário pouco flexível e bastante complexo.

O ponto favorável é que Genexus busca o nivel hard de automatização para o desenvolvedor e já realiza a maioria do trabalho, o desfavorável é a baixa flexibilidade. Porém, ao longo do tempo, várias características foram incorporadas para aumentar o nivel de liberdade dos desenvolvedores.A história de Genexus é bem interessante e sob o ponto de vista das interfaces, temos aqui uma pequena referência.

Para quem nunca trabalhou com Genexus este modelo será mais simples, mas será necessário entender um pouco do contexto, principalmente porque estamos descolando um pouco do cenário tradicional, buscando criar interfaces diferentes, deixando um pouco de lado o caminho da produção 'automatica' das coisas pelo Genexus, mas buscando criar um modelo de interface mais dinâmica, ágil, leve e padronizada.
