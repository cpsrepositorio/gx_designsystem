# O QUE É UM COMPONENTE
Um componente no pacote UC é uma procedure que produz elementos HTML + CSS e em alguns casos JS que definem a forma do controle na interface. Um conjunto de componentes que produzem conteúdos 'padronizados' são empacotados em uma DLL externa criada por um recurso chamado Package em Genexus. O resultado do empacotamento é um objeto com extensão OPC que poderá ser inserido em qualquer KB.

## Objetivos estratégicos
Desenvolver interfaces em Genexus é pouco produtivo se você não estiver utilizando os Patterns, pois cada interface deve ser definida em termos de controles padrões, em seguida configurações, e depois carga de dados. 

Muitas vezes o desenvolvedor gasta uma energia imensa para produzir coisas muito simples que em linguagens tradicionais como C#, PHP, ou outra similiar, se faria com uma única linha de código. O resultado é um pouco de frustração.

Neste modelo temos uma situação na qual o formato de um certo controle, por exemplo, um BOTÃO, já foi definido. Classes CSS dão a forma visual do controle e a programação de uma procedure a estrutura do botão. É mais simples produzir algo que já foi programado, apenas pela sua chamada do que programar um botão em seu formato original toda vez que se precisa de um. Chama-se a procedure (controle) uc_botao, e o resultado é o código que cria o mesmo com todas as caracteristicas incorporadas.

Este modelo automatiza a construção da interface, padroniza, simplifica manutenção, simplifica o design system entre diversos projetos, produz a operação de tratamento de eventos, incrementa segurança, ou seja, é um cenário que produz a forma, sustentação e operacionalização para interfaces. Quando se produz ajustes em um controle e um novo pacote é gerado, todos os sistemas que atualizarem seu pacote aplicarão os ajustes produzidos.

Para que o componente seja apresentado na interface, será necessário que o resultado de sua chamada seja apresentado em um Textblock em formato HTML. Esta característica, já estabelece um diferencial em relação aos tradicionais User Controls que exigiriam configuração e instalações do Genexus para serem incorporados.

O agrupamento dos componentes em um Package (OPC) também permite que as mesmas não sejam alteradas de forma indiscriminada nas Kbs que os utilizam, mantendo um padrão regular. Pois, caso seja necessário, altera-se a procedure equivalente e se gera uma nova versão do Package para todas as kbs.

O desafio maior é construir controles que sejam uteis e de uso frequente pelos desenvolvedores, alcançar as caracteristicas desejadas, incrementem a usabilidade, a assessibilidade de pessoas PCD e um recurso que automatize a construção do SDT nos controles.


## configuração do controle
Associado ao controle teremos sempre um SDT com os parametros necessários para a sua construção.
O nome deste objeto é o mesmo que o do controle seguido de um IN no final (para determinar INPUT)
Exemplo, para o controle **uc_tabela** temos um SDT **uc_tabelaIN** que permitirá a configuração das propriedades que criam a tabela.

## contribuições
Para contribuir, baixe a kb CEETEPS_DESIGNSYSTEM18 e programe os controles na pasta UC.
