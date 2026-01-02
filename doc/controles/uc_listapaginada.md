# uc_listapaginada
A lista paginada é um controle tipo lista que apresenta páginas de registros ao invés da carga completa da tabela,  cabendo ao usuário a ação de solicitar a próxima página ou a anterior que deseja ser carregada.

O controle é bastante simples, porém necessita de recursos adicionais para a carga dos registros.

No evento **Start** se deve definir a página inicial e o tamanho da página e a rotina de 'load' deve ser acionada.
```
&pg = 1		
&pgsize = 10	
do 'load'	
``` 

## Data provider
O controle precisa de um **DataProvider** que faça a carga dos registros de forma paginada, de forma que ocor
Para simplificar, utilize um SDT que possa ser carregado por etapas.

```
cargaSDT [count=&pgsize][skip=(&pg-1)*&pgsize]
order Id
where Id =&id when &id<>0
{
 Id			
 Nome		
 Foto		
 Endereco	
 Cidade
}
```
O **count=&pgsize** determina o total de registros a ser retornado, e **skip=(&pg-1)*&pgsize** calcula o primeiro registro da lista em função da pagina a ser carrega.
Na chamada ao DataProvider se deve passar o **&pgsize** que é fixado no Start, e o **&pg** que altera conforme a navegação do usuário. 
O DP inclui um filtro para o caso do usuário queira filtrar um registro.

```
sub 'load'
 &registros.Clear()
 &registros = cargaDP(&id, &pgsize, &pg)
 do 'grid'
endsub
```

|var|tipo|
|-----------------|---------------------------|
|&registros | cargaSDT collection|


A chamada ao **cargaDP** retorna os registros da página carregada, e aqui podemos acionar um truquezinho, e utilizar um SDT padrão para não ter que criar, para cada tabela uma estrutura específica. Lembre-se que o controle é uma lista que apresenta um titulo apenas, portanto, não precisariamos de um tipo específico. Ver [row](/doc/tecnicas/row.md) para maiores detalhes

## Montagem da lista
A lista de registros é carregada para o controle **uc_listapaginada**, que inclui algumas propriedades adicionais.

| propriedade 			|  conteúdo     |  significado |
|-----------------------|---------------|-----------------------------|
| &uc_listin.pagging 	|true           | liga a operação de paginação|
| &uc_listin.paggingposition | uc_position.bottom| posiciona os botões na parte inferior do controle. |
| &uc_listIN.paggingpgsize	|&pgsize| tamanho da página, ou a quantidade de registros a ser apresentada ao usuário |
| &uc_listIN.paggingpg		|&pg| página corrente sendo apresentada, iniciando com um (1) e éatualizada quando ocorre a paginação.|
| &uc_listIN.paggingtrec	|count(nome)| total de registros da tabela que está sendo paginada. Um Count(<nome do atributo>) já retorna o total de registros de uma tabela.|

O **for &reg in &registros** percorre a lista de registros retornado pelo DataProvider, e o inclui na lista.
O total de registros da tabela deve ser informado através de **&uc_listIN.paggingtrec**, que pode ser facilmente obtido pelo **count(nome_do_atributo)**, sendo que é importante informar um atributo secundário da tabela que se deseja recuperar.
O controle vai dividir o total de registros pelo tamanho das paginas para obter a última pagina, e assim realizar o controle de incremento até chegar ao final.
```
sub 'grid'
 /* botão INS */
 &uc_botaoiconein.id = 'LISTA'
 &uc_botaoiconein.interface = &Pgmname.ToUpper()
 &botoes.Clear()
 &botoes.Add("NOVO:")
 &uc_botaoiconein.botoes = &botoes.ToJson()

 /* lista de registros */
 &uc_listin.id = 'LISTA'
 &uc_listin.interface = &Pgmname.ToUpper()
 &uc_listin.pagging = true
 &uc_listin.paggingposition = uc_position.bottom
 &uc_listIN.paggingpgsize = &pgsize
 &uc_listIN.paggingpg = &pg
 &uc_listIN.paggingtrec = count(nome)
 &uc_listin.toolbox  = UC.uc_botaoicone(&uc_botaoiconein.ToJson())
 &uc_listin.classetoolbox = 'uc_flex-r uc_flex-jce uc_mb10' 

 /* carga dos registros da lista */
 &uc_listin.itens.Clear()
 for &reg in &registros
  &uc_botaoiconein = new()
  &uc_botaoiconein.id = 'LISTA'
  &uc_botaoiconein.interface = &Pgmname.ToUpper()
  &uc_botaoiconein.classebar = 'uc_flex-r uc_flex-nowrap'
  &uc_botaoiconein.classebotao = 'uc_btspace uc_bt-icon uc_pointer'
  &uc_botaoiconein.classeicon = ''
  &botoes.Clear()
  &botoes.Add("EDITAR:")
  &botoes.Add("APAGAR:")
  &uc_botaoiconein.botoes = &botoes.ToJson()
		
  &item = new()
  &item.titulo = &reg.Nome.ToUpper().Trim()
  &item.tooltip = &reg.Nome.ToUpper().Trim()
  &item.evento = 'ABRIR:'+&reg.Id.ToString().Trim()
  &item.imagem.classe  = 'uc_imagemredonda15px'
  &item.imagem.image = &reg.Foto.Trim()
  &item.imagem.tooltip = &reg.Nome.ToUpper().Trim()
  &item.toolbox = UC.uc_botaoicone(&uc_botaoiconein.ToJson())
  &uc_listin.itens.Add(&item)

 endfor
 html.Caption = UC.uc_listapaginada(&uc_listin.ToJson())
endsub
```

|var|tipo|
|-----------------|---------------------------|
|&registros | cargaSDT collection|
|&reg | cargaSDT |
|&uc_botaoiconein | uc_botaoiconein|
|&botoes|varchar(40) collection|
|&uc_listin|uc_listin|
|&item|uc_listin.item|


## Evento de paginação
A paginação no controle exige mais um pequeno detalhe, na interceptação do Bootstrapclick.

Observe se o controle que causou o evento é chamado de 'PAGGING', e em caso positivo, deve-se obter a página que o usuário selecionou, e o 'load' para recarregar os registros.

```
case  &uc_btclickparms.Item(uc_btitem.controle) = 'PAGGING'
 &pg = &uc_btclickparms.Item(uc_btitem.parm1).ToNumeric()
 do 'load'
```
O controle de qual página o controle vai acionar é definido pelo **uc_listapaginada**, que já calcula e determina no próprio botão.
```
Event Bootstrapclick1.Click
 &uc_btclick = Bootstrapclick1.ButtonId
 navEvent2(&uc_btclick, &uc_btclickparms, &url, &isok)
	
 do case 
  case  &uc_btclickparms.Item(uc_btitem.controle) = 'PAGGING'
   &pg = &uc_btclickparms.Item(uc_btitem.parm1).ToNumeric()
   do 'load'
  endcase

  msg(
   ' interface:'	+ &uc_btclickparms.Item(uc_btitem.interface)
  +' controle:'	+ &uc_btclickparms.Item(uc_btitem.controle)
  +' acao:'		+ &uc_btclickparms.Item(uc_btitem.acao)
  +' parametro:'	+ &uc_btclickparms.Item(uc_btitem.parm1)
  )
EndEvent
```

|var|tipo|
|-----------------|---------------------------|
|&pg | numeric(4)|
|&uc_btclickparms | uc_btclickparms |
|&uc_btclick | uc_btclick|


