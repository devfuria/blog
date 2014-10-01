---
layout: post
title:  Jekyll, uma limitação irritante!
---


[Jekyll](http://jekyllrb.com/) é sensacional! Não vou falar mal de Jekyll, afinal de contas este blog é feito com Jekyll.
O meu site [www.devfuria.com.br](www.devfuria.com.br) é Jekyll, o meu [blog pessoal](https://flaviomicheletti.github.io/)
é feito com Jekyll. Eu seria o cara mais suspeito para falar mal de Jekyll, mas eu encontrei uma limitação e venho 
compartilhar ela com você.

O problema está no workflow de trabalho ao criar uma página, uma única pagina. Não há uma forma de gerar uma pequena parte
de seu site, imagine que você queira gerar uma pasta ou um único arquivo, não dá.

E porque eu quero gerar uma única página? Aí está o foco do problema, agora terei que explicar melhor sobre o que eu 
quero dizer quanto a "workflow de trabalho". Vamos imaginar um cenário...

Você começa um site pequeno (umas 5 páginas) com Jekyll. O comando `jekyll server -w` gerar todo o seu site e fica 
"escutando" para gerar a cada alteração que você fizer. A cada pequena alteração ele gera todo o seu site, ele faz isso 
de forma incrivelmente rápida. O esperado acontece, conforme seu site cresce o Jekyll levará mais tempo para gerar 
todo o site. Natural que seja assim, e confesso que nem é muito tempo, repito o Jekyll é rápido. Isso porque eu nem
instalei o [suporte a LCI](http://octopress.nayaklabs.com/blog/2014/08/07/for-10x-faster-lsi-support/).

Continuando com o cenário, imagine que para gerar todo o seu site o Jekyll esteja levando 15 segundos. Agora você decide
incluir mais um página, após 15 segundos temos o resultado. Olhando para a página em seu navegador você se depara com
um título inadequado e resolve mudar... após 15 segundos temos o resultado. Tudo bem, você continua a leitura e se depara
com alguns erros gramaticais (eu sou bom nisso, rsss) concerta um e... após 15 segundos temos o resultado. Concerta outro
e... após 15 segundos temos o resultado. Aí você resolve concertar todos os erros de uma só vez, obviamente. Mas quando
acho que terminou decide alterar uma frase e... após 15 segundos temos o resultado.

E aí, consegui te irritar tanto quanto o Jekyll me irritou?

Resumindo, o problema está quando você tem um site grande (+ de 70 páginas/posts) e quer criar/alterar uma única página.
__A cada pequena alteração você terá que esperar pelo tempo total de construção do todo o site/blog!__


Meu site contava com 70 páginas quando descobri a limitação. Eu achei um paliativo, é um band-aid, uma gambi. No arquivo
de configuração `_config.yml` é possível especificar o que fica de fora, ou seja, o que não será gerado. No meu caso,
tenho os conteúdos bem definidos e separados por pastas posso fazer:

	exclude: [pasta1, pasta2, pasta3]

O Jekyll irá gerar só a `pasta4`, isso ameniza. Engraçado que eu queria fazer exatamente o inverso, dizer "ei Jekyll seja
bonzinho comigo e inclua apenas esse ou aquele arquivo", pronto! Estaria tudo resolvido, mas os caras que mantém o Jekyll
são turrões. Nos logs do GitHub, desde 2011, há discussões calorosas à respeito. Logo, mudar a cultura de desenvolvimento 
do Jekyll está descartada. Veja nessa [issue](https://github.com/jekyll/jekyll-help/issues/123) como os caras são taxativos.

A uma [discussão](https://github.com/jekyll/jekyll/issues/380), paralela e inútil (digasse de passagem), a respeito da geração incremental. É uma conversa sem fim.

Cogitei mudar para [Pelican](http://blog.getpelican.com/). O Pelican gera aquilo que você quer que ele gere, foi a 
primeira coisa que testei. Você pode ter 1000 páginas (esse foi meu teste) e ele gera apenas a que você pedir. Obviamente
que ao entrar em "watch" ele será extremamente eficaz, pois terá que gerar apenas uma única página. Mas desisti do Pelican
também, depois eu conto as razões em outro post.

Cogitei mudar para o [DocPad](http://docpad.org/). Cara que encrenca! Tem um [problema](https://github.com/docpad/docpad/issues/885) para ser resolvido até hoje, ele entra em um loop infinito. Nâo cheguei a fazer o teste das 1000 páginas, vou esperar a issue ser fechada... eles devem estar esperando eu pagar para ter o suporte, justo! 

Experimentei outros [geradores estáticos](https://github.com/pinceladasdaweb/Static-Site-Generators), existem uma centenas
deles. Mas em certo ponto parei, pois estava perdendo um longo e precioso tempo no meio de tanta documentação, incrível 
como os caras perdem o foco na hora de escrever manuais.

Talvez exista um plugin, ou alguma solução (solução != gambiarra) que eu desconheça. Se você conhece, me avise por favor!


Conclusão?
---

Se você me perguntar se eu indico o Jekyll? Indico claro!

Se me perguntar qual é o melhor Jekyll, Pelican ou DocPad? Eu prefiro o Jekyll (gosto pessoal)!

Se você vai montar um site pequeno, o Jekyll pode cair como uma luva, experimente! Se vai montar um site grande, lembre-se
que nem tudo é perfeito.

Só mais uma coisa, [WordPress](https://wordpress.com/) ou Jekyll? Que papinho de estagiário! WordPress gera de forma
dinâmica e o Jekyll de forma estática, são coisas diferentes. E antes que você pense que sou um ferrenho defensor de
PHP e WordPress, eu não uso mais PHP e nunca usei WordPress (confesso que fiz alguma manutenção, mas só isso).