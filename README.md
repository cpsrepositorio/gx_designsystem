# gx_usercontrol
Tradicionalmente a construção de interfaces no Genexus são baseadas em controles padrões [Genexus Controls](https://wiki.genexus.com/commwiki/wiki?5925,Category%3AGeneXus+Controls), que permitem fazer o básico em termos de apresentar informações, obter dados dos usuários, interceptar eventos. Porém, de certa maneira esse conjunto básico limita absurdamente a capacidade do que a ferramenta poderia fazer. A partir da versao Geneus X um novo recurso chamado UserControl passou a oferecer uma ampliação significativa da capacidade da interface, porém sob um custo alto de complexidade para sua produção. Nas versoes mais recentes um novo objeto [UserControl](https://wiki.genexus.com/commwiki/wiki?39356,Category%3AUser+Control+object) foi apresentado como uma forma de reduzir a complexidade.
A evolução foi significativa, porém, ainda complexa. Uma outra tecnologia interessante [Pattern](https://wiki.genexus.com/commwiki/wiki?2814,Category%3APatterns) completa o time, e foi criada para gerar de forma automática objetos Genexus segundo padrões desejados, normalmente um GRID que abre um registro e suas relações, e vários 'parceiros' comerciais começaram a apresentar soluções para esta tecnologia. Pattern é um gerador de objetos de um gerador de fontes, ou seja, um cenário de fortissima capacidade de produção de interfaces.

De forma reduzida, a construção de uma interface em Genexus exige que se incluam controles na interface e em seguida, ocorra a 'programação' do conteúdo, ação, forma, desses controles. Flexível sob o ponto de se permitir fazer qualquer coisa, porém, dificil pois exige várias abas, propriedades e mecanismos para sua programação.

Desta forma, este repositório oferece uma alternativa para se construir interfaces, de forma totalmente 'programativa', ou seja, deixou-se de lado a preocupação visual da inclusão do controle na interface, e em contrapartida, objetivou-se que apenas um único TEXTBLOCK fosse suficiente para construir praticamente a interface inteira. Pode haver um certo exagero nesta frase, me desculpe. Mas na prática, temos um modelo em que temos controles com certo nivel de padronização, que se constrói a partir de propriedades fornecidas em um formato JSON.

De todos os modelos que estudei até este momento, e que programei ao longo de tantos anos com a ferramenta, me parece que este cenário é o mais eficiente e rápido. Porém, compreendo que seria muito bom se tivessemos associado a este cenário um modelo de produção de objetos automatizados com o Pattern. Fica a dica para a próxima evolução.

Neste repositório voce encontrara informações para construir interfaces interessantes utilizando este modelo difernte.

## UC
É o nome pouco criativo que escolhemos para denominar esse pacote de componentes, para fazer um minimo de referencia ao termo User Control da ferramenta, mas na prática, as semelhanças terminam no nome. O modelo utiliza um único UserControl para interceptar eventos de Click. Uma KB é utilizada para programar os componentes chamada de CEETEPS_DESIGNSYSTEM, que pode ser baixada e manipulada para ajustar os controles, e produzir o Package.

O Package ao ser instalado em qualquer KB permitirá:

1) Geração de componentes em formato simples baseado na definição de SDT, buscando reduzir ao máximo a necessidade de inserção de elementos HTML, CSS. 

2) Entrega de recursos para a montagem de interfaces leves, sem a necessidade de variáveis, ou dados estruturados em tela.

3) Manutenção de uma biblioteca de estilos padronizada e em acordo com o CPS_Elements

4) Encriptação de parametros nas interfaces por meio da definição de uma chave pelo próprio desenvolvedor que poderá ser estatica ou dinamica.

O objetivo deste pacote é acelerar ao máximo a obtenção de componentes, sem que seja necessário programação excessiva, além de promover a padronização da interface para auxiliar o usuário.

Seguindo a filosofia Gx de automatizar ao máximo os recursos para se alcançar resultados rápidos e satisfatórios, o pacote entrega uma parte importante que é a automação das interfaces.

1) Genexus cuida da operação de banco de dados, da modelagem, relacionamento, estrutura da operação, com a recuperação, inserção, manutenção dos registros.

2) UC cuida da construção das interfaces.

## ESTILO
Os controles são desenvolvidos através de elementos tradicionais de HTML + CSS. Para compatibilizar as versões das folhas de estilo (CSS), de maneira que todas as soluções utilizem as mesmas definições, adotou-se a publicação dos diversos arquivos em um repositório centralizado. E neste local encontram-se todos os arquivos na sua última versão.

Para realizar a carga das folhas de estilo é necessário chamar um procedimento:

	`form.HeaderRawHTML  = uc_css()`

E neste 

´&stylepath = &websession.get('STYLEPATH')
if &stylepath.IsEmpty()
	&stylepath = Config_STYLEPATH_GET()
	&websession.Set("STYLEPATH", &stylepath.Trim())
endif

&html  = UC.uc_cssCARGA(&stylepath) 
´

## PRIMEIROS PASSOS
Para saber mais a respeito deste pacote sugerimos, e iniciar nos primeiros passos no uso dos componentes, sugerimos as seguintes leituras:

**Para utilizar o componente** 
1) Acesse a documentação da estrutura de user controls disponiveis, instale o pacote de componentes na sua KB e inicie a operação. [Informações aqui](/doc/instalacao.md).
2) Crie um painel de testes e comece a utilizar [Painel de teste](/doc/primeiropainel.md)
3) Se tiver interesse em saber o que é um componente, temos este texto [O que é?](oquee.md)

**Para participar da construção**
Baixe a KB CEETEPS_DESIGNSYSTEM no Genexus 18 e auxilie na construção dos recursos. Informações aqui.

**Para atuar na modelagem visual (css)**
Altere o conteúdo dos arquivos CSS da pasta style e publique no repositório de estilos. Informações aqui.

## APRENDENDO CADA CONTROLE 
Você também pode optar por aprender a operação de cada controle. Um caminho é acompanhar o [índice de controles](/doc/controles/indexcontrole.md)

## TECNICAS 
Em seguida, será interessante você aprender algumas técnicas mais avançadas para integrar controles, estratégias para apresentação. Um caminho é acompanhar o [índice de técnicas](/doc/tecnicas/indextecnica.md) 

## RECURSOS 
Montamos uma pagina para incluir os recursos necessários para trabalhar no pacote UC. [Lista de Recursos](/recursos/indicerecursos.md) 
