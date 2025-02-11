---
title: Modulação e multiplexação
sidebar_position: 3
slug: /modulation
---

import SyncProblem from '@site/static/img/sync_problem.png';

# Conceitos de modulação e multiplexação

## 1. Non-return-to-zero

Quando vemos uma onda quadrada, geralmente assumimos que o sinal começa em 0,
mas nem sempre isso é o que acontece de fato. Considerando que alguns dos meios
de comunicação tem atenuação de componentes de baixa frequência, isso significa
filtrar qualquer variação causada na média de potência do sinal. A implicação
disso é que um sinal desequilibrado pode acabar se degradando. A solução?
Modificar os níveis lógicos de modo que o valor lógico baixo seja um nível de
tensão negativa. Surge então o sinal **Non-return-to-zero**.

<img 
  src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTqaqJfnTJ-Q2DtgxQvm3z3WzfB6OWrPft5AQ&s"
  alt="NRZ" 
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '40vh',
    marginRight: 'auto'
  }} 
/>
<p><center>Fig. - O sinal do tipo Non-Return-to-Zero, como o nome implica, não
retorna a zero. Isso ajuda a manter o sinal balanceado.</center></p>

## 2. O problema da sincronização

Considere o seguinte: foi enviado, através de um fio condutor, o sinal abaixo.

<img 
  src={SyncProblem}
  alt="Sync Problem"
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '40vh',
    marginRight: 'auto'
  }} 
/>
<p><center>Fig. - Sinal digital enviado e o seu clock gerador.</center></p>

Do que precisamos para interpretar o sinal eletronicamente? De nada mais do que
um sistema capaz de ler os níveis lógicos do sinal com velocidade o suficiente
de modo que satisfaça o período natural de sua oscilação. Em outras palavras,
precisamos de um leitor que seja ao menos capaz de realizar a leitura na
frequência do sinal de *clock*.

Os mais atentos já devem ter identificado o problema. Afinal, não é comum que
se envie junto aos dados também o sinal de *clock*; isso imputa ao destinatário
a missão de decodificar, também, o período de comunicação do sinal obtido. Essa
missão não é particularmente problemática quando consideramos os períodos em
que há variação de sinal - quando o pulso de 1 ou 0 dura exatamente um ciclo -;
no entanto, há ocasiões em que o sinal passa alguns ciclos em 1 ou em 0. Quando
isso ocorre, não há nenhuma maneira de encontrar o período do sinal. Em outras
palavras, não há como **sincronizar o clock**.

Uma solução ingênua é passar a enviar o sinal de clock junto do sinal de dados.
O problema dessa abordagem é um tanto óbvio: custo. Não é economicamente viável
- em especial quando há significativa distância entre o remetente e o
destinatário - utilizar um segundo condutor para outro sinal apenas para
sincronização de clock.

A segunda pior solução possível, mas que ainda resolve de forma definitiva o
problema, é utilizar a **codificação manchester**.

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/XKtxxZ327UM" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

Com essa codificação, é possível enviar o sinal de clock junto com os dados em
um único condutor. Melhor, mas tem um outro problema claro: a taxa de
transmissão necessária para enviar um sinal com codificação manchester
**dobra**. Mesmo com essa clara limitação, a solução por codificação manchester
era utilizada nas primeiras versões do protocolo Ethernet.

### Non-return-to-zero inverted (NRZ-I)

Outra solução é o NRZ-I (Non-Return-to-Zero Inverted), onde a transição de
nível de tensão ocorre apenas quando um bit '1' é transmitido. Isso resolve o
problema para sequências de uns, pois mantém uma alternância mínima no sinal.
No entanto, ainda apresenta dificuldades para longas sequências de zeros, onde
não há mudanças de estado, tornando a sincronização desafiadora.

Para mitigar os problemas do NRZ-I, surgiram técnicas de codificação como o
4B/5B e o 8B/10B. No esquema 4B/5B, cada grupo de 4 bits é convertido em um
código de 5 bits, garantindo que haja transições suficientes para
sincronização. Já no 8B/10B, utilizado em redes de alta velocidade como o
Gigabit Ethernet e Fibre Channel, 8 bits são mapeados para 10 bits, assegurando
um balanceamento de carga DC e a presença de transições regulares no sinal.
Essas técnicas evitam longas sequências de zeros com um overhead menor do que o
código Manchester, sendo amplamente utilizadas em redes modernas de alta
velocidade. No esquema 4B/5B, cada grupo de 4 bits é convertido em um código de
5 bits, garantindo que haja transições suficientes para sincronização. Já no
8B/10B, utilizado em redes de alta velocidade como o Gigabit Ethernet e Fibre
Channel, 8 bits são mapeados para 10 bits, assegurando um balanceamento de
carga DC e a presença de transições regulares no sinal. Essas técnicas evitam
longas sequências de zeros com um overhead menor do que o código Manchester,
sendo amplamente utilizadas em redes modernas de alta velocidade.

## 3. Modulação

A modulação é a técnica utilizada para transmitir sinais digitais em meios
analógicos, transformando bits em símbolos. Essa conversão é necessária porque
muitos meios de transmissão, como ondas de rádio e fibra óptica, operam melhor
com sinais contínuos ao invés de pulsos discretos. Além disso, a modulação
permite que diferentes sinais compartilhem o mesmo meio sem interferência
significativa, aumentando a eficiência da transmissão e permitindo comunicações
de longa distância com menor perda de qualidade. Esse processo é fundamental
para permitir a transmissão eficiente de informações em diferentes meios
físicos, como cabos coaxiais, fibra óptica e ondas de rádio. Cada símbolo pode
representar múltiplos bits, influenciando diretamente a taxa de transmissão
(baud rate) e a eficiência espectral do sistema.

### Tipos de modulação

- **Modulação por amplitude (ASK - Amplitude Shift Keying)**: A informação é
  transmitida variando a amplitude da onda portadora. No caso binário, a
  presença ou ausência de um sinal pode representar os bits 1 e 0,
  respectivamente. Esse método é simples, mas suscetível a ruídos e
  interferências, tornando-o menos confiável em ambientes ruidosos.

- **Modulação por frequência (FSK - Frequency Shift Keying)**: Diferentes
  frequências são utilizadas para representar os bits. Por exemplo, uma
  frequência mais baixa pode indicar um bit 0, enquanto uma frequência mais
  alta pode indicar um bit 1. Essa modulação é mais robusta contra ruídos do
  que a ASK e é utilizada em sistemas como modems antigos e comunicação via
  rádio.

- **Modulação por fase (PSK - Phase Shift Keying)**: A fase da onda portadora é
  alterada para codificar informações. Um exemplo comum é o BPSK (Binary PSK),
  onde dois estados de fase distintos representam os bits 0 e 1. Uma variação
  mais eficiente é o QPSK (Quadrature PSK), que utiliza quatro estados de fase
  para transmitir dois bits por símbolo, dobrando a eficiência espectral.

- **Modulação por quadratura (QAM - Quadrature Amplitude Modulation)**: Essa
  técnica combina variações na amplitude e na fase da onda portadora,
  permitindo representar múltiplos bits por símbolo. Por exemplo, o esquema
  16-QAM usa 16 estados distintos, cada um representando 4 bits. A QAM é
  amplamente utilizada em sistemas modernos como redes Wi-Fi, televisão digital
  e comunicação via satélite, pois permite um alto rendimento de dados sem
  aumentar excessivamente a largura de banda necessária.

Essas técnicas são essenciais para aumentar a eficiência espectral e a taxa de
transmissão sem exigir proporcionalmente mais largura de banda. A escolha do
tipo de modulação depende do meio de transmissão, da robustez necessária contra
ruídos e da capacidade de processamento dos dispositivos envolvidos.

## 4. Multiplexação

A multiplexação é a técnica de combinar múltiplos sinais em um único canal de
transmissão, otimizando o uso dos recursos disponíveis. Um exemplo prático
disso é o uso da multiplexação por divisão de tempo (TDM) em redes de
telefonia, onde múltiplas chamadas de voz compartilham o mesmo meio físico
alternando pequenos intervalos de tempo para cada transmissão. Outro exemplo é
a multiplexação por divisão de frequência (FDM) usada na transmissão de rádio e
televisão, onde diferentes estações ocupam diferentes faixas de frequência
dentro do espectro disponível. Para isso, são utilizadas bandas de guarda para
evitar interferências entre os sinais.

### Tipos de multiplexação

- **Multiplexação por divisão de frequência (FDM)**: Cada sinal é transmitido
  em uma faixa de frequência distinta dentro do mesmo meio físico.
- **Multiplexação por divisão de tempo (TDM)**: Os sinais compartilham o mesmo
  canal físico, mas em intervalos de tempo diferentes.
- **Multiplexação por divisão de código (CDM)**: Cada usuário transmite
  utilizando um código único, permitindo que múltiplos sinais coexistam sem
  interferência significativa.

Essas técnicas são fundamentais para otimizar a transmissão de dados em redes
de computadores, permitindo um uso mais eficiente da infraestrutura de
comunicação.
