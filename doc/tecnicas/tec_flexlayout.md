# Flex Layout
Para se obter maior controle na interface Genexus é necessário alterar o Design do objeto MainTable para Flex, executando uma operação Convert to Flex. Botão direito sobre a interface, selecione a MainTable e execute o Convert to Flex. O Genexus aceita vários tipos de layouts, veja a documentação [aqui](gx_designsystem/doc/layout.md)

É até possível utilizar o ResponsiveTable nas interfaces com os controles, mas o resultado vai exigir mais ajustes nos CSS, porque o Genexus vai incluir os controles de Bootstrap na interface e muito mais classes interferindo.

## Sections
A organização das seções de nossa interface deve ser feita preferencialmente com controles tipo Section.

Um conjunto de classes de controle de layout (uc_flex-r, uc_flex-c) e outros de dimensionamento e margens (uc_p, uc_m, uc_w), são suficientes para contruir interfaces complexas.

A inserção de Sections dentro de outras Sections também será necessário para dividir as áreas da interface.

## Classes de posicionamento em linha
As classes de posicionamento em linha são obtidas pelo **display:flex; flex-direction:row;** que são programadas em **uc_flex-r**
![padrao](https://raw.githubusercontent.com/cpsrepositorio/gx_designsystem/refs/heads/main/doc/imagens/uc_flexr.png)

| classe         | programação da classe      | efeito  |
|----------------|------------------|---------|
|**uc_flex-jcs** |{justify-content:flex-start; align-items: flex-start;} |Posicionamento do objeto no inicio da linha |
|**uc_flex-jcsb** | {justify-content:space-between;}|Posicionamento de mais de um objeto em porções equivalentes na interface. Se dois objetos, coloca cada um nas pontas da linha. |
|**uc_flex-jcc** |{justify-content:center;} |Centraliza os objetos na linha.|
|**uc_flex-jce** |{justify-content:flex-end;} |Posiciona os objetos no fim da linha |

## Wrap
Os objetos podem ser reposicionados caso não exista espaço suficiente para serem apresentados na linha.  

| classe        | programação da classe    | efeito  |
|---------------|------------------|---------|
|**uc_flex-w**  |{flex-wrap:wrap;} |Quebra as linhas |
|**uc_flex-nw** |{flex-wrap:nowrap;}|Não reposiciona os objetos na linha |

## Classes de posicionamento em coluna
As classes de posicionamento em coluna são obtidas pelo **display:flex; flex-direction:column;** que são programadas em **uc_flex-c**
![padrao](https://raw.githubusercontent.com/cpsrepositorio/gx_designsystem/refs/heads/main/doc/imagens/uc_flexc.png)

## Dimensionamento e margens
As seções devem ser dimensionadas para produzir o efeito desejado na interface.

![padrao](https://raw.githubusercontent.com/cpsrepositorio/gx_designsystem/refs/heads/main/doc/imagens/section.png)

Classes que determinam a larguras dos objetos.
| classe        | programação da classe | 
|---------------|-----------------------|
|**uc_w100***  |{width:100%;} |
|**uc_w90** |{width:90%;}|
|**uc_w80** |{width:80%;} |
|**uc_w75** |{width:75%;} |
|**uc_w70** |{width:70%;} |
|**uc_w60** |{width:60%;} |
|**uc_w50** |{width:50%;} |
|**uc_w40** |{width:40%;} |
|**uc_w30** |{width:30%;} |
|**uc_w25** |{width:25%;} |
|**uc_w20** |{width:20%;} |
|**uc_w10** |{width:10%;} |
|**uc_w5** |{width:5%;} |
|**uc_w1000px** |{width:1000px;} |
|**uc_w900px** | {width:900px;}|
|**uc_w800px** | {width:800px;}|
|**uc_w700px** |{width:700px;} |
|**uc_w600px** |{width:600px;} |
|**uc_w500px** |{width:500px;} |
|**uc_w400px** |{width:400px;} |
|**uc_w300px** |{width:300px;} |
|**uc_w200px** |{width:200px;} |
|**uc_w150px** |{width:150px;} |
|**uc_w100px** |{width:100px;} |

Margens gerais, que aplicam a mesma largura em todos os lados do objeto.
| classe        | programação da classe| 
|---------------|----------------------|
|**uc_m100**    |{margin:100px;}       |
|**uc_m90**|{margin:90px;} |
|**uc_m80**|{margin:80px;} |
|**uc_m70**|{margin:70px;} |
|**uc_m60**|{margin:60px;} |
|**uc_m50**|{margin:50px;} |
|**uc_m40**|{margin:40px;} |
|**uc_m30**|{margin:30px;} |
|**uc_m20**|{margin:20px;} |
|**uc_m15**| {margin:15px;}|
|**uc_m10**|{margin:10px;} |
|**uc_m5**| {margin:5px;}|
|**uc_m3**| {margin:3px;}|
|**uc_m2**| {margin:2px;}|
|**uc_m1**| {margin:1px;}|

Além das margens gerais temos também as margens especificas que definem a largura de uma determinada margem. As dimensões são as mesmas 
| classe        | programação da classe| 
|---------------|----------------------|
|**uc_mt<nnn>**   |Define a margem do topo, onde <nnn> podem ser os valores [1,2,3,5,10,15,20,30,40,50,60,70,80,90,100] |
|**uc_mr<nnn>**   |Define a margem da direita, onde <nnn> podem ser os valores [1,2,3,5,10,15,20,30,40,50,60,70,80,90,100] |
|**uc_mb<nnn>**   |Define a margem da base, onde <nnn> podem ser os valores [1,2,3,5,10,15,20,30,40,50,60,70,80,90,100] |
|**uc_ml<nnn>**   |Define a margem da esquerda, onde <nnn> podem ser os valores [1,2,3,5,10,15,20,30,40,50,60,70,80,90,100] |



Flex Layout não é coisa de outro mundo para entender, parte do principio de definir uma DIV com os objetos em **Row** ou **Column**, fora isso o que temos é alinhamento, dimensionamento dos objetos. É até simples.

Em Genexus, é usual colocar uma Section na interface e em seguida definir a classe para torná-la uma **Row** ou **Column**. Utilizamos as classes definidas em uc_flex.css, para trabalhar com esse layout.


* **uc_flex-aic**			{align-items:center;}
* **uc_flex-eq**            {flex: 1;}
* **uc_flex-db**            {flex: 2;}

Portanto, para criar uma linha, basta inserir uma Section e na propriedade Class informar **uc_flex-r**, em seguida, para acrescentar alinhamentos utilize  **uc_flex-jcsb** ou **uc_flex-jcc** ou **uc_flex-jce**.

As larguras das colunas podem ser definidas com as classes **uc_flex-eq** e **uc_flex-db**, ou ainda, por meio das classes em uc_root.css, de largura:



Genexus permite inserir Section dentro de outra Section, então fica mais simples montar tudo.

Veja um exemplo na construção de uma master page cheia de Sections em [MasterPage](/doc/tecnicas/tec_masterpage.md)
