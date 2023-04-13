<div id="content" class="topic-text" data-wv="http://www.openlinksw.com/Virtuoso/WikiV/" data-vi="http://www.openlinksw.com/virtuoso/xslt/" data-ie="http://www.openlinksw.com/Virtuoso/InclEng/" data-fn2="http://www.w3.org/2004/07/xpath-functions" data-xmlns="http://www.w3.org/1999/xhtml">

<div class="MACRO_TOC">

## Table of Contents

  - [Disclaimer](#Disclaimer)

  - [ODBC Overview](#ODBC%20Overview)

  - [Preface](#Preface)

  - [Installing Python](#Installing%20Python)

  - [Installing iODBC](#Installing%20iODBC)

  -   - [Compiling iODBC from
        source](#Compiling%20iODBC%20from%20source)

  - [Testing ODBC](#Testing%20ODBC)

  - [Building Egenix' mxODBC
    module](#Building%20Egenix%27%20mxODBC%20module)

  - [Sample script to use the
    module](#Sample%20script%20to%20use%20the%20module)

  - [References](#References)

</div>

## <span id="Disclaimer"></span>Disclaimer

The following is a HOWTO document for installing Python with iODBC on
Linux or Unix. Feel free to criticize, suggest modifications, or ask
further questions. It is currently maintained by Tim Haynes of Openlink
Software (iodbc@openlinksw.com)

Prerequisites include basic Unix familiarity, such as creating
directories and users, using an editor, etc.

This HOWTO is intended to assist in connecting python to back-end
databases via ODBC in a development environment and should not take the
place of thorough testing before deployment on a production system.

## <span id="ODBC%20Overview"></span> ODBC Overview

ODBC (Open Database Connectivity) is an operating system- and database-
independent communication API for database connectivity. It enables ODBC
compliant client applications to connect transparently to back-end
databases via ODBC function calls which are implemented by ODBC Drivers
for target back-end databases.

ODBC provides your applications with database-independence;
consequentially, you no longer have to incur the development and
maintenance cost of inextricably binding your application to backend
database engines via their proprietary data-access (aka native) APIs.

ODBC connections involve an ODBC-compliant Application or Data Access
Layer, ODBC Driver Manager, ODBC Driver, and back-end Database. The ODBC
Driver Manager for Microsoft Windows platforms is administered via the
ODBC Administrator Control Panel applet at setup and configuration time.
The Driver Manager registers a set of ODBC driver connection parameters
called a Data Source Name (DSN), and maintains (in persistent form) a
relationship between the DSN and an underlying ODBC Driver that will
honor data access request via that DSN.

At runtime an application looks to the driver manager for a DSN, and
then passes the connection parameters specified in the DSN to the
appropriate driver, which makes the actual database connection. Under
non-Windows platforms you may need to install a Driver Manager if this
isn't delivered as an integral part of your operating environment.
Platform independent ODBC (aka iODBC) is an Open Source ODBC project
(dual license LGPL / BSD)for non Windows platforms maintained by
OpenLink Software that consists of an ODBC SDK (libraries and header
files) and ODBC Runtime components (Administrator and Driver Manager).

## <span id="Preface"></span> Preface

You will also need an ODBC Driver and Database to complete the
architecture.

If you need ODBC drivers to connect to a third-party database on the
same or another machine, OpenLink ODBC Drivers are available, and may be
downloaded from <http://www.openlinksw.com>

The Virtuoso database may also be downloaded from
<http://virtuoso.openlinksw.com/>

Both sets of ODBC Drivers are available on a free 30 day evaluation
basis.

Support for setting up the OpenLink Drivers may be obtained at
<http://support.openlinksw.com/>

## <span id="Installing%20Python"></span> Installing Python

If you already have Python installed and running, you probably do not
need to rebuild it. Otherwise, you can compile it from source if you
wish, thus:

First, download the latest source distribution from
<http://www.python.org/> - currently this is version 2.2.3.

Unpack it into a build directory with the command

    gzip -cd < Python-2.2.3.tgz | tar xvpf -

Enter the build directory, and run configure, specifying any optional
configurations as desired:

    cd Python-2.2.3/
    zsh, purple  2:50PM Python-2.2.3/ % ./configure --help
    Usage: configure [options] [host]
    Options: [defaults in brackets after descriptions]
    Configuration:
    --cache-file=FILE       cache test results in FILE
    [snip]
    Directory and file names:
    --prefix=PREFIX         install architecture-independent files in PREFIX
    [/usr/local]
    [snip]
    --with-libs='lib1 ...'          link against additional libs
    --with-signal-module            disable/enable signal module
    --with-dec-threads              use DEC Alpha/OSF1 thread-safe libraries
    --with(out)-threads[=DIRECTORY] disable/enable thread support
    [snip]
    zsh, purple  2:50PM Python-2.2.3/ % ./configure --prefix=/usr/local/stow/python-2.2.3
    creating cache ./config.cache
    checking MACHDEP... linux2
    checking for --without-gcc... no
    checking for --with-cxx=<compiler>... no
    checking for c++... g++
    checking whether the C++ compiler (g++  ) works... yes
    checking whether the C++ compiler (g++  ) is a cross-compiler... no
    [snip]
    creating Makefile.pre
    creating Modules/Setup.config
    creating pyconfig.h
    creating Setup
    creating Setup.local
    creating Makefile
    zsh, purple  2:52PM Python-2.2.3/ % make
    gcc -c -DNDEBUG -g -O3 -Wall -Wstrict-prototypes -I. -I./Include -DHAVE_CONFIG_H  -o Modules/python.o Modules/python.c
    gcc -c -DNDEBUG -g -O3 -Wall -Wstrict-prototypes -I. -I./Include -DHAVE_CONFIG_H  -o Parser/acceler.o Parser/acceler.c
    running build_scripts
    creating build/scripts-2.2
    copying and adjusting /home/tim/public_html/docs/python-HOWTO/Python-2.2.3/Tools/scripts/pydoc -> build/scripts-2.2
    zsh, purple  2:59PM Python-2.2.3/ % su
    bash-2.05b# make install
    [snip]
    Creating directory /usr/local/stow/python-2.2.3/man
    Creating directory /usr/local/stow/python-2.2.3/man/man1
    /bin/install -c -m 644 ./Misc/python.man        /usr/local/stow/python-2.2.3/man/man1/python.1

## <span id="Installing%20iODBC"></span> Installing iODBC

If you do not already have iODBC installed, either install an RPM from
[iODBC.org](http://www.iodbc.org/), or install from source:

### <span id="Compiling%20iODBC%20from%20source"></span> Compiling iODBC from source

Requirements: C-compiler; optionally gtk+-1.2 (required if building from
CVS).

As before, unpack the iODBC sources, enter the build directory,
configure, make and make install:

    zsh, purple  4:13PM C/ % tar xvpfz libiodbc-3.51.1.tar.gz
    libiodbc-3.51.1/
    libiodbc-3.51.1/admin/
    libiodbc-3.51.1/admin/Makefile.am
    libiodbc-3.51.1/admin/Makefile.in
    libiodbc-3.51.1/admin/acinclude.m4
    [snip]
    libiodbc-3.51.1/samples/Makefile.in
    libiodbc-3.51.1/samples/iodbctest.c
    zsh, purple  4:14PM C/ % cd libiodbc-3.51.1
    zsh, purple  4:14PM libiodbc-3.51.1/ % ./configure --prefix=/usr/local/stow/iodbc-3.51.1
    checking for a BSD-compatible install... /bin/install -c
    checking whether build environment is sane... yes
    checking for gawk... gawk
    [snip]
    config.status: executing depfiles commands
    config.status: executing default commands
    zsh, purple  4:15PM libiodbc-3.51.1/ % make
    Making all in admin
    make[1]: Entering directory `/home/tim/C/libiodbc-3.51.1/admin'
    [snip]
    make[1]: Leaving directory `/home/tim/C/libiodbc-3.51.1'
    zsh, purple  4:15PM libiodbc-3.51.1/ % su root -c 'make install'

It's advisable to install into /usr/local, or stow your installation
into /usr/local, as that is searched by most other applications trying
to locate iODBC.

## <span id="Testing%20ODBC"></span> Testing ODBC

Now is a good time to configure iODBC, by adding a DSN - create a file
\~/.odbc.ini, edit it to look something like this:

    [ODBC Data Sources]
    PostgreSQL native localhost = PostgreSQL native driver
    Local Virtuoso Demo = localhost virtuoso (demo instance)
    Local Virtuoso = localhost virtuoso
    
    [Local Virtuoso Demo]
    Description = Virtuoso 3.1
    Driver      = /home/tim/virtuoso/lib/virtodbc31.so
    Address     = localhost:1112
    UserName    = dba
    User        = dba
    
    [Local Virtuoso]
    Description = Virtuoso 3.1
    Driver      = /home/tim/virtuoso/lib/virtodbc31.so
    Address     = localhost:1111
    UserName    = dba
    User        = dba
    
    [PostgreSQL native localhost]
    Driver     = /usr/lib/postgresql/lib/libodbcpsql.so
    Host       = localhost
    Server     = localhost
    ServerName = localhost
    Database   = tim
    UserName   = tim
    UID        = tim
    Port       = 5432

It is advisable to export the environment variable ODBCINI to point to
this file, too - depending on your shell, either:

    echo 'export ODBCINI=$HOME/.odbc.ini' >> .bashrc

or

    echo 'setenv ODBCINI $HOME/.odbc.ini' >> .tcshrc

as appropriate.

You can now make a test connection with the
<span class="c2">iodbctest</span> utility, thus:

    zsh, purple  4:54PM libiodbc-3.51.1/ % which iodbctest
    /usr/local/bin//iodbctest
    zsh, purple  4:54PM libiodbc-3.51.1/ % iodbctest      
    iODBC Demonstration program
    This program shows an interactive SQL processor
    Driver Manager: 03.51.0001.0908
    
    Enter ODBC connect string (? shows list): ?
    
    DSN                            | Description                   
    ---------------------------------------------------------------
    Local Virtuoso                 | localhost virtuoso 
    Local Virtuoso Demo            | localhost virtuoso (demo instance)
    MySQL                          | MySQL native driver           
    PostgreSQL native localhost    | PostgreSQL native driver      
    PostgreSQL OpenLink localhost  | PostgreSQL over OpenLink multi-tier
    Virtuoso30                     | OpenLink Virtuoso 3.0         
    
    Enter ODBC connect string (? shows list): DSN=Local Virtuoso Demo;UID=dba;PWD=cens0red
    Driver: 03.50.2505 OpenLink Virtuoso ODBC Driver
    
    SQL>

If you see the SQL\> prompt there, then all has gone well.

## <span id="Building%20Egenix%27%20mxODBC%20module"></span> Building Egenix' mxODBC module

The last infrastructure hurdle to overcome is the building of Egenix's
mxODBC module; download the sources from
<http://www.egenix.com/files/python/mxODBC.html,> and run the following:

    zsh, purple  4:21PM egenix-mx-commercial-2.0.6/ % python setup.py install

This requires root privileges, and will install in your python
site-packages directory, thus:

    zsh, purple  4:24PM tim/ % ls /usr/lib/python2.2/site-packages/mx/ODBC 
    COPYRIGHT  LazyModule.py   Misc/     ODBC.pyo     __init__.pyc  unixODBC/
    Doc/       LazyModule.pyc  ODBC.py   README       __init__.pyo
    LICENSE    LazyModule.pyo  ODBC.pyc  __init__.py  iODBC/

## <span id="Sample%20script%20to%20use%20the%20module"></span> Sample script to use the module

Finally, a small script to link it all together. You can use this to
test simple functionality of iODBC, mxODBC and Python.

    #!/usr/bin/python
    
    import mx.ODBC.iODBC
    
    dsn="Local Virtuoso Demo"
    
    conn=mx.ODBC.iODBC.Connect (dsn, "dba", "cens0red")
    
    print "Content-Type: text/plain
    
    "
    print "Database Type: " + conn.getinfo (17)[1] + "
    "
    
    curshandle=conn.cursor()
    
    print "Top 10 in Shippers table:"
    curshandle.execute ("select top 10 * from Demo.demo.Shippers")
    for i in curshandle.fetchall():
    print i
    
    #print curshandle.fetchall()
    
    print "
    Creating and populating timtest table:"
    
    try:
    curshandle.execute ("drop table timtest") 
    except: 
    pass
    
    curshandle.execute ("create table timtest (id integer, str varchar (255))")
    curshandle.execute ("insert into timtest values (99, 'testing')")
    curshandle.execute ("select * from timtest")
    
    for i in curshandle.fetchall():
    print i

On running it, you should see the following output:

    zsh, purple 11:22AM python/ % ./dbi-test.py
    Database Type: OpenLink Virtuoso
    
    Top 10 in Shippers table:
    (1, 'Speedy Express', '(503) 555-9831')
    (2, 'United Package', '(503) 555-3199')
    (3, 'Federal Shipping', '(503) 555-9931')
    
    Creating and populating timtest table:
    (99, 'testing')

## <span id="References"></span> References

  - [iODBC](http://www.iodbc.org)
  - History of [ODBC on
    Unix](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCOnUnix)
  - [OpenLink Software](http://www.openlinksw.com/) -
    [Support](http://www.openlinksw.com/support/suppindx.htm) ,
    [links](http://www.openlinksw.com/support/teclinks.htm) and
    [white-papers](http://www.openlinksw.com/info/docs/odbcwhp/tableof.htm)

</div>
