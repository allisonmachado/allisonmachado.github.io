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

<h2 id="2-Adapters">2 - Adapters</h2>

<pre>
  <code>
    interface BookInterface
    {
        public function open();
        public function turnPage();
    }

    class Person {
        public function read(BookInterface $book)
        {
            $book->open();
            $book->turnPage();
        }
    }

    class Book implements BookInterface
    {
        public function open()
        {
            echo 'Open the book.' . PHP_EOL;
        }

        public function turnPage()
        {
            echo 'Turn the page to read.' . PHP_EOL;
        }
    }

    class Kindle
    {
        public function turnOn()
        {
            echo 'Turn the kindle on.' . PHP_EOL;
        }

        public function pressNextButton()
        {
            echo 'Press the next button to read.' . PHP_EOL;
        }
    }

    class KindleAdapter implements BookInterface
    {
        private $kindle;

        public function __construct(Kindle $kindle)
        {
            $this->kindle = $kindle;
        }

        public function open()
        {
            $this->kindle->turnOn();
        }

        public function turnPage()
        {
            $this->kindle->pressNextButton();
        }
    }

    $allison = new Person();
    $allison->read(new Book());
    $allison->read(new KindleAdapter(new Kindle()));
  </code>
</pre>