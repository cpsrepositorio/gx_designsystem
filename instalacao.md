PROCEDIMENTO DE INSTALAÇÃO

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


## CRIAR KB DE TESTE
Para utilizar o pacote você pode optar por criar um projeto do zero (criando uma kb), e em seguida o configurando para receber o pacote de componentes.

1) Ligue o Genexus
2) Crie uma Kb, File – New knowledge base, dando o nome de GrupoEstudosGx18, selecionando em Prototyping: .Net Framework e Sql Server

## INSTALAR O PACOTE UC
Obtenha a última versão do pacote de modulos e o instale a partir dos seguintes procedimentos.

1) Abra no Gx o Knowledge Manager->Manage Module References.
2) Selecione do lado esquerdo a opção LOCAL, e com o botão direito do mouse, selecione UPLOAD FROM FILE
3) Aponte para o arquivo OPC do pacote de controles. O arquivo possui um nome similar a UC_nn.nnn.nn onde os valores de n refletem a versão do componente, como por exemplo: UC_18.1.9.20.opc
4) Uma vez selecionado pressione INSTALL
5) Aguardar o término da instalação.
6) Uma pasta aparecerá no KB EXPLORER - REFERENCES - UC, que conterá os elementos (readonly) importados do arquivo OPC.


## CRIAR KB DE TESTE
7) 


5. Va até o fim da lista e localize o pacote que foi adicionado: UC (última versão), pressione o botão Install
6. Ao término da instalação já será possível visualizar o pacote: References - UC
7. Instalar o XPZ: Em Knowledge Manager, selecione Import, pressione o botão …, e selecione o arquivo UC_nn.nn.nn.xpz
8. Execute o Genexus, ele vai solicitar que se crie um database. Edit Connection, selecione o banco de dados, usuário, senha, e o nome do banco do projeto, e em seguida clique no link CreateDatabase, Ok e Finish
 
9. Pressionar Create para criar a tabela Lixo_teste
 
10. Importar as classes de estilo dos componentes. Para isso abrir a pasta web e copiar a pasta style. No menu, selecione Tools -> Explore Target Environment Directory. 
11. Descompactar o arquivo UC_18.1.9.3.zip que vai criar uma pasta chamada UC_18.1.9.3. Dentro desta pasta haverá uma outra pasta chamada style. Copie esta pasta e cole no diretório da pasta web aberto no item 11.
 
12. A pasta style tem os CSS’s que dão forma aos componentes.
13. Vamos executar um webpanel para testar se está tudo ok, selecione na lista Launchpad, o objeto uc_botao
1.3. Criando um webpanel para testar os componentes
1. Na kb recém-criada, crie um webpanel.
2. Altere a propriedade do objeto colocando em WebMasterPanel o valor (None)
3. Selecione Toolbox e inclua um Textblock. Em seguida clique sobre este e pressione F4 para alterar a propriedade para Format: HTML
4. Na área Events do objeto, crie um Event Start.

Event Start
   …	
Endevent
5. Dentro deste evento programe:
Event Start
                 textblock1.caption = ‘<div style=”border:1px solid red;”>teste</div>’
              Endevent
6. Salve o objeto
7. Execute o Genexus

1.4. Atualizando o pacote de componentes
O pacote UC pode passar por diversas atualizações para incrementar sua capacidade. Para atualizar para as versões mais recentes é necessário.
1.	Obter o pacote mais atual de componentes, que é um arquivo OPC
2.	Em Knowledge Manager, selecione Manage Module References.
3.	Selecione Local e com o botão direito do mouse, selecione Upload from file
4.	Localize o arquivo mais recente do pacote de componentes (opc) em seu compudador.
5.	Va até o fim da lista de módulos e localize o pacote que foi adicionado: UC (versão...), pressione o botão Update
6.	Aguarde até que se encerre a instalação
7.	Pode ser que seja necessário atualizar a pasta Style e reimportar o arquivo XPZ.
