Title: RabbitMQ tutorial - Topics | RabbitMQ
Mapped Topic: Queues and message-driven systems
Source URL: https://www.rabbitmq.com/tutorials/tutorial-five-javascript
Source Type: official_docs
Trust Score: 93
Fetched At: 2026-04-17T07:09:23+00:00
Mapped From CSE.md Section: Part 2: E. Distributed systems, backend systems, APIs

# Content

# RabbitMQ tutorial - Topics

## Topics[](https://www.rabbitmq.com#topics)

### (using the amqp.node client)[](https://www.rabbitmq.com#using-the-amqpnode-client)

### Prerequisites[](https://www.rabbitmq.com#prerequisites)

[installed](https://www.rabbitmq.com/docs/download) and running on
`localhost`

on the [standard port](https://www.rabbitmq.com/docs/networking#ports) (5672). In case you
use a different host, port or credentials, connections settings would require
adjusting.

### Where to get help[](https://www.rabbitmq.com#where-to-get-help)

[GitHub Discussions](https://github.com/rabbitmq/rabbitmq-server/discussions) or [RabbitMQ community Discord](https://www.rabbitmq.com/discord).

[previous tutorial](https://www.rabbitmq.com/tutorials/tutorial-four-javascript) we improved our
logging system. Instead of using a `fanout`

exchange only capable of
dummy broadcasting, we used a `direct`

one, and gained a possibility
of selectively receiving the logs.

`direct`

exchange improved our system, it still has
limitations - it can't do routing based on multiple criteria.

[ syslog](http://en.wikipedia.org/wiki/Syslog) unix tool, which
routes logs based on both severity (info/warn/crit...) and facility
(auth/cron/kern...).

To implement that in our logging system we need to learn about a more
complex `topic`

exchange.

## Topic exchange[](https://www.rabbitmq.com#topic-exchange)

`topic`

exchange can't have an arbitrary
`routing_key`

- it must be a list of words, delimited by dots. The
words can be anything, but usually they specify some features
connected to the message. A few valid routing key examples:
`stock.usd.nyse`

, `nyse.vmw`

, `quick.orange.rabbit`

. There can be as
many words in the routing key as you like, up to the limit of 255
bytes.

`topic`

exchange is similar to a `direct`

one - a message sent with a
particular routing key will be delivered to all the queues that are
bound with a matching binding key. However there are two important
special cases for binding keys:

`*`

(star) can substitute for exactly one word.`#`

(hash) can substitute for zero or more words.

It's easiest to explain this in an example:

`<speed>.<colour>.<species>`

.

`*.orange.*`

and Q2 with `*.*.rabbit`

and `lazy.#`

.

These bindings can be summarised as:

- Q1 is interested in all the orange animals.
- Q2 wants to hear everything about rabbits, and everything about lazy animals.

`quick.orange.rabbit`

will be delivered to both queues. Message
`lazy.orange.elephant`

also will go to both of them. On the other hand
`quick.orange.fox`

will only go to the first queue, and
`lazy.brown.fox`

only to the second. `lazy.pink.rabbit`

will
be delivered to the second queue only once, even though it matches two bindings.
`quick.brown.fox`

doesn't match any binding so it will be discarded.

`orange`

or `quick.orange.new.rabbit`

? Well,
these messages won't match any bindings and will be lost.

`lazy.orange.new.rabbit`

, even though it has four
words, will match the last binding and will be delivered to the second
queue.

## Topic exchange

[]Topic exchange is powerful and can behave like other exchanges.

`#`

(hash) binding key - it will receive all the messages, regardless of the routing key - like in`fanout`

exchange.`*`

(star) and`#`

(hash) aren't used in bindings, the topic exchange will behave just like a`direct`

one.

## Putting it all together[](https://www.rabbitmq.com#putting-it-all-together)

`topic`

exchange in our logging system. We'll
start off with a working assumption that the routing keys of logs will
have two words: `<facility>.<severity>`

.

The code is almost the same as in the
[previous tutorial](https://www.rabbitmq.com/tutorials/tutorial-four-javascript).

The code for `emit_log_topic.js`

:

`#!/usr/bin/env node`

const amqp = require('amqplib');

async function main() {

const connection = await amqp.connect('amqp://localhost');

const channel = await connection.createChannel();

const exchange = 'topic_logs';

const args = process.argv.slice(2);

const key = (args.length > 0) ? args[0] : 'anonymous.info';

const msg = args.slice(1).join(' ') || 'Hello World!';

await channel.assertExchange(exchange, 'topic', {

durable: false

});

channel.publish(exchange, key, Buffer.from(msg));

console.log(" [x] Sent %s: '%s'", key, msg);

setTimeout(function() {

connection.close();

process.exit(0);

}, 500);

}

main();

The code for `receive_logs_topic.js`

:

`#!/usr/bin/env node`

const amqp = require('amqplib');

const args = process.argv.slice(2);

if (args.length === 0) {

console.log("Usage: receive_logs_topic.js <facility>.<severity>");

process.exit(1);

}

async function main() {

const connection = await amqp.connect('amqp://localhost');

const channel = await connection.createChannel();

const exchange = 'topic_logs';

await channel.assertExchange(exchange, 'topic', {

durable: false

});

const q = await channel.assertQueue('', {

exclusive: true

});

console.log(' [*] Waiting for logs. To exit press CTRL+C');

for (const key of args) {

await channel.bindQueue(q.queue, exchange, key);

}

channel.consume(q.queue, function(msg) {

console.log(" [x] %s:'%s'", msg.fields.routingKey, msg.content.toString());

}, {

noAck: true

});

}

main();

To receive all the logs:

`./receive_logs_topic.js "#"`

To receive all logs from the facility `kern`

:

`./receive_logs_topic.js "kern.*"`

Or if you want to hear only about `critical`

logs:

`./receive_logs_topic.js "*.critical"`

You can create multiple bindings:

`./receive_logs_topic.js "kern.*" "*.critical"`

And to emit a log with a routing key `kern.critical`

type:

`./emit_log_topic.js "kern.critical" "A critical kernel error"`

(Full source code for [emit_log_topic.js](https://github.com/rabbitmq/rabbitmq-tutorials/blob/main/javascript-nodejs/src/emit_log_topic.js)
and [receive_logs_topic.js](https://github.com/rabbitmq/rabbitmq-tutorials/blob/main/javascript-nodejs/src/receive_logs_topic.js))

Next, find out how to do a round trip message as a remote procedure call in [tutorial 6](https://www.rabbitmq.com/tutorials/tutorial-six-javascript)
