# Rubame

Rubame is a simple Ruby websocket game server.  I was originally using EventMachine for a private project, but it became apparent that EM may not be the most suitable tool.  EM is designed (as I understand it) for servers that will handle lots of low duration connections, whereas my project will involve only a small handful (between 1 and 20, likely) that are long lasting.  However, the primary concern I had was how EM takes over the thread.  In order to have game logic run, it seemed the options were to create a new thread, or use periodic timers to have a game loop called.

Neither seemed ideal, and I wanted to have more control in order to better manage cpu usage.  Rubame allows me to run the network loop when it suits me, allowing the game logic/engine to be the primary tool.

Rubame makes use of [WebSocket Ruby](https://github.com/imanel/websocket-ruby) to handle the websocket protocol, and the standard ruby sockets libraries for the actual network connections.

I am by no means a Ruby expert, so I expect there to be many ways I could improve this.  I also expect there are ways I have done this that will make someone proficient in Ruby cringe.  If you have such comments, please [email me](mailto:me@marksaward.com).  I also expect to improve the code as my project progresses, and my needs grow.  However, I will keep improvements to only be those that are of general use, and not specific to my project.


## Example Use

```ruby
require 'rubame'

server = Rubame::Server.new("0.0.0.0", 25252)
while true
  server.run do |client|
    client.onopen do
      puts "Server reports:  client open"
    end
    client.onmessage do |mess|
      puts "Server reports:  message received: #{mess}"
    end
    client.onclose do
      puts "Server reports:  client closed"
    end
  end
end
```

## RSpec

The RSpec is quite incomplete for now.  I expect to add more tests later.

## License

(The MIT License)

Copyright © 2012 Mark Saward

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the ‘Software’), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED ‘AS IS’, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
