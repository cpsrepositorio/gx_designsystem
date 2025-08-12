# Estilos
Os estilos dos controles do pacote são definidos em arquivos CSS, que ficam disponibilizados em um repositório centralizado.


Para realizar a carga das folhas de estilo é necessário chamar um procedimento:

``` 
 form.HeaderRawHTML  = uc_css() 
```

E neste, uma programação para definir o local onde se encontra os arquivos e a carga da procedure do módulo. 

``` 
&stylepath = 'https://siga.cps.sp.gov.br/style/'
&html  = UC.uc_cssCARGA(&stylepath) 
``` 
Para que o navegador não bloqueie a carga com mensagem de CORS, será necessário incluir no web.config a seguinte definição:
```
<appSettings>
...
<add key="GX_CORS_ALLOW_ORIGIN" value="https://siga.cps.sp.gov.br" />
</appSettings>
```

