# construindo interfaces diferentes
É dificil para uma ferramenta como o Genexus, que objetiva criar tudo, trabalhar com a flexibilidade necessária para permitir que o desenvolvedor faça 'alguma coisa diferente', os mundos se chocam, pois para criar a ferramenta precisa partir de um conhecimento prévio, normalmente sob os objetos 'padrões'. Infelizmente é um cenário que reduz bastante a inovação.

Porém, nem tudo está perdido. Como alternativa a este nivel de restrição, construímos um pacote de controles que podem ser facilmente incorporados nos projetos, objetivando sempre a simplicidade de uso e flexibilidade. O objetivo foi o de permitir construir interfaces com o minimo de esforço (porém, com algum esforço).

Criamos um pacote a partir de uma KB chamada DESIGN_SYSTEM18, que reune os controles, exemplos, SDTs, dominios e demais recursos utilizados.

A diferença fundamental dos modelos, no UC os controles são criados de uma forma 'mais programativa', seguindo um modelo de carregar as propriedades desejadas em um SDT e em seguida, passando-se para que uma Procedure execute e construa o objeto desejado, e buscamos um cenário minimalista onde apenas é necessário um TEXTBLOCK e um User Control para interceptar os eventos de click (veja o capitulo SETUP).

De forma bastante simplificada, este modelo constrói os codigos HTML + JS necessários para executar um componente na interface, em tempo de execução, mas no final das contas, pela simplificação e otimização dos recursos, acaba produzindo um desempenho muito superior à interface Genexus tradicional.

Pode parecer simplista, mas este modelo, de todos que utilizei até este momento, me parece que é o mais eficiente e rápido. 

- User Control: dificil de desenvolver, testar e manter
- User Control Object: simples de desenvolver, mas não contribui muito com a padronização
- UC: um pacote com todos os controles padronizados melhora a dinamica da equipe na construção e manutenção. O pacote agrega o controle, a gestão de dados, segurança, baixa exposição na interface.

Ou seja, o pacote traz não apenas a preocupação dos controles, mas também uma forma de padronizar as interfaces para buscar um nivel de produtividade maior. Porém, compreendo que seria muito bom se um dia pudermos associar a este cenário um modelo de produção de objetos automatizados com o Pattern. Fica a dica para a próxima evolução do pacote.

Neste documento voce encontrara informações para construir interfaces interessantes utilizando este modelo diferentão.