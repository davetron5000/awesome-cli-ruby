!SLIDE
# ② Be helpful

!SLIDE commandline smaller incremental
# Example - Not Helpful

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
## (Command Suite application)
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
    
!SLIDE bullets incremental
# Be Helpful #
## Simple ##
### `my_cmd`

* Don't do anything destructive by default
* Show a brief help statement

!SLIDE bullets incremental
# Be Helpful #
## Simple ##
### `my_cmd -h`

* Show a fuller help statement
* Also support `--help`

!SLIDE bullets incremental
# Be Helpful #
## Command Suite ##
### `my_cmd`

* List available commands
* List globally-applicable options
* Oh, and maybe say what your app is for

!SLIDE bullets incremental
# Be Helpful
## Command Suite
### `my_cmd help`
* Same thing

!SLIDE bullets incremental
# Be Helpful #
## Command Suite ##
### `my_cmd help command_name`

* help on `command_name` 
* i.e. what it does
* and the options available

!SLIDE bullets incremental
# Oh, and useful error messages
* “undefined method `[]' for nil:NilClass (NoMethodError)”

!SLIDE bullets incremental
# One `if` and 3 minutes later…
* “Please specify your username”
* _(or whatever)_
