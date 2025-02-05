---
title: As camadas de rede
sidebar-position: 2
slug: /layers
---

import Admonition from '@theme/Admonition';

# Modelos de comunicação

## 1. O que é TCP/IP e Modelo OSI?

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/CRdL1PcherM" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>

Não é nada controverso afirmar que hoje um computador incapaz de se comunicar
com outros dispositivos tem sua funcionalidade severamente reduzida e,
portanto, sua utilidade limitada. No entanto, como é possível que computadores
troquem informações? Em última instância - assim como tudo que envolve
computação - trata-se de uma composição de 1s e 0s sendo enviados entre
dispositivos. 

Nesse momento, pode ser que surja uma pergunta bastante oportuna: se basta
apenas estabelecer uma conexão física através da qual é possível transmitir
informações binárias, por quê diabos há tantos padrões e protocolos envolvidos
nas tecnologias de redes de computadores? A pergunta, apesar de ser bastante
oportuna, tem uma resposta bem simples: padronização. Assim como existem
convenções e normas que definem como pode-se combinar bits para formar
estruturas de dados e tipos de variáveis, também fez-se necessário estabelecer
padrões para a comunicação entre computadores. Quando se fala em modelos de
comunicação em rede, os dois padrões que valem a pena ser discutidos são os
modelos OSI (Open Systems Interconnection) e TCP/IP (Transmission Control
Protocol / Internet ProtocolTCP/IP (Transmission Control Protocol / Internet
Protocol).

## 1.1. Modelo OSI

O Modelo OSI (Open Systems Interconnection) é um modelo conceitual que
caracteriza e padroniza as funções de um sistema de telecomunicações ou
computação em sete camadas abstratas. Este modelo foi desenvolvido pela
International Organization for Standardization (ISO) em 1984. Este modelo é
composto por sete camadas, que podem ser vistas na imagem a seguir:

<img 
  src="https://cecead.com/wp-content/uploads/2020/07/Modelo-OSI.png"
  alt="Camadas do modelo OSI" 
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '40vh',
    marginRight: 'auto'
  }} 
/>

### 1.1.1. Camada Física (Physical)

A Camada Física é responsável pela transmissão e recepção de dados brutos não
estruturados através de um meio físico. Ela lida com a conexão física entre
dispositivos e a transmissão de bits.

Cabos Ethernet, conectores RJ45 e a transmissão de sinais elétricos ou ópticos
através de fibras ópticas são exemplos práticos desta camada.

### 1.1.2. Camada de Enlace de Dados (Data Link)

Esta camada garante a transferência de dados livre de erros entre dois
dispositivos fisicamente conectados. Ela detecta e, opcionalmente, corrige
erros que possam ocorrer na camada física.

O protocolo Ethernet, que define como os pacotes de dados são formatados e
processados para transmissão e recepção, é um exemplo. Switches de rede operam
principalmente nesta camada.

### 1.1.3. Camada de Rede (Network)

A Camada de Rede é responsável pelo roteamento de pacotes, incluindo o
endereçamento, a decomposição e o reagrupamento de pacotes. Ela lida com a
transferência de dados entre diferentes redes.

O protocolo IP (Internet Protocol) é um exemplo clássico, onde endereços IP são
utilizados para encaminhar pacotes de dados para o destino correto.

### 1.1.4. Camada de Transporte (Transport)

Esta camada assegura a entrega correta e completa dos dados entre pontos
finais. Ela oferece controle de fluxo, segmentação/dessegmentação e controle de
erros.

Os protocolos TCP (Transmission Control Protocol) e UDP (User Datagram
Protocol) são exemplos desta camada. Enquanto o TCP oferece conexões orientadas
à conexão e confiáveis, o UDP oferece um serviço mais simples e sem conexão.

### 1.1.5. Camada de Sessão (Session)

A Camada de Sessão estabelece, gerencia e termina as sessões entre dois pontos
de comunicação. Ela também oferece controle de diálogo e sincronização.

APIs de sockets em sistemas operacionais que permitem a abertura, a manutenção
e o encerramento de sessões são exemplos desta camada. 

### 1.1.6. Camada de Apresentação (Presentation)
Esta camada é responsável pela tradução, compressão e criptografia de dados.
Ela garante que os dados enviados por uma aplicação em um sistema sejam
legíveis pelo aplicativo de destino em outro sistema.

Formatos de dados como JPEG para imagens ou SSL/TLS para a segurança da
informação são tratados nesta camada.

### 1.1.7. Camada de Aplicação (Application)
A Camada de Aplicação é a mais próxima do usuário final. Ela fornece serviços
de rede para aplicativos de software.

Protocolos como HTTP para navegação na web, FTP para transferência de arquivos
e SMTP para e-mail são exemplos que operam nesta camada.

## 1.2. O modelo TCP/IP e sua relação com o OSI

O Modelo TCP/IP, desenvolvido pelo Departamento de Defesa dos Estados Unidos na
década de 1970, é um conjunto de protocolos de comunicação usados para
interconectar dispositivos de rede na Internet. Este modelo é mais simplificado
que o OSI, sendo estruturado em quatro camadas: Camada de Link de Rede
(equivalente às camadas física e de enlace de dados do OSI), Camada de Internet
(similar à camada de rede do OSI), Camada de Transporte e Camada de Aplicação.
O TCP/IP é amplamente utilizado na prática, principalmente por ser o modelo
base para a Internet, garantindo a interoperabilidade entre diferentes sistemas
e dispositivos em uma rede global. A figura abaixo demonstra claramente as
camadas do modelo TCP/IP e sua correlação com o modelo OSI.

<img 
  src="https://www.guru99.com/images/1/102219_1135_TCPIPvsOSIM1.png"
  alt="TCP/IP vs OSI" 
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '40vh',
    marginRight: 'auto'
  }} 
/>

Apesar de o modelo TCP/IP ser mais utilizado na prática, especialmente no que
se refere à Internet, o modelo OSI ainda é muito referenciado e ensinado no
âmbito acadêmico e profissional. O motivo para isso é sua natureza detalhada e
descritiva, que oferece uma compreensão mais clara e organizada das diferentes
funções e processos em uma rede. O Modelo OSI é frequentemente utilizado como
um guia teórico para entender melhor a interação entre diferentes camadas de
rede, facilitando o aprendizado e a análise de problemas de rede. Mesmo que o
TCP/IP seja mais prevalente em implementações práticas, o conhecimento do
modelo OSI é valioso para profissionais da área de redes para compreender os
princípios subjacentes à comunicação de dados.

## 1.3. Exemplo prático de modelos de rede

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/3kfO61Mensg" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
