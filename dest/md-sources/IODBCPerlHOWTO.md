::: {#content .topic-text wv="http://www.openlinksw.com/Virtuoso/WikiV/" vi="http://www.openlinksw.com/virtuoso/xslt/" ie="http://www.openlinksw.com/Virtuoso/InclEng/" fn2="http://www.w3.org/2004/07/xpath-functions" xmlns="http://www.w3.org/1999/xhtml"}
Tim Haynes, OpenLink Software, Tue Mar 23 17:51:50 2004

::: {.MACRO_TOC}
Table of Contents {#table-of-contents .toc}
-----------------

-   [Introduction](#Introduction)
-   [ODBC client download and
    installation](#ODBC%20client%20download%20and%20installation)
-   [iODBC Driver Manager Source and
    SDK](#iODBC%20Driver%20Manager%20Source%20and%20SDK)
-   [Creating and Testing an ODBC
    DSN](#Creating%20and%20Testing%20an%20ODBC%20DSN)
-   -   [Manual mode](#Manual%20mode)
    -   -   [Create your DSN](#Create%20your%20DSN)
        -   [Run \"iodbctest\"](#Run%20%22iodbctest%22)

    -   [Graphical mode](#Graphical%20mode)

-   [](#)
-   [](#)
-   [Compiling the Perl Modules for ODBC
    support](#Compiling%20the%20Perl%20Modules%20for%20ODBC%20support)
-   -   [DBI](#DBI)
    -   [DBD::ODBC](#DBD%3A%3AODBC)
    -   -   [](#)
        -   [Testing DBD::ODBC](#Testing%20DBD%3A%3AODBC)
        -   [Installation](#Installation)

-   [Footnotes](#Footnotes)
-   [Glossary](#Glossary)
:::

[]{#Introduction}Introduction
-----------------------------

The following is a HOWTO document for installing Perl modules with the
OpenLink iODBC SDK or iODBC Driver Manager as an Apache module on
Linux/Unix systems. Feel free to criticize, suggest modifications, or
ask further questions. It is currently being maintained by
<iodbc@openlinksw.com>.

Prerequisite: Basic Unix, Linux or MacOS X familiarity (creating
directories and users, using an editor, etc). Knowledge of how Perl
modules work is useful.

[]{#ODBC%20client%20download%20and%20installation}ODBC client download and installation
---------------------------------------------------------------------------------------

This installation will provide the iODBC Driver Manager, header files,
and example program without source code. Additional ODBC driver download
is necessary.

For the latest version, visit the following OpenLink Software download
pages and choose your download based on your client operating system:

-   SDK download page
-   Multi-Tier ODBC Client download page (choose only Client option to
    download); see footnote 1.
-   or Single-Tier driver download page

The SDK includes the header files required for compilation. The second
download is only required if you have not already installed a third
party driver to connect to your database. (See also footnote 2.)

b\. Create a new Openlink directory, such as /usr/openlink

c\. Copy the \"install.sh\" file and the ODBC SDK .taz archive(s) into
[*usr* openlink]{.c1}

d\. Navigate to that directory, and run:

    sh install.sh

This will extract the software, creating lib/ (for the driver) and
include/ (for the compilation) directories under /usr/openlink/odbcsdk

e\. (Optional) Copy your Single-Tier or Multi-Tier ODBC Client .taz file
and the install.sh into the /usr/openlink/odbcsdk directory, navigate to
that directory, and subsequently run:

    sh install.sh

f\. (Optional) For the Multi-Tier server side download, visit the
OpenLink Software Multi-Tier download page and choose your download
based on your server operating system.

g\. Unzip the archive and perform an installation (see
<http://docs.openlinksw.com/mt/> for more).

h\. Make sure the OpenLink Request Broker (oplrqb) is started.

[]{#iODBC%20Driver%20Manager%20Source%20and%20SDK} iODBC Driver Manager Source and SDK
--------------------------------------------------------------------------------------

The iODBC Driver Manager is recommended for programmers or those with
experience with non-OpenLink drivers. Following these steps will perform
a generic installation of the driver manager onto your system. The files
are installed under /usr/local, unless you specify otherwise with a
different \--prefix directive at configure-time. It is also recommended
that you refer to the README and INSTALL files prior to proceeding.

a\. From http:/www.iodbc.org/, download the appropriate component (for
the Driver Manager)

b\. Extract the archive using the following command:

    gzip -dc < file.taz| tar -xvf -

where file.taz is the file you downloaded.

c\. Move to the source directory which was just created from the
extraction

d\. Execute the following commands:

    ./configure
    make
    make check
    make install

[]{#Creating%20and%20Testing%20an%20ODBC%20DSN} Creating and Testing an ODBC DSN
--------------------------------------------------------------------------------

You need to create an ODBC DSN (data source). This will exist in your
client-side odbc.ini file, and can be done in one of two ways:

### []{#Manual%20mode}Manual mode

You can also review the instructions at the \"OpenLink iODBC SDK for
Unix\" link from the Client Components Installation section of the
Multi-Tier Release 4.0 documentation. A sample odbc.ini file can be
found in the doc subdirectory from your OpenLink iODBC SDK installation.
To begin: a. Set and export the ODBCINI environment variable (this
assumes you have not moved that file to another directory):

    export ODBCINI=/usr/openlink/odbcsdk/doc/odbc.ini

or

    setenv ODBCINIT /usr/openlink/odbcsdk/doc/odbc.ini

depending on your shell.

#### []{#Create%20your%20DSN}Create your DSN

For example, to connect to an MS Access database on Windows, you can
create a \[dsn\_access\] section, change the Host, ServerType, Database,
Username and Password entries to match your server settings. Here is
part of the odbc.ini file:

    [dsn_access]
    Driver = /usr/openlink/odbcsdk/lib/oplodbc.so.1
    Host =
    ServerType = Odbc
    Database =
    UserName = sa
    Password =
    ;FetchBufferSize = 30

where Host is the machine hosting your MS Access database, and Database
the is the name of the MS Access driver DSN you set up in the Windows
ODBC control panel.

#### []{#Run%20%22iodbctest%22} Run \"iodbctest\"

    cd /usr/openlink/odbcsdk/examples
    ./iodbctest

d\. At the prompt, type a valid connect string, such as
\`DSN=dsn\_access\' (from above example)

e\. Once you get a prompt, you are connected and can execute any valid
SQL against your database, or \`[tables]{.c1}\' to obtain a list of
tables in that database.

### []{#Graphical%20mode}Graphical mode

You can configure data sources by using the Admin Assistant HTML wizards
(accessible once the Request Broker is started on the client). (See
footnote 3.)

1\. Ensure that your openlink.sh file has been sourced in the current
shell.

2\. Start the Request Broker:

    cd /usr/openlink/bin
    ./oplrqb

c\. Navigate to <http://localhost:8000/> on the client machine.

d\. In \"Client Components Administration\", proceed to configure an ODBC
Data Source and test.

 FreeBSD-specific Concerns
-------------------------

On FreeBSD, it has been found to help if perl is compiled with
threading; to do this, you need to build it from the lang/perl58/ port,
and define WITH\_THREADS (e.g. in /etc/make.conf).

 MacOS X-specific Concerns
-------------------------

On MacOS X, you have the option to compile libraries either as
traditional unix-like shared libraries, or as a \`framework\'. On OS X,
the latter is generally preferred - for example, iODBC is built as a
framework, most of the Perl modules are, etc.

The instructions below for DBI apply regardless; however, for DBD::ODBC
you have a choice of one or other method.

[]{#Compiling%20the%20Perl%20Modules%20for%20ODBC%20support} Compiling the Perl Modules for ODBC support
--------------------------------------------------------------------------------------------------------

Perl\'s DBI is a generic database interface module for Perl; DBD is a
range of specific database interfaces, DBD::Pg, DBD::Sybase,
DBD::Oracle, DBD::ODBC, etc, loaded by DBI.

### []{#DBI} DBI

Download the DBI module from CPAN - this is frequently provided as a
package with your operating system; alternatively, you can download it
from CPAN (http:/search.cpan.org) under the \"Database Interfaces\"
category.

Assuming you have a working Perl installation already installed on your
system, we recommend the following method - using Perl\'s CPAN module -
to automate the whole process:

    bash# perl -MCPAN -e shell
    cpan>
    CPAN: Storable loaded ok
    Going to read /root/.cpan/Metadata
    Database was generated on Wed, 02 Oct 2002 18:22:45 GMT
    CPAN: LWP::UserAgent loaded ok
    Fetching with LWP:
    [snip]
    cpan> install DBI
    DBI is up to date.

More documentation on this method is to be found at
http:/www.perldoc.com/perl5.6/pod/perlmodinstall.html .

### []{#DBD::ODBC} DBD::ODBC

Download the DBD::ODBC module from CPAN. You can either download it by
hand from http:/www.perl.com/CPAN-local/modules/index.html, or use the
following to obtain it - note that we only recommend getting it this way
rather than attempting a full install, as some intervention is necessary
to configure and compile it:

    bash# perl -MCPAN -e shell
    cpan>
    CPAN: Storable loaded ok
    Going to read /root/.cpan/Metadata
    Database was generated on Wed, 02 Oct 2002 18:22:45 GMT |
    [snip]
    cpan> get DBD::ODBC
    Running get for module DBD::ODBC
    CPAN: Digest::MD5 loaded ok
    Checksum for
    /root/.cpan/sources/authors/id/J/JU/JURL/DBD-ODBC-0.45.tar.gz  ok
    Scanning cache /root/.cpan/build for sizes
    DBD-ODBC-0.45/
    DBD-ODBC-0.45/Changes
    DBD-ODBC-0.45/dbdimp.c
    DBD-ODBC-0.45/dbdimp.h
    DBD-ODBC-0.45/fixup_c.h
    DBD-ODBC-0.45/fixup_t.h
    DBD-ODBC-0.45/Makefile.PL
    DBD-ODBC-0.45/MANIFEST
    (and so on.)

Now enter the build directory (cd /root/.cpan/build/ DBD-ODBC-0.45
above), and run:

    bash# env ODBCHOME=/opt/openlink/odbcsdk perl Makefile.PL
    Configuring DBD::ODBC ...

    >>>Remember to actually *READ* the README file!
    And re-read it if you have any problems.

    Using DBI 1.30 installed in /usr/lib/perl5/auto/DBI
    Using ODBC in /opt/openlink/odbcsdk

    Umm, this looks like a iodbc type of driver manager.

    We expect to find the isql.h, isqlext.h and iodbc.h files (which were
    supplied with iODBC) in $ODBCHOME/include directory alongside the
    /opt/openlink/odbcsdk/lib/libiodbc.a /opt/openlink/odbcsdk/lib/libiodbc.so
    library.

    Using DBI 1.30 installed in /usr/lib/perl5/auto/DBI
    Writing Makefile for DBD::ODBC

This tells this particular compilation of DBD::ODBC to use the iODBC
installation in the openlink odbcsdk distribution. To perform the actual
build, simply type \`make\'.

Note: There is a bug in some versions of DBD::ODBC\'s Makefile.PL
whereby the generated Makefile is invalid - typically you get an error
such as

    Makefile:313: *** missing separator.  Stop.

You can simply comment-out the offending line, thus:

    config :: $(changes_pm)
    #    @$(NOOP)

Alternatively, replacing the leading spaces with a TAB character will
also fix it.

####  MacOSX-specific note

Instead of typing \`make\' above, if you wish to build this module as a
framework instead of a shared library, you will have to edit the
generated Makefile; you still use the same \`perl Makefile.PL -o
/path/to/iodbc\' command to generate the Makefile (it will fail if it
can\'t find the lib/ directory, and fail to compile if it can\'t find
the headers to include), but the references to \`-liodbc\' should become
\`-framework iODBC\' throughout, and the \`-L\'(path to iodbc/lib)
should be removed, thus:

    VERSION_FROM = ODBC.pm
    INC = -I. -I/Library/Perl/darwin/auto/DBI
    DEFINE = -I/Users/openlink/tim/iodbc-shared/include
    OBJECT = $(O_FILES)

    # DBD::ODBC might depend on some other libraries:
    # See ExtUtils::Liblist for details
    #
    EXTRALIBS = -framework iODBC
    LDLOADLIBS = -framework iODBC
    BSLOADLIBS =
    LD_RUN_PATH = # /Users/openlink/tim/iodbc-shared/lib

#### []{#Testing%20DBD%3A%3AODBC}Testing DBD::ODBC

You should also run through the tests - assign values to these
variables:

    The DBD::ODBC tests will use these values for the database connection:
    DBI_DSN=e.g. dbi:ODBC:demo
    DBI_USER=
    DBI_PASS=

and execute \`make test\'. Optionally, for maximum verbosity, use

    make test TEST_VERBOSE=1

instead.

#### []{#Installation}Installation

Finally, become root if you were not already, using su or sudo or
equivalent, and type

    make install

to install DBD::ODBC into your perl tree. A short sample perl script
using DBD::ODBC might be the following:

    bash# cat > dbitest.pl
    #!/usr/bin/perl

    use DBI;
    use DBD::ODBC;

    $|=1;

    map {
    print "Data sources for $_: " . join("
    ", DBI->data_sources($_)). "
    "
    }
    grep(!/ADO|template/, DBI->available_drivers);

which, when you run it, lists all data-sources for all the installed
DBD:: drivers, now including ODBC:

    bash# perl ./dbitest.pl
    Data sources for CSV:
    DBI:CSV:f_dir=mytest
    DBI:CSV:f_dir=t
    DBI:CSV:f_dir=blib
    Data sources for ODBC:
    DBI:ODBC:DB2v7.x(linux)
    DBI:ODBC:DB2v7.x(aix32bit)
    DBI:ODBC:DB2v7.x(solaris)

[]{#Footnotes} Footnotes
------------------------

1.  OpenLink Multi-tier drivers involve installation on both the client-
    and server-sides.\
    \
2.  A known bug was discovered when using certain versions of the
    OpenLink iODBC SDK coupled with Perl DBD, whereby a disconnect in
    the Perl script would cause a core dump. The bug did not prove to
    affect script functionality; it was driver-specific. The problem has
    been addressed in the latest ODBC SDK available at OpenLink
    Software\'s web site (see the iODBC SDK option). For this reason,
    unless you are using non-OpenLink drivers to connect in your
    scripts, it is recommended that you install the OpenLink iODBC SDK
    option for your ODBC home.\
    \
3.  If you configure a DSN using the Admin Assistant, you\'ll have to
    copy the modified odbc.ini file into either the home directory (or
    \" \~/.\") of the Perl account, or export ODBCINI to point at it,
    for it to be recognized at run-time.\
    \

[]{#Glossary} Glossary
----------------------

-   **Admin Assistant** - the Admin Assistant is an HTML-based interface
    which simplifies the process of configuring text-based configuration
    files used in the OpenLink Multi-Tier data architecture. It is made
    available via the OpenLink Request Broker, which is available for
    download for your Unix/ Linux client from the OpenLink Multi-Tier
    download page. Since the Request Broker is a server component, you
    obtain it by specifying your server platform as your Unix/ Linux
    client. Once downloaded, you can install the archive into your ODBC
    home directory. It will be installed as the file \"oplrqb\" in a bin
    subdirectory. More information can be found at the link \"ODBC
    Client Components for Unix\" (Wizards-Based Data Source Management)
    in the OpenLink Multi-Tier Release 4.0 documentation.

<!-- -->

-   **Database Agent** - an OpenLink Database Agent is an executable
    process which initiates a connection to the specified database (in
    the ServerType odbc.ini parameter). For ServerTypes of \"Odbc\", it
    acts as a generic agent, acting as a proxy to the actual database
    driver which will complete the connection on the server.

<!-- -->

-   **ODBC home directory** - this is the directory to which you have
    installed either the iODBC driver manager or the OpenLink iODBC SDK.
    It will contain directories like include and lib directly under it.

<!-- -->

-   **Request Broker** - the OpenLink Request Broker is a server daemon
    which listens on a specified TCP port (default of 5000) and
    broadcasts on a UDP port. It acts exactly as its name suggests,
    \"brokering\" out incoming connection requests to the appropriate
    Database Agent process. The Request Broker implicitly starts another
    server daemon called \"www\_sv\" which acts as a stand-alone web
    server providing easy configuration for initialization files.
:::
