# Row
Que tal ter apenas um SDT para recuperar os dados de todas as tabelas do sistema? Isso é o buscamos fazer com o **row**, e com isso otimizar a programação.

Praticamente precisamos de um campo que possa representar a chave da tabela, e temos três possíveis: **Id** (numeric), **IdText** (Character) e **Guid**.

```
ROW {
 Id
 IdText
 Guid
 Nome
 Descricao
 Link
 Flag
}
```
Em seguida precisamos de um texto para apresentar nos controles, **Nome** ou **Descrição**. Eventualmente algum **Link** para alguma ação especial. E um **Flag** para indicar se o registro está apagado ou não.

Com isso, conseguiremos carregar os dados de qualquer tabela e apresentar em controles do tipo Lista. 

Quando falamos de Tabelas, dai a conversa é outra, pois novas colunas serão necessárias e o Row provavelmente limitará a operação. Neste caso, compensa criar um SDT próprio.

## Utilizando o Row
Precisaremos basicamente de uma coleção de Row que normalmente chamamos de **&Rows**, e esta será recebida no DataProvider de carga. Algo semelhante ao apresentado a seguir.

```
 &rows = OpcoesDP(&op, &pgsize, &pg)
```
O DataProvider OpcoesDP é bem simples de ser montado, seguindo um padrão. 

1) O tipo de retorno do DP deve ser Row e Collection=true
2) Defina nos campos Id, Titulo e Flag os valores dos campos da tabela desejada
3) Não esqueça do Count e Skip, caso esteja utilizando o controle uc_listapaginada.

```
Row  [count=&pgsize][skip=(&pg-1)*&pgsize]
from OPCOES
order OpcaoId
where OpcaoId = &Id when &Id>0
{
	Id = OpcaoId
	Titulo = OpcaoTitulo
	Flag = OpcaoApagado
}

```

Para montar a lista, basta percorrer a coleção de registros obtida do DP, adicionando ao controle.
```
 for &row in &rows 
   &item = new()
   &item.titulo = &row.Titulo
   &item.evento = 'ABRIR:'+&row.Id.ToString()
   &item.strikethrough = &row.Flag
   uc_listin.itens.add(&item)
 endfor
```
### Informações adicionais
Temos mais uma otimização à sua disposição, veja a procedure [GridGET](/doc/tecnicas/tec_gridget.md)


