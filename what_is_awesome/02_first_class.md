!SLIDE bullets incremental
# ① Act First Class #
* It's not a “script”
* …it's an _application_
* Approach it as you would first-class application

!SLIDE smaller
# Example - Not First Class #
## [SBT](http://code.google.com/p/simple-build-tool/wiki/Setup) ##

    @@@ bash
    # Put the jar in your ~/bin directory, put the line
    # java -Xmx512M -jar `dirname $0`/sbt-launch.jar "$@"
    # in a file called sbt in your ~/bin directory and do 
    # chmod u+x ~/bin/sbt

!SLIDE commandline incremental
# Example - First Class #
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

!SLIDE bullets incremental
# How?
* Don't start off in `bash`…use Ruby
* Plan ahead for a _real_ UI, installation, maintainability, documentation, etc.
* If you plan ahead, this stuff isn't that hard
