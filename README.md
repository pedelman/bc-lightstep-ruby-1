# bc-lightstep-ruby - LightStep distributed tracing

[![Build Status](https://travis-ci.com/bigcommerce/bc-lightstep-ruby.svg?token=D3Cc4LCF9BgpUx4dpPpv&branch=master)](https://travis-ci.com/bigcommerce/bc-lightstep-ruby)

Adds [LightStep](https://lightstep.com) tracing support for Ruby.

## Installation

```ruby
gem 'bc-lightstep-ruby', git: 'git@github.com/bigcommerce/bc-lightstep-ruby'
```

Then in an initializer or before use:

```ruby
require 'bigcommerce/lightstep'
Bigcommerce::Lightstep.configure do |c|
  c.component_name = 'myapp'
  c.access_token = 'abcdefg'
  c.host = 'my.lightstep.service.io'
  c.port = 8080
  c.verbosity = 1
end
```

Then in your script:

```ruby
tracer = Bigcommerce::Lightstep::Tracer.instance
tracer.start_span('my-span', context: request.headers) do |span|
  span.set_tag('my-tag', 'value')
  # do thing to measure
end
```

### Environment Config

bc-lightstep-ruby can be automatically configured from these ENV vars, if you'd rather use that instead:

| Name | Description |
| ---- | ----------- |
| LIGHTSTEP_COMPONENT_NAME | The component name to use |
| LIGHTSTEP_ACCESS_TOKEN | The access token to use to connect to the collector |
| LIGHTSTEP_HOST | Host of the collector. Defaults to `lightstep-collector.linkerd` |
| LIGHTSTEP_PORT | Port of the collector. Defaults to `4140` |
| LIGHTSTEP_SSL_VERIFY_PEER | If using 443 as the port, toggle SSL verification. Defaults to true. |
| LIGHTSTEP_VERBOSITY | The verbosity level of lightstep logs. Defaults to 1. |

Most BC systems will only need to customize the component name.

## License

Copyright (c) 2018-present, BigCommerce Pty. Ltd. All rights reserved 

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated 
documentation files (the "Software"), to deal in the Software without restriction, including without limitation the 
rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit 
persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the 
Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE 
WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR 
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR 
OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
