# Use Factory Girl in Rails Console

I include FactoryGirl in my dev/test environments, but normally do `require: false` in my Gemfile due to it adding a bunch of loading to the dev environment. That being said, sometimes it is useful to have access to FactoryGirl in the `rails console`. The following lines include FG, load the model defs, and then include the FG syntax methods to the console.  

```ruby
require 'factory_girl'
FactoryGirl.find_definitions
include FactoryGirl::Syntax::Methods
```
