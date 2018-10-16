---
title: Conceitos Básicos
---
<script src='https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML' async></script>

# Conceitos Básicos

Para ter sucesso no uso de qualquer Braço Robótico, mesmo que inferior em recursos quanto ao ARR-7, é preciso o domínio de alguns conceitos fundamentáis, como o que é Tensão e Corrente, módulos básicos do Arduino e um pouco de programação.

<!--more-->

## O que é Tensão e Corrente

Nesta oficina não iremos aprofundar no conceito de tensão e corrente, já que para sua compreensão é necessário também o entendimento do que é Resistência. Porém até o momento iremos nos conter como entendimento ludico destes conceitos.

A Tensão é medida em Volts, não se usa o termo "Voltagem" pois é um erro de tradução deslegante para o conceito. 

A Tensão pode ser comparado de forma didática a força que se exerce a uma corda, imagine uma corda de pular sendo esticada, por duas crianças que puxam de cada lado, A tensão está ali presente, de forma equilibrada quando as duas crianças aplicam a mesma força nas duas pontas. Porém se uma das crianças for mais forte que a outra, haverá o movimento para o lado da criança mais forte este movimento podemos chamar de corrente, e ele será tão intenso quanto a força que se aplica a um dos lados, chamaremos o lado mais forte de "positivo" o mais fraco de "negativo", com a presença de movimento temos então a corrente, que se for muito grande pode junto com a tensão muito alta, calsar o rompimento da corda ou a queda de um dos jovens danificando o circuito (no caso os dois jovens e a corda). 

Neste exemplo lúdico a tensão causará o movimento (corrente), que é medida em _Amper_ e erroneamente é chamada de _amperagem_ também por um erro de tradução do termo. A corrente, então, fluirá do lado mais fraco (negativo) para o lado mais forte (positivo), e haverá uma resistência a este movimento, quanto maior for a resistência menor é a corrente, quanto maior a tenção maior é a corrente. A Resistência é medida em _ohms_ e usa a letra grega Omega para representa-la.

Sendo assim, neste simples exemplo  temos uma fórmula matemática que representa  a relação entre estes conceitos, sendo **T** o valor da Tensão em volts (_v_), **I** o valor da corrente em Amperes (_A_) e **R** o valor da resistência em _ohms_ ( $ \Omega $ ):

$$
I = \frac{T}{R}
$$

Nestes projetos iremos sempre lidar com baixas tensões, que deverão ser sempre o valor de 5V, mas a corrente vária e veremos mais a frente mais detalhes. Em nosso projetos lidaremos com baixas correntes, mas se algo for montado errado poderá causar a queima da fonte por drenar muita corrente da mesma.

Observe o quanto isso é importante. A tensão deve sempre ser a especificada no caso 5V a fonte usada deve ser, portanto, capaz de atender esta tensão, mas pode fornecer corrente maior que a necessária, é sempre bom deixarmos uma margem de 10%, ou seja, se no total seu circuito drenar uma corrente de 800mA (oitocentos mileamper), é bom que sua fonte seja capaz de fornecer 1A, escolhemos este valor porque é o mais próximo do comercialmente disponível.

Fique atento, como pode ver o valor da tensão é fixo o circuito sempre irá funcionar na tensão especificada, no caso dos nossos serão 5V na sua maioria. Mas a corrente, varia conforme o funcionamento do circuito, podendo ocorrer picos, e a fonte deve ser capaz de atender a estes picos.

## Arduino e Módulos Básicos

## A programação

Não será possível entrar em detalhes sobre o que se precisa aprender de programação aqui, pois não é nosso objetivo aqui apresentar os conceitos mínimos necessário, espera-se que o usuário já tenha conhecimento básico de programação com o Arduino, por exemplo seja capaz de instalar uma nova biblioteca, comunicar via serial, usar a função setup() e loop(), criar novas funções simples, usar as funções das bibliotecas instaladas.

Não usaremos nenhum recurso avançado do Arduino aqui, todos os recursos são básicos e no caso da funções intermediário.
