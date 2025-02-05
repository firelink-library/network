---
title: Introdução
sidebar-position: 1
slug: /intro
---

# As redes de computadores

A origem da fala - de neanderthal a homo sappiens. Motivo da atribuição aos
neanderthais: complexidade das ferramentas utilizadas. Precisavam ensinar uns
aos outros.

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
