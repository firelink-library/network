---
title: Comunicação cabeada
sidebar_position: 1
slug: /cables
---

import fullSignal from '@site/static/img/full_signal.png';
import partialSignals from '@site/static/img/partial_signals.png';

# Fundamentos da camada física

## 1. Relembrando Série de Fourier

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/r6sGWTCMz2k" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

## 2. Energia transmitida

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/Gka11q5VfFI" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

Os vídeos acima demonstram os conceitos básicos por trás do uso de séries de
senóides para a reconstrução de qualquer sinal e como isso pode ser analisado
de modo que sua distribuição de potência no espectro das frequências possa ser
avaliada. A pergunta que pode restar é: por quê fazer isso? Como isso se
encaixa no contexto de condutores elétricos?

A resposta é simples: os condutores elétricos servem para conduzir *sinais*.
Esses sinais, por sua vez, podem ser representados por uma somatória de ondas
senóides de frequências e amplitudes distintas. Sendo assim, qual é o requisito
básico para que um sinal chegue de forma **inteligível** ao seu destino? Antes
de responder a essa pergunta, permitam-me utilizar um exemplo do livro
"Computer Networks", de Tanembaum. Vamos avaliar um sinal digital e suas
componentes harmônicas - ou seja, a amplitude das senóides de cada frequência
que, quando juntas, reproduzem o sinal enviado -.

<img 
  src={fullSignal}
  alt="Sinal digital e suas harmônicas" 
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '40vh',
    marginRight: 'auto'
  }} 
/>
<p><center>Fig. - Um sinal digital e suas componentes harmônicas.</center></p>

Percebe-se, pela amplitude dos harmônicos apresentados acima, que a natureza do
sinal - sua frequência natural e a informação em si nele contida - influencia
diretamente na distribuição de potência por frequência (afinal, a amplitude dos
senóides tem proporção direta com a potência do sinal naquela frequência). Como
para nós é particularmente interessante a reconstrução desse sinal, vejamos
abaixo o impacto causado quando restringimos o sinal original a apenas alguns
de seus harmônicos.

<img 
  src={partialSignals}
  alt="Sinais parciais com harmônicos cortados" 
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '40vh',
    marginRight: 'auto'
  }} 
/>
<p><center>Fig. - Conforme diminuímos ou aumentamos a quantidade de harmônicos
disponíveis para representar o sinal original, diminui ou aumenta, também, a
fidelidade de sua reconstrução.</center></p>

Conseguimos, portanto, concluir dois aspectos elementares que regem a
transmissão de dados na camada física:

1. Todo sinal, não importa sua natureza, tem uma assinatura harmônica única.
   Sinais de alta frequência vão ter boa parte de sua potência atribuídas aos
   harmônicos de alta frequência.
2. Quando perdemos algumas frequências harmônicas, o sinal se degrada em
   proporção direta à contribuição dessas frequências com a potência do sinal.

Essas conclusões em si não nos dizem por quê é tão importante a análise no
espectro de frequências até que consideremos mais um fato a respeito da
transmissão de sinais:

**Com a exceção do vácuo perfeito, todo e qualquer meio para transmissão de
ondas (eletromagnéticas ou não) age como um filtro de frequências**


<img 
  src="https://i.redd.it/8nm53zavodr61.jpg"
  alt="Sinais parciais com harmônicos cortados" 
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '40vh',
    marginRight: 'auto'
  }} 
/>
<p><center>Surprised Gon</center></p>

Especificamente sobre condutores guiados (cabos), eles agem como filtros passa
baixa.

## 3. Banda de transmissão e ruído

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/BT_mWQjO-bo" 
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
        src="https://www.youtube.com/embed/FcXZ28BX-xE" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>


## 4. Tipos de transmissão

### 4.1. Pares trançados

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/JSb0xNMFyHY" 
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
        src="https://www.youtube.com/embed/ha3zVvwzMvY" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

### 4.2. Cabo coaxial

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/qzalvldADcQ" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>

### 4.3. Fibra ótica

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/G1Ke-H8I1uk" 
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
        src="https://www.youtube.com/embed/P8SFBKFvKFQ" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>
