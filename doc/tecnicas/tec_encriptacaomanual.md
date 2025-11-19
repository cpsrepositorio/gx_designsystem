# Encriptação de parametros Manual

A encriptação manual é necessária em algumas circunstâncias e deve ser utilizada quando a encriptação de parametros estiver ligada.

Considere que por alguma razão voce decide criar um componente próprio, em formato HTML e gostaria que o evento fosse interpretado da mesma maneira que os controles.

Por exemplo: Imagine um DIV que voce espera que seja interceptado pelo BootstrapClick.

```
textblock.caption = '<div onclick="CLICKNODIV">clique aqui</div>'
```
Esta construção será ignorada pelo BootstrapClick que espera que o evento esteja em um formato padrão, similar a:

```
<div onclick="gx.getObj('', false).getUserControl('BOOTSTRAPCLICK1Container').bootstrapclick('OBJETO:GRID:CLIQUEAQUI');">clique aqui</div>

```
O melhor caminho para gerar esse evento seria chamar uma função do próprio UC que produz esta ação de forma encriptada.
```
&key = &websession.get("SECURITYPARMKEY")
&click = uc.uc_clickENC('OBJETO:GRID:CLIQUEAQUI', &key, &click, &evento)

textblock.caption = '<div '+&click.trim()+'>clique aqui</div>'
```
Para tratar o evento encriptado, veja este [documento](doc/tecnicas/tec_encriptacaobootstrapclick.md).
