::: {#content .topic-text wv="http://www.openlinksw.com/Virtuoso/WikiV/" vi="http://www.openlinksw.com/virtuoso/xslt/" ie="http://www.openlinksw.com/Virtuoso/InclEng/" fn2="http://www.w3.org/2004/07/xpath-functions" xmlns="http://www.w3.org/1999/xhtml"}
::: {.MACRO_TOC}
Table of Contents {#table-of-contents .toc}
-----------------

-   [Abstract](#Abstract)
-   [Required Components](#Required%20Components)
-   -   [iODBC Driver Manager](#iODBC%20Driver%20Manager)
    -   -   [Linux](#Linux)
        -   [Mac OS X](#Mac%20OS%20X)
        -   [Other Unix operating
            systems](#Other%20Unix%20operating%20systems)
        -   [Configuring and Testing
            iODBC](#Configuring%20and%20Testing%20iODBC)

    -   [Ruby](#Ruby)
    -   -   [Linux](#Linux)
        -   [Mac OS X](#Mac%20OS%20X)
        -   [From Source](#From%20Source)

    -   [Ruby/ODBC Binding](#Ruby%2FODBC%20Binding)
    -   -   [Linux](#Linux)
        -   [Mac OS X, other Unix platforms: build from
            source](#Mac%20OS%20X%2C%20other%20Unix%20platforms%3A%20build%20from%20source)
        -   [Testing](#Testing)

    -   [Ruby/DBI DBD::ODBC
        Driver](#Ruby%2FDBI%20DBD%3A%3AODBC%20Driver)
    -   -   [Cross-platform: Ruby GEM](#Cross-platform%3A%20Ruby%20GEM)
        -   [Linux Packages](#Linux%20Packages)
        -   [Mac OS X and other Unix-like systems: building from
            source](#Mac%20OS%20X%20and%20other%20Unix-like%20systems%3A%20building%20from%20source)
        -   -   [DBI](#DBI)
            -   [DBD::ODBC](#DBD%3A%3AODBC)
            -   [Testing Ruby, DBI,
                ODBC](#Testing%20Ruby%2C%20DBI%2C%20ODBC)
:::

[]{#Abstract}Abstract
---------------------

This HOWTO is intended to walk you through the process of installing and
configuring iODBC, Ruby and the Ruby/ODBC bridge module with a goal of
writing and executing simple scripts to effect a database connection. It
is currently maintained by Tim Haynes of [OpenLink
Software](http://www.openlinksw.com/){.absuri}, \<\<none\>\>, that is
`iodbc` at `openlinksw.com`.

We assume you have some familiarity with using either Terminal on Apple
Mac OS X or the shell on a GNU/Linux platform such as Ubuntu, Debian,
RedHat, or Fedora Core, etc.

[]{#Required%20Components}Required Components
---------------------------------------------

### []{#iODBC%20Driver%20Manager}iODBC Driver Manager

We start by installing the iODBC Driver Manager.

#### []{#Linux}Linux

Some Linux distributions (Debian, Ubuntu, Gentoo) have their own
packages for iODBC, so you should only need to type a command such as
one of

-   `sudo apt-get install libiodbc2 iodbc`
-   `sudo emerge libiodbc`
-   `sudo yum install iodbc`

to install it, and possibly some dependencies (GTK+ libraries for the
adminstrator utility), automatically.

#### []{#Mac%20OS%20X} Mac OS X

For Mac OS X users, we provide a DMG installer on our
[Downloads](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/Downloads){.wikiword}
page. This will install the iODBC Framework, development environment and
graphical configuration utility.

Note that this supersedes the version of iODBC supplied by Apple with
Mac OS X, as it resolves two bugs:

-   on 64-bit machines, ruby would be built in 64-bit mode by default
    but the system libiodbc is only 32-bit, making building the
    ruby-odbc bridge impossible;
-   the handling of SQLError() in ruby-odbc.

#### []{#Other%20Unix%20operating%20systems}Other Unix operating systems

On other unix operating systems, you need to compile iODBC from source.
This is generally easy:

-   [Download](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/Downloads){.wikiword}
    the iODBC source tarball
-   unpack it using a command such as
    `gzip -cd         libiodbc-3.52.7.tar.gz| tar xvf -`
-   `./configure         --prefix=/usr/local/iODBC/`
-   `make`
-   become root and run `make install`, e.g.,
    `su root -c 'make install'`

Of course you can also build the same way on linux; the `./configure`
script takes a few options you might want to vary, notably
`--with-prefix=` for where the files will be installed and
`--enable-gui` for whether to build the GTK+ Administrator or not.

If you wish to build from source on Mac OS X, after unpacking the
archive, run

-   `cd mac`
-   `make`
-   `sudo make install`

This will build the Framework version and create a subdirectory under
/usr/local/iODBC/ so that other applications (eg PHP, Perl, Ruby) can
link against it without having to modify them to look for frameworks.

#### []{#Configuring%20and%20Testing%20iODBC}Configuring and Testing iODBC

It is wise to test that iODBC works directly before trying to layer any
Ruby ODBC module on top. Either:

-   use the graphical Administrator application (**iodbcadm-gtk** on
    linux/unix or **iODBC Administrator.app** (/Applications/iODBC/) on
    Mac OS X) to register an ODBC driver, add a System or User DSN using
    the driver, and test it, or
-   edit your own `odbc.ini` (`/etc/odbc.ini`, `~/.odbc.ini`, or
    `$ODBCINI` environment variable) to contain something similar to the
    following:

<!-- -->

    [ODBC Data Sources]
    pgdata = Native PostgreSQL ODBC driver

    [pgdata]
    Driver=/usr/lib/odbc/psqlodbcw.so
    Host       = data
    Server     = data
    ServerName = data
    Database   = me
    UserName   = me
    UID        = me
    Port       = 5432

From the commandline you should be able to run `iodbctest DSN=pgdata`
and it should attempt to connect:

    zsh, ubuntu libiodbc-3.52.7/ % iodbctest DSN=pgdata 
    iODBC Demonstration program
    This program shows an interactive SQL processor
    Driver Manager: 03.52.0709.0909
    Driver: 08.03.0200 (psqlodbcw.so)

    SQL>

The `SQL>` prompt there shows iodbctest has connected and is now
awaiting a SQL command as input; additionally it understands the command
\``tables`\' which lists tables visible in the current database.

Note the \`DSN=pgdata\' parameter: this is part of an ODBC connection
string, not just a data-source name. As such it takes the form

    DSN=somedsn;[param=value[;]]*

where the parameters are specific to the ODBC driver being used. In this
case, the PostgreSQL native ODBC driver requires Host, Database and
Port, above. For MySQL and OpenLink drivers, the parameters vary.

The [iODBC
FAQ](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/FAQ){.wikiword}
contains a section of common error messages in the event of something
going wrong at this stage.

### []{#Ruby}Ruby

Ruby is an open-source, interpreted, dynamic, object-oriented scripting
language in the same space as Perl, Python on the desktop and with the
famous Ruby-on-Rails engine in web-space (to compare with PHP).

There are two ways in which Ruby interfaces with ODBC: a ruby-odbc
binding module which presents the ODBC API at the Ruby layer with little
abstraction, maintained by Christian Werner; and a DBD::ODBC module that
provides a driver compatible with DBI (a database-interaction
specification familiar to Perl users, now implemented in Ruby). The
DBD::ODBC driver depends upon the ruby-odbc binding, so we continue
building the packages in hierarchical order.

#### []{#Linux}Linux

Most Linux distributions have packages for
[Ruby](http://www.ruby-lang.org/en/){.absuri} already. Remember if your
distribution distinguishes between runtime and development versions
packages, you will need to install the development libraries in order to
compile other packages from source against them.

-   Debian/Ubuntu: `sudo apt-get install ruby         ruby-dev`
-   Gentoo: `sudo emerge -av ruby`

#### []{#Mac%20OS%20X}Mac OS X

Mac OS X, from Tiger onwards, comes with Ruby 1.8 by default. No further
installation is required, unless you really want to build it from source
yourself.

#### []{#From%20Source}From Source

For other unix environments, it might be required to build Ruby from
source. That process is not documented here except to say that it
follows a similar path to iODBC from source: download, unpack, run
`./configure`, `make` and `sudo make install`.

### []{#Ruby%2FODBC%20Binding}Ruby/ODBC Binding

Christian Werner maintains the [ruby-odbc binding
module](http://ch-werner.de/rubyodbc/){.absuri}.

#### []{#Linux}Linux

Some GNU/Linux distributions (debian and ubuntu in particular) have
already packaged the ruby-odbc binding, so a simple

    zsh, ubuntu ruby/ % sudo apt-get install libodbc-ruby1.8 

is all that\'s required.

However, for better handling of SQLError(), we recommend you use the
latest iODBC (3.52.7) and ruby-odbc module (0.9997) so you might still
need to build from source, as follows.

#### []{#Mac%20OS%20X%2C%20other%20Unix%20platforms%3A%20build%20from%20source} Mac OS X, other Unix platforms: build from source

The following instructions apply equally to Linux, Mac OS X, and other
Unix-like operating systems, as we\'re building from source here.

Download this and unpack it as usual:

    zsh, pizza C/ % tar xvfz ruby-odbc-0.9997.tar.gz
    ./ruby-odbc-0.9997/
    ./ruby-odbc-0.9997/doc/
    ./ruby-odbc-0.9997/doc/odbc.html
    ./ruby-odbc-0.9997/test/
    ...
    zsh, pizza C/ % cd ruby-odbc-0.9997 
    zsh, pizza ruby-odbc-0.9997/ % 

To configure it, run

    zsh, pizza ruby-odbc-0.9997/ % ruby extconf.rb --with-odbc-dir=/usr/local/iODBC
    checking for version.h... yes
    checking for sql.h... yes
    checking for sqlext.h... yes
    checking for SQLTCHAR in sqltypes.h... yes
    checking for SQLLEN in sqltypes.h... yes
    checking for SQLULEN in sqltypes.h... yes
    checking for odbcinst.h... yes
    checking for SQLAllocConnect() in -liodbc... yes

**Note** three things:

-   first, we tell it where to find the iODBC libraries using
    \--with-odbc-dir (which works well with Mac OS X, where ordinarily
    libraries are provided using frameworks, so to avoid needing to use
    those, the iODBC installer package provides a /usr/local/iODBC/
    directory with symbolic links into the Frameworks directory);
-   secondly, it must report successful checking using `-liodbc`, not
    -lodbc - unless you\'ve symlinked the two libraries together;
-   thirdly, you need iODBC version 3.52.7 and ruby-odbc version 0.9997
    to fix a bug in the handling of SQLError()

We continue to build and install it:

    zsh, pizza ruby-odbc-0.9997/ % make
    /usr/bin/gcc-4.0 -I. -I. -I/usr/local/ruby/1.8/powerpc-darwin8 -I. \
            -DHAVE_VERSION_H -DHAVE_SQL_H -DHAVE_SQLEXT_H -DHAVE_TYPE_SQLTCHAR \
            -DHAVE_TYPE_SQLLEN -DHAVE_TYPE_SQLULEN -DHAVE_ODBCINST_H \ 
            -DHAVE_SQLINSTALLERERROR -I/usr/local/iODBC/include -I/opt/local/include \ 
            -D_XOPEN_SOURCE -D_DARWIN_C_SOURCE  -I/opt/local/include -fno-common \
            -O2  -fno-common -pipe -fno-common   \
            -c init.c
    ...
    zsh, pizza ruby-odbc-0.9997/ % sudo make install
    Password:
    /usr/bin/install -m 0755 odbc.bundle /usr/local/ruby/site_ruby/1.8/powerpc-darwin8

To check that it built correctly, run one of the following commands to
see the shared library dependencies; there should be a mention of
\`iodbc\' somewhere in the output:

On Mac OS X:

    zsh, pizza ruby-odbc-0.9997/ % otool -L /usr/local/ruby/site_ruby/1.8/powerpc-darwin8/odbc.bundle 
    /usr/local/ruby/site_ruby/1.8/powerpc-darwin8/odbc.bundle:
            /usr/local/lib/libruby.dylib (compatibility version 1.8.0, current version 1.8.7)
            /usr/local/lib/libiodbcinst.1.dylib (compatibility version 2.0.0, current version 2.0.0)
            /usr/local/lib/libiodbc.1.dylib (compatibility version 2.0.0, current version 2.0.0)

On Linux/Unix:

    zsh, ubuntu ruby-odbc-0.9997/ % ldd /usr/lib/ruby/site_ruby/1.8/i486-linux/odbc.so 
    [...]
            libc.so.6 => /lib/libc.so.6 (0xb7d0e000)
            libiodbc.so.2 => /usr/local/lib/libiodbc.so.2 (0xb7cc6000)
            libiodbcinst.so.2 => /usr/local/lib/libiodbcinst.so.2 (0xb7cb3000)
            /lib/ld-linux.so.2 (0xb7fd2000)

#### []{#Testing}Testing

Having installed the ruby-odbc binding module, you can write a simple
ruby script to test it such as the attached which makes a connection and
probes some metadata available through the ODBC connection:

-   [odbc-metadata.rb](IODBCRubyHOWTO/odbc-metadata.rb){.c2}

<!-- -->

    zsh, ubuntu ruby/ % ./odbc-metadata.rb pgdata "" ""
    Connecting to [pgdata, , ]
    Connected: true

    Data-types:

    Type integer:
    Native: int4
      TYPE_NAME:           int4
      DATA_TYPE:           4
      PRECISION:           10
      LITERAL_PREFIX:      
      LITERAL_SUFFIX:      
      CREATE_PARAMS:       
      NULLABLE:            1
      CASE_SENSITIVE:      0
      SEARCHABLE:          2
      UNSIGNED_ATTRIBUTE:  0
      MONEY:               0
      AUTO_INCREMENT:      0
      LOCAL_TYPE_NAME:     
      MINIMUM_SCALE:       0
      MAXIMUM_SCALE:       0
      SQL_DATA_TYPE:       4
      SQL_DATETIME_SUB:    
      NUM_PREC_RADIX:      10
      INTERVAL_PRECISION:  0
    ...

    Trying type SQL_CURSOR_ROLLBACK_BEHAVIOR (String): ret=[2]

    Trying type SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (String): ret=[0]

    Trying type SQL_KEYWORDS (String): ret=[]

    Trying type SQL_LIKE_ESCAPE_CLAUSE (String): ret=[N]

    Trying type SQL_COLUMN_ALIAS (String): ret=[Y]

    Trying type SQL_ORDER_BY_COLUMNS_IN_SELECT (String): ret=[N]

### []{#Ruby%2FDBI%20DBD%3A%3AODBC%20Driver}Ruby/DBI DBD::ODBC Driver

The second method to connect Ruby to ODBC is using the DBI interface;
this provides a higher-level interface, consisting of an controlling
module (DBI) that invokes drivers for specific databases
(DBD::\<something\> modules) as required, one of which is DBD::ODBC.

#### []{#Cross-platform%3A%20Ruby%20GEM}Cross-platform: Ruby GEM

Ruby has its own packaging system, known as rubygems, which includes the
dbi module.

    zsh, pizza C/ % sudo gem install dbi dbd-odbc  --remote
    Password:
    Successfully installed dbi-0.4.3
    Successfully installed dbd-odbc-0.2.5
    2 gems installed
    Installing ri documentation for dbi-0.4.3...
    Installing ri documentation for dbd-odbc-0.2.5...
    Installing RDoc documentation for dbi-0.4.3...
    Installing RDoc documentation for dbd-odbc-0.2.5...

If you are using gems for maintaining ruby packages, no further
installation is required after this.

#### []{#Linux%20Packages}Linux Packages

As before, some GNU/Linux distributions (Debian and Ubuntu) already have
packages for Ruby\'s DBI and DBD modules, so a simple

    sudo apt-get install libdbd-odbc-ruby1.8 

suffices, and will include the DBI module as a dependency too.

#### []{#Mac%20OS%20X%20and%20other%20Unix-like%20systems%3A%20building%20from%20source} Mac OS X and other Unix-like systems: building from source

On other platforms, if not using the gems above, you have the option to
build DBI & DBD::ODBC from source.

##### []{#DBI}DBI

Download the ruby-dbi module from
[ruby-forge](http://ruby-dbi.rubyforge.org/){.absuri} and unpack it:

    zsh, ubuntu C/ % tar xvfz dbi-0.4.3.tar.gz
    dbi-0.4.3/
    dbi-0.4.3/build/
    dbi-0.4.3/build/rake_task_lib.rb
    dbi-0.4.3/build/Rakefile.dbi.rb
    dbi-0.4.3/Rakefile
    ...
    zsh, ubuntu C/ % cd dbi-0.4.3 
    zsh, ubuntu dbi-0.4.3/ % ls
    bin/    ChangeLog  lib/     Rakefile  setup.rb
    build/  examples/  LICENSE  README    test/

Then run the following 3 commands to build and install it:

-   `ruby setup.rb config`
-   `ruby setup.rb setup`
-   `sudo ruby setup.rb install`

<!-- -->

    zsh, ubuntu dbi-0.4.3/ % ruby setup.rb config
    ---> bin
    <--- bin
    ---> lib
    ---> lib/dbi
    ---> lib/dbi/utils
    <--- lib/dbi/utils
    ---> lib/dbi/handles
    <--- lib/dbi/handles
    ---> lib/dbi/base_classes
    <--- lib/dbi/base_classes
    ---> lib/dbi/sql
    <--- lib/dbi/sql
    <--- lib/dbi
    <--- lib

    zsh, ubuntu dbi-0.4.3/ % ruby setup.rb setup 
    ---> bin
    updating shebang: test_broken_dbi
    updating shebang: dbi
    <--- bin
    ---> lib
    ---> lib/dbi
    ---> lib/dbi/utils
    <--- lib/dbi/utils
    ---> lib/dbi/handles
    <--- lib/dbi/handles
    ---> lib/dbi/base_classes
    <--- lib/dbi/base_classes
    ---> lib/dbi/sql
    <--- lib/dbi/sql
    <--- lib/dbi
    <--- lib

    zsh, ubuntu dbi-0.4.3/ % sudo ruby setup.rb install
    rm -f InstalledFiles
    ---> bin
    mkdir -p /usr/local/stow/ruby/bin
    install test_broken_dbi /usr/local/stow/ruby/bin/
    install dbi /usr/local/stow/ruby/bin/
    <--- bin
    ---> lib
    mkdir -p /usr/local/stow/ruby/lib/ruby/site_ruby/1.9.1
    install dbi.rb /usr/local/stow/ruby/lib/ruby/site_ruby/1.9.1/
    ...

##### []{#DBD::ODBC}DBD::ODBC

The installation of ruby dbd-odbc follows a similar path to the dbi
module.

Download and unpack dbd-odbc from
[ruby-forge](http://rubyforge.org/frs/?group_id=234&release_id=36729){.absuri}:

    zsh, ubuntu C/ % tar xvfz dbd-odbc-0.2.5.tar.gz 
    dbd-odbc-0.2.5/
    dbd-odbc-0.2.5/ChangeLog
    dbd-odbc-0.2.5/README
    dbd-odbc-0.2.5/lib/
    dbd-odbc-0.2.5/lib/dbd/
    dbd-odbc-0.2.5/lib/dbd/odbc/
    zsh, ubuntu dbd-odbc-0.2.5/ % ls
    build/  ChangeLog  lib/  LICENSE  Rakefile  README  setup.rb  test/

Then run the following 3 commands to build and install it:

-   `ruby setup.rb config`
-   `ruby setup.rb setup`
-   `sudo ruby setup.rb install`

<!-- -->

    zsh, ubuntu dbd-odbc-0.2.5/ % ruby setup.rb config
    ---> lib
    ---> lib/dbd
    ---> lib/dbd/odbc
    <--- lib/dbd/odbc
    <--- lib/dbd
    <--- lib

    zsh, ubuntu dbd-odbc-0.2.5/ % ruby setup.rb setup 
    ---> lib
    ---> lib/dbd
    ---> lib/dbd/odbc
    <--- lib/dbd/odbc
    <--- lib/dbd
    <--- lib

    zsh, ubuntu dbd-odbc-0.2.5/ % sudo ruby setup.rb install
    rm -f InstalledFiles
    ---> lib
    mkdir -p /usr/local/stow/ruby/lib/ruby/site_ruby/1.9.1
    ---> lib/dbd
    mkdir -p /usr/local/stow/ruby/lib/ruby/site_ruby/1.9.1/dbd
    install ODBC.rb /usr/local/stow/ruby/lib/ruby/site_ruby/1.9.1/dbd
    ---> lib/dbd/odbc
    ... 

##### []{#Testing%20Ruby%2C%20DBI%2C%20ODBC}Testing Ruby, DBI, ODBC

The attached script is a quick demonstration of some of DBI\'s
capabilities, going via the ODBC driver.

-   [odbc-test-dbd.rb](IODBCRubyHOWTO/odbc-test-dbd.rb){.c2}

<!-- -->

    zsh, ubuntu C/ % ./odbc-test-dbd.rb pgdata "" ""
    [1, "This is a varchar 10"]
    [2, "This is a varchar 40"]
    [3, "This is a varchar 90"]
    [4, "This is a varchar 160"]
    [5, "This is a varchar 250"]
    [6, "This is a varchar 360"]
    [7, "This is a varchar 490"]
    [8, "This is a varchar 640"]
    [9, "This is a varchar 810"]
    [10, "This is a varchar 1000"]

First the script connects; then it drops and recreates a table called
\`test\'; then it inserts 10 rows and selects them back, before closing
off the statement and connection handles.
:::
