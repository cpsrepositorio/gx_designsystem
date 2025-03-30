# PRIMEIRO PAINEL (ALO MAMAE!)
Comecemos de forma simples, apresentando os fundamentos de uso do pacote UC.
Se você ainda não está familiarizado com Genexus sugerimos que estude, pois aqui não estaremos detalhando a funcionalidade dos objetos.

Voce vai precisar de um Webpanel.

1) Na kb recém-criada, crie um webpanel.
2) Altere a propriedade do objeto colocando em Master Page o valor nulo (em branco)
3) Selecione Toolbox e inclua um controle Textblock na aba WebLayout.
4) Em seguida clique sobre este e pressione F4 para alterar a propriedade para Format: HTML
5) Na área Events do objeto, crie um Event Start.

```
Event Start
   …	
Endevent
```
6) Dentro deste evento programe:
```
Event Start
 textblock1.caption = '<div style="border:1px solid red;">teste</div>'
Endevent
```
7) Salve o objeto
8) Execute o Genexus

Voce deve ter observado que é possivel a partir de um Textblock simples apresentar comandos HTML na interface. Pois o pacote UC é baseado nesta capacidade.

Parece ser um modelo tão elementar, mas na prática, todo conteúdo baseado na internet parte da estrutura HTML incluido informações texto. O pacote UC utiliza desta capacidade para inserir na interface padrão Genexus as tags HTML que apresentarão recursos complexos.



