---
title: UDP vs TCP
sidebar_position: 2
slug: /udptcp
---

# Os protocolos da camada de transporte

## 1. UDP

O UDP é muito simples. Quase todas as preocupações da camada de transporte (que
são opcionais) não são feitas neste protocolo. A troca é muito clara: mais
performance, menos garantias. Sendo assim, o cabeçalho UDP é extremamente
simples:

*Cabeçalho UDP*

Aqui temos apenas o endereço (porta) de origem - que só é utilizado quando
espera-se alguma resposta -, o endereço de destino, o tamanho da mensagem e um
checksum opcional. Simples, mas com poucas garantias. Sem controle de fluxo,
sem controle de congestão, sem protocolo de retransmissão, sem handshakes. O
UDP foi feito para ser utilizado quando há a necessidade de minimizar os
recursos computacionais utilizados e há uma tolerância maior para erros e
perdas de pacotes. O exemplo clássico de utilização do UDP é o streaming de
vídeo, mas há também utilizações mais simples, como o sistema de DNS, que
veremos quando estudarmos a camada de aplicação.

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/VjBDgcNno-Q" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

## 2. TCP

### 2.1. Transmissão de dados confiável

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/nyUHUtmxWg0" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/vxgH6r-II2Q" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

Abandonando a simplicidade do protocolo UDP, precisamos começar a discutir
sobre o que é preciso para que uma comunicação seja confiável mesmo quando usa
como base protocolos que não garantem a integridade da mensagem ou a conexão.
Antes de mais nada, vamos definir claramente os problemas que precisamos
mitigar ou corrigir:

* Mensagens que se corrompem no meio do caminho
* Mensagens que se perdem no meio do caminho
* Mensagens que não se perdem, mas chegam muito atrasadas

Para as mensagens que se corrompem, temos como adicionar códigos de verificação
de erro. No entanto, pode surgir a dúvida: o destinatário consegue perceber
quando uma mensagem chega para ele corrompida, mas como o remetente é alertado
a respeito dessa corrupção? Eis que surge o conceito de **ACKNOWLEDGEMENT**.

A ideia é simples: sempre que uma mensagem chegar corretamente ao destinatário,
este envia uma mensagem especial ao remetente deixando claro que recebeu e
verificou que a mensagem foi recebida sem erros. Assim, quando o remetente
recebe um sinal *ACK*, ele sabe que o pacote enviado foi recebido com sucesso.
Caso ele não receba esse sinal em um tempo pré-estabelecido ou mesmo receba um
*NACK*, ele sabe que precisa reenviar o pacote.

Mas, como saber qual *ACK* está relacionado com qual pacote enviado? Aqui
entram alguns algoritmos de controle. O primeiro deles é o *stop and go*. 

A ideia do *stop and go* é muito simples; o remetente sempre aguarda a chegada
do *ACK* de um pacote para enviar o próximo. Assim, ele pode utilizar apenas um
    bit para identificar o pacote enviado. Se formos considerar os **estados**
    do remetente, temos:

* Aguardando pela mensagem 0 para ser enviada; 
* Aguardando pelo *ACK* 0;
* Aguardando pela mensagem 1 para ser enviada;
* Aguardando pelo *ACK* 1.

Caso o *ACK* esperado não chegue, o remetente retransmite a mensagem. O bit
identificador ou **bit de sequência** faz com que exista um sincronismo entre o
remetente e o destinatário, de modo que ambos sabem exatamente qual o
identificador da mensagem que deve vir a seguir. Esse arranjo serve inclusive
para lidar com o caso especial da própria mensagem de *ACK* estar corrompida.
Nesse caso, temos um destinatário que já recebeu um pacote, mas um remetente
que não sabe que o pacote foi recebido corretamente. Digamos que o pacote era o
pacote 0. O remetente vai tentar retransmitir o pacote 0, o destinatário - ao
receber novamente o pacote 0 quando já estava esperando pelo pacote 1 -, vai
ignorar o pacote e reenviar o *ACK 0*.

### 2.2. O protocolo TCP

[RFC 9293](https://datatracker.ietf.org/doc/html/rfc9293)

### 2.3. Gestão TCP

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/UYJP-6mhF6E" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/E4I6t0mI_is" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

### 2.4. Controle de congestão

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/Fm92xvIp6JY" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/cIHiSR4j3g4" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>


## 3. RPCs e RTPs

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/gnchfOojMk4" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

O conceito de enviar um pedido a um servidor e receber dele uma resposta se
assemelha muito ao uso de subrotinas na programação. O conceito de *remote
procedure call* (RPC) surge justamente para tornar invisível para o usuário
essa diferença. Para isso, este protocolo determina uma maneira unificada de
codificar as informações que devem ser transferidas através da rede, saindo de
um cliente e indo para um servidor. Essa abstração torna possível criar
integração entre serviços disponibilizados na web entre linguagens
completamente diferentes. Efetivamente, o RPC é a linguagem que manda no mundo
dos *microsserviços*.

RPCs podem ser utilizados tanto com TCP quanto com UDP. Originalmente, era mais
comum a sua utilização com UDP, mas implementações famosas como o *gRPC*,
criado pelo Google, tornaram comum o seu uso em conexões TCP.

O que é exclusivamente utilizado com conexões UDP, no entanto, é o
protocolo de transmissão de dados em tempo real (RTP/RTCP).

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/FD-MoBXsG1M" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>
