# Rustic Result

![CICD](https://github.com/linkdd/rustic_result/actions/workflows/test-suite.yml/badge.svg)
[![Hex.pm](http://img.shields.io/hexpm/v/rustic_result.svg?style=flat)](https://hex.pm/packages/rustic_result)
![License](https://img.shields.io/hexpm/l/rustic_result)
[![Hex Docs](https://img.shields.io/badge/hex-docs-lightgreen.svg)](https://hexdocs.pm/rustic_result/)

Result monad for Elixir inspired by Rust
[Result](https://doc.rust-lang.org/std/result/) type.

## Installation

This package can be installed by adding `rustic_result` to your list of
dependencies in `mix.exs`:

```elixir
def deps do
  [
    {:rustic_result, "~> 0.1.0"}
  ]
end
```

## Usage

```elixir
import Rustic.Result

ok(42)
# {:ok, 42}

err(:not_found)
# {:error, :not_found}

ok(1) |> and_then(fn v -> ok(v + 1) end)
# ok(2)

ok(1) |> and_then(fn _ -> err(:not_found) end)
# err(:not_found)

err(:not_found) |> and_then(fn v -> ok(v + 1) end)
# err(:not_found)

ok(1) |> or_else(fn _ -> ok(2) end)
# ok(2)

err(:not_found) |> or_else(fn :not_found -> ok(1) end)
# ok(1)

err(:not_found) |> or_else(fn :not_found -> err(:invalid) end)
# err(:invalid)

ok(1) |> unwrap!()
# 1

err(:not_found) |> unwrap!()
# ** (Rustic.Result.UnhandledError) Expected an ok result, ":not_found" given.
```
