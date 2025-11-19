# Encriptação de parâmetros
Na era dos hackers, encriptar coisas é uma forma de 'tentar' diminuir o impacto do roubo de informações ou coisas piores.

Não dá para programar nada sem encriptação nos dias atuais.

No caso do UC os eventos gerados ficam expostos para que curiosos investiguem. Por exemplo, a seguir temos a construção do evento BootstrapClick na interface, e como é possivel observar, temos elementos muito esquisitos, mas também outros bem visiveis e identificáveis.

```
<div class="divTableHead  uc_pointer uc_link" onclick="gx.getObj('', false).getUserControl('BOOTSTRAPCLICK1Container').bootstrapclick('HISTORICOGRID:GRID:ABRIR:ADM001');">Sigla<i class="fas fa-long-arrow-alt-down uc_ml5 uc_textclear"></i></div>
```
Sem muito conhecimento científico, é possível observar uma sequencia importante na linha:

```
('HISTORICOGRID:GRID:ABRIR:ADM001')
```
E é possível intuir, com a ação provocada, que a ação trata-se de ABRIR um registro cujo Id e ADM001.

Melhor se isso seja escondido do usuário.

## Como encriptar eventos

Por incrível que pareça a operação é muito simples para o desenvolvedor, porque todo processo é previsto e programado nos próprios controles.

Normalmente a operação deve ser realizada no primeiro objeto que o usuário acesso, por exemplo o login.

```
login.aspx

Event Start
 	form.HeaderRawHTML = uc_cssLOAD()
	form.Meta.AddItem("viewport", "width=device-width,initial-scale=1")

	/* segurança com parametros encriptados */
	&websession.Set("SECURITYPARMON", "0")
	&websession.set("SECURITYPARMKEY", getEncryptionKey())

	do 'load'		
Endevent
```
O processo utiliza duas variáveis de sessão: **SECURITYPARMON** e **SECURITYPARMKEY** para definir a ligação encriptação.

**SECURITYPARMON** valendo zero (0), expõe o conteúdo dos parametros. Um (1) encripta automaticamente os parametros.

**SECURITYPARMKEY** é a chave de encriptação a ser utilizada, consistindo de uma string hexadecimal de 32 caracteres. Uma procedure getEncryptionKey() pode gerá-la automaticamente. Um exemplo de chave é 8E0D67ECC88419BD7B1CE3042F015400.

>[!NOTA]
>O getEncryptionKey() gera uma nova chave de encriptação a cada carga da interface, portanto, é um método importante para causar mais atraso no ataque hacker, uma vez que descobrir a chave, outra já terá sido gerada.

Para tratar o evento encriptado, veja este [documento](doc/tecnicas/tec_encriptacaobootstrapclick.md).
