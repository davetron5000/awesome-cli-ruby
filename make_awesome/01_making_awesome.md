!SLIDE bullets incremental
# Why Ruby? #
* Low-level system access
* High-level abstractions
* More portable than <code>sh</code>

!SLIDE smaller
# Hand-jammed #

    @@@ Ruby
    #!/usr/bin/env ruby
    $LOAD_PATH.unshift File.join(File.dirname(__FILE__), '..', 'lib')

    require 'showoff'
    command = ARGV.shift

    case command
      when 'create'
        ShowOffUtils.create
      when 'add'
        ShowOffUtils.add_slide
      when 'heroku'
        ShowOffUtils.heroku
      when 'serve'
        ShowOff.run! :host => 'localhost', :port => 9090
      when 'static' 
        ShowOff.do_static(ARGV)
      else
        ShowOffUtils.help
    end

!SLIDE 
# Hand-jammed #
## Make host/port cli params? ##

    @@@ Ruby
      when 'serve'
        ShowOff.run! :host => ARGV[0] || 'localhost', 
                     :port => (ARGV[1] || '9090').to_i


!SLIDE bullets incremental
# Hand-jammed #
* Not extensible
* Leads to a mess
* Hand-roll help, too

!SLIDE smaller
# <code>OptionParser</code> #

    @@@ Ruby
    help = <<HELP
    Jekyll is a blog-aware, static site generator.

    Basic Command Line Usage:
      jekyll                                                   # . -> ./_site
      <snip>
    HELP
    require 'optparse'
    exec = {}; options = {}
    opts = OptionParser.new do |opts|
      opts.banner = help

      opts.on("--no-auto", "No auto-regenerate") do
        options['auto'] = false
      end

      opts.on("--server [PORT]", "Start web server (default port 4000)") do |port|
        options['server'] = true
        options['server_port'] = port unless port.nil?
      end
      # <snip>
    end 
    # Read command line options into `options` hash
    opts.parse!

!SLIDE bullets incremental
# <code>OptionParser</code> - Good #
* Easy
* Fairly clear code
* Can convert some classes (e.g. lists)
* outputs option summary

!SLIDE bullets incremental
# <code>OptionParser</code> - Not As Good #
* Still some boilerplate
* "git" style is a bit trickier
* just parses command line

!SLIDE
# <code>GLI</code>

