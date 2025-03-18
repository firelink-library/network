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

### 2.2. O protocolo TCP

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
