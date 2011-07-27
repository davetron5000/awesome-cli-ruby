!SLIDE
# Poor subprocess management

    @@@Ruby
    include FileUtils

    date = Time.now.to_s
    filename = "#{date}_foo_db.sql"
    tmp = "#{filename}.tmp"
    %x[mysqldump foo_db > #{tmp}]
    mv(tmp,filename)
    %x[gzip #{filename}]
    # Hope nothing went wrong!

!SLIDE bullets incremental
# How you should do it
* *Check exit codes* - plays well!
* *Log the command* - helpful!
* *Capture the output* - helpful!
* Think of "future you"

!SLIDE smaller 
# Use `open3`

    @@@Ruby
    command = "/full/path/to/some_external_command.sh"
    stdout,stderr,status = Open3.capture3(command)
    STDERR.puts(stderr) # Their stderr is our stderr

    if status.success?
      stdout.split(/\n/).each do |line|
        # Do our work
      end
      true
    else
      STDERR.puts("Problem running #{command}")
      false
    end

!SLIDE smaller
# Throw it in a method

    @@@Ruby
    include FileUtils

    def sh(command)
      # Stuff from previous slide...
    end

    date = Time.now.to_s
    filename = "#{date}_foo_db.sql"
    tmp = "#{filename}.tmp"
    if sh("mysqldump foo_db > #{tmp}")
      if mv(tmp,filename)
        if sh("gzip #{filename}")
          exit 0
        else
          exit 1
        end
      else
        rm(tmp)
        exit 2
      end
    else
      rm(tmp)
      exit 3
    end

!SLIDE bullets incremental
# Awesome subprocess management
* Customize it...
* ...put it in a gem...
* ...and use it instead of `system` or `%x[]`
* External calls are now bulletproof
* And it's the same LOC

