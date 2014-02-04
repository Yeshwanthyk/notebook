==============================
`Working with Unix Processes`_
==============================
By `Jesse Storimer`_

The book uses ruby to explore UNIX processes. Jesse also gives the corresponding man page the command maps to.

---
PID
---

* On any UNIX system. Just type *man <command_name>*
* Each process has a **PID**:

.. code-block:: ruby

    puts Process.pid

* maps to *getpid(2)*
* A global (albeit implicit) way to retreive the current pid is using *$$*

----
PPID
----

* Each process has a Parent process **PPID**:

.. code-block:: ruby

        puts Process.ppid

*maps to *getppid(2)*

---------------
File Descriptor
---------------

* In UNIX everything is treated as a file(resource). Any time a resource is opened within a process it is assigned a **file descriptor** number.
* File descriptor are *NOT* shared between unrelated processes. They live and die with the process they are bound to:

.. code-block:: ruby

        passwd = File.open('/etc/passwd')
        puts passwd.fileno                  => 3

* In ruby, open resources are represented by IO class
* The fileno is the way kernel keeps track of the resource:

.. code-block:: ruby

        passwd = File.open('/etc/passwd')
        puts passwd.fileno                  => 3

        hosts = File.open('/etc/hosts')
        puts hosts.fileno                   => 4

        passwd.close

        null = File.open('/dev/null')
        puts null.fileno                    => 3

* Key points from the above example
    - File descriptors take the lowest unused value.
    - Once a descriptor is closed, the number becomes available again.
* *What* happened to 0,1 and 2 file descriptors?

.. code-block:: ruby

        puts STDIN.fileno       => 0
        puts STDOUT.fileno      => 1
        puts STDERR.fileno      => 2

* Ruby IO maps to *open(2)*, *close(2)*, *read(2)*, *write(2)*,
    *pipe(2)*, *fsync(2)*, *stat(2)* etc

--------------
Resource Limit
--------------

* Limits are imposed by the kernel:

.. code-block:: ruby

        Process.getrlimit(:NOFILE) => [2560, big_number]

* getrlimit return a 2-element array
    - First number is the soft limit
    - Second number is hard limit
* The soft limit can be bumped by:

.. code-block:: ruby

        Process.setrlimit(:NOFILE, 4096)

To set soft limit to the hard limit:

.. code-block:: ruby

        Process.setrlimit(:NOFILE, Process.getrlimit(:NOFILE)[1])

* If you exceed the soft limit, an exception will be raised (Errno::EMFILE)
* Real world examples:
    - If you want to handle thousands of sumultaneous network connections
    - Restrain system resources when executing third part code
* Maps to *getrlimit(2)* and *setrlimit(2)*

--------------------------
Environment of the Process
--------------------------

* A little ruby heavy chapter
* Every process inherits environment variable from its parent. Its set per process and global to each process.
* Ruby ENV used hash-style accessor, but doesn't implement all the **Hash** API:

.. code-block:: ruby

    puts ENV['EDITOR']
    puts ENV.has_key?('PATH')

* Access to special Array called **ARGV**
* You can change the name of the process:

.. code-block:: ruby

    puts $PROGRAM_NAME

    10.downto(1) do |num|
        $PROGRAM_NAME = "Process: #{num}"
        puts $PROGRAM_NAME
    end

* Somewhat maps to *setenv(2)* and *getenv(2)*. Also, *environ(2)*


.. _Working with Unix Processes: http://www.jstorimer.com/products/working-with-unix-processes
.. _Jesse Storimer: http://www.jstorimer.com/
