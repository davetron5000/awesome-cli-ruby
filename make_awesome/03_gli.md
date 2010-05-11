!SLIDE bullets incremental
# <code>GLI</code> - Git Like Interface
* Designed for 'command suite' style
* Designed to make polished app easy to create
* Syntax inspired by Rake

!SLIDE commandline smaller
# Bootstrap your Application

    $ sudo gem install gli
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
        
    

!SLIDE smaller
# GLI #
## Scaffold app ##

    @@@ Ruby
    #!/usr/bin/ruby
    $: << File.expand_path(File.dirname(__FILE__) + '/../lib')
    require 'rubygems'
    require 'gli'

    include GLI

    # Define any global options you want
    desc 'Describe some switch here'
    switch [:s,:switch]

    desc 'Describe some flag here'
    default_value 'the default'
    arg_name 'The name of the argument'
    flag [:f,:flagname]

    # define subcommands
    # specify special error handling
    # pre/post hooks

    GLI.run(ARGV)

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
        ShowOff.run! :host => 'localhost', 
                     :port => options[:p].to_i
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
      if command.nil? || command.name == :help
        # not creating a trac instance
      else
        $url = global[:url]
        raise "You must specify a URL" if $url.nil?
        $trac = Trac.new($url,global[:u],global[:p])
      end
      true
    end

    post do |global,command,options,args|
      # Post logic here
    end

!SLIDE bullets incremental
# GLI #
## Other Features ##
* Generate RDoc documentation
* Parse an "rc" file for user-defined defaults

!SLIDE bullets
# Thanks! #
* [@davetron5000](http://www.twitter.com/davetron5000)
* [OptionParser](http://rubyforge.org/projects/optionparser/)
* [GLI](http://github.com/davetron5000/gli/)
