---
layout: post
title:  Ensaiando Design Patterns (PHP)
tags:
- PHP
- Padrões
---

<h2 id="1-Decorator">1 - Decorator</h2>

<pre>
  <code>
    <?php

    class Sentence
    {
        private $text;

        public function __construct($text)
        {
            $this->text = $text;
        }

        public function log()
        {
            echo $this->text;
        }
    }

    abstract class SentenceDecorator
    {
        protected $sentence;

        public function __construct($sentence)
        {
            $this->sentence = $sentence;
        }

        public abstract function log();
    }

    class SentenceNewLineDecorator extends SentenceDecorator
    {
        public function log()
        {
            $this->sentence->log();
            echo PHP_EOL;
        }
    }

    class SentenceExclamationDecorator extends SentenceDecorator
    {
        public function log()
        {
            $this->sentence->log();
            echo '!!!';
        }
    }

    $sentence = new SentenceNewLineDecorator(
      new SentenceExclamationDecorator(
        new Sentence('Hello World')
      )
    );
    $sentence->log();
  </code>
</pre>