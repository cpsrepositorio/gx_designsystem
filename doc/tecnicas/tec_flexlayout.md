# Flex Layout
Para se obter maior controle na interface Genexus é necessário alterar o Design do objeto MainTable para Flex, executando uma operação Convert to Flex. Botão direito sobre a interface, selecione a MainTable e execute o Convert to Flex. O Genexus aceita vários tipos de layouts, veja a documentação [aqui](gx_designsystem/doc/layout.md)

É até possível utilizar o ResponsiveTable nas interfaces com os controles, mas o resultado vai exigir mais ajustes nos CSS, porque o Genexus vai incluir os controles de Bootstrap na interface e muito mais classes interferindo.

## Sections
A organização das seções de nossa interface deve ser feita preferencialmente com controles tipo Section.
Um conjunto de classes de controle de layout (uc_flex-r, uc_flex-c) e outros de dimensionamento e margens (uc_p, uc_m, uc_w)

![padrao](https://raw.githubusercontent.com/cpsrepositorio/gx_designsystem/refs/heads/main/doc/imagens/section.png)



![padrao](https://raw.githubusercontent.com/cpsrepositorio/gx_designsystem/refs/heads/main/doc/imagens/uc_flexc.png)
![padrao](https://raw.githubusercontent.com/cpsrepositorio/gx_designsystem/refs/heads/main/doc/imagens/uc_flexr.png)



Flex Layout não é coisa de outro mundo para entender, parte do principio de definir uma DIV com os objetos em **Row** ou **Column**, fora isso o que temos é alinhamento, dimensionamento dos objetos. É até simples.

Em Genexus, é usual colocar uma Section na interface e em seguida definir a classe para torná-la uma **Row** ou **Column**. Utilizamos as classes definidas em uc_flex.css, para trabalhar com esse layout.


* **uc_flex-r**				{display:flex; flex-direction:row;}
* **uc_flex-c**				{display:flex; flex-direction:column;}
* **uc_flex-w**				{flex-wrap:wrap;}
* **uc_flex-nw** 			{flex-wrap:nowrap;}
* **uc_flex-jcs** 			{justify-content:flex-start; align-items: flex-start;}
* **uc_flex-jcsb**			{justify-content:space-between;}
* **uc_flex-jcc**			{justify-content:center;}
* **uc_flex-jce**	 		{justify-content:flex-end;}
* **uc_flex-aic**			{align-items:center;}
* **uc_flex-eq**            {flex: 1;}
* **uc_flex-db**            {flex: 2;}

Portanto, para criar uma linha, basta inserir uma Section e na propriedade Class informar **uc_flex-r**, em seguida, para acrescentar alinhamentos utilize  **uc_flex-jcsb** ou **uc_flex-jcc** ou **uc_flex-jce**.

As larguras das colunas podem ser definidas com as classes **uc_flex-eq** e **uc_flex-db**, ou ainda, por meio das classes em uc_root.css, de largura:

* **.uc_w100**              {width:100%;}
* **.uc_w90**               {width:90%;}
* **.uc_w80**               {width:80%;}
* **.uc_w70**               {width:70%;}
* **.uc_w60**               {width:60%;}
* **.uc_w50**               {width:50%;}
* **.uc_w40**               {width:40%;}
* **.uc_w30**               {width:30%;}
* **.uc_w20**               {width:20%;}
* **.uc_w10**               {width:10%;}
* **.uc_w5**                {width:5%;}

Genexus permite inserir Section dentro de outra Section, então fica mais simples montar tudo.

Veja um exemplo na construção de uma master page cheia de Sections em [MasterPage](/doc/tecnicas/tec_masterpage.md)
