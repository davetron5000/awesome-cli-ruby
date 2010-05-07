!SLIDE bullets incremental
# Act First Class #
* It's not a "script"
* It's an _application_
* Approach it as a first class application

!SLIDE smaller
# Not First Class #
## [SBT](http://code.google.com/p/simple-build-tool/wiki/Setup) ##

    @@@ bash
    # Put the jar in your ~/bin directory, put the line
    # java -Xmx512M -jar `dirname $0`/sbt-launch.jar "$@"
    # in a file called sbt in your ~/bin directory and do 
    # chmod u+x ~/bin/sbt

!SLIDE commandline incremental
# First Class #
    $ gem install showoff
    $ showoff help
    usage: showoff command

    Commands:
        add, new     - Add a new slide at the end in a given dir
        create, init - Create new showoff presentation
        help         - Shows list of commands or help for 
                       one command
        heroku       - Setup your presentation to serve 
                       on Heroku
        serve        - Serves the showoff presentation in the 
                       current directory

