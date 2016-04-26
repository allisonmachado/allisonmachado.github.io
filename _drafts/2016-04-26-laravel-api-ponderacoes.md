---
layout: post
title:  Laravel API - Ponderações
tags:
- API
- PHP
- Laravel
---

<h2 id="1-Tratamento">1 - Tratamento</h2>

<h3 id="1.1-O-Problema">1.1 - O Problema</h3>

<p>Para responder a uma simples requisição, é tentador escrever um controller que apenas retorne os valores contidos em uma tabela como no exemplo a seguir:</p>

<pre>
  <code>
      class PostsController extends BaseController {
        public function index() {
          return Post::all();
        }
      }
  </code>
</pre>

<p>Sabe-se que o framework Laravel é capaz de retornar os valores em formato JSON de forma transparente para o browser. Então, qual é o problema?</p>

<p>Primeiro, com este tipo de abordagem a resposta fica fortemente acoplada à estrutura contida no banco de dados da aplicação. Logo, em caso de mudança no banco, a resposta à requisição também muda. Portanto, os clientes podem não estar preparados a esta mudança no formato dos dados.</p>

<p>Outro problema é a falta de tratamento de possíveis erros de execução. Não há o devido tratamento dos códigos contios no cabeçalho de resposta das requisições. E também não há o envio de metadados que podem ser úteis aos consumidores da aplicação.</p>

<h3 id="1.2-Códigos-de-Resposta">1.2 - Códigos de Resposta</h3>

<p>Dependendo do resultado da requisição, é necessário atribuir um código de resposta HTTP apropriado, indicando o situação da requisição. Observe um exemplo:</p>

<pre>
  <code>
    public function show($id) {
      $post = Post::find($id);

      if (!$post) {
        return Response::json([
          'error' => ['message' => 'Post does not exist']
        ], 404);
      }

      return Response::json([
        'data' => $post->toArray()
      ], 200);
    }
  </code>
</pre>

<p>No exemplo acima, os códigos <code>200</code> e <code>404</code> são atribuídos de acordo com o resultado do processamento da requisição.</p>