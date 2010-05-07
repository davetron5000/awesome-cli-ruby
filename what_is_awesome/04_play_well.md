!SLIDE bullets
# Play Well With Others #
## [Unix Philosophy](http://www.faqs.org/docs/artu/ch01s06.html) ##
### _(ii) Expect the output of every program to become the input to another, as yet unknown, program. Don't clutter output with extraneous information. Avoid stringently columnar or binary input formats. Don't insist on interactive input._ ###

!SLIDE  bullets incremental
# Play Well With Others #
* machine-parsable (e.g. delimited)
* line-oriented (greppable)
* exit codes! (0 for success, -1 for failure)
* messaging (stderr) vs. output (stdout)

!SLIDE 

    @@@Ruby

    matches = 0
    $stdin.readlines do |line|
      if line =~ /foo/
        puts line 
        matches += 1
      end
      $stderr.puts "Checking #{line}" if verbose
    end

    exit -1 if matches == 0
    exit 0

!SLIDE commandline
# Plays Horribly With Others #

    $ mvn test && start_server.sh
    Fill this in

!SLIDE commandline incremental
# Plays Well With Others #

    $ svn stat
    M Rakefile
    C README.rdoc
    ? bin/my_cmd
    C test/tc_cmd.rb
    $ svn stat | grep ^C
    C README.rdoc
    C test/tc_cmd.rb
    $ svn stat | grep ^C | awk '{print $2}'
    README.rdoc
    test/tc_cmd.rb
    $ vi `svn stat | grep ^C | awk '{print $2}'`
    # Now editing all files with conflicts
    $ svn stat | grep ^C | awk '{print $2}' | xargs svn resolved
    Resolved conflicted state of 'README.rdoc'
    Resolved conflicted state of 'test/tc_cmd.rb'
