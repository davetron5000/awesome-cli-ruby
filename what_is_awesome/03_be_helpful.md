!SLIDE commandline incremental
# Be Helpful #
## Simple ##
    $ my_cmd -h
    lists common options
    $ my_cmd --help
    should do same thing as -h

!SLIDE commandline incremental
# Be Helpful #
## git-style ##
    $ my_cmd
    lists available sub commands and global options
    $ my_cmd help
    same thing
    $ my_cmd help subcommand
    help on `subcommand` as well as options for that command

!SLIDE bullets incremental
# Be Helpful #
* no news is good news
* useful error messages

!SLIDE commandline smaller
# Not Helpful

    $ latex
    This is pdfeTeX, Version 3.141592-1.21a-2.2 (Web2C 7.5.4)
    **
    ^C
    $ latex help
    This is pdfeTeX, Version 3.141592-1.21a-2.2 (Web2C 7.5.4)
    entering extended mode
    ! I can't find file `help'.
    <*> help
            
    Please type another input file name:^C
    ! I can't find file `help'.
    <*> help
            
    Please type another input file name: ^D
    ! Emergency stop.
    <*> help
            
    No pages of output.
    Transcript written on texput.log.

!SLIDE commandline small
# Helpful

    $ git
    usage: git [--version] [--exec-path[=GIT_EXEC_PATH]] [--html-path]
               [-p|--paginate|--no-pager]
               [--bare] [--git-dir=GIT_DIR] [--work-tree=GIT_WORK_TREE]
               [--help] COMMAND [ARGS]

    The most commonly used git commands are:
       add        Add file contents to the index
       bisect     Find by binary search the change that introduced a bug
       <snip>
       tag        Create, list, delete or verify a tag object signed with GPG

    See 'git help COMMAND' for more information on a specific command.
    
!SLIDE bullets
# Play Well With Others #
## [Unix Philosophy](http://www.faqs.org/docs/artu/ch01s06.html) ##
### _(ii) Expect the output of every program to become the input to another, as yet unknown, program. Don't clutter output with extraneous information. Avoid stringently columnar or binary input formats. Don't insist on interactive input._ ###
