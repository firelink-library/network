---
title: Introdução
sidebar-position: 1
slug: /intro
---

# As redes de computadores

No que consiste a comunicação? Há aqui três acepções possíveis. A primeira
define comunicação como a continuidade entre uma coisa e outra. Quando há, por
exemplo, um caminho que ligue a cozinha de uma casa ao seu quintal, diz-se que
há comunicação entre os dois ambientes. Uma segunda acepção possível é a de
notificar alguém acerca de um evento ou acontecimento. Quando um casal envia
convites ao seu casamento, efetivamente comunica aos convidados que estes são
bem vindos à cerimônia. A terceira e - para nós - mais importante acepção é a
de transmitir informações através de um meio.

Utilizando a terceira acepção, é possível definir os pré requisitos para que a
comunicação ocorra. A saber:

* Deve-se haver um *meio*. Tal qual o mar oferece morada para as correntes e
  estas, por sua vez, enfurecem o ar para a criação de ventos, também esse
  próprio ar oferece morada para as palavras humanas.
* Tais palavras seriam apenas perdidas ao vento sem a existência de um
  *destinatário*. Sem um destino, as palavras do homem tem tanta gravidade
  quanto o silêncio do espaço. Sem ter quem o ouça, vive o *remetente* em
  condições similares a um astronauta submetido ao vácuo do espaço.
* Precisa-se, portanto, que exista esse *remetente* para proferir suas
  palavras.
* Por fim, tais palavras são fruto de uma *mensagem* que teve sua origem e
  forma original na consciência do *remetente* e, havendo também um
  *destinatário* e um *meio* que una a consciência do segundo ao primeiro,
  passa a existir também a interpretação da mensagem - a manifestação dessa
  união.

## 1. A história da comunicação humana

A tarefa de retraçar, através das evidências fossilizadas, a linha evolutiva
humana até o momento em que - pela primeira vez - sons foram embutidos com
significado é quase como tatear no escuro em busca de uma agulha em mar de
palha. Há, no entanto, razões para imaginar que esse momento já havia
acontecido tão cedo quanto da existência dos Neanderthais. Essas razões são
resumidas em duas asserções:

1. A análise da composição ossea dos Neanderthais indica que nele já havia todo
   o aparato necessário para produzir e modular sons, assim como faz hoje o
   homem.
2. Há evidências de que nossos antepassados já utilizavam ferramentas
   suficientemente complexas de modo que é razoável assumir que seu manejo
   precisaria ser ensinado.

Escondida nessa segunda asserção fica o motivo pelo qual navegamos em águas tão
antigas: desde que se tem informações para avaliar, é clara a conclusão de que
a comunicação é como a chama Prometeica; capaz de iluminar novas eras na
existência humana.

Qualquer professor ou aluno de história é capaz de repetir que a existência
humana pode ser dividida entre um período ao qual chamamos de pré-história -
que expande-se no decorrer de dezenas de milhares de anos -, e o período,
comparativamente muito menor, a partir do qual é possível obter informações o
suficiente para que este se subdivida. Não há dúvida quanto ao evento que
separa exatamente estes dois períodos: a escrita.

Novamente


Era paleolítica - primeiras pinturas em cavernas; petróglifos. Calendário
lunar. Idéias foram ficando mais complexas e surge o conceito de aprendizado
geracional.

Origem dos sistemas de escrita - ideogramas. Mais tarde, sistemas de escrita
permitem a invenção dos livros. Coincide com o começo da história registrada,
fim da pré história. Um divisor de águas na existência humana.

A impresa e o encurtamento de distâncias. Revolução da informação através dos
periódicos. Prelúdio da revolução da telecomunicação.

## 1. O princípio das telecomunicações

O que é a comunicação? Quais são os requisitos e componentes para que a
comunicação seja possível?

Origem do termo telecomunicação. Comparação com os componentes estabelecidos
como os mínimos para que haja a comunicação "tradicional".

O princípio da telecomunicaçãõ: Sinais sonoros, de fumaça, bandeiras, etc.
Gerar a ideia de que comunicação transmitida pelo ar é mais simples do que pode
parecer.

O telégrafo e o telefone - aparecem os sinais elétricos e eletronicamente
amplificados. Importância para as telecomunicações. Surge o rádio, a partir do
qual muitos dos conceitos utilizados nas redes de computadores se apoiam.

As redes de computadores - como e por quê dois computadores precisariam se
comunicar? Vincular com o princípio da computação em si, a transição da era dos
mainframes single thread para os teleterminais. A vantagem de se ter
dispositivos periféricos que precisam apenas implementar uma interface em comum
e, por fim, a internet em si, que revolucionou novamente a comunicação humana.

## 2. Níveis de redes

Personal Area Network - comunicação a nível de dispositivo. Geralmente de um
dispositivo principal com seus periféricos. Aqui entra VGA, RS232, USB,
Bluetooth. Fundamental para a multifuncionalidade dos computadores. Explicar em
um pouco mais de detalhes ao menos um dos protocolos expostos acima.

Local Area Network - Surgem as figuras dos switches e access points, conectando
um computador ao outro. Aqui, torna-se importante o endereçamento de
dispositivos utilizando protocolos como MAC Address e IP. Também faz sentido
mencionar o conceito de VLANs para seccionar redes locais.

Metropolitan Area Network - atuação já a nível de cidades. Interconecta redes
locais utilizando meios mais resistentes a interferência e com maior largura de
banda. Já exige a atuação de orgãos governamentais para concessão de direitos
de distribuição e sistemas como 5g, TV a cabo e até mesmo provedores de
internet.

Wide Area Network - nível global/continental. Cada aumento de nível aumenta o
grau de dificuldade e diminui a eficiência da comunicação. Torna-se mais caro.
Aqui atuam os serviços de provedores de internet e de infraestrutura das redes
que interconectam o globo. Torna-se mais importante o uso de bons algoritmos de
transmissão e roteamento.

Internet - definição de internet como aglutinação de redes com protocolos ou
arquiteturas heterogêneas. Surgem os gateways.

## 3. Hierarquia de pacotes

Necessidade de padronização para expansão dos dispositivos capazes de se
intercomunicar. Aqui traçamos um paralelo com as abstrações e padronizações de
um sistema operacional. Surgem as camadas de rede (ainda não vamos falar de OSI
ou TCP/IP)

Definição dos termos para essa abstração - camadas, protocolos, interfaces e
pacotes.

Exemplo do livro do tanembaum de um tradutor para um filósofo.

Conclusão sobre camadas - a camada inferior não sabe da existência da superior,
que vai carregar a sua mensagem e os seus metadados na forma de um cabeçalho
e/ou um terminador. O remetente empilha cabeçalhos e possivelmente divide a
mensagem em múltiplas partes, para que o destinatário faça o caminho oposto até
ter a mensagem em sua camada de "aplicação"
