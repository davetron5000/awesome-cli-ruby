!SLIDE
# Simple #
## <code>OptionParser</code> ##

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

!SLIDE bullets incremental
# <code>OptionParser</code>
* Easy
* Fairly clear code
* Can convert some types 
* outputs option summary
* command suites/"git-style" is difficult

!SLIDE bullets incremental
# Trollop #
* Less code than <code>OptionParser</code>
* Single-file distro -- easy to include
* More verbose for command-suite (but easier than <code>OptionParser</code>)

