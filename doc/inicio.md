# gx_designsystem
O **gx_designsystem** é um recurso para construção de interfaces Web que pode ser utilizado em Kbs Genexus (18). O pacote inclui um Package, Classes CSS, SDTs, documentação técnica e exemplos.

Com um olhar excessivamente simplista, a construção de uma interface em Genexus segue um ritual de inserir controles em um editor estranho, e em seguida configurar suas propriedades. O conteúdo, as ações, formas, são, de certa maneira, limitados pelas caracteristicas do proprio controle.

O editor é meio esquisito porque é conceitual e não reflete exatamente como será a interface final, é usado mais ou menos para definir os controles que precisamos para montar nossa interface e só isso. É chamado de Abstract Editor, portanto, precisamos abstrair bastante para imaginar como será a interface. Alguns controles nesse editor, como Grid, são até mesmo visiveis, mas nem todos tem um comportamento mais visual.

Para se obter interfaces diferentes, é necessário produzir novos 'controles', que nesse caso se chamam 'user controls'. Mas este é um cenário pouco flexível e bastante complexo.

O ponto favorável é que Genexus busca o nivel hard de automatização para o desenvolvedor e já realiza a maioria do trabalho, o desfavorável é a baixa flexibilidade. Porém, ao longo do tempo, várias características foram incorporadas para aumentar o nivel de liberdade dos desenvolvedores.A história de Genexus é bem interessante e sob o ponto de vista das interfaces, temos aqui uma [pequena referência](doc/genexus.md).

Para quem nunca trabalhou com Genexus este modelo será mais simples, mas será necessário entender um pouco do contexto, principalmente porque estamos descolando um pouco do cenário tradicional, buscando criar [interfaces diferentes](/doc/interfacesdiferentes.md), deixando um pouco de lado o caminho da produção 'automatica' das coisas pelo Genexus, mas buscando criar um modelo de interface mais dinâmica, ágil, leve e padronizada.

## como começar?

* Começe entendendo [o que é](/doc/oquee.md)
* Instale o pacote na sua kb Genexus [instalacao](/doc/instalacao.md)
* Vamos para o [alomamae](/doc/alomamae.md)
* Infelizmente tem coisas esquisitas para aprender como [eventos](/doc/eventos.md), por exemplo.
* Depois vamos ao checklist para os herois que desejam contribuir com seu benvindo esforço: [o que falta fazer](/doc/oquefalta.md)

## agora vamos ao nivel master
Depois de feitas as devidas apresentações, vamos evoluir para um nivel superior, tratando carga de registros, estratégias de interface, estratégias de encriptação.

*  [Estratégias](/doc/tecnicas/tec_estrategias.md)
*  [Estratégias de carga de registros](/doc/tecnicas/tec_estrategiascarga.md)
*  [Estratégias de interface](/doc/tecnicas/tec_estrategiasinterface.md)
*  [Estratégias de controle de eventos](/doc/tecnicas/tec_estrategiaseventos.md)