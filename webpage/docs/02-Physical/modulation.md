---
title: Modulação e multiplexação
sidebar_position: 3
slug: /modulation
---

# Conceitos de modulação e multiplexação

## 1. Non-return-to-zero

Os sinais digitais podem ser representados por ondas quadradas, onde cada nível
de tensão corresponde a um valor binário (0 ou 1). Esse tipo de representação é
intuitivo e simples de implementar, mas apresenta alguns desafios importantes.
Um dos principais problemas é o consumo de potência, já que mudanças bruscas de
nível de tensão aumentam a dissipação de energia no meio de transmissão e nos
circuitos eletrônicos envolvidos.

Além disso, a transmissão contínua de um mesmo nível de tensão pode dificultar
a sincronização entre transmissor e receptor, o que leva à necessidade de
técnicas para evitar a perda de alinhamento temporal dos bits.

O esquema Non-Return-to-Zero (NRZ) é uma técnica básica de codificação onde o
sinal mantém o mesmo nível de tensão para representar um bit durante todo o
período de símbolo. Isso simplifica a geração do sinal e reduz a largura de
banda necessária para a transmissão. No entanto, quando há longas sequências de
zeros ou uns, a falta de transições no sinal pode causar dificuldades para o
receptor identificar corretamente os limites dos bits. Isso ocorre porque a
ausência de variação no nível de tensão pode impedir que o receptor
re-sincronize seu clock de amostragem, resultando em erros de interpretação dos
dados transmitidos. Para mitigar esse problema, técnicas como a codificação de
linha, incluindo o uso do código Manchester e esquemas como 4B/5B e 8B/10B, são
aplicadas para garantir que transições periódicas aconteçam, facilitando a
recuperação do sinal e reduzindo a taxa de erro na transmissão. resultando em
erros de interpretação e exigindo técnicas auxiliares para garantir a
sincronização adequada.

## 2. O problema da sincronização

A sincronização é essencial para garantir que o receptor interprete
corretamente os dados transmitidos. O clock do sistema define a taxa na qual os
bits são transmitidos, mas quando o receptor não consegue sincronizar-se com o
transmissor, ocorrem erros de interpretação, resultando em perda de pacotes e
degradação do sinal.

Uma solução simples seria enviar um sinal de clock junto com os dados,
permitindo que o receptor acompanhe a temporização correta. No entanto, isso
aumentaria a quantidade de condutores necessários, elevando os custos e a
complexidade da transmissão. Além disso, em meios de comunicação sem fio ou de
alta velocidade, essa abordagem pode ser impraticável devido à atenuação e
interferências externas.

### Código Manchester

Uma alternativa eficiente é o código Manchester, uma técnica de codificação
onde cada bit é representado por uma transição de nível dentro do período do
símbolo. No caso do Manchester diferencial, a transição ocorre
independentemente do nível anterior, reduzindo a possibilidade de erros de
interpretação causados por inversões de fase.

Esse método garante que haja sempre uma mudança de nível, permitindo que o
receptor sincronize-se automaticamente ao identificar transições no sinal. No
entanto, essa técnica tem como desvantagem o fato de dobrar a frequência de
transmissão, exigindo uma largura de banda maior. Por exemplo, ao comparar o
código Manchester com a codificação 4B/5B, percebe-se que o primeiro requer o
dobro da largura de banda do sinal original, enquanto o segundo adiciona apenas
25% de overhead. Essa diferença torna o código Manchester menos eficiente em
cenários onde a largura de banda é um recurso crítico, como em enlaces de longa
distância ou redes de alta velocidade. Por esse motivo, é mais comum em redes
locais de curta distância, como a Ethernet clássica, onde a qualidade do sinal
pode ser melhor controlada.

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
