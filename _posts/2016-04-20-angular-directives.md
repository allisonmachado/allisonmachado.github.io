---
layout: post
title:  Angular JS - Diretivas
tags:
- News
- Tags
- Blog
- Post
---

<h2 id="1-introducao">1 - Introdução</h2>

<p>Por meio de diretivas é possível extender o comportamento de atributos HTML.</p>

<p>Estrutura da definição de uma diretiva por meio de um objeto de configuração:</p>

<pre>
  <code>
    angular.module('myApp', []).directive('myDirective', function() {
     return {
      restrict: String,
      priority: Number,
      terminal: Boolean,
      template: String || Template Function: function(tElement, tAttrs) {...},
      replace: Boolean || String,
      scope: Boolean || Object,
      transclude: Boolean,
      controller: String || function (scope, elementattrs, transclude) {...},
      require: String,
      link: function(scope, iElement, iAttrs) {...},
      compile: function(tElement, tAttrs) {...}
     };
    });
  </code>
</pre>

<p>O objetivo principal das diretivas é ser o agente de manipulação de DOM.</p>

<h3 id="1.1-restrict">1.1 - restrict</h3>

<ul>
  <li>E - elemento: <code>&#60;mydirective /&#62;</code></li>
  <li>A - atributo: <code>&#60;div my-directive="expression"&#62;&#60;/div&#62;</code></li>
  <li>C - classe: <code>&#60;div class="my-directive: expression;"&#62;&#60;/div&#62;</code></li>
  <li>M - comentário: <code>&#60;!-- directive: my-directive expression --&#62;</code></li>
</ul>

<p>Valores podem ser combinados: <code>restrict: 'AE'</code></p>

<h3 id="1.2-replace">1.2 - replace</h3>

<ul>
  <li><code>true</code>: Indica que o elemento em que a diretiva foi declarada será substituido pelo template da diretiva.</li>
  <li><code>false</code>: Indica que o template da diretiva será anexado ao elemento em que a diretiva foi declarada.</li>
</ul>

<h3 id="1.3-scope">1.3 - scope</h3>

<ul>
  <li><code>true</code>: Não é criado um novo escopo. A diretiva herda o escopo de acordo com a hierarquia DOM. <em>*Este é o valor padrão em caso de omissão.</em></li>
  <li><code>false</code>: Será criado um novo escopo, mas herda atributos do escopo pai, podendo sobreescrevê-los.</li>
  <li><code>Object</code>: Escopo isolado e independente.</li>
</ul>

<h2 id="2-compilacao-vs-linkagem">2 - Compilação vs Linkagem</h2>

<p>A função de compilação <code>compile</code> não tem acesso ao escopo. Esta função é executada antes da função de linkagem <code>link</code>.</p> 

<p>O objetivo da função de compilação é modificar aquilo que é comum a todos os elementos definidos por meio da diretiva. Por exemplo, modificar parte do template que é comum a todos os elementos.</p>

<p>A função de linkagem tem acesso ao escopo e é executada de forma individual para cada elemento.</p>

<h2 id="3-possibilidades">3 - Possibilidades</h2>

<h3 id="3.1-observar-escopo">3.1 - Observar escopo</h3>
<p>Em uma diretiva, para atualizar um elemento de acordo com a alteração de uma variável do escopo, utiliza-se a função de linkagem (<code>watch</code>):</p>

<pre>
  <code>
    $scope.$watch('name', function(name) {
      iElement.text('Hello ' + name + '!');
    });
  </code>
</pre>

<p></p>

<h3 id="3.2-parametros-para-linkagem">3.2 - Parâmetros para função de linkagem</h3>

<p>É possível passar parâmetros para a função de linkagem por meio de atributos e acessá-los por meio de <code>attrs</code></p>

<h3 id="3.3-escutar-eventos">3.3 - Escutar eventos</h3>

<p>Também é possível escutar por eventos dentro de uma diretiva na função de linkagem</p>

<pre>
  <code>
    iElement.bind('click', function() {
      $scope.name = 'abc';
      $scope.apply(); // Propagar mudança de escopo que ocorre dentro da diretiva
    })
  </code>
</pre>

<p>Para capturar exceções lançadas em <code>apply()</code>:</p>
<pre>
  <code>
    iElement.bind('click', function() {
      $scope.apply(function() {
        $scope.name = 'abc';
      });
    })
  </code>
</pre>

<h3 id="3.4-acessar-parametros-em-eventos">3.4 - Acessar parâmetros em eventos</h3>

<p>Eventos são executados fora do contexto do framework Angular. Para acessar parâmetros de fora deste contexto, use o serviço <code>$parse</code>:</p>

<pre>
  <code>
    myApp.directive('demoGreet', function($parse) {
      return {
        link: function linkFn(scope, iElement, attrs {
          iElement.bind('click', function() {
            $scope.apply(function() {
              $parse(attrs.demoGreet).assign(scope, 'abc');
            });
          })      
        }
      };
    });
  </code>
</pre>