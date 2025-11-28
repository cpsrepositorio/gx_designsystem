# Criando webpanel´s
Tudo começa com uma interface Web, que em Genexus é definida a partir de um objeto WebPanel, mas não é muito simples de se compreender a principio.

Primeiramente, é necessário compreender que o Genexus é um gerador de código e ele sempre vai querer incluir um monte de coisas a mais, que consideramos desnecessárias e o pior, que atrapalham no design da tela.

Para reduzir o trabalho de configuração, utilizamos com maior frequencia o **flex layout** em nossos sistemas (mais informações [aqui](/doc/layout.md)).

## Section, Textblocks e BootstrapClick
Outro objeto importante para adicionar em nosso projeto de interface são os controles **Section** do Genexus, que produzem **<div>...</div>** na interface.
Utilizaremos as sections para organizar agrupamentos de controles na interface.
Os **textblocks** são os controles que utilizaremos para apresentar o conteúdo que criamos no sistema.
O **BootstrapClick** é o controle de evento de Click dos nossos componentes.

## Exemplo completo
Nesse exemplo, padrão para interfaces com o controle de lista, temos um conjunto de Sections e alguns textblocks.

![padrao](https://raw.githubusercontent.com/cpsrepositorio/gx_designsystem/refs/heads/main/doc/imagens/uc_padrao.png)

**Sections**
(1) tb_titulo
(2) tb_toolbox
(3) tb_content
(4) tb_detail
(5) tb_search

E dentro das sections, os **textblocks**:
(1) titulo
(2) buttonbar
(3) alerta e grid
(5) icone

A interface opera para carregar os textblocks com conteúdos.

O programa é constituido por três áreas:

* **ESTRUTURA DA INTERFACE**, define as maneiras que a interface se comporta conforme a operação que será realizada pelo usuário.
* **CARGA DE DADOS**, define a carga dos registros nas tabelas e em seguida a montagem do **grid**
* **CONTROLE DE EVENTOS**, define as ações dos usuários.

```
Event Start
 form.HeaderRawHTML = uc_carga()
	
 /* estrutura da informação */
 &pg = 1
 &pgsize = 5
	
 /* controles em modo default */
 do 'seguranca'
 do 'load'
Endevent

/* ------------------------ ESTRUTURA DA INTERFACE -------------------------- */
sub 'seguranca'
//	segurancaGET(&Pgmname)
	
 /* detalhes do programa */
 &HelpSDT= HelpGET(&Pgmname)
 &uc_tituloin.titulo = &HelpSDT.HelpTitle
 &uc_tituloin.tituloclasse = 'uc_title'
 &uc_tituloin.texto = &HelpSDT.HelpText.Trim()
 &uc_tituloin.textoclasse = 'uc_titletext'
 &uc_tituloin.textovisible = false
 titulo.Caption = UC.uc_titulo(&uc_tituloin.ToJson())
endsub

sub 'ui_modo_default'
 alerta.Caption = ''
 grid.Caption 	= ''
 icone.Caption 	= '<i class="fas fa-filter uc_pr10"></i>'
 &search.Visible = 1
 tb_detail.Visible = 0
	
 &ButtonBarSDT.programa  	= &Pgmname
 &ButtonBarSDT.inserir	= true
 &ButtonBarSDT.fechar	= false
 &ButtonBarSDT.detalhe	= false
 &ButtonBarSDT.doc      	= false
 do 'ui_buttonbar'
endsub

sub 'ui_modo_detail'
 alerta.Caption = ''
 grid.Caption = ''
 icone.Caption 	= ''
 &search.Visible	= 0
 tb_detail.Visible 	= 1
	
 &ButtonBarSDT.programa  	= &Pgmname
 &ButtonBarSDT.inserir	= false
 &ButtonBarSDT.fechar	= true
 &ButtonBarSDT.detalhe	= false
 &ButtonBarSDT.doc      	= false
 do 'ui_buttonbar'
endsub

sub 'ui_buttonbar'
 &uc_botaoin = ButtonBarGET(&ButtonBarSDT)
 buttonbar.Caption = '<div class="uc_flex-r uc_flex-jce">'+UC.uc_botao(&uc_botaoin.ToJson())+'</div>'
endsub

/* ------------------------ CARGA DE DADOS ----------------------------- */
sub 'load'
 do 'ui_modo_default'
 &rows.Clear()
 &rows = exemploDP(&id, &pgsize, &pg)
 &rows.Sort('Descricao')
 do 'ui_grid'
endsub

sub 'ui_grid'
 &GridViewSDT.id = 'LISTA'
 &GridViewSDT.programa = &Pgmname
 &GridViewSDT.pagging = true
 &GridViewSDT.pg = &pg
 &GridViewSDT.pgsize = 5
 &GridViewSDT.totalrec = count(LIXO_TesteNome)
 &GridViewSDT.typeid = typeid.Numero
 &GridViewSDT.toolbar.inserir = false
 &GridViewSDT.toolbar.abrir  = false
 &GridViewSDT.toolbar.editar = true
 &GridViewSDT.toolbar.apagar = true

 /* apresenta */
 &uc_listin = GridGET(&rows, &GridViewSDT)
 grid.Caption = UC.uc_listapaginada(&uc_listin.ToJson())
endsub

/* ----------------------- CONTROLE DE EVENTOS ---------------------------- */
Event Bootstrapclick1.Click

 &uc_btclick = Bootstrapclick1.ButtonId
 navEvent2(&uc_btclick, &uc_btclickparms, &url, &isok)
 if &isok
  GlobalEvents.MPHOME(&uc_btclickparms)
 endif

 /* eventos */
 do case
  case &uc_btclickparms.Item(uc_btitem.interface)=&Pgmname.toupper()
   do case

    /* botão INSERIR */
    case &uc_btclickparms.Item(uc_btitem.acao)='INSERIR'
     do 'ui_modo_detail'
     &id = 0
     component1.Object = LIXO_Teste.Create(trnmode.Insert, &id)

    /* botão EDITAR */
    case &uc_btclickparms.Item(uc_btitem.acao)='EDITAR'
     do 'ui_modo_detail'
     &id = &uc_btclickparms.Item(uc_btitem.parm1).ToNumeric()
     component1.Object = LIXO_Teste.Create(trnmode.Update, &id)

    /* botão APAGAR */
    case &uc_btclickparms.Item(uc_btitem.acao)='APAGAR'
     &id = &uc_btclickparms.Item(uc_btitem.parm1).ToNumeric()
     &LIXO_Teste.Load(&id)
     &LIXO_Teste.Delete()
     if &LIXO_Teste.Success()
      commit
      do 'load'
     else
      msg('Erro '+&LIXO_Teste.GetMessages().Item(1).Description)
     endif

    /* botão PAGGING */
    case &uc_btclickparms.Item(uc_btitem.controle)='PAGGING'
     &pg = &uc_btclickparms.Item(uc_btitem.parm1).ToNumeric()
     do 'ui_modo_default'
     do 'load'

   endcase
 endcase
EndEvent

Event Enter
 do 'load'
Endevent

```

## Master page
Para aumentar a capacidade da interface, continue a programação incluindo uma [master page](doc/tecnicas/tec_masterpage.md)

