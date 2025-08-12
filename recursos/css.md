# Estilos
Os estilos dos controles do pacote são definidos em arquivos CSS, que ficam disponibilizados em um repositório centralizado.


Para realizar a carga das folhas de estilo é necessário chamar um procedimento:

	``` form.HeaderRawHTML  = uc_css() ```

E neste 

´&stylepath = &websession.get('STYLEPATH')
if &stylepath.IsEmpty()
	&stylepath = Config_STYLEPATH_GET()
	&websession.Set("STYLEPATH", &stylepath.Trim())
endif

&html  = UC.uc_cssCARGA(&stylepath) 
´

