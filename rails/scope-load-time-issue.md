# ActiveRecord `scope` Load Time Issue

When creating scopes, if they include any `Date` or `DateTime` usage then they'll likely be introducing a bug. For example, `DateTime.now` is evaluated at class load time, causing the date to be constant instead of variable. This can be seen through the code here:

```ruby
class User < ActiveRecord::Base
  scope :recently_updated, where('updated_at <= ?', Date.today - 2.days)
end
```

This can be fixed by using lambda's to always execute the Date code when the scope is invoked:

```ruby
class User < ActiveRecord::Base
  scope :recently_updated, lambda { where('updated_at <= ?', Date.today - 2.days) }
end
```
