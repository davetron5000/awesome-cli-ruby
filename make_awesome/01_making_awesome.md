!SLIDE bullets incremental
# Why Ruby? #
## System facilities
* <code>system("whatever you want")</code>
* <code>stdout = \`some other command\`</code>
* <code>$?</code> gets access to results, e.g. <code>$?.success?</code>
* <code>FileUtils</code> - cross platform UNIX-style
* More portable than <code>sh</code>

!SLIDE bullets incremental
# Why Ruby? #
## Language facilities
* High-level abstractions
* <code>gem</code> packaging/distribution
* Fast - No VM to start up

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
        # Should actually exit nonzero here :(
    end

!SLIDE smaller
# Hand-jammed #
## Make host/port cli params? ##

    @@@ Ruby
      when 'serve'
        ShowOff.run! :host => ARGV[0] || 'localhost', 
                     :port => (ARGV[1] || '9090').to_i
      # can't just specify the port

!SLIDE smaller
# Hand-jammed #
## Make host/port cli params? ##

    @@@ Ruby
      when 'serve'
        if ARGV[0] == '-h'
          ARGV.shift
          host = ARGV.shift
        end
        port = '9090'
        if ARGV[0] == '-p'
          ARGV.shift
          port = ARGV.shift
        end
        ShowOff.run! :host => host
                     :port => port.to_i
      # showoff serve -p 9090 -h 127.0.0.1 doesn't work


!SLIDE bullets incremental
# Hand-jammed #
* Not extensible
* Leads to a mess
* Must handjam help messages, too

