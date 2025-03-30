# PRIMEIRO PAINEL (ALO MAMAE!)
Comecemos de forma simples, apresentando os fundamentos de uso do pacote UC.
Se você ainda não está familiarizado com Genexus sugerimos que estude, pois aqui não estaremos detalhando a funcionalidade dos objetos.

Voce vai precisar de um Webpanel.

1) Na kb recém-criada, crie um webpanel.
2) Altere a propriedade do objeto colocando em Master Page o valor nulo (em branco)
3) Selecione Toolbox e inclua um controle Textblock na aba WebLayout.
4) Em seguida clique sobre este e pressione F4 para alterar a propriedade para Format: HTML
4. Na área Events do objeto, crie um Event Start.
5. 
```
Event Start
   …	
Endevent
```
5) Dentro deste evento programe:
```
Event Start
 textblock1.caption = '<div style="border:1px solid red;">teste</div>'
Endevent
```
6. Salve o objeto
7. Execute o Genexus
