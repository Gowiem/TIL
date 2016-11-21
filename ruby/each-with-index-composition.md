# Composing Ruby's `each_with_index` + other Enumerable methods

You can loop over items in a collection with their index by first calling `each_with_index` and then using any corresponding Enumerable method:

```ruby
arr = [10, 20, 30]
arr.each_with_index.map { |value, index| puts "Value: #{value}, Index: #{index}" }
# Output:
# Value: 10, Index: 0
# Value: 20, Index: 1
# Value: 30, Index: 2

arr.each_with_index.reduce(0) { |memo, (val, idx)| memo += val + idx }
# Output: 63
```
