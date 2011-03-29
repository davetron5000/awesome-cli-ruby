!SLIDE small
# Simple Apps
## `OptionParser`

    @@@ Ruby
    require 'optparse'

    options = {}
    opts = OptionParser.new do |opts|
      opts.banner = "Jeklly is a static site generator"

      # option specifications go here

    end
    opts.parse!

!SLIDE 
# <code>OptionParser</code>
## Parsing switches

    @@@ Ruby
      opts.on("--auto", "Auto-regenerate") do
        options['auto'] = true
      end

!SLIDE small
# <code>OptionParser</code>
## Negatable switches

    @@@ Ruby
      opts.on("--[no-]auto", "Auto-regenerate") do |auto|
        options['auto'] = auto
      end

!SLIDE smaller
# <code>OptionParser</code>
## Parsing flags

    @@@ Ruby
      options['port'] = 4000
      opts.on("-s","--server [PORT]", 
              "Start web server (def #{options['port']})") do |port|

        raise "Port must be >= 1000" if port && port.to_i < 1000

        options['server_port'] = port.to_i if port
      end

!SLIDE smaller
# <code>OptionParser</code>
## Casting

    @@@ Ruby
    opts.on("--time [TIME]", 
            Time, 
            "Begin execution at given time") do |time|
      options['time'] = time # This is a Time instance
    end

!SLIDE bullets incremental
# `OptionParser`
* Built-in
* Formatted help screen
* Dead simple
* No excuse, really
