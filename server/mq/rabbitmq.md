RabbitMQ
========

[RabbitMQ](https://www.rabbitmq.com/) 用了比較高階的協定實作

PHP example
-----------

參考 [RebbitMQ Tutorials](https://www.rabbitmq.com/getstarted.html) 第二個，當作是 Hello World 練習，以下使用 PHP 當主要語言，其他套件如下

* [php-amqplib](https://github.com/php-amqplib/php-amqplib) ，它有需要的 ext 可以參考 `composer.json`
* [symfony console](http://symfony.com/doc/current/components/console.html) ，可以直接下指令送訊息
* [Docker RebbitMQ](https://hub.docker.com/_/rabbitmq/)

`send.php` 程式碼

```php
use Symfony\Component\Console\Command\Command;
use Symfony\Component\Console\Input\InputInterface;
use Symfony\Component\Console\Output\OutputInterface;
use PhpAmqpLib\Connection\AMQPStreamConnection;
use PhpAmqpLib\Message\AMQPMessage;

class Send extends Command
{
    protected function configure()
    {
        $this
            ->setName('send')
            ->setDescription('Send message')
            ->setHelp("Send message");
    }

    protected function execute(InputInterface $input, OutputInterface $output)
    {
        $connection = new AMQPStreamConnection('localhost', 5672, 'guest', 'guest');
        $channel = $connection->channel();

        $channel->queue_declare('task_queue', false, false, false, false);

        foreach (range(1, 10000) as $v) {
            $msg = new AMQPMessage("[$v] Hello World!", array('delivery_mode' => 2));
            $channel->basic_publish($msg, '', 'task_queue');

            echo " [$v] Sent 'Hello World!'\n";
        }

        $channel->close();
        $connection->close();
    }
}
```

`receive.php` 程式碼

```php
use Symfony\Component\Console\Command\Command;
use Symfony\Component\Console\Input\InputInterface;
use Symfony\Component\Console\Output\OutputInterface;
use PhpAmqpLib\Connection\AMQPStreamConnection;

class Receive extends Command
{
    protected function configure()
    {
        $this
            ->setName('receive')
            ->setDescription('Send message')
            ->setHelp("Send message");
    }

    protected function execute(InputInterface $input, OutputInterface $output)
    {
        $connection = new AMQPStreamConnection('localhost', 5672, 'guest', 'guest');
        $channel = $connection->channel();

        $channel->queue_declare('hello', false, false, false, false);

        echo ' [*] Waiting for messages. To exit press CTRL+C', "\n";

        $count = 1;
        $callback = function($msg) use (&$count) {
            echo " [$count] Received ", $msg->body, "\n";
            $count++;
        };

        $channel->basic_qos(null, 1, null);
        $channel->basic_consume('task_queue', '', false, true, false, false, $callback);

        while(count($channel->callbacks)) {
            $channel->wait();
        }
    }
}
```

結果： Receiver 可以開很多個去監聽，原本一對一是 receiver 來不及，可是開到十多個時，幾乎是 send 一傳好，就完成了
