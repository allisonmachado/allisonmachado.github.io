---
layout: post
title:  Alarme Simples
tags:
- DIY
- Eletrônica
- Homemade
- Circuits
---

<h2 id="Descrição">Descrição</h2>

<p>
    O projeto demonstra o funcionamento básico de Transistores e Relês. É um projeto caseiro e artesanal, que porém funcionou
    muito bem apesar da minha pouca habilidade com soldagem de pequenos componentes eletrônicos. Foi utilizado um Transistor
    2N222 e um Relê JRC-19F.
</p>

<h2 id="Circuito-do-alarme">Circuito do Alarme</h2>

<p>
    O circuito abaixo, desenhado à mão, expõe o estado inicial da aplicação. O Alarme encontra-se desligado pois o
    <i>switch on/off</i> está aberto. As portas ou janelas estão fechadas e o <i>switch de controle</i> (localizado no centro) não
    está ligado a nenhum polo:
</p>

<img src="{{ site.baseurl }}static/img/posts/alarme-simples/Alarme_01.jpg" class="img-responsive">

<p>
    Para aplicar tensão ao circuito, planejado para funcionar com 9VDC, ligue o <i>switch on/off</i>. O LED superior deve
    indicar que o circuito está energizado:
</p>

<img src="{{ site.baseurl }}static/img/posts/alarme-simples/Alarme_02.jpg" class="img-responsive">

<p>
    Conectando o <i>switch de controle</i> no polo superior, habilitamos o modo de controle, onde a <i>base</i> do transistor
    continua sem tensão, não podendo ativar o relê. Neste modo é possível saber se a janela/porta está devidamente
    fechada antes de se ativar o alarme. Observe o LED inferior neste modo, para saber se a porta/janela está devidamente
    fechada:
</p>

<img src="{{ site.baseurl }}static/img/posts/alarme-simples/Alarme_03.jpg" class="img-responsive">

<p>
    O próximo passo é ativar o circuito, invertendo o <i>switch de controle</i>, conectando-o no polo inferior. Nesta configuração,
    a tensão aplicada na <i>base</i> do transistor permanece baixa, próxima de 0VDC, pois recebe "voltagem negativa" por meio
    da conexão com o relê. A tensão positvia do resistor <i>pullup</i> conectada à base do transistor é sobreposta pela tensão negativa
    caso a porta/janela continue fechada:
</p>

<img src="{{ site.baseurl }}static/img/posts/alarme-simples/Alarme_04.jpg" class="img-responsive">

<p>
    Caso a porta/janela seja aberta, será aplicada tensão positiva na <i>base</i> do transistor que, por sua vez, permite a
    passagem de corrente ativando o relê. Quando o relê troca suas conexões internas, fornece tensão a um circuito responsável
    por ativar uma sirene ou auto-falante, soando o alarme. Observe que ao mesmo tempo, o relê perde a conexão com a tensão
    negativa (capaz de fornecer baixa tensão à <i>base</i> do transistor). Portanto, depois que o alarme soar, já não é
    sufisciente fechar a janela/porta para desativar o alarme, pois não será possível abaixar a tensão na base do transistor:
</p>

<img src="{{ site.baseurl }}static/img/posts/alarme-simples/Alarme_05.jpg" class="img-responsive">

<p>
    Para desativar o alarme, será necessário utilizar o <i>switch on/off</i>.
</p>

<h2 id="Circuito-oscilador">Circuito Oscilador</h2>

<p>
    Para soar o alarme foi utilizado um Alto-falante de duas polegadas e 6Ohms de impedância. Não basta aplicar 9V de
    corrente contínua direto no alto-falande, é necessário oscilar a tensão para que, no nosso caso, o alto-falante produza um ruído de alarme.
    O <i>circuito oscilador</i> utilizado foi o seguinte:
</p>

<img src="{{ site.baseurl }}static/img/posts/alarme-simples/Oscilador_01.jpg" class="img-responsive">

<p>
    Infelizmente não anotei os valores dos resistores e capacitores utilizados. Como processo para encontrá-los foi uma verdadeira
    descoberta (conectei os componentes em uma protoboard, e testei valores diferentes de resistores e capacitors), acabei 
    soldando o circuito e esquecendo fazer as anotações.
</p>

<h2 id="Imagens-da-montagem">Imagens da montagem</h2>

<p>
    A seguir, várias imagens da soldagem do circuito do alarme:
</p>

<img src="{{ site.baseurl }}static/img/posts/alarme-simples/CircuitoAlarme_01.jpg" class="img-responsive">
<img src="{{ site.baseurl }}static/img/posts/alarme-simples/CircuitoAlarme_02.jpg" class="img-responsive">
<img src="{{ site.baseurl }}static/img/posts/alarme-simples/CircuitoAlarme_03.jpg" class="img-responsive">
<img src="{{ site.baseurl }}static/img/posts/alarme-simples/CircuitoAlarme_04.jpg" class="img-responsive">
<img src="{{ site.baseurl }}static/img/posts/alarme-simples/CircuitoAlarme_05.jpg" class="img-responsive">

<p>
    A seguir, algumas imagens da soldagem do circuito oscilador:
</p>

<img src="{{ site.baseurl }}static/img/posts/alarme-simples/CircuitoOscilador_01.jpg" class="img-responsive">
<img src="{{ site.baseurl }}static/img/posts/alarme-simples/CircuitoOscilador_02.jpg" class="img-responsive">

<p>
    A seguir, algumas imagens da montagem do alarme:
</p>

<img src="{{ site.baseurl }}static/img/posts/alarme-simples/Montagem_01.jpg" class="img-responsive">
<img src="{{ site.baseurl }}static/img/posts/alarme-simples/Montagem_02.jpg" class="img-responsive">
<img src="{{ site.baseurl }}static/img/posts/alarme-simples/Montagem_03.jpg" class="img-responsive">
<img src="{{ site.baseurl }}static/img/posts/alarme-simples/Montagem_04.jpg" class="img-responsive">
<img src="{{ site.baseurl }}static/img/posts/alarme-simples/Montagem_05.jpg" class="img-responsive">

<h2 id="Instalação">Instalação</h2>

<p>
    Para instalar o alarme em portas ou janelas, é indicado o uso de sensores magnéticos como o da imagem a seguir:
</p>

<img src="{{ site.baseurl }}static/img/posts/alarme-simples/Sensor_01.png" class="img-responsive">

<p>
    Nos esquemas apresentados acima, com o objetivo de simplificar a explicação do funcionamento do circuito, utilizei o simbolo de um <i>switch</i>
    para representar este sensor aberto ou fechado.
</p>