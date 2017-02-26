# Better Enumerable Reduction with Enumerable#each_with_object

It's a common pattern to use [reduce](https://ruby-doc.org/core-2.2.3/Enumerable.html#method-i-reduce)/[inject](https://ruby-doc.org/core-2.2.3/Enumerable.html#method-i-inject) on an Array or Hash and transform it into something more useful like so:
```ruby
initial = [{ id: 123, val: "value" }, { id: 234, val: "value2" }, { id: 345, val: "value3"}]
result = initial.reduce({}) do |memo, obj|
  memo[obj[:id]] = obj[:val]
  memo
end

puts result # => {123=>"value", 234=>"value2", 345=>"value3"}
```

This is great and provides a ton of power, but it feels kludgy due to need to return the `memo` at the block. It could be more terse without sacrificing readability. [Enumerable#each_with_object](https://ruby-doc.org/core-2.2.3/Enumerable.html#method-i-each_with_object) provides that:

```ruby
initial = [{ id: 123, val: "value" }, { id: 234, val: "value2" }, { id: 345, val: "value3"}]
result = initial.each_with_object({}) { |obj, memo| memo[obj[:id]] = obj[:val] }

puts result # => {123=>"value", 234=>"value2", 345=>"value3"}
```

The only thing to watch out for is that they have switched up the position of the memo as it is passed to the block across these two methods, so you'll want to watch out for that inconsistency.  
