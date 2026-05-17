Title: redis-rs guide (Rust) | Docs
Mapped Topic: Caching and in-memory data structures
Source URL: https://redis.io/docs/latest/develop/clients/rust/
Source Type: official_docs
Trust Score: 94
Fetched At: 2026-04-17T07:09:10+00:00
Mapped From CSE.md Section: Part 2: E. Distributed systems, backend systems, APIs

# Content

# redis-rs guide (Rust)

Connect your Rust application to a Redis database

[ redis-rs](https://github.com/redis-rs/redis-rs) is the

[Rust](https://www.rust-lang.org/)client for Redis. The sections below explain how to install

`redis-rs`

and connect your application to a Redis database.`redis-rs`

, it is a third-party
client library and is not developed or supported directly by Redis.`redis-rs`

requires a running Redis server. See [here](https://redis.io/docs/latest/operate/oss_and_stack/install/) for Redis Open Source installation instructions.

##
Install
[
](https://redis.io#install)

To use the synchronous API, add the `redis`

crate as a dependency in your
`Cargo.toml`

file:

```
[dependencies]
redis = "1.0.4"
```

If you want to use the asynchronous API, you should also enable either
[ tokio](https://tokio.rs/) or

[as your async platform:](https://crates.io/crates/smol)

`smol`

```
[dependencies]
# if you use tokio
tokio = { version = "1.32.0", features = ["full"] }
redis = { version = "1.0.4", features = ["tokio-comp"] }
# if you use smol
smol = "2.0.2"
redis = { version = "1.0.4", features = ["smol-comp"] }
```

##
Connect
[
](https://redis.io#connect)

Start by importing the `Commands`

or `AsyncCommands`

trait from the `redis`

crate:

```
mod landing_tests {
use redis::Commands;
fn run() {
let mut r = match redis::Client::open("redis://127.0.0.1") {
Ok(client) => {
match client.get_connection() {
Ok(conn) => conn,
Err(e) => {
println!("Failed to connect to Redis: {e}");
return;
}
}
},
Err(e) => {
println!("Failed to create Redis client: {e}");
return;
}
};
if let Ok(res) = r.set("foo", "bar") {
let res: String = res;
println!("{res}"); // >>> OK
} else {
println!("Error setting foo");
}
match r.get("foo") {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> bar
},
Err(e) => {
println!("Error getting foo: {e}");
return;
}
};
let hash_fields = [
("model", "Deimos"),
("brand", "Ergonom"),
("type", "Enduro bikes"),
("price", "4972"),
];
if let Ok(res) = r.hset_multiple("bike:1", &hash_fields) {
let res: String = res;
println!("{res}"); // >>> OK
} else {
println!("Error setting bike:1");
}
match r.hget("bike:1", "model") {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> Deimos
},
Err(e) => {
println!("Error getting bike:1 model: {e}");
return;
}
}
match r.hget("bike:1", "price") {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> 4972
},
Err(e) => {
println!("Error getting bike:1 price: {e}");
return;
}
}
match r.hgetall("bike:1") {
Ok(res) => {
let res: Vec<(String, String)> = res;
for (key, value) in res {
println!("{key}: {value}");
}
// >>> model: Deimos
// >>> brand: Ergonom
// >>> type: Enduro bikes
// >>> price: 4972
},
Err(e) => {
println!("Error getting bike:1: {e}");
return;
}
}
}
}
```

```
mod tests {
use redis::AsyncCommands;
async fn run() {
let mut r = match redis::Client::open("redis://127.0.0.1") {
Ok(client) => {
match client.get_multiplexed_async_connection().await {
Ok(conn) => conn,
Err(e) => {
println!("Failed to connect to Redis: {e}");
return;
}
}
},
Err(e) => {
println!("Failed to create Redis client: {e}");
return;
}
};
if let Ok(res) = r.set("foo", "bar").await {
let res: String = res;
println!("{res}"); // >>> OK
} else {
println!("Error setting foo");
}
match r.get("foo").await {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> bar
},
Err(e) => {
println!("Error getting foo: {e}");
return;
}
};
let hash_fields = [
("model", "Deimos"),
("brand", "Ergonom"),
("type", "Enduro bikes"),
("price", "4972"),
];
if let Ok(res) = r.hset_multiple("bike:1", &hash_fields).await {
let res: String = res;
println!("{res}"); // >>> OK
} else {
println!("Error setting bike:1");
}
match r.hget("bike:1", "model").await {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> Deimos
},
Err(e) => {
println!("Error getting bike:1 model: {e}");
return;
}
}
match r.hget("bike:1", "price").await {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> 4972
},
Err(e) => {
println!("Error getting bike:1 price: {e}");
return;
}
}
match r.hgetall("bike:1").await {
Ok(res) => {
let res: Vec<(String, String)> = res;
for (key, value) in res {
println!("{key}: {value}");
}
// >>> model: Deimos
// >>> brand: Ergonom
// >>> type: Enduro bikes
// >>> price: 4972
},
Err(e) => {
println!("Error getting bike:1: {e}");
return;
}
}
}
}
```

The following example shows the simplest way to connect to a Redis server:

```
mod landing_tests {
use redis::Commands;
fn run() {
let mut r = match redis::Client::open("redis://127.0.0.1") {
Ok(client) => {
match client.get_connection() {
Ok(conn) => conn,
Err(e) => {
println!("Failed to connect to Redis: {e}");
return;
}
}
},
Err(e) => {
println!("Failed to create Redis client: {e}");
return;
}
};
if let Ok(res) = r.set("foo", "bar") {
let res: String = res;
println!("{res}"); // >>> OK
} else {
println!("Error setting foo");
}
match r.get("foo") {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> bar
},
Err(e) => {
println!("Error getting foo: {e}");
return;
}
};
let hash_fields = [
("model", "Deimos"),
("brand", "Ergonom"),
("type", "Enduro bikes"),
("price", "4972"),
];
if let Ok(res) = r.hset_multiple("bike:1", &hash_fields) {
let res: String = res;
println!("{res}"); // >>> OK
} else {
println!("Error setting bike:1");
}
match r.hget("bike:1", "model") {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> Deimos
},
Err(e) => {
println!("Error getting bike:1 model: {e}");
return;
}
}
match r.hget("bike:1", "price") {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> 4972
},
Err(e) => {
println!("Error getting bike:1 price: {e}");
return;
}
}
match r.hgetall("bike:1") {
Ok(res) => {
let res: Vec<(String, String)> = res;
for (key, value) in res {
println!("{key}: {value}");
}
// >>> model: Deimos
// >>> brand: Ergonom
// >>> type: Enduro bikes
// >>> price: 4972
},
Err(e) => {
println!("Error getting bike:1: {e}");
return;
}
}
}
}
```

```
mod tests {
use redis::AsyncCommands;
async fn run() {
let mut r = match redis::Client::open("redis://127.0.0.1") {
Ok(client) => {
match client.get_multiplexed_async_connection().await {
Ok(conn) => conn,
Err(e) => {
println!("Failed to connect to Redis: {e}");
return;
}
}
},
Err(e) => {
println!("Failed to create Redis client: {e}");
return;
}
};
if let Ok(res) = r.set("foo", "bar").await {
let res: String = res;
println!("{res}"); // >>> OK
} else {
println!("Error setting foo");
}
match r.get("foo").await {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> bar
},
Err(e) => {
println!("Error getting foo: {e}");
return;
}
};
let hash_fields = [
("model", "Deimos"),
("brand", "Ergonom"),
("type", "Enduro bikes"),
("price", "4972"),
];
if let Ok(res) = r.hset_multiple("bike:1", &hash_fields).await {
let res: String = res;
println!("{res}"); // >>> OK
} else {
println!("Error setting bike:1");
}
match r.hget("bike:1", "model").await {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> Deimos
},
Err(e) => {
println!("Error getting bike:1 model: {e}");
return;
}
}
match r.hget("bike:1", "price").await {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> 4972
},
Err(e) => {
println!("Error getting bike:1 price: {e}");
return;
}
}
match r.hgetall("bike:1").await {
Ok(res) => {
let res: Vec<(String, String)> = res;
for (key, value) in res {
println!("{key}: {value}");
}
// >>> model: Deimos
// >>> brand: Ergonom
// >>> type: Enduro bikes
// >>> price: 4972
},
Err(e) => {
println!("Error getting bike:1: {e}");
return;
}
}
}
}
```

After connecting, you can test the connection by storing and retrieving
a simple [string](https://redis.io/docs/latest/develop/data-types/strings/):

```
mod landing_tests {
use redis::Commands;
fn run() {
let mut r = match redis::Client::open("redis://127.0.0.1") {
Ok(client) => {
match client.get_connection() {
Ok(conn) => conn,
Err(e) => {
println!("Failed to connect to Redis: {e}");
return;
}
}
},
Err(e) => {
println!("Failed to create Redis client: {e}");
return;
}
};
if let Ok(res) = r.set("foo", "bar") {
let res: String = res;
println!("{res}"); // >>> OK
} else {
println!("Error setting foo");
}
match r.get("foo") {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> bar
},
Err(e) => {
println!("Error getting foo: {e}");
return;
}
};
let hash_fields = [
("model", "Deimos"),
("brand", "Ergonom"),
("type", "Enduro bikes"),
("price", "4972"),
];
if let Ok(res) = r.hset_multiple("bike:1", &hash_fields) {
let res: String = res;
println!("{res}"); // >>> OK
} else {
println!("Error setting bike:1");
}
match r.hget("bike:1", "model") {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> Deimos
},
Err(e) => {
println!("Error getting bike:1 model: {e}");
return;
}
}
match r.hget("bike:1", "price") {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> 4972
},
Err(e) => {
println!("Error getting bike:1 price: {e}");
return;
}
}
match r.hgetall("bike:1") {
Ok(res) => {
let res: Vec<(String, String)> = res;
for (key, value) in res {
println!("{key}: {value}");
}
// >>> model: Deimos
// >>> brand: Ergonom
// >>> type: Enduro bikes
// >>> price: 4972
},
Err(e) => {
println!("Error getting bike:1: {e}");
return;
}
}
}
}
```

```
mod tests {
use redis::AsyncCommands;
async fn run() {
let mut r = match redis::Client::open("redis://127.0.0.1") {
Ok(client) => {
match client.get_multiplexed_async_connection().await {
Ok(conn) => conn,
Err(e) => {
println!("Failed to connect to Redis: {e}");
return;
}
}
},
Err(e) => {
println!("Failed to create Redis client: {e}");
return;
}
};
if let Ok(res) = r.set("foo", "bar").await {
let res: String = res;
println!("{res}"); // >>> OK
} else {
println!("Error setting foo");
}
match r.get("foo").await {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> bar
},
Err(e) => {
println!("Error getting foo: {e}");
return;
}
};
let hash_fields = [
("model", "Deimos"),
("brand", "Ergonom"),
("type", "Enduro bikes"),
("price", "4972"),
];
if let Ok(res) = r.hset_multiple("bike:1", &hash_fields).await {
let res: String = res;
println!("{res}"); // >>> OK
} else {
println!("Error setting bike:1");
}
match r.hget("bike:1", "model").await {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> Deimos
},
Err(e) => {
println!("Error getting bike:1 model: {e}");
return;
}
}
match r.hget("bike:1", "price").await {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> 4972
},
Err(e) => {
println!("Error getting bike:1 price: {e}");
return;
}
}
match r.hgetall("bike:1").await {
Ok(res) => {
let res: Vec<(String, String)> = res;
for (key, value) in res {
println!("{key}: {value}");
}
// >>> model: Deimos
// >>> brand: Ergonom
// >>> type: Enduro bikes
// >>> price: 4972
},
Err(e) => {
println!("Error getting bike:1: {e}");
return;
}
}
}
}
```

You can also easily store and retrieve a [hash](https://redis.io/docs/latest/develop/data-types/hashes/):

```
mod landing_tests {
use redis::Commands;
fn run() {
let mut r = match redis::Client::open("redis://127.0.0.1") {
Ok(client) => {
match client.get_connection() {
Ok(conn) => conn,
Err(e) => {
println!("Failed to connect to Redis: {e}");
return;
}
}
},
Err(e) => {
println!("Failed to create Redis client: {e}");
return;
}
};
if let Ok(res) = r.set("foo", "bar") {
let res: String = res;
println!("{res}"); // >>> OK
} else {
println!("Error setting foo");
}
match r.get("foo") {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> bar
},
Err(e) => {
println!("Error getting foo: {e}");
return;
}
};
let hash_fields = [
("model", "Deimos"),
("brand", "Ergonom"),
("type", "Enduro bikes"),
("price", "4972"),
];
if let Ok(res) = r.hset_multiple("bike:1", &hash_fields) {
let res: String = res;
println!("{res}"); // >>> OK
} else {
println!("Error setting bike:1");
}
match r.hget("bike:1", "model") {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> Deimos
},
Err(e) => {
println!("Error getting bike:1 model: {e}");
return;
}
}
match r.hget("bike:1", "price") {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> 4972
},
Err(e) => {
println!("Error getting bike:1 price: {e}");
return;
}
}
match r.hgetall("bike:1") {
Ok(res) => {
let res: Vec<(String, String)> = res;
for (key, value) in res {
println!("{key}: {value}");
}
// >>> model: Deimos
// >>> brand: Ergonom
// >>> type: Enduro bikes
// >>> price: 4972
},
Err(e) => {
println!("Error getting bike:1: {e}");
return;
}
}
}
}
```

```
mod tests {
use redis::AsyncCommands;
async fn run() {
let mut r = match redis::Client::open("redis://127.0.0.1") {
Ok(client) => {
match client.get_multiplexed_async_connection().await {
Ok(conn) => conn,
Err(e) => {
println!("Failed to connect to Redis: {e}");
return;
}
}
},
Err(e) => {
println!("Failed to create Redis client: {e}");
return;
}
};
if let Ok(res) = r.set("foo", "bar").await {
let res: String = res;
println!("{res}"); // >>> OK
} else {
println!("Error setting foo");
}
match r.get("foo").await {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> bar
},
Err(e) => {
println!("Error getting foo: {e}");
return;
}
};
let hash_fields = [
("model", "Deimos"),
("brand", "Ergonom"),
("type", "Enduro bikes"),
("price", "4972"),
];
if let Ok(res) = r.hset_multiple("bike:1", &hash_fields).await {
let res: String = res;
println!("{res}"); // >>> OK
} else {
println!("Error setting bike:1");
}
match r.hget("bike:1", "model").await {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> Deimos
},
Err(e) => {
println!("Error getting bike:1 model: {e}");
return;
}
}
match r.hget("bike:1", "price").await {
Ok(res) => {
let res: String = res;
println!("{res}"); // >>> 4972
},
Err(e) => {
println!("Error getting bike:1 price: {e}");
return;
}
}
match r.hgetall("bike:1").await {
Ok(res) => {
let res: Vec<(String, String)> = res;
for (key, value) in res {
println!("{key}: {value}");
}
// >>> model: Deimos
// >>> brand: Ergonom
// >>> type: Enduro bikes
// >>> price: 4972
},
Err(e) => {
println!("Error getting bike:1: {e}");
return;
}
}
}
}
```

##
More information
[
](https://redis.io#more-information)

See the [ redis-rs](https://docs.rs/redis/latest/redis/) documentation
and the

[GitHub repository](https://github.com/redis-rs/redis-rs)for more information and examples.
