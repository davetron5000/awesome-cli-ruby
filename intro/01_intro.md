!SLIDE smbullets
# Use Ruby to Start Making Awesome Command Line Applications
## Dave Copeland
* [@davetron5000](http://www.twitter.com/davetron5000) 
* `davidcopeland (at) naildrivin5.com`
* `david.copeland (at) livingsocial.com`
* [naildrivin5.com/blog](http://www.naildrivin5.com/blog)
* [www.awesomecommandlineapps.com](http://www.awesomecommandlineapps.com)

!SLIDE commandline incremental
# Who am I? #

    $ who am i
    Dave Copeland
    $ ps
    Engineer at LivingSocial

!SLIDE center

<img src="book_cover.jpg" />

!SLIDE commandline incremental
# Who am I? #

    $ history
    1986  c64 basic
    1991  C # vi cursor keys didn't work
    1995  Perl
    1998  Java
    2008  Ruby
    $ history | grep IDE
    2010 history | grep IDE

!SLIDE 
# Why care about command-line apps? #

!SLIDE
# An all too familiar tale...

!SLIDE commandline incremental
# Emergency! #

    $ vi one_off_script.sh
    $ ./one_off_script.sh -x /tmp/foo.csv > /top/magic.txt
    done.
    $ git add one_off_script.sh
    $ git commit -m 'automated stuff in time for launch'

!SLIDE center
# 6 Months Later... #
<img src="rage1.jpg" />

!SLIDE center
# 6 Months Later... #
<img src="rage2.jpg" />

!SLIDE center
# 6 Months Later... #
<img src="rage3.jpg" />

!SLIDE center
# Challenge Accepted
<img src="challenge.png" height='600'/>

!SLIDE commandline incremental
# Challenge Accepted
    $ ./one_off_script.sh 
    -bash: /tmp/intermediate.xml: not found 
    $ ./one_off_script.sh help
    -bash: help: command not found
    $ ./one_off_script.sh --help
    done.
    $ ./one_off_script.sh /?
    ls: /? No such file or directory

!SLIDE center
## <tt>vi ./one\_of\_script.sh</tt>
<img src="ok.png" />


!SLIDE bullets incremental
# Why care about command-line apps? #
* You *will* have to write them
* And they *will* become someone's job
* And you *will* be on the hook to fix them
* Think about "future you"

!SLIDE
# Also, the command-line is an **infinitely flexible** way to **glue disparate systems** together and being able to write them makes you a **better, more versatile** developer
!SLIDE bullets incremental
# Make even your one-off scripts awesome #

* No script is really a one-off
* Be kind to "future you"
* Ruby can make it easy
