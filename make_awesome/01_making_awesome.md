!SLIDE bullets incremental
# Why Ruby?
* High-level abstractions
* Still close to the “metal” (e.g. `FileUtils`)
* Simple packaging/distribution with RubyGems
* Fast - no heavyweight VM to start up
* Part of the culture

!SLIDE
# Give me something I can use…

!SLIDE bullets incremental
# Biggest signs of un-awesome
* Poor `system` error handling
* Poor user interface

!SLIDE
# Poor `system` error handling

    @@@Ruby
    results = %x[some_external_command.sh]
    # Of course, everythning worked, right?
    results.readlines.each do |line|
      # Wait, is this stdout or stderr?!?!
    end

!SLIDE commandline

    $ my_script.rb
    sh: some_external_command.sh: command not found

!SLIDE bullets incremental
# How to really do it
* *Check exit codes* - plays well!
* *Log the command* - helpful!
* *Capture the output* - helpful
* Be kind to “future you”

!SLIDE smaller 
# Check exit codes

    @@@Ruby
    output = %x[some_external_command.sh]
    if $?.success?
      stdout.readlines.each do |line|
        # Do our work
      end
    else
      $stderr.puts("Problem running some_external_command.sh")
    end

!SLIDE smaller 
# Log command aka DRY it up

    @@@Ruby
    require 'logger'
    $logger = Logger.new("my_cmd.log")

    command = "some_external_command.sh"
    $logger.debug("Executing '#{command}'})
    output = %x[#{command}]
    if $?.success?
      stdout.readlines.each do |line|
        # Do our work
      end
    else
      $logger.error("Problem running #{command}")
    end

!SLIDE smaller
# Capture the output
## Use `open3`

    @@@Ruby
    require 'open3'
    require 'logger'
    $logger = Logger.new("my_cmd.log")

    $logger.debug("Executing '#{command}'})
    command = "some_external_command.sh"
    stdout,stderr,status = Open3.capture3(command)
    if status == 0
      log_output(command,stdout => :debug, stderr => :warn)
      stdout.readlines.each do |line|
        # Do our work
      end
    else
      log_output(command,stdout => :info, stderr => :error)
      $logger.error("Problem running #{command}")
    end

    def log_output(command,streams)
      streams.each do |stream,level)
        stream.split(/\n/).each do |line|
          $logger.send(level,"#{command} - #{line}")
        end
      end
    end

!SLIDE bullets incremental
#WTF?
## That's like…22 lines! 
* Stash it in a method somewhere,
* and use it instead of `system` or `%x[]`
* External calls are now bulletproof
* Diagnostics built-in when `cron` dies at 3am

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

!SLIDE
# Poor User Interface
* Hard to maintain
* Hard to enhance
* *More* work than using libraries
* Unpolished and inflexible
