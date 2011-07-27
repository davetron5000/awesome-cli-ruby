!SLIDE
# Poor User Interface
## Simple Apps

    @@@Ruby

    if ARGV[0] == '-f'
      filename = ARGV[1]
    end

!SLIDE small
# Poor User Interface
## Command-suite

    @@@ Ruby
    command = ARGV.shift

    case command
      when 'create'
        ShowOffUtils.create
      when 'heroku'
        ShowOffUtils.heroku
      when 'serve'
        ShowOff.run! :host => 'localhost', :port => 9090
      when 'static' 
        ShowOff.do_static(ARGV)
      else
        ShowOffUtils.help
    end

!SLIDE subsection
# If you manipulate `ARGV`, you're doing it wrong

!SLIDE bullets incremental
# Poor User Interface
* Hard to maintain & enhance
* Hard for _others_ to maintain & enhance
* *More* work than using libraries

