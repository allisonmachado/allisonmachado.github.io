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

<h3 id="5-Chain-of-Responsibility">5 Chain of Responsibility</h3>

<pre>
    <code>
        class Car
        {
            public $brakeIsFine = true;
            public $tireIsFine  = true;
            public $wiperIsFine = true;
        }

        abstract class Checker
        {
            private $successor;

            public abstract function check($item);

            public function setSuccessor(Checker $successor)
            {
                $this->successor = $successor;
            }

            public function next($item)
            {
                if ($this->successor) {
                    $this->successor->run($item);
                }
            }

            public function run($item)
            {
                $this->check($item);
                $this->next($item);
            }
        }

        class BrakeChecker extends Checker
        {
            public function check($car)
            {
                if(!$car->brakeIsFine) {
                    throw new Exception('Brake in poor condition, Abort!');
                }
            }
        }

        class TireChecker extends Checker
        {
            public function check($car)
            {
                if(!$car->tireIsFine) {
                    throw new Exception('Tire in poor condition, Abort!');
                }
            }
        }

        class WiperChecker extends Checker
        {
            public function check($car)
            {
                if(!$car->wiperIsFine) {
                    throw new Exception('Windshield wiper in poor condition, Abort!');
                }
            }
        }

        $car = new Car();
        $car->wiperIsFine = false;

        $checker = new BrakeChecker();
        $tireChecker = new TireChecker();
        $wiperChecker = new WiperChecker();

        $tireChecker->setSuccessor($wiperChecker);
        $checker->setSuccessor($tireChecker);

        $checker->run($car);
    </code>
</pre>