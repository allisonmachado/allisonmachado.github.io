---
layout: post
title:  Angular JS - Mentalidade
tags:
- Angular
- Javascript
- Front-end
---

<h2 id="1-Mentalidade">1 - Mentalidade</h2>

<ul>
  <li>Separar manipulação de DOM da lógica da aplicação;</li>
  <li>Disassociar o desenvolvimento back-end do front-end, para permitir o desenvolvimento paralelo por meio de interfaces bem definidas;</li>
  <li>Fazer com que tarefas comuns se tornem triviais;</li>
  <li>Manipular o DOM de forma declarativa (alto nível);</li>
  <li>Estender a sintaxe HTML para expressar componentes da sua aplicação de forma clara e sucinta.</li>
</ul>

<h2 id="2-Organização">2 - Organização</h2>

<ul>
  <li>Controllers não devem manipular o DOM;</li>
  <li>Controllers devem declarar o comportamento:</li>
  <ul>
    <li>O que acontece se o usuário disparar tal evento?</li>
    <li>Onde encontro este dado?</li>
  </ul>
  <li>Services não devem manipular o DOM;</li>
  <li>Services definem regras de negócio e contém lógica independente de view;</li>
  <li>Diretivas são reponsáveis por manipular o DOM e extender HTML;</li>
  <li>Nos <u>templates</u> o <strong>escopo</strong> é para <em>leitura</em>, e nos <u>controllers</u> para <em>escrita</em>;</li>
  <li>O escopo não é o model, mas contém referência para os models;</li>
  <li>Use módulos como um grupamento de código reutilizável - controllers, services, diretivas e etc;</li>
  <li>Geralmente um módulo por aplicação;</li>
  <li>Caso tenha multiplos módulos por aplicação, agrupe-os por funcionalidade e não por tipo de estrutura (e.g. um módulo para controllers, outro para services e etc).</li>
</ul>