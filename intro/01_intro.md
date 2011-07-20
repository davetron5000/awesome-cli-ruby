!SLIDE smbullets
# Start making Awesome Command-Line Apps
## (with Ruby)
### Dave Copeland
* [@davetron5000](http://www.twitter.com/davetron5000) / davidcopeland (at) naildrivin5.com
* [naildrivin5.com/blog](http://www.naildrivin5.com/blog)

!SLIDE commandline incremental
# Who am I? #

    $ who am i
    Dave Copeland
    $ ps
    Principal Engineer at OPOWER
    $ whois OPOWER
    An energy-efficiency software company in DC
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
# An all too familiar tale…

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
<img src="challenge.png" height='600'/>

!SLIDE commandline incremental
# Opposite of fun
    $ ./one_off_script.sh 
    -bash: /tmp/intermediate.xml: not found 
    $ ./one_off_script.sh help
    -bash: help: command not found
    $ ./one_off_script.sh --help
    done.
    $ ./one_off_script.sh /?
    ls: /? No such file or directory

!SLIDE center
## <tt>vi ./one_off_script.sh</tt>
<img src="ok.png" />


!SLIDE bullets incremental
# Why care about command-line apps? #
* You *will* have to write them
* And they *will* become someone's job
* And you *will* be on the hook to fix them

!SLIDE
# Also, the command-line is an infinitely flexible way to glue disparate systems together and you should totally write more command-line apps in general, because they are super helpful to developers and sysadmins alike!
!SLIDE bullets incremental
# Make even your one-off scripts awesome #

* No script is really a one-off
* Be kind to “future you”
* Ruby can make it easy
