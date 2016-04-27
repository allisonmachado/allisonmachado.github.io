---
layout: post
title:  Angular JS - Mentalidade
tags:
- Angular
- Javascript
- Front-end
---

Pense no Angular como uma camada de software acima do JQuery e do DOM, capaz de organizar a estrutura font-end de uma aplicação, paralelamente eliminando a escrita de código <em>boilerplate</em>.  

<h2 id="1-Mentalidade">1 - Mentalidade</h2>

<ul>
  <li>Manipular o DOM de forma declarativa (alto nível) - manipule o dado e deixe o framework sincronizar a interface;</li>
  <li>Separar manipulação de DOM da lógica da aplicação;</li>
  <li>Fazer com que tarefas comuns se tornem triviais;</li>
  <li>Estender a sintaxe HTML para expressar componentes da sua aplicação de forma clara e sucinta.</li>
  <li>Disassociar o desenvolvimento back-end do front-end, para permitir o desenvolvimento paralelo por meio de interfaces bem definidas;</li>
</ul>

<h2 id="2-Organização">2 - Organização</h2>

<h3 id="2.1-Modules">2.1 - Modules (módulos)</h3>

<ul>
  <li>Módulo é o que o AngularJS usa para inicializar uma aplicação;</li>
  <li>Use módulos como um grupamento de código reutilizável - controllers, services, diretivas e etc;</li>
  <li>Módulos podem registrar outros módulos como dependências;</li>
  <li><code>ng-app</code> define o módulo de entrada da aplicação;</li>
</ul>

<h3 id="2.2-Controllers">2.2 - Controllers</h3>

<ul>
  <li>Use os controllers para declarar o estado inicial do escopo.</li>
  <li>Controllers devem declarar o comportamento do escopo:</li>
  <ul>
    <li>O que acontece se o usuário disparar tal evento?</li>
    <li>Onde encontro este dado?</li>
  </ul>
  <li>Controllers não devem manipular o DOM;</li>
  <li>Controllers não devem formatar entrada ou saída de dados;</li>
  <li>Controllers não devem compartilhar código da aplicação, devem conter a lógica de apenas uma view;</li>
  <li>Controllers não devem compartilhar o estado da aplicação;</li>
  <li>Considere como o <em>gateway</em> entre a view e o model.</li>
</ul>

<h3 id="2.3-Services">2.3 - Services</h3>

<ul>
  <li>Services definem regras reutilizáveis e implementações mutáveis;</li>
  <li>São singletons;</li>
  <li>Services não devem manipular o DOM;</li>
  <li>Services definem regras de negócio e contém lógica independente de view;</li>
</ul>

<h3 id="2.4-Scopes">2.4 - Scopes (escopo)</h3>

<ul>
  <li>O escopo é a ligação entro o controller e a view;</li>
  <li>O escopo não é o model, mas contém referência para os models;</li>
  <li>Nos <u>templates</u> o <strong>escopo</strong> é para <em>leitura</em>, e nos <u>controllers</u> para <em>escrita</em>;</li>
  <li>Controllers e diretivas possuem ponteiros para o escopo, não possuem ligação entre si.</li>
</ul>

<h3 id="2.5-Directives">2.5 - Directives (diretivas)</h3>

<ul>
  <li>Diretivas são reponsáveis por extender o comportamento de elementos HTML;</li>
  <li>Diretivas são reponsáveis por manipular o DOM;</li>
  <li>Prefira <u>definir</u> diretivas através <strong>tags</strong> e <strong>atributos</strong> em vez de <em>comentários</em> ou <em>classes</em>;</li>
  <li>Prefira declarar diretivas usando um <strong>objeto de definição</strong> em vez de uma <u>função de retorno</u>;</li>
  <li>Para evitar conflitos de nomes, definas suas próprias diretivas usando prefixos;</li>
  <li>Use um elemento quando for criar uma linguagem específica de domínio para as partes do seu sistema;</li> 
  <li>Use um atributo quando você está decorando um elemento existente com novas funcionalidades;</li>
  <li>Use a opção de escopo para criar escopos isoladas, criando diretivas reutilizáveis;</li>
</ul>

<h2 id="3-Dicas-e-Notas">3 - Dicas e Notas</h2>

<h3 id="3.1-ControllerAs-Sintax">3.1 - ControllerAs Sintax</h3>

<p>Existem duas formar de declaras o controller numa aplicação angular:</p>

<p>1. Injetando o escopo</p>
<pre>
  <code>
    &lt;html ng-app=&quot;main&quot;&gt;
      &lt;body ng-controller=&quot;simple&quot;&gt;
        &lt;h1&gt;&#123;{ message }}&lt;/h1&gt;
        &lt;script src=&quot;angular.js&quot;&gt;&lt;/script&gt;
        &lt;script type=&quot;text/javascript&quot;&gt;
          angular.module('main', []).
          controller('simple', ['$scope', function($scope){
            $scope.message = 'Hello World!';
          }])
        &lt;/script&gt;
      &lt;/body&gt;
    &lt;/html&gt;
  </code>
</pre>

<p>2. ControllerAs Sintax</p>
<pre>
  <code>
    &lt;html ng-app=&quot;main&quot;&gt;
      &lt;body ng-controller=&quot;simple as ctrl&quot;&gt;
        &lt;h1&gt;{% raw %}&#123;{ ctrl.message }}&lt;/h1&gt;
        &lt;script src=&quot;angular.js&quot;&gt;&lt;/script&gt;
        &lt;script type=&quot;text/javascript&quot;&gt;
          angular.module('main', []).
          controller('simple', ['$scope', function($scope){
            this.message = 'Hello World!';
          }])
        &lt;/script&gt;
      &lt;/body&gt;
    &lt;/html&gt;
  </code>
</pre>

<p>A vantagem de se usar a <em>ControllerAs Sintax</em> é que ela deixa explícita no HTML qual variável está sendo fornecida por qual controller. Quando o <code>$scope</code> é injetado, a herança de escopos pode tornar confusa a definição e o entendimento de qual variável do escopo está sendo utilizada.</p>