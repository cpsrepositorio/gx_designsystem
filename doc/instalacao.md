# PROCEDIMENTO DE INSTALAÇÃO (SETUP)

Para utilizar os componentes será necessário instalar o pacote UC em sua última versão disponível. 

## BootstrapClick
As interceptações dos cliques na interface é por meio do UserControl BootstrapClick.
Para utilizar será necessário instalar no Genexus, através do procedimento a seguir.

1. Descompactar o arquivo bootstrapclick.zip em uma pasta
2. Descompactar o arquivo, vai gerar uma pasta BootstrapClick e dentro dela alguns arquivos (UserControl)
3. Fechar o Genexus
4. Abrir um CMD do Windows e posicionar na pasta C:\Program Files (x86)\GeneXus\GeneXus18\UserControls
5. Copiar a pasta BootstrapClick com os arquivos dentro da pasta C:\Program Files (x86)\GeneXus\GeneXus18\UserControls
5. Retorne a pasta C:\Program Files (x86)\GeneXus\GeneXus18\ e em seguida executar o instalador: genexus -install

## Criação da Kb de teste
Para utilizar o pacote você pode optar por criar um projeto do zero (criando uma kb), e em seguida o configurando para receber o pacote de componentes.

1) Ligue o Genexus
2) Crie uma Kb, File – New knowledge base, dando o nome de GrupoEstudosGx18, selecionando em Prototyping: .Net Framework e Sql Server

## Instalação do pacote UC
Obtenha a última versão do pacote de modulos e o instale a partir dos seguintes procedimentos.

1) Abra no Gx o Knowledge Manager->Manage Module References.
2) Selecione do lado esquerdo a opção LOCAL, e com o botão direito do mouse, selecione UPLOAD FROM FILE
3) Aponte para o arquivo OPC do pacote de controles. O arquivo possui um nome similar a UC_nn.nnn.nn onde os valores de n refletem a versão do componente, como por exemplo: UC_18.1.9.20.opc. Neste documento você encontrará a última versão do pacote: [uc distribuição](/recursos/uc.md)
4) Uma vez selecionado pressione INSTALL
5) Aguardar o término da instalação.
6) Uma pasta aparecerá no KB EXPLORER - REFERENCES - UC, que conterá os elementos (readonly) importados do arquivo OPC.


## Executar a KB

1) Para completar a operação execute a KB para criar a pasta WEB
2) No menu, selecione Tools -> Explore Target Environment Directory para abrir a pasta WEB. 
3) Copiar a pasta STYLE nessa pasta, descompactando o arquivo UC_nn.nn.nn.zip. Nos arquivos descompactados localiza uma pasta chamada STYLE.
4) O projeto, neste ponto está configurado para iniciar os trabalhos.

## Atualização do pacote UC_nn.nn

O pacote de componentes passa por atualizações constantes para incrementar sua capacidade e é sempre importante manter a última versão instalada.
1) Obter o pacote mais atual de componentes, que é um arquivo OPC. Neste documento você encontrará a última versão do pacote: [uc distribuição](/recursos/uc.md)
2)	Em Knowledge Manager, selecione Manage Module References.
3)	Selecione Local e com o botão direito do mouse, selecione Upload from file
4)	Localize o arquivo mais recente do pacote de componentes (opc) em seu compudador.
5)	Va até o fim da lista de módulos e localize o pacote que foi adicionado: UC (versão...), pressione o botão Update
6) Aguarde até que se encerre a instalação
7)	Pode ser que seja necessário atualizar a pasta Style e reimportar o arquivo XPZ.

