!SLIDE
# Poor `system` error handling

    @@@Ruby
    results = %x[some_external_command.sh]
    # Of course, everythning worked, right?
    results.readlines.each do |line|
      # Wait, is this stdout or stderr?!?!
    end

!SLIDE commandline

    $ my_script.rb
    sh: some_external_command.sh: command not found

!SLIDE 
# Worse

    @@@Ruby
    date = Time.now.to_s
    filename = "#{date}_foo_db.sql"
    system("mysqldump foo_db > #{filename}.tmp")
    FileUtils.mv("#{filename}.tmp",#{filename})
    system("gzip #{filename}")
    # Great for filling a disk!

!SLIDE bullets incremental
# How to really do it
* *Check exit codes* - plays well!
* *Log the command* - helpful!
* *Capture the output* - helpful!
* Think of “future you”

!SLIDE smaller 
# Use `open3`

    @@@Ruby
    command = "/full/path/to/some_external_command.sh"
    stdout,stderr,status = Open3.capture3(command)
    $stderr.split(/\n/).each { |line| $stderr.puts(line) }
    if status == 0 # Only in UNIX does 0 mean success
      stdout.split(/\n/).each do |line|
        # Do our work
      end
      true
    else
      $stderr.puts("Problem running #{command}")
      false
    end

!SLIDE smaller
# Throw it in a method

    @@@Ruby
    date = Time.now.to_s
    filename = "#{date}_foo_db.sql"
    if awe_sh("mysqldump foo_db > #{filename}.tmp")
      if FileUtils.mv("#{filename}.tmp",#{filename})
        if awe_sh("gzip #{filename}")
          exit 0
        else
          exit -1
        end
      else
        FileUtils.rm("#{filename}.tmp")
        exit -2
      end
    else
      FileUtils.rm("#{filename}.tmp")
      exit -3
    end

!SLIDE bullets incremental
# Poor `system` handling
* Customize it…
* …put it in a gem… 
* …and use it instead of `system` or `%x[]`
* External calls are now bulletproof
* And it's the same LOC

