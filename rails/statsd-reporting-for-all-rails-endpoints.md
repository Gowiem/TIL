# Add Statsd Reporting for Rails endpoints and Status Code counts

Simple rack middleware that does timing for all controller/actions + counts all status codes:

```ruby
# Heavily inspired by:
# scout_statsd_rack -- https://github.com/scoutapp/scout_statsd_rack/blob/master/lib/scout_statsd_rack.rb
# trashed -- https://github.com/basecamp/trashed
# Add to Rails App: `config.middleware.use RackStats`
class RackStats
  attr_accessor :app

  def initialize(app)
    @app = app
  end

  def call(env)
      (status, headers, body), response_time = call_with_timing(env)

      collect_metrics(status, response_time, env['action_controller.instance'])

      # Rack response
      [status, headers, body]
  rescue Exception
    increment("rack.response_codes.5xx")
    raise
  end

  def collect_metrics(status, response_time, controller)
    response_code = status.to_s.gsub(/\d{2}$/,'xx')

    if controller
      name    = controller.controller_name
      action  = controller.action_name
      format  = controller.content_type || :none

      timing("rack.response.#{name}", response_time)
      timing("rack.response.#{name}.#{action}", response_time)
      increment("rack.response_codes.#{name}.#{response_code}")
      increment("rack.response_codes.#{name}.#{action}.#{response_code}")
      increment("rack.format.#{format}")
    end

    timing("rack.response.all", response_time)
    increment("rack.response_codes.#{response_code}")
  rescue Exception => e
    Airbrake.notify(e)
  end

  def call_with_timing(env)
    start = Time.now
    result = @app.call(env)
    [result, ((Time.now - start) * 1000).round]
  end

  def increment(key)
    $statsd.increment("#{key}._t_env.#{Rails.env}")
  end

  def timing(key, time)
    $statsd.timing("#{key}._t_env.#{Rails.env}", time)
  end
end
```