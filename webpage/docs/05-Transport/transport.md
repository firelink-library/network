---
title: A camada de transporte
sidebar_position: 1
slug: /transport
---

# Introdução à camada de transporte

Camada física - se preocupa com o transporte de informação. A unidade de medida
é em bits. Lida com interferência e sincronização de clock.

Camada de enlace - se preocupa com controle de fluxo, endereçamento local,
detecção e correção de erros. Unidade de medida é em frames - sincronização
usando cabeçalho e terminadores.

Camada de rede - se preocupa com roteamento, controle de congestão e tradução
de protocolos. Lida com pacotes (datagramas).

O que sobrou para a camada de transporte? Já não temos a garantia de que a
mensagem sai de A até B sem interferência, com controle de erros, controle de
fluxo, controle de congestão, tradução entre protocolos e encaminhamento
otimizado? O que falta é controle do usuário.

A camada de transporte entrega, pela primeira vez, todas essas preocupações
para o hardware do usuário. Sendo assim, pode-se argumentar que é a camada mais
importante que temos.

## 1. Os serviços da camada de transporte

A camada de transporte entrega os seguintes serviços para a camada superior:

* Endereçamento
* Estabelecimento de conexão
* Controle de erros
* Controle de fluxo
* Multiplexação
* Controle de congestão

A maioria desses serviços já foi oferecido em outras camadas, mas aqui é a
primeira vez que eles são oferecidos de ponta a ponta.

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/lAvhH0XJLNE" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

### 1.1. Endereçamento e multiplexação

Estamos acostumados a entender endereçamento na camada de transporte como as
portas UDP ou TCP que utilizamos, mas é importante notar que a abstração por
camadas não é vinculada a protocolos específicos, então vamos seguir utilizando
os termos *ponto de acesso do serviço de transporte* (TSAP, em inglês) e *ponto
de acesso do serviço de rede* (NSAP, em inglês). Sim, para a internet o TSAP é
a porta TCP/UDP e o NSAP é o IP, mas vamos tomar o cuidado de não enviesar a
discussão muito para esses protocolos.

O que geralmente acontece é que um mesmo NSAP mapeia para diversos TSAPs. Sendo
assim, precisamos ser capazes de:

1. Mapear corretamente as aplicações que estão escutando por informações em
   cada TSAP;
2. Entender que há uma concorrência de recursos para o uso da NSAP 

Para atender à capacidade 1 o que geralmente é utilizado é um processo especial
responsável por mapear TSAPs para nomes de aplicações, algo como uma
telefonista. Em sistemas UNIX, esse processo é um *daemon* chamado *inetd*.

A capacidade 2 exige uma solução para multiplexação.

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/CekW6ipRrGA" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

### 1.2. (O problema do) Estabelecimento de conexão

Estabelecer conexões é uma preocupação de protocolos que são baseados em
conexão. Essa tarefa pode parecer simples a primeira vista, mas se
considerarmos que é possível (e comum) que a camada de transporte equilibre um
protocolo baseado em conexão (e.g. TCP) em cima de uma pilha de protocolos que
não são baseados em conexão (e.g. Ethernet, IP), é fácil perceber algumas
coisas:

1. É possível fazer com que uma abstração de alto nível mantenha uma conexão
   virtual sem que os níveis abaixo dela tenham essa garantia; mas
2. Esse arranjo introduz uma dificuldade a mais para o sistema que faz a
   manutenção dessa conexão.

Considere o seguinte: um sistema envia uma requisição de conexão para um
servidor. Essa mensagem é empacotada e entregue à camada de rede, que por si
utiliza um protocolo *best-effort* para a entrega de pacotes, mas sem garantia
alguma (e.g. IP). Não é possível que esse pacote se perca ou tenha um atraso
significativo em seu roteamento, de modo que o sistema remetente não tem como
saber se a mensagem vai chegar ou não? O que faz, então, o sistema remetente?
Envia novamente o pacote de conexão.

Vamos supor que o pacote original havia apenas sido desviado por uma congestão
momentânea na camada de rede. Efetivamente existe uma possibilidade real de
chegarem dois pedidos de conexão distintos vindos do mesmo sistema para o
servidor. A nível de camada de transporte, como podemos lidar com essa
possibilidade?

1. Utilizar um TSAP diferente para cada pacote;
2. Utilizar um identificador único para cada pacote;
3. Adicionar um limite de vida para cada pacote;

A opção 1 resolve o problema, mas introduz uma série de outros problemas:
* Como lidar e sincronizar entre cliente e servidor as mudanças de portas?
* Como lidar com a maior probabilidade de colisão de portas?

A resposta é sobrecarregar o processo mapeador de portas. Essa solução acaba
sendo pouco usada.

A opção 2 também resolve o problema, porém como sincronizar esse ID único entre
o cliente e o servidor? Podemos usar algo como um id autoincrementável, mas
isso precisa que o estabelecimento da conexão em si crie um consenso do
primeiro id a ser utilizado.

A solução 3 não resolve exatamente o problema, mas mitiga um pouco. Aqui, temos
duas opções:

* Usar um "hop counter" e adicionar ao payload, assim cada roteador pode
  desempacotar o payload e decrementar o hop counter. Quando chegar a 0, o
  pacote é deixado de lado como obsoleto.
* Considerar o tempo decorrido desde que a mensagem foi enviada. Essa solução
  envolve, novamente, sincronizar cliente e servidor e todos os roteadores para
  que eles concordem com o mesmo tempo.

Uma solução interessante para essa sincronização de tempos envolve utilizar um
ponto temporal de comum acordo para todos os dispositivos e sempre referenciar
o tempo decorrido por esse ponto em comum. Aqui o que faz mais sentido é
utilizar o tempo UNIX. Assim, podemos equipar todos os dispositivos com um
contador interno que acompanha o timestamp UNIX alimentado por bateria.
Podemos, também, criar protocolos específicos para sincronizar esse tempo
periodicamente com um servidor de timestamp unix e minimizar o erro que pode se
acumular com o decorrer do tempo.

Com essa implementação do relógio de tempo real, torna-se possível inclusive
criar uma solução híbrida, que utiliza um id de lifetime para cada pacote.
Basicamente o pacote recebe os bits menos significativos do timestamp UNIX e
utiliza-os como um id. Esse id pode facilmente ser verificado por cada
dispositivo no caminho até o destino final do pacote. Com isso, pode-se
verificar facilmente se o pacote ainda é válido utilizando uma estratégia de
janela deslizante.

Utilizando essa estratégia de id temporal e janelas deslizantes, pode-se
utilizar também um handshake de três vias e garantir que o estabelecimento de
conexão seja robusto e com poucos erros.

*Imagem three-way handshake*

### 1.3. Controle de ponta a ponta

Os conceitos relacionados ao controle e correção de erros, controle de fluxo e
controle de congestão são exatamente os mesmo já estudados em outras camadas de
rede. A diferença na camada de transporte é que eles são aplicados de ponta a
ponta pela primeira vez. Embora não sejam obrigatórios, isso torna o seu uso
consideravelmente mais importante do que em outras camadas.

O uso de um checksum na camada de transporte é muito mais efetivo do que o seu
uso na camada de enlace, por exemplo.

Apenas para recordar algumas das soluções vistas antes:

* Detecção e correção de erros pode ser feita através de bits/bytes redundantes
  no payload que são usados para operações com o payload original e gerar um
  sinal que indica a integridade da mensagem original;
* O controle de fluxo é feito quando equlizamos a taxa de envio de um
  dispositivo para não sobrecarregar o seu destino;
* O controle de congestão acontece quando o meio de comunicação fica saturado e
  as mensagens começam a ser perdidas com mais frequência. Aqui podemos usar
  estratégias de curto prazo, como load shedding, ou de longo prazo, como
  provisionamento de rede.
* Para todos os casos acima, o comum é a reemissão da mensagem enviada em caso
  de problemas. No entanto, não costuma-se enviar a mensagem imediatamente após
  o erro. É comum impor um período de espera. Quanto maior esse período, menor
  a chance de um novo erro, mas também menor é o throuput da rede. Sendo assim,
  geralmente começamos com uma janela de intervalos pequena e vamos deslizando
  essa janela para que os tempos de espera continuem sendo aleatórios, mas
  aumentando gradativamente.

## 2. Primitivas da camada de transporte

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/_iHMMo7SDfQ" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>
