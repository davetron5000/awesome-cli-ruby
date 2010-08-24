!SLIDE
# Simple #
* <code>OptionParser</code>

!SLIDE commandline
# <code>OptionParser</code> #

    $ ri OptionParser
    # It's actually already installed!

!SLIDE smaller
# <code>OptionParser</code> #

    @@@ Ruby
    help = <<HELP
    Jekyll is a blog-aware, static site generator.

    Basic Command Line Usage:
      jekyll                         # . -> ./_site
      <snip>
    HELP
    require 'optparse'
    exec = {}; options = {}
    opts = OptionParser.new do |opts|
      opts.banner = help

      # option specifications go here
    end
    opts.parse!

!SLIDE smaller
# <code>OptionParser</code>
## Parsing switches

    @@@ Ruby

      opts.on("--no-auto", "No auto-regenerate") do
        options['auto'] = false
      end

!SLIDE smaller
# <code>OptionParser</code>
## Parsing flags

    @@@ Ruby
      opts.on("--server [PORT]", 
              "Start web server (def 4000)") do |port|
        raise "Port must be >= 1000" if port < 1000
        options['server'] = true
        options['server_port'] = port unless port.nil?
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
# <code>OptionParser</code> - Good #
* Easy
* Fairly clear code
* Can convert some types 
* outputs option summary

!SLIDE bullets incremental
# <code>OptionParser</code> - Not As Good #
* Still some boilerplate
* command suites/"git-style" is difficult
* just parses command line

