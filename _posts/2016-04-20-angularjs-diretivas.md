---
layout: post
title:  Angular JS - Diretivas
tags:
- News
- Tags
- Blog
- Post
---

<h2 id="Conteúdo">Conteúdo</h2>

<ol>
  <li><a href="{{ baseurl }}#1-introducao">Introdução</a></li>
    <ol>
      <li><a href="{{ baseurl }}#1.1-restrict">restrict</a></li>
      <li><a href="{{ baseurl }}#1.2-replace">replace</a></li>
      <li><a href="{{ baseurl }}#1.3-scope">scope</a></li>
    </ol>
  <li><a href="{{ baseurl }}#2-compilacao-vs-linkagem">Compilação vs Linkagem</a></li>
  <li><a href="{{ baseurl }}#3-utilidades-basicas">Utilidades Básicas</a></li>
    <ol>
      <li><a href="{{ baseurl }}#3.1-parametros">Parametros</a></li>
      <li><a href="{{ baseurl }}#3.2-observar-escopo">Observar escopo</a></li>
      <li><a href="{{ baseurl }}#3.3-escutar-eventos">Ecutar eventos</a></li>
      <li><a href="{{ baseurl }}#3.4-acessar-parametros-em-eventos">Aessar parametros em eventos</a></li>
      <li><a href="{{ baseurl }}#3.5-utilizando-binding-de-forma-simples">Uilizando binding de forma simples</a></li>
      <li><a href="{{ baseurl }}#3.6-capturar-conteudo-da-diretiva">Capturar conteudo da diretiva</a></li>
    </ol>
</ol>

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

<h2 id="3-utilidades-basicas">3 - Utilidades Básicas</h2>

<h3 id="3.1-parametros">3.1 - Parâmetros</h3>
É possível enviar parâmetros para as diretivas e acessá-los em suas funções:
<pre>
  <code>   
    &lt;!doctype html&gt;
    &lt;html ng-app=&quot;myApp&quot;&gt;
      &lt;head&gt;
        &lt;meta charset=&quot;UTF-8&quot;&gt;
      &lt;/head&gt;
      &lt;body&gt;
        &lt;div&gt;
          &lt;greet name=&quot;Allison&quot;&gt;&lt;/greet&gt;
          &lt;greet name=&quot;Alessandra&quot;&gt;&lt;/greet&gt;
        &lt;/div&gt;
        &lt;script src=&quot;angular.min.js&quot;&gt;&lt;/script&gt;
        &lt;script type=&quot;text/javascript&quot;&gt;
          angular.module('myApp', [])
          .directive('greet', function() {
            return {
              scope: true,
              restrict: 'EA',
              template: function (element, attrs) {
                return '&lt;h1&gt;Hello '+ attrs.name +'!&lt;/h1&gt;';
              },
              replace: true
            };
          });
        &lt;/script&gt;
      &lt;/body&gt;
    &lt;/html&gt;
  </code>
</pre>


<h3 id="3.2-observar-escopo">3.2 - Observar escopo</h3>
<p>Em uma diretiva, para atualizar um elemento de acordo com a alteração de uma variável do escopo, utiliza-se a função de linkagem (<code>watch</code>):</p>

<pre>
  <code>
    &lt;!doctype html&gt;
    &lt;html ng-app=&quot;myApp&quot;&gt;
      &lt;head&gt;
        &lt;meta charset=&quot;UTF-8&quot;&gt;
      &lt;/head&gt;
      &lt;body ng-controller=&quot;myController&quot;&gt;
        &lt;div&gt;
          &lt;label&gt;Nome:&lt;/label&gt;
          &lt;input type=&quot;text&quot; ng-model=&quot;person.name&quot;&gt;&lt;br/&gt;
          &lt;greet name=&quot;Allison&quot;&gt;&lt;/greet&gt;
          &lt;greet name=&quot;Alessandra&quot;&gt;&lt;/greet&gt;
        &lt;/div&gt;
        &lt;script src=&quot;angular.min.js&quot;&gt;&lt;/script&gt;
        &lt;script type=&quot;text/javascript&quot;&gt;
          angular.module('myApp', [])
          .directive('greet', function() {
            return {
              scope: true,
              restrict: 'EA',
              replace: true,
              template: function (element, attrs) {
                return '&lt;h1&gt;Hello '+ attrs.name +'!&lt;/h1&gt;';
              },
              link: function (scope, element, attrs) {
                scope.$watch('person.name', function(name) {
                  if (name) 
                    element.text('Hello ' + name + '!');
                });
              }
            };
          })
          .controller('myController', ['$scope', function($scope){
            $scope.person = { name: null };
          }]);
        &lt;/script&gt;
      &lt;/body&gt;
    &lt;/html&gt;
  </code>
</pre>

<p></p>

<h3 id="3.3-escutar-eventos">3.3 - Escutar eventos</h3>

<p>Também é possível escutar por eventos dentro de uma diretiva na função de linkagem</p>

<pre>
  <code>

    &lt;!doctype html&gt;
    &lt;html ng-app=&quot;myApp&quot;&gt;
      &lt;head&gt;
        &lt;meta charset=&quot;UTF-8&quot;&gt;
      &lt;/head&gt;
      &lt;body ng-controller=&quot;myController&quot;&gt;
        &lt;div&gt;
          &lt;label&gt;Nome:&lt;/label&gt;
          &lt;input type=&quot;text&quot; ng-model=&quot;person.name&quot;&gt;&lt;br/&gt;
          &lt;greet name=&quot;Allison&quot;&gt;&lt;/greet&gt;
          &lt;greet name=&quot;Alessandra&quot;&gt;&lt;/greet&gt;
        &lt;/div&gt;
        &lt;script src=&quot;angular.min.js&quot;&gt;&lt;/script&gt;
        &lt;script type=&quot;text/javascript&quot;&gt;
          angular.module('myApp', [])
          .directive('greet', function() {
            return {
              scope: true,
              restrict: 'EA',
              replace: true,
              template: function (element, attrs) {
                return '&lt;h1&gt;Hello '+ attrs.name +'!&lt;/h1&gt;';
              },
              link: function (scope, element, attrs) {
                scope.$watch('person.name', function(name) {
                  if (name) 
                    element.text('Hello ' + name + '!');
                });

                element.bind('click', function() {
                  scope.$apply(function() {
                    scope.person.name = 'Mouse';
                  });
                })
              }
            };
          })
          .controller('myController', ['$scope', function($scope){
            $scope.person = { name: null };
          }]);
        &lt;/script&gt;
      &lt;/body&gt;
    &lt;/html&gt;

  </code>
</pre>

<h3 id="3.4-acessar-parametros-em-eventos">3.4 - Acessar parâmetros em eventos</h3>

<p>Eventos são executados fora do contexto do framework Angular. Para acessar parâmetros de fora deste contexto, use o serviço <code>$parse</code>:</p>

<pre>
  <code>
    element.bind('click', function() {
      scope.$apply(function() {
        $parse(attrs.paramName).assign(scope.person.name, 'newName');
      });
    });
  </code>
</pre>

<h3 id="3.5-utilizando-binding-de-forma-simples">3.5 - Utilizando binding de maneira simplificada</h3>

<pre>
  <code>
    &lt;!doctype html&gt;
    &lt;html ng-app=&quot;myApp&quot;&gt;
      &lt;head&gt;
        &lt;meta charset=&quot;UTF-8&quot;&gt;
      &lt;/head&gt;
      &lt;body ng-controller=&quot;myController&quot;&gt;
        &lt;div&gt;
          &lt;greet bind=&quot;allison&quot;&gt;&lt;/greet&gt;
          &lt;greet bind=&quot;alessandra&quot;&gt;&lt;/greet&gt;
        &lt;/div&gt;
        &lt;script src=&quot;angular.min.js&quot;&gt;&lt;/script&gt;
        &lt;script type=&quot;text/javascript&quot;&gt;
          angular.module('myApp', [])
          .directive('greet', function() {
            return {
              scope: true,
              restrict: 'EA',
              replace: true,
              template: function (element, attrs) {
                var template =  
                '&lt;div&gt;' + 
                  '&lt;h2&gt;Cumprimentar:&lt;/h2&gt;' +
                  '&lt;input type=&quot;text&quot; ng-model=&quot;person.'+ attrs.bind +'.name&quot;&gt;&lt;br/&gt;' + 
                  '&lt;h2&gt;Hello &#123;&#123; person.'+ attrs.bind +'.name &#125;&#125;!&lt;/h2&gt;' + 
                '&lt;/div&gt;';

                return template;
              }
            };
          })
          .controller('myController', ['$scope', function($scope){
            $scope.person = {};
          }]);
        &lt;/script&gt;
      &lt;/body&gt;
    &lt;/html&gt;
  </code>
</pre>

<h3 id="3.6-capturar-conteudo-da-diretiva">3.6 - Capturar conteúdo da diretiva</h3>

<p>Para recuperar o conteúdo presente dentro do elemento de sua diretiva, use <code>transclude</code>:</p>

<pre>
  <code>&lt;!doctype html&gt;
&lt;html ng-app=&quot;myApp&quot;&gt;
  &lt;head&gt;
    &lt;meta charset=&quot;UTF-8&quot;&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;div&gt;
      &lt;greet name=&quot;Allison&quot;&gt;&lt;em&gt;You are wellcome!&lt;/em&gt;&lt;/greet&gt;
      &lt;greet name=&quot;Alessandra&quot;&gt;&lt;strong&gt;How are you?&lt;/strong&gt;&lt;/greet&gt;
    &lt;/div&gt;
    &lt;script src=&quot;angular.min.js&quot;&gt;&lt;/script&gt;
    &lt;script type=&quot;text/javascript&quot;&gt;
      angular.module('myApp', [])
      .directive('greet', function() {
        return {
          transclude: true,
          restrict: 'EA',
          replace: true,
          template: function (element, attrs) {
            var template =  
            '&lt;div&gt;' + 
              '&lt;span&gt;Hello '+ attrs.name +', &lt;/span&gt;' +
              '&lt;span ng-transclude&gt;&lt;/span&gt;' +
            '&lt;/div&gt;';

            return template;
          }
        };
      });
    &lt;/script&gt;
  &lt;/body&gt;
&lt;/html&gt;</code>
</pre>