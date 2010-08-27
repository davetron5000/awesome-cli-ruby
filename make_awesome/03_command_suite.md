!SLIDE
# Command Suite #

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

!SLIDE bullets incremental
# Hand-jammed #
* Not extensible
* Leads to a mess
* Must handjam help messages, too
* Suprisingly prolific

!SLIDE bullets incremental
# <code>GLI</code> - Git Like Interface
* Designed for 'command suite' style
* Designed to make polished app easy to create

!SLIDE commandline smaller
# Bootstrap your Application

    $ gli init my_cmd ls rm init
    Creating dir ./my_cmd/lib...
    Creating dir ./my_cmd/bin...
    Creating dir ./my_cmd/test...
    Created ./my_cmd/bin/my_cmd

!SLIDE commandline smaller incremental
# We've written no code, yet

    $ my_cmd/bin/my_cmd 
    usage: my_cmd command [options]

    Options:
        -f, --flagname=The name of the argument - Describe some flag here (default: 
                                                  the default)
        -s, --switch                            - Describe some switch here

    Commands:
        help - Shows list of commands or help for one command
        init - Describe init here
        ls   - Describe ls here
        rm   - Describe rm here
      
!SLIDE commandline incremental
# GLI #

    $ bin/my_cmd help ls
    ls [options] Describe arguments to ls here
        Describe ls here

        Options:
            -s arg - Describe a flag to ls (default: default)
    

!SLIDE smaller
# GLI #
## Scaffold app ##

    @@@ Ruby
    desc 'Force overwriting files'
    switch [:f,:force]

    desc 'Output data to this file'
    default_value 'ouput.yml'
    arg_name 'Path to the file'
    flag [:f,:file]

!SLIDE small
# GLI #
## Define Sub-commands ##

    @@@ Ruby
    desc 'Serves the showoff presentation in the current dir'
    command :serve do |c|

      c.desc 'Port on which to run'
      c.default_value "9090"
      c.flag [:p,:port]

      c.action do |global_options,options,args|
        if !File.exists?(ShowOffUtils::SHOWOFF_JSON_FILE)
          raise "fail. not a showoff directory"
        end
        unless global_options[:dryrun]
          ShowOff.run! :host => 'localhost', 
                       :port => options[:p].to_i
        end
      end
    end

!SLIDE small
# GLI #
## Special Error Handling ##

    @@@ Ruby
    on_error do |exception|
      # Error logic here
      # return false to skip default error handling
      true
    end

!SLIDE  small
# GLI #
## Hooks ##

    @@@ Ruby
    pre do |global,command,options,args|
      $url = global[:url]
      raise "You must specify a URL" if $url.nil?
      $trac = Trac.new($url,global[:u],global[:p])
      if $trac.valid?
        true
      else
        $stderr.puts "Couldn't connect to Trac at #{$url}!"
        false
      end
    end

    post do |global,command,options,args|
      # Post logic here
    end

!SLIDE bullets incremental
# GLI #
## Other Features ##
* Generate RDoc documentation
* Parse an "rc" file for user-defined defaults

!SLIDE bullets incremental
# Commander #
* Similar syntax to GLI
* glues many gems together (highline, asciitables, growl)
* No hooks or config file support 

!SLIDE bullets incremental
# Thor #
* Define tasks in ruby files and install them in a central repo
* Call those tasks from anywhere: <code>thor my_app:some_task</code>

!SLIDE bullets incremental
# The Point #
* Your command-line apps should be awesome
* Ruby provides *many* ways to do that
* Be kind to future you

!SLIDE smbullets
# Thanks! #
* [@davetron5000](http://www.twitter.com/davetron5000)
* OptionParser - [http://rubyforge.org/projects/optionparser/](http://rubyforge.org/projects/optionparser/)
* Trollop - [http://trollop.rubyforge.org/](http://trollop.rubyforge.org/)
* GLI - [http://github.com/davetron5000/gli/](http://github.com/davetron5000/gli/)
* Commander - [http://visionmedia.github.com/commander/](http://visionmedia.github.com/commander/)
* Highline (user interaction)- [http://highline.rubyforge.org/](http://highline.rubyforge.org/)
* Asciitables - [http://github.com/visionmedia/terminal-table](http://github.com/visionmedia/terminal-table)
* Rainbow (colorful output) - [http://github.com/sickill/rainbow](http://github.com/sickill/rainbow)
* Term-ansicolor (colorful output) - [http://github.com/flori/term-ansicolor](http://github.com/flori/term-ansicolor)
* Thor - [http://github.com/wycats/thor](http://github.com/wycats/thor)
