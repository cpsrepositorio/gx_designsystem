# O que é
O **Designsystem** é um conjunto de controles HTML + CSS, e em alguns casos JS, criados pela chamada de procedures padrões. Cada procedure cria um certo componente de interface que pode ser utilizado nos sistemas Genexus. Este conjunto de procedures é empacotado em um Package, e as versões são distribuídas para os desenvolvedores.

Os packages são arquivos com extensão OPC, que são, na prática DLLs que são criadas pelo Genexus para serem incorporadas em outros projetos Genexus. É o mesmo conceito de biblioteca de funções. Ao instalarmos esse pacote na KB adicionamos funcionalidades ao Genexus.

## Porque preciso disso?
Desenvolver interfaces em Genexus é pouco produtivo se você não estiver utilizando os Patterns, pois cada interface deve ser definida em termos de controles padrões, em seguida configurações, e depois carga de dados. Muitas vezes o desenvolvedor gasta uma energia imensa para produzir coisas muito simples que em linguagens tradicionais como C#, PHP, ou outra similiar, se faria com uma única linha de código. O resultado é um pouco de frustração.

O **gxdesignsystem** oferece os recursos para criar os controle, como BOTõES, TABELAS, MENUS, que são criados a partir do padrão que foi programado na procedure, com as classes CSS previamente definidas. O resultado é um controle na interface do usuário, criado de forma mais simples que a programação Genexus tradicional.

Este modelo automatiza a construção da interface, padroniza, simplifica manutenção, simplifica o design system entre diversos projetos, produz a operação de tratamento de eventos, incrementa segurança, ou seja, é um cenário que produz a forma, sustentação e operacionalização para interfaces. Quando se produz ajustes em um controle e um novo pacote é gerado, todos os sistemas que atualizarem seu pacote aplicarão os ajustes produzidos.

Para inserir os controles na interface será necessário um simples controle Textblock (html), que recebe o retorno da procedure. Dessa forma, as interfaces criadas a partir deste modelo são muito mais simples, e não exige muitas configurações e instalações adicionais, como a utilização dos User Controls tradicionais.

Uma outra vantagem desse modelo é que todos os projetos que utilizam o package (exteensão OPC) acabam produzindo interfaces padronizadas, e no caso de alguma alteração no pacote, todas passam a refletir os ajustes.

## Configuração do controle
Associado ao controle teremos sempre um tipo SDT que oferece os parametros necessários para a sua construção do controle.
Para facilitar um pouco, o nome da procedure é semelhante ao nome do SDT. Por exemplo, para o controle **uc_botao** temos um SDT **uc_botaoIN** que oferece as propriedades para se criar um botão.

Veja um exemplo que cria um Botão.
```
&botao = new()
&botao.evento = 'ABRIR:1'
&botao.icone = '<i class="fas fa-eye"></i>'
&botao.titulo = 'Abrir'
&botao.tooltip = 'Abrir o registro'

&uc_botaoin.id = 'id'
&uc_botaoin.interface = 'interface'	
&uc_botaoin.botoes.Add(&botao)
	
textblock1.Caption = UC.uc_botao(&uc_botaoin.ToJson())
```
Os detalhes das propriedades que precisam ser informadas são apresentados nos exemplos disponíveis nessa documentação.



