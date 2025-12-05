# Setup

Para utilizar os componentes será necessário instalar o pacote UC em sua última versão disponível. 

## BootstrapClick
As interceptações dos cliques na interface é por meio do UserControl BootstrapClick.
Para utilizar será necessário instalar no Genexus, através do procedimento a seguir.

1. Descompactar o arquivo [bootstrapclick.zip](https://raw.githubusercontent.com/cpsrepositorio/gx_designsystem/refs/heads/main/recursos/BootstrapClick.zip) em uma pasta no seu computador
2. Descompactar o arquivo, vai gerar uma pasta BootstrapClick e dentro dela alguns arquivos (UserControl)
3. Fechar o Genexus
4. Abrir um CMD do Windows e posicionar na pasta C:\Program Files (x86)\GeneXus\GeneXus18\UserControls
5. Copiar a pasta BootstrapClick com os arquivos dentro da pasta C:\Program Files (x86)\GeneXus\GeneXus18\UserControls
5. Retorne a pasta C:\Program Files (x86)\GeneXus\GeneXus18\ e em seguida executar o instalador: genexus -install

## Criação da Kb de teste
Para utilizar o pacote você pode optar por criar um projeto do zero (criando uma kb), e em seguida o configurando para receber o pacote de componentes.

1) Ligue o Genexus
2) Crie uma Kb selecionando em Prototyping: .Net Framework e Sql Server
3) Crie os Webpanels para testar os componentes

## Instalação do pacote de componentes
Obtenha a última versão do pacote de modulos e o instale a partir dos seguintes procedimentos.

1) Baixe a última versão do pacote de componentes [UC.zip](https://raw.githubusercontent.com/cpsrepositorio/gx_designsystem/refs/heads/main/recursos/UC.zip)
2) Abra no Gx o Knowledge Manager->Manage Module References.
3) Selecione do lado esquerdo a opção LOCAL, e com o botão direito do mouse, selecione UPLOAD FROM FILE
4) Aponte para o arquivo OPC do pacote de controles. O arquivo possui um nome similar a UC_nn.nnn.nn onde os valores de n refletem a versão do componente, como por exemplo: UC_18.1.9.20.opc. 
5) Uma vez selecionado pressione INSTALL
6) Aguardar o término da instalação.
7) Ao término, se no ZIP for disponibilizado um arquivo XZP, realize também a importação do mesmo no Knowledge Manager - Import, em seguida localize o arquivo XPZ e o importe.

## Configure as classes de estilo e execute a Kb

1) Antes de executar ainda teremos que configurar a carga dos arquivos de estilo
2) Observe os detalhes apontados no [Classes de estilo](/doc/classes.md)
3) Esta operação é importante, senão os objetos serão apresentados incorretamente na interface.
4) Assim que configurar, execute a Kb e inicie o projeto.

## Atualização do pacote UC_nn.nn

O pacote de componentes passa por atualizações constantes para incrementar sua capacidade e é sempre importante manter a última versão instalada.
Desta forma será necessário realizar a atualização do pacote de tempos em tempos, baixando a última versão [UC.zip](https://raw.githubusercontent.com/cpsrepositorio/gx_designsystem/refs/heads/main/recursos/UC.zip)
Cuidado porque pode ser que tenhamos que atualizar os SDTs também, além do pacote.

