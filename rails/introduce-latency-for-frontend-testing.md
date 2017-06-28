# Introduce Latency to Rails for Frontend Testing

When adding loading spinners to an Emberjs frontend app I was working on I kept refreshing the screen trying to see the spinner before my models loaded. Super easy way to make the frontend load the models slow: introduce some latency!

```ruby
class ApplicationController < ActionController::Base
  before_action :add_latency

  private

  # Delays each request by 1 second
  def add_latency
    sleep 1
  end
end

```
