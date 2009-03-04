# Rack::Unbasic

Wraps HTTP authentication in more friendly workflows.

## Usage

    use Rack::Unbasic do |on|
      on.bad_request '/login'
      on.unauthorized '/login'
    end

A response with a 401 or 400 status code will be redirected to the routes you
specify in the config, with the `env['rack-unbasic.code']` set to whatever the
original status code was, and `env['rack-unbasic.return-to']` set to whatever
the requested URI was.

When a request comes in with `:username` and `:password` params, those will be
mapped to basic auth credentials, and the appropriate headers will be added.

Once authorized, the appropriate credentials will be stashed in the session. These
can then be used to automatically set the appropriate headers as needed.