!SLIDE 
# ② Play Well With Others

!SLIDE bullets incremental
# The UNIX Way
## [http://www.faqs.org/docs/artu/ch01s06.html](http://www.faqs.org/docs/artu/ch01s06.html) ##
### _(ii) Expect the output of every program to become the input to another, as yet unknown, program. Don't clutter output with extraneous information. Avoid stringently columnar or binary input formats. Don't insist on interactive input._ ###

!SLIDE  bullets incremental
# The UNIX Way ##
* machine-parsable (e.g. delimited)
* line-oriented (greppable)
* exit codes! (0 for success, -1 for failure)
* messaging (stderr) vs. output (stdout)

!SLIDE commandline incremental smaller
# Example - Plays Horribly With Others #

    $ mvn test -Dtest=TestHeatingComparison
    [INFO] Scanning for projects...
    [INFO] ------------------------------------------------------------------------
    [INFO] Building Standalone Core Library
    [INFO]    task-segment: [test]
    [INFO] ------------------------------------------------------------------------
    [INFO] [resources:copy-resources {execution: default}]
    [INFO] Using 'UTF-8' encoding to copy filtered resources.
    [INFO] skip non existing resourceDirectory /Users/davec/Projects/opower/core/null/null/trunk/src/main/resources/webclientconfig/clients/null/assets
    [INFO] [svn-revision-number:revision {execution: default}]
    [INFO] inspecting /Users/davec/Projects/opower/core
    [INFO] [resources:resources {execution: default-resources}]
    [INFO] Using 'UTF-8' encoding to copy filtered resources.
    [INFO] Copying 9 resources
    [INFO] Copying 1 resource
    [INFO] Copying 332 resources to patches/core
    [INFO] Copying 23 resources to postpatches/core
    [INFO] [compiler:compile {execution: default-compile}]
    [INFO] Compiling 16 source files to /Users/davec/Projects/opower/core/target/classes
    [INFO] [checkstyle:checkstyle {execution: checkstyle}]
    [INFO] Starting audit...
    Audit done.

    [INFO] Setting property: classpath.resource.loader.class => 'org.codehaus.plexus.velocity.ContextClassLoaderResourceLoader'.
    [INFO] Setting property: velocimacro.messages.on => 'false'.
    [INFO] Setting property: resource.loader => 'classpath'.
    [INFO] Setting property: resource.manager.logwhenfound => 'false'.
    [INFO] ************************************************************** 
    [INFO] Starting Jakarta Velocity v1.4
    [INFO] RuntimeInstance initializing.
    [INFO] Default Properties File: org/apache/velocity/runtime/defaults/velocity.properties
    [INFO] Default ResourceManager initializing. (class org.apache.velocity.runtime.resource.ResourceManagerImpl)
    [INFO] Resource Loader Instantiated: org.codehaus.plexus.velocity.ContextClassLoaderResourceLoader

!SLIDE commandline smaller
# Plays Horribly With Others (con't) #

    $ mvn test -Dtest=TestHeatingComparison # con't
    [INFO] ClasspathResourceLoader : initialization starting.
    [INFO] ClasspathResourceLoader : initialization complete.
    [INFO] ResourceCache : initialized. (class org.apache.velocity.runtime.resource.ResourceCacheImpl)
    [INFO] Default ResourceManager initialization complete.
    [INFO] Loaded System Directive: org.apache.velocity.runtime.directive.Literal
    [INFO] Loaded System Directive: org.apache.velocity.runtime.directive.Macro
    [INFO] Loaded System Directive: org.apache.velocity.runtime.directive.Parse
    [INFO] Loaded System Directive: org.apache.velocity.runtime.directive.Include
    [INFO] Loaded System Directive: org.apache.velocity.runtime.directive.Foreach
    [INFO] Created: 20 parsers.
    [INFO] Velocimacro : initialization starting.
    [INFO] Velocimacro : adding VMs from VM library template : VM_global_library.vm
    [ERROR] ResourceManager : unable to find resource 'VM_global_library.vm' in any resource loader.
    [INFO] Velocimacro : error using  VM library template VM_global_library.vm : org.apache.velocity.exception.ResourceNotFoundException: Unable to find resource 'VM_global_library.vm'
    [INFO] Velocimacro :  VM library template macro registration complete.
    [INFO] Velocimacro : allowInline = true : VMs can be defined inline in templates
    [INFO] Velocimacro : allowInlineToOverride = false : VMs defined inline may NOT replace previous VM definitions
    [INFO] Velocimacro : allowInlineLocal = false : VMs defined inline will be  global in scope if allowed.
    [INFO] Velocimacro : initialization complete.
    [INFO] Velocity successfully started.
    [INFO] [resources:testResources {execution: default-testResources}]
    [INFO] Using 'UTF-8' encoding to copy filtered resources.
    [INFO] Copying 501 resources
    [INFO] Copying 9 resources
    [INFO] [compiler:testCompile {execution: default-testCompile}]
    [INFO] Compiling 1 source file to /Users/davec/Projects/opower/core/target/test-classes
    [INFO] [surefire:test {execution: default-test}]

!SLIDE commandline smaller
# Plays Horribly With Others (con't) #

    $ mvn test -Dtest=TestHeatingComparison # still con't
    [INFO] Surefire report directory: /Users/davec/Projects/opower/core/target/surefire-reports

    -------------------------------------------------------
     T E S T S
    -------------------------------------------------------
    Running poscore.model.TestHeatingComparison
    Tests run: 6, Failures: 1, Errors: 0, Skipped: 0, Time elapsed: 0.133 sec <<< FAILURE!

    Results :

    Failed tests: 
      testSetters(poscore.model.TestHeatingComparison)

    Tests run: 6, Failures: 1, Errors: 0, Skipped: 0

    [INFO] ------------------------------------------------------------------------
    [ERROR] BUILD FAILURE
    [INFO] ------------------------------------------------------------------------
    [INFO] There are test failures.

    Please refer to /Users/davec/Projects/opower/core/target/surefire-reports for the individual test results.
    [INFO] ------------------------------------------------------------------------
    [INFO] For more information, run Maven with the -e switch
    [INFO] ------------------------------------------------------------------------
    [INFO] Total time: 13 seconds
    [INFO] Finished at: Fri May 07 13:50:01 EDT 2010
    [INFO] Final Memory: 54M/527M
    [INFO] ------------------------------------------------------------------------

    $ echo $?
    0
    
!SLIDE commandline incremental
# Example - Plays Well With Others #

    $ svn stat
    M Rakefile
    C README.rdoc
    ? bin/my_cmd
    C test/tc_cmd.rb
    $ vi `svn stat | grep ^C | awk '{print $2}'`
    # Now editing all files with conflicts
    $ svn stat | grep ^C | awk '{print $2}' | xargs svn resolved
    Resolved conflicted state of 'README.rdoc'
    Resolved conflicted state of 'test/tc_cmd.rb'

