!SLIDE bullets incremental
# What about command-suite?
* `OptionParser` not well suited
* A few other options

!SLIDE bullets incremental
# `GLI`
* Tailor-made for command-suite
* Make it easy for a polished UI
* Easy to get started

!SLIDE commandline small incremental

    $ gem install gli
    Successfully installed gli
    $ gli init todo new list complete
    Creating dir ./todo/lib...
    Creating dir ./todo/bin...
    Creating dir ./todo/test...
    Created ./todo/bin/todo
    $ cd todo ; ls
    Gemfile       README.rdoc    Rakefile
    bin/          lib/           test/         
    todo.gemspec  todo.rdoc
    $ todo/bin/todo
    usage: todo [global options] command [command options]

    Version: 0.0.1

    Global Options:
        -f, --flagname=The name of the argument - Describe some flag here 
                                                  (default: the default)
        -s, --switch                            - Describe some switch here

    Commands:
        complete - Describe complete here
        help     - Shows list of commands or help for one command
        list     - Describe list here
        new      - Describe new here
   
!SLIDE bullets incremental
# What did we just get?
* Command and option parsing
* Complex help formatting
* Boilerplate gem-ified project

!SLIDE
# Make UI

    @@@Ruby
    desc 'List all todo items'
    command :list do |c|
      c.desc 'List in long form'
      c.switch :l

      c.desc 'Show all items, even completed'
      c.switch [:a,:all]

      c.desc 'Specify sort order'
      c.arg_name '[date|name|completed]'
      c.flag [:s,:sort]
      c.action do |global_options,options,args|
        # Logic goes here
      end
    end
   
!SLIDE commandline incremental
# And now…
    $ bin/todo help
    usage: todo command [command options]

    Version: 0.0.1

    Commands:
        complete - Complete one or more items
        help     - Shows list of commands or help for one command
        list     - List all todo items
        new      - Create a new todo item
    $ bin/todo help list
    list [command options] 
        List all todo items

    Command Options:
        -a, --all                        - Show all items, even 
                                           completed ones
        -l                               - List in long form
        -s, --sort=[date|name|completed] - Specify sort order


!SLIDE bullets incremental
# But wait…there's more
* Pre and Post hooks
* Custom error handling
* One-line config file support
