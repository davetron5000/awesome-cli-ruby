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
* messaging (stdout) vs. output (file)

!SLIDE commandline
# Plays Horribly With Others #

    $ mvn test && start_server.sh
    Fill this in

!SLIDE commandline incremental
# Plays Well With Others #

    $ touch foo
    $ ls foo
    foo
    $ rm foo
    $ ls foo
    $ rm foo
    rm: foo: No such file or directory
