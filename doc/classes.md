# Classes
Os controles são definidos visualmente por classes do tipo css, que estão armazenados em diversos arquivos que são carregados a partir da chamada de **uc.uc_cssCARGA()**

É possível colocar a pasta com esses arquivos no próprio sistema, mas recomendamos a utilização de uma das instalações disponíveis, para que se tenha o padrão das classes.

## Criando um cssLOAD()
A forma mais simples de realizar a operação de chamada a carga de CSS é criar uma procedure.

**uc_cssLOAD**

```
&stylepath =' https://siga.cps.sp.gov.br/style'
&html  	 = UC.uc_cssCARGA(&stylepath)
&html 	+= UC.uc_fontCDN()
```

**&stylepath** é uma variável Varchar(40) que aponta para um dos links onde se encontram os arquivos CSS. 

|   link                                               | conteúdo                |
|------------------------------------------------------|-------------------------|
| https://siga.cps.sp.gov.br/style                     | Ambiente de produção    |
| http://siga-dev.brazilsouth.cloudapp.azure.com/style | Ambiente de homologação |

O controle também necessita de algumas definições adicionais que se encontram em **UC.uc_fontCDN()**, que também deve ser chamada.

## Carregando 
Para carregar as classes nos exemplos, programe no evento Start a chamada a rotina de carga.

```
Event Start
	form.HeaderRawHTML = uc_cssLOAD()
	form.Meta.AddItem("mobile-web-app-capable",'content="yes"')
	
	...
EndEvent
```

Repita essa definição para todos os WebPanels que construir.

