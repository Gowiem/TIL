# Use IEx.pry with ExUnit

Probably a noob tip for myself, but to get `IEx.py` to work it's required to run through `iex -S`. The following does the trick:

```elixir
require IEx
defmodule SomeModule.SomeTest do
  use ExUnit.Case

  test "this is a test of the emergency broadcast system" do
    IEx.pry
  end
end
```

Run the tests with `iex -S mix test` and the `.pry` will halt execution giving you a shell.
