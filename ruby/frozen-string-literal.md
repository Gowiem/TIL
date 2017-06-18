# The `# frozen_string_literal: true` comment

Adding `# frozen_string_literal: true` to the top of a Ruby file will make all String literals frozen (immutable) starting in Ruby 2.3. This will be the default in Ruby 3.0 and the comment mechanism is an opt in way to make the transition early. This is a performance improvement. More info:

1. Matz's thread on Twitter: https://twitter.com/yukihiro_matz/status/634386185507311616
2. Ruby-lang issue: https://bugs.ruby-lang.org/issues/11473
3. Where I originally found this: https://github.com/rails/rails/pull/29447
