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

<h3 id="3-Template-Method">3 - Template Method</h3>

<pre>
  <code>
    abstract class Html
    {
        private $title;

        public function __construct($title)
        {
            $this-&gt;title = $title;
        }

        public function build()
        {
            return '&lt;!DOCTYPE html&gt;'
                . '&lt;html&gt;'
                    . $this-&gt;makeHeader()
                    . $this-&gt;makeBody()
                . '&lt;/html&gt;';
        }

        private function makeHeader()
        {
            return '&lt;head&gt;'
                    . '&lt;title&gt;'. $this-&gt;title . '&lt;/title&gt;'
                 . '&lt;/head&gt;';
        }

        protected abstract function makeBody();
    }

    class HelloHtml extends Html
    {
        protected function makeBody()
        {
            return '&lt;body&gt;&lt;/body&gt;&lt;h1&gt;Hello World!&lt;/h1&gt;&lt;/body&gt;';
        }
    }

    class NotFoundHtml extends Html
    {
        protected function makeBody()
        {
            return '&lt;body&gt;&lt;h1&gt;404 - Page not found&lt;/h1&gt;&lt;/body&gt;';
        }
    }

    $response = new HelloHtml('Hello');
    echo $response-&gt;build();

    $response = new NotFoundHtml('Error');
    echo $response-&gt;build();
  </code>
</pre>

<h3 id="4-Strategy-Pattern">4 - Strategy Pattern</h3>

<pre>
    <code>
        interface Logger
        {
            public function log($data);
        }

        class FileLogger implements Logger
        {
            public function log($data)
            {
                echo 'Loggin to file -> ' . $data;
            }
        }

        class DatabaseLogger implements Logger
        {
            public function log($data)
            {
                echo 'Loggin to database -> ' . $data;
            }
        }

        class App
        {
            private $logger;

            public function __construct(Logger $logger)
            {
                $this->logger = $logger;
            }

            public function run()
            {
                $this->logger->log('Running app');
            }
        }

        $app = new App(new FileLogger());
        $app->run();
    </code>
</pre>