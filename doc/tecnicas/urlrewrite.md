# urlrewrite
Podemos utilizar o objeto URLRewrite para criar rotas e ocultar informações a respeito do objeto em execução no navegador.

`
login 		    => login;
home			=> home;

admin		    => home_admin;
contratacao 	=> home_contratacao;

// objeto segurança
seguranca		=> home_seguranca;
segincidente	=> IncidenteUI;
segseveridade	=> NivelSeveridadeUI;
segorigem		=> OrigemNotificacaoUI;
segsituacao	    => SituacaoIncidenteUI;
segtipo		    => TipoIncidenteUI;
`