Title: Predis guide (PHP) | Docs
Mapped Topic: Caching and in-memory data structures
Source URL: https://redis.io/docs/latest/develop/clients/php/
Source Type: official_docs
Trust Score: 94
Fetched At: 2026-04-17T07:09:02+00:00
Mapped From CSE.md Section: Part 2: E. Distributed systems, backend systems, APIs

# Content

# Predis guide (PHP)

Connect your PHP application to a Redis database

[ Predis](https://github.com/predis/predis) is the recommended

[PHP](https://php.net/)client for Redis. The sections below explain how to install

`Predis`

and connect your application to a Redis database.`Predis`

, it is a third-party
client library and is not developed or supported directly by Redis.`Predis`

requires a running Redis server. See [here](https://redis.io/docs/latest/operate/oss_and_stack/install/) for Redis Open Source installation instructions.

##
Install
[
](https://redis.io#install)

Use [Composer](https://getcomposer.org/) to install the `Predis`

library
with the following command line:

```
composer require predis/predis
```

##
Connect and test
[
](https://redis.io#connect-and-test)

Connect to a locally-running server on the standard port (6379) with the following code:

```
<?php
require 'vendor/autoload.php';
use Predis\Client as PredisClient;
$r = new PredisClient([
'scheme' => 'tcp',
'host' => '127.0.0.1',
'port' => 6379,
'password' => '',
'database' => 0,
]);
echo $r->set('foo', 'bar'), PHP_EOL;
// >>> OK
echo $r->get('foo'), PHP_EOL;
// >>> bar
$r->hset('user-session:123', 'name', 'John');
$r->hset('user-session:123', 'surname', 'Smith');
$r->hset('user-session:123', 'company', 'Redis');
$r->hset('user-session:123', 'age', 29);
echo var_export($r->hgetall('user-session:123')), PHP_EOL;
/* >>>
array (
'name' => 'John',
'surname' => 'Smith',
'company' => 'Redis',
'age' => '29',
)
*/
```

Store and retrieve a simple string to test the connection:

```
<?php
require 'vendor/autoload.php';
use Predis\Client as PredisClient;
$r = new PredisClient([
'scheme' => 'tcp',
'host' => '127.0.0.1',
'port' => 6379,
'password' => '',
'database' => 0,
]);
echo $r->set('foo', 'bar'), PHP_EOL;
// >>> OK
echo $r->get('foo'), PHP_EOL;
// >>> bar
$r->hset('user-session:123', 'name', 'John');
$r->hset('user-session:123', 'surname', 'Smith');
$r->hset('user-session:123', 'company', 'Redis');
$r->hset('user-session:123', 'age', 29);
echo var_export($r->hgetall('user-session:123')), PHP_EOL;
/* >>>
array (
'name' => 'John',
'surname' => 'Smith',
'company' => 'Redis',
'age' => '29',
)
*/
```

Store and retrieve a [hash](https://redis.io/docs/latest/develop/data-types/hashes/)
object:

```
<?php
require 'vendor/autoload.php';
use Predis\Client as PredisClient;
$r = new PredisClient([
'scheme' => 'tcp',
'host' => '127.0.0.1',
'port' => 6379,
'password' => '',
'database' => 0,
]);
echo $r->set('foo', 'bar'), PHP_EOL;
// >>> OK
echo $r->get('foo'), PHP_EOL;
// >>> bar
$r->hset('user-session:123', 'name', 'John');
$r->hset('user-session:123', 'surname', 'Smith');
$r->hset('user-session:123', 'company', 'Redis');
$r->hset('user-session:123', 'age', 29);
echo var_export($r->hgetall('user-session:123')), PHP_EOL;
/* >>>
array (
'name' => 'John',
'surname' => 'Smith',
'company' => 'Redis',
'age' => '29',
)
*/
```

##
More information
[
](https://redis.io#more-information)

The [Predis wiki on Github](https://github.com/predis/predis/wiki) has
information about the different connection options you can use.

See also the pages in this section for more information and examples:
