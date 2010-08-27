!SLIDE
# Be helpful


!SLIDE commandline smaller incremental
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

!SLIDE commandline small incremental
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
    
!SLIDE commandline incremental
# Be Helpful #
## Simple ##

    $ my_cmd
    # should not have done anything destructive
    # maybe just a help statement
    $ my_cmd -h
    # lists common options
    $ my_cmd --help
    # should do same thing as -h
    $ my_cmd -help
    # Have pity on X-Windows refugees

!SLIDE commandline incremental
# Be Helpful #
## Command Suite ##

    $ my_cmd
    # lists available sub commands and global options
    $ my_cmd help
    # same thing
    $ my_cmd help subcommand
    # help on `subcommand` as well as options for that command

!SLIDE 
# Be Helpful #
## Useful error messages ##
### (or at least trap the errors) ###

    @@@Ruby
    cmd = "mv #{src}/*.csv #{dest}"
    unless system(cmd)
      $stderr.puts "Error executing #{cmd}"
      $stderr.puts $?
    end


