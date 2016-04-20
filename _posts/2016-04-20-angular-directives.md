---
layout: post
title:  Angular JS - Diretivas
tags:
- News
- Tags
- Blog
- Post
---

<h2>1 - Definição</h2>

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