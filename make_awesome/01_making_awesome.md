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
        # Should actually exit nonzero here :(
    end

!SLIDE smaller
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

