# Recursive Pattern Matching Functions

I thought this was a pretty sweet Elixir function:

```elixir
@spec keep(list :: list(any), fun :: ((any) -> boolean)) :: list(any)
def keep([], _) do [] end
def keep([head | tail], fun) do
  if fun.(head) do
    [head] ++ keep(tail, fun)
  else
    keep(tail, fun)
  end
end
```

The above is an implementation of `filter` from [my exercism](http://exercism.io/submissions/c11665becd584ed59aa52a358e37b5df) which recurses over the given list, calling the given function on the head of the list to determine whether or not to include that element in the final result. The pattern matching in the function parameter declaration gives it a termination condition. Simple Elixir stuff, but cool non-the-less.
