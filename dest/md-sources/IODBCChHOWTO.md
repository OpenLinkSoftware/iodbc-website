::: {#content .topic-text wv="http://www.openlinksw.com/Virtuoso/WikiV/" vi="http://www.openlinksw.com/virtuoso/xslt/" ie="http://www.openlinksw.com/Virtuoso/InclEng/" fn2="http://www.w3.org/2004/07/xpath-functions" xmlns="http://www.w3.org/1999/xhtml"}
[]{#Disclaimer} Disclaimer
--------------------------

The following is a HOWTO document for installing Ch with iODBC on Linux
or Unix. Feel free to criticize, suggest modifications, or ask further
questions. It is currently maintained by Tim Haynes of Openlink Software
(iodbc\@openlinksw.com)

Prerequisites include basic Unix familiarity, such as creating
directories and users, using an editor, etc.

This HOWTO is intended to assist in connecting Ch to back-end databases
via ODBC in a development environment and should not take the place of
thorough testing before deployment on a production system.

[]{#ODBC%20Overview} ODBC Overview
----------------------------------

ODBC (Open Database Connectivity) is an operating system- and database-
independent communication API for database connectivity. It enables ODBC
compliant client applications to connect transparently to back-end
databases via ODBC function calls which are implemented by ODBC Drivers
for target back-end databases.

ODBC provides your applications with database independence;
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
isn\'t delivered as an integral part of your operating environment.
Platform independent ODBC (aka iODBC) is an Open Source ODBC project
(dual license LGPL / BSD)for non Windows platforms maintained by
OpenLink Software that consists of an ODBC SDK (libraries and header
files) and ODBC Runtime components (Administrator and Driver Manager).

[]{#HOWTO%20Preface%3A} HOWTO Preface:
--------------------------------------

You will also need an ODBC Driver and Database to complete the
architecture.

If you need ODBC drivers to connect to a third-party database on the
same or another machine, OpenLink ODBC Drivers are available, and may be
downloaded from <http://www.openlinksw.com>

The Virtuoso database may also be downloaded from
<http://virtuoso.openlinksw.com/>

Both sets of ODBC Drivers are available on a free 30-day evaluation
basis.

Support for setting up the OpenLink Drivers may be obtained at
<http://support.openlinksw.com/>

[]{#Installing%20Ch} Installing Ch
----------------------------------

If you already have Ch installed and running, you probably do not need
to rebuild it. Otherwise, you should install it, thus:

First, download the latest distribution appropriate to your OS from
<http://www.softintegration.com/> - currently this is version 4.0.

Unpack it with a command like

    gzip -cd < chstandard-4.0.0.linux2.2.5.intel.tar.gz | tar xvpf -

Enter the resultant directory, and run the install script:

    zsh, purple  1:05PM chstandard-4.0.0.linux2.2.5.intel/ % ls
    README  ch.bin  install.sh*  license.txt
    zsh, purple  1:05PM chstandard-4.0.0.linux2.2.5.intel/ % ./install.sh

You will also probably need to set the CHHOME environment variable to
the base directory you chose as Ch\'s installation destination -
depending on your current shell, choose one or other of the following:

    echo 'setenv CHHOME $HOME/ch4' >> .tcshrc

or

    echo 'export CHHOME=$HOME/ch4' >> .bashrc

These are not necessary if Ch is installed as root into a default
system-wide location.

After installation, if you run the command

    ch -d

It will create a \~/.chrc file for you with useful default settings.

### []{#Installing%20Ch%20on} Installing Ch on MacOS X

First, download the compressed Ch from
<http://www.softintegration.com/download>

Your Mac OS X shuttle will uncompress the file and create a directory
such as chsandard-4.0.0.macosx in your Desktop. If not, you can
decompress and untar the downloaded file with the command:

    gzip -cd chstandard-4.0.0.macosx.tgz |tar xvf -

Goto the chstandard-4.0.0.macosx folder on the Mac OS X Desktop,
double-click chstandard-4.0.0.pkg, then follow the instructions to
install.

[]{#Installing%20iODBC} Installing iODBC
----------------------------------------

If you do not already have iODBC installed, either install an RPM from
<http://www.iodbc.org/,> or install from source:

### []{#Compiling%20iODBC%20from%20source} Compiling iODBC from source

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

It\'s advisable to install into /usr/local, or stow your installation
into /usr/local, as that is searched by most other applications trying
to locate iODBC.

### []{#Testing%20iODBC} Testing iODBC

Now is a good time to configure iODBC, by adding a DSN - create a file
\~/.odbc.ini, edit it to look something like this:

    [ODBC Data Sources]
    PostgreSQL native localhost = PostgreSQL native driver
    Local Virtuoso Demo = localhost virtuoso (demo instance)
    Local Virtuoso = localhost virtuoso

    [Local Virtuoso Demo]
    Description = Virtuoso 3.2
    Driver      = /home/tim/virtuoso/lib/virtodbc32.so
    Address     = localhost:1112
    UserName    = dba
    User        = dba

    [Local Virtuoso]
    Description = Virtuoso 3.2
    Driver      = /home/tim/virtuoso/lib/virtodbc32.so
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

You can now make a test connection with the [iodbctest]{.c1} utility,
thus:

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

[]{#Interfacing%20with%20Ch} Interfacing with Ch
------------------------------------------------

SoftIntegration.com provide a module for Ch to interface with iODBC -
you should download the chiodbc module from
<http://www.softintegration.com/.>

Installing this is simple; unpack the tarball into \$CHHOME/package/
directory, thus:

    zsh, purple  1:49PM chstandard-4.0.0.linux2.2.5.intel/ % cd ~/ch4/package 
    zsh, purple  1:49PM package/ % gzip -cd < ~/Downloads/chiodbc-3.5.0.linux2.2.5.intel.tar.gz| tar xvpf -

Now you need to set two variables in Ch\'s startup script to tell it
where to find the system-wide installation of iODBC - edit
\$CHHOME/config/chrc or \~/.chrc and insert the following two lines:

    _ppath = stradd(_ppath, "/home/tim/ch4/package/iodbc;");
    _ipath = stradd(_ipath, "/home/tim/ch4/package/iodbc/include;");

You can also export the ODBCINI environment variable from within Ch,
thus:

    echo 'putenv("ODBCINI=$HOME/.odbc.ini");' >> .chrc

[]{#Sample%20script%20combining%20Ch%20and%20iODBC} Sample script combining Ch and iODBC
----------------------------------------------------------------------------------------

Having configured a DSN above, you should be able to use both the
simple.c and odbctest.c scripts, thus:

    zsh, purple  2:05PM demos/ % ch
    Ch 
    Standard edition, version 4.0.0.11291 
    (C) Copyright 2001-2003 SoftIntegration, Inc.
    http://www.softintegration.com
    /home/tim/ch4/package/iodbc/demos> cd $CHHOME/package/iodbc/demos
    /home/tim/ch4/package/iodbc/demos> ls
    odbctest.c  simple.c
    /home/tim/ch4/package/iodbc/demos> ./simple.c
    SQLAllocHandle() OK
    SQLSetEnvAttr() ok
    SQLAllocHandle() ok
    SQLSetConnectAttr() ok

    /home/tim/ch4/package/iodbc/demos> ./odbctest.c
    OpenLink ODBC Demonstration program
    This program shows an interactive SQL processor

    Enter ODBC connect string (? shows list): DSN=Local Virtuoso Demo;UID=dba;PWD=cens0red
    Driver: 03.50.2604 OpenLink Virtuoso ODBC Driver (virtodbc.so)

    SQL>select * from Demo.demo.Shippers

    ShipperID  |CompanyName                             |Phone                   
    -----------+----------------------------------------+------------------------
    1          |Speedy Express                          |(503) 555-9831          
    2          |United Package                          |(503) 555-3199          
    3          |Federal Shipping                        |(503) 555-9931          

    result set 1 returned 3 rows.

[]{#Additional%20Resources} Additional Resources
------------------------------------------------

-   [iodbc.org](http://www.iodbc.org){.absuri} , the home of iODBC
-   [SoftIntegration.com](http://www.softintegration.com/){.absuri} ,
    authors of Ch
-   [Ch iODBC
    home](http://www.softintegration.com/products/toolkit/odbc/){.absuri}
-   History of [ODBC on Unix](index.php?page=docs/odbcstory){.c2}
-   [OpenLink Software](http://www.openlinksw.com/){.absuri} -
    [Support](http://www.openlinksw.com/support/suppindx.htm){.absuri} ,
    [links](http://www.openlinksw.com/support/teclinks.htm){.absuri} and
    [white-papers](http://www.openlinksw.com/info/docs/odbcwhp/tableof.htm){.absuri}
:::
