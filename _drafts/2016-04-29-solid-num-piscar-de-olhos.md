---
layout: post
title:  SOLID num piscar de olhos
tags:
- API
- PHP
- Laravel
---

<h2 id="1-Single Responsability">1 - Single Responsability</h2>

<p>Uma classe deve conter apenas uma responsabilidade. Deve-se extrair funcionalidades distintas em suas próprias classes, e fazer do sistema um conjunto de classes que interagem entre si. <em>"Programe para uma interface, não para uma implementação"</em> - defina as necessidades de sua classe por meio de interfaces. As implementações concretas destas interfaces devem se preocupar em como realizar e execuar o trabalho específico.</p>

<h2 id="2-Open-losed">2 - Open-Closed (extensão/modificação)</h2>

<p>Entidades devem estar abertas para extensão, porém fechadas para modificação. O objetivo é ter entidades capazes de ampliar suas funcionalidades sem modificar o código fonte. Para alcançar este objetivo, substitua o comportamento que pode ser estendido por uma interface. Novamente <em>"Programe para uma interface, não para uma implementação"</em>.</p>