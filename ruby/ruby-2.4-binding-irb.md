# Ruby 2.4 with Binding#irb

[This commit](https://github.com/ruby/ruby/commit/493e48897421d176a8faf0f0820323d79ecdf94a) introduces a Binding#pry like method through the standard lib.

```ruby
require 'irb'

class Example
  def self.hello(name)
    binding.irb # Opens a REPL for inline debugging!
    puts "Hello #{name}"
  end
end

puts Example.hello('George Bailey')
```
