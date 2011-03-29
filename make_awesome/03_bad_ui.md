!SLIDE
# Poor User Interface
## Simple Apps

    @@@Ruby

    if ARGV[0] == '-f'
      filename = ARGV[1]
    end

!SLIDE smaller
# Poor User Interface
## Command-suite

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

!SLIDE bullets incremental
# Poor User Interface
* Hard to maintain
* Hard to enhance
* *More* work than using libraries
* Unpolished and inflexible

!SLIDE
# If you mainpulate `ARGV`
## You're doing it wrong
