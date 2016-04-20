---
layout: post
title:  Angular JS - Diretivas
tags:
- News
- Tags
- Blog
- Post
---

<h2>1 - Introdução</h2>

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

<h3>1.1 - restrict</h3>

<ul>
  <li>E - elemento: <code>&#60;mydirective /&#62;</code></li>
  <li>A - atributo: <code>&#60;div my-directive="expression"&#62;&#60;/div&#62;</code></li>
  <li>C - classe: <code>&#60;div class="my-directive: expression;"&#62;&#60;/div&#62;</code></li>
  <li>M - comentário: <code>&#60;!-- directive: my-directive expression --&#62;</code></li>
</ul>

<p>Valores podem ser combinados: <code>restrict: 'AE'</code></p>

<h3>1.2 - replace</h3>

<ul>
  <li><code>true</code>: Indica que o elemento em que a diretiva foi declarada será substituido pelo template da diretiva.</li>
  <li><code>false</code>: Indica que o template da diretiva será anexado ao elemento em que a diretiva foi declarada.</li>
</ul>

<h3>1.3 - scope</h3>

<ul>
  <li><code>true</code>: Não é criado um novo escopo. A diretiva herda o escopo de acordo com a hierarquia DOM. <em>*Este é o valor padrão em caso de omissão.</em></li>
  <li><code>false</code>: Será criado um novo escopo, mas herda atributos do escopo pai, podendo sobreescrevê-los.</li>
  <li><code>Object</code>: Escopo isolado e independente.</li>
</ul>

<h2>2 - Definição</h2>

<p>A função de compilação <code>compile</code> não tem acesso ao escopo. Esta função é executada antes da função de linkagem <code>link</code>.</p>

