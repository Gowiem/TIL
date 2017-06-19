# Elixir variables are immutable in Functions

This is probably a no-brainer for functional folks, but it's something that hung me up. All side effects are thrown away when made in anonymous functions. [This is explained well here](https://elixir-lang.readthedocs.io/en/latest/technical/scoping.html). This is because anonymous functions copy the surrounding scope and don't hold reference to the values. This can be seen from the following:

```elixir
iex> x = 1
1
iex> z = fn -> y = 1; x + y end
#Function<6.90072148/1 in :erl_eval.expr/5>
iex> z.()
2
iex> y
** (RuntimeError) undefined function: y/0

#
# Note that, even though the anonymous function can access the variable x, the variable y cannot be accessed from outside. Furthermore, changing the variable x in the outer scope does not affect the copy of x inside the function:
#

iex> x = 10
10
iex> z.()
2
```
