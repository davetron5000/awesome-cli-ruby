!SLIDE small
# Simple Apps
## `OptionParser`

    @@@ Ruby
    require 'optparse'

    options = {}
    opts = OptionParser.new do |opts|
      executable_name = File.split($0)[1]
      opts.banner = <<-EOS
    Jekyll is a static site generator

    Usage: #{executable_name} [options] args...
      EOS

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
    opts.on("-s","--server PORT", 
            "Start web server on PORT") do |port|

      # Do some sanity checking
      if port && port.to_i < 1000
        raise "Port must be >= 1000" 
      end

      options['server_port'] = port.to_i
    end

!SLIDE smaller
# <code>OptionParser</code>
## Awesome Validation

    @@@ Ruby
    opts.on("--ip IP",
            /^\d+\.\d+\.\d+\.\d+$/,
            "IP address to bind to") do |ip|
      options['ip'] = ip # <- matches the regex
    end

!SLIDE commandline small incremental
# <code>OptionParser</code>
## Awesome Help
    $ awesome_app -h
    My awesome app is awesome

    Usage: awesome_app [options] args...

        --[no-]auto                  Auto-regenerate
    -s, --server  PORT               Start web server (def 4000)
        --ip IP                      IP address to bind to
    $ awesome_app --help 
    # same thing

!SLIDE bullets incremental
# `OptionParser`
* Easy for others to modify, too
* No excuse, really
