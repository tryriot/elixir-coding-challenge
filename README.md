# Elixir technical test

This technical test is for backend developers who **already know** elixir & OTP. The test will take 1h15.

## General acceptance criteria

- You **cannot** use external dependencies.
- Code accuracy matters. A readable, safe, refactorable code is a plus.

## The project

You will create a very simple in memory key-value store (a simpler Redis clone) in elixir.

Usage example:

```elixir
iex> Redis.execute(["PING"])
"PONG"

iex> Redis.execute(["SET", "hello", 42])
:ok

iex> Redis.execute(["GET", "hello"])
42
```

Each command is an elixir list where the head is the command name and the rest of the list are the arguments.

### Commands to implement

**PING**

`PING [message]`

Returns `PONG` if no argument is provided, otherwise return a copy of the argument.

**SET**

`SET key value`

Set `key` to hold the string `value`. If `key` already holds a value, it is overwritten, regardless of its type.

**GET**

`GET key`

Get the value of `key`. If the key does not exist the special value `nil` is returned.

**EXPIRE**

`EXPIRE key seconds`

Set a timeout on `key`. After the timeout has expired, the key will automatically be deleted. A key with an associated timeout is often said to be *volatile* in Redis terminology.

**PERSIST**

`PERSIST key`

Remove the existing timeout on `key`, turning the key from *volatile* (a key with an expire set) to *persistent* (a key that will never expire as no timeout is associated).

### How to store the state?

There are multiple way to store state in elixir. Choose the one you like best and explain to me what the tradeoffs are (verbally during the code review).

## Bonus (not required)

Accept TCP connections on port `6379`.

We should be able to use the 5 commands listed above using the redis CLI as a client.

Example:

```bash
$ brew install redis

$ redis-cli PING
"PONG"
```

You will need to deserialize / serialize data using the **[Redis Protocol specification](https://redis-doc-test.readthedocs.io/en/latest/topics/protocol/).**