<div id="content" class="topic-text" data-wv="http://www.openlinksw.com/Virtuoso/WikiV/" data-vi="http://www.openlinksw.com/virtuoso/xslt/" data-ie="http://www.openlinksw.com/Virtuoso/InclEng/" data-fn2="http://www.w3.org/2004/07/xpath-functions" data-xmlns="http://www.w3.org/1999/xhtml">

<div class="MACRO_TOC">

## Table of Contents

  - [About iODBC.org](#About%20iODBC.org)

  -   - [What does iODBC stand
        for?](#What%20does%20iODBC%20stand%20for%3F)
      - [Under what license is iODBC
        available?](#Under%20what%20license%20is%20iODBC%20available%3F)
      - [How do I get support for
        iODBC](#How%20do%20I%20get%20support%20for%20iODBC)
      - [What is the relationship
        between](#What%20is%20the%20relationship%20between)
      - [What happened to the Forum Archive
        (wwwboard)?](#What%20happened%20to%20the%20Forum%20Archive%20%28wwwboard%29%3F)

  - [Technical](#Technical)

  -   - [What's an odbc.ini and what do I put in
        it?](#What%27s%20an%20odbc.ini%20and%20what%20do%20I%20put%20in%20it%3F)
      - [Just get me connected\!](#Just%20get%20me%20connected%21)
      - [I've got this linux box with PHP and
        Apache...](#I%27ve%20got%20this%20linux%20box%20with%20PHP%20and%20Apache...)
      - [What's a libiodbc and what goes in my Driver= lines in
        odbc.ini?](#What%27s%20a%20libiodbc%20and%20what%20goes%20in%20my%20Driver%3D%20lines%20in%20odbc.ini%3F)

  - [Common Error Messages](#Common%20Error%20Messages)

  -   - [\[iODBC\]\[Driver Manager\]Data source name not found and no
        default driver specified. Driver could not be loaded,
        SQLSTATE=IM002](#%5BiODBC%5D%5BDriver%20Manager%5DData%20source%20name%20not%20found%20and%20no%20default%20driver%20specified.%20Driver%20could%20not%20be%20loaded%2C%20SQLSTATE%3DIM002)
      - [\[iODBC\] \[Driver Manager\]Specified driver could not be
        loaded](#%5BiODBC%5D%20%5BDriver%20Manager%5DSpecified%20driver%20could%20not%20be%20loaded)

  - [Driver-Specific Errors](#Driver-Specific%20Errors)

  -   - [MyODBC: \[TCX\]\[MyODBC\]No DSN entered (0)
        SQLSTATE=S1000](#MyODBC%3A%20%5BTCX%5D%5BMyODBC%5DNo%20DSN%20entered%20%280%29%20SQLSTATE%3DS1000)

  - [Segfault with Perl
    DBD::ODBC](#Segfault%20with%20Perl%20DBD%3A%3AODBC)

  - [Tracing Application Behavior](#Tracing%20Application%20Behavior)

  -   - [Tracing Application
        Behavior](#Tracing%20Application%20Behavior)

</div>

This document is a list of Frequently Asked Questions concerning the
iODBC project. It is currently maintained by `iodbc@openlinksw.com`;
please feel free to send nominations for FAQ-worthy topics to this
address.

## <span id="About%20iODBC.org"></span> About iODBC.org

### <span id="What%20does%20iODBC%20stand%20for%3F"></span> What does iODBC stand for?

iODBC is an acronym for "Independent Open Database Connectivity". See
[About
iODBC](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/About) for
more.

### <span id="Under%20what%20license%20is%20iODBC%20available%3F"></span> Under what license is iODBC available?

iODBC is dual-licensed under both the
[BSD](http://www.opensource.org/licenses/bsd-license.php) and
[LGPL](http://www.opensource.org/licenses/lgpl-license.php) licenses.

Please see the [License
Page](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/License) for
more details.

### <span id="How%20do%20I%20get%20support%20for%20iODBC"></span>How do I get support for iODBC

Support for iODBC is available through [several mailing-lists hosted by
SourceForge.net](https://sourceforge.net/p/iodbc/mailman/), where the
wider community (and OpenLink employees) contribute to the best of their
ability. The previous forum has been archived but may contain useful
reference material. Commercial support may also be contracted from
OpenLink Software.

### <span id="What%20is%20the%20relationship%20between"></span>What is the relationship between OpenLink Software and iODBC?

[OpenLink Software](http://www.openlinksw.com/) is a software company
specializing in data access, management, and integration technologies
including ODBC, JDBC, ADO.NET, OLE DB, XMLA, SQL, SPARQL, and others.
Products include [UDA, a suite of data access
drivers/providers/connectors](http://uda.openlinksw.com/) and [Virtuoso
Universal Server](http://virtuoso.openlinksw.com/) a multi-model RDBMS.

iODBC is an open-source project (released under the LGPL or BSD
licenses) hosted by OpenLink Software for the benefit of the wider
community, to implement and improve a free and Open ODBC Driver Manager
component for Linux, macOS, Unix-like, VMS, and other platforms.

iODBC copyright is co-owned by Ke Jin and OpenLink Software. OpenLink
are the sole project custodian and sponsor.

**Advertising:** OpenLink may benefit from the publicity of hosting
iODBC.org, with its links to various vendors of ODBC drivers for
assorted platforms and RDBMS, but we don't set out to abuse the
open-source project for commercial gain. There are plenty of free and
open-source database drivers for free databases (MySQL, PostgreSQL,
Firebird, and others). The OpenLink philosophy is to facilitate OS- and
database-independent connectivity through ODBC, to which end having an
open-source driver-manager component is advantageous.

**Resources:** Various OpenLink employees work on actively developing
and maintaining the authoritative CVS sources of the iODBC project,
administering the server on which the site runs, maintaining the
www.iodbc.org website, responding to posts on the public forums, etc.

**Executive summary:** Think *nice `.com` hosts free `.org`* and you'll
not be far from the truth.

### <span id="What%20happened%20to%20the%20Forum%20Archive%20%28wwwboard%29%3F"></span> What happened to the Forum Archive (wwwboard)?

After a long innings, wwwboard proved too susceptible to spam and other
undesirable phenomena, and the underlying wwwboard implementation was
unpleasant to maintain, becoming corrupt with increasing frequency. As
such, it has been replaced with the mailing-lists, hosted by
SourceForge.

In the process, the old wwwboard has been left in stasis; a small
cleanup operation was mounted to remove off-topic and dubious /
offensive / illegal material and links, but not extending as far as
censorship: if someone said iODBC or OpenLink suck, you'll see it
represented as-stated there.

Since then, the wwwboard service has succumbed to bitrot. Old postings
may be reviewed via
[archive.org](https://web.archive.org/web/20010302094845/http://195.153.164.12:80/wwwboard/wwwboard.html).

## <span id="Technical"></span>Technical

### <span id="What%27s%20an%20odbc.ini%20and%20what%20do%20I%20put%20in%20it%3F"></span> What's an odbc.ini and what do I put in it?

An `odbc.ini` is the main configuration file in which all your DSNs and
much of the ODBC configuration parameters are stored. iODBC has a
search-path for finding such a configuration file: first, the
environment variable `ODBCINI` is inspected to see if it points at a
suitable file, or `~/.odbc.ini` (analagous to User DSNs on Windows) then
`/etc/odbc.ini` ("system-wide") are fall-back locations.

The `odbc.ini` file comprises 3 parts: a set of ODBC options, a list of
DSNs, and then the datasource definitions themselves, thus:

    [ODBC Data Sources]
    PostgreSQL native localhost = PostgreSQL native driver
    PostgreSQL OpenLink localhost = PostgreSQL over OpenLink multi-tier
    
    [PostgreSQL native localhost]
    Driver     = /usr/lib/postgresql/lib/libodbcpsql.so
    Host       = localhost
    Server     = localhost
    ServerName = localhost
    Database   = tim
    UserName   = tim
    UID        = tim
    Port       = 5432
    
    [PostgreSQL OpenLink localhost]
    Description     = PostgreSQL, over openlink MT
    Driver          = /opt/openlink/lib/oplodbc.so
    ServerType      = PostgreSQL95
    Host            = localhost
    Database        = tim
    Username        = tim
    LastUser        = tim
    User            = tim
    FetchBufferSize = 99
    
    [ODBC]
    ;Trace = 1
    ;TraceFile = /tmp/odbctrace.log
    ;Debug = 1
    ;DebugFile = /tmp/odbcdebug.log

The list of ODBC Data Sources correlate with the file `odbcinst.ini` (or
environment variable `ODBCINSTINI`): for every value used as a
description of the driver, there should be a corresponding section in
`odbcinst.ini` listing both the `Driver` and `Setup` library (to assist
with graphical configuration using `iodbcadm-gtk`, and also used to
display an input box in the event of insufficient options being
presented at connection-time).

The list of attributes is driver-dependent, as the above shows: the
native `postgresql` driver calls them different things from OpenLink UDA
Enterprise Edition, so you have to check your driver's documentation.

With iODBC, assuming you downloaded/installed/compiled it, you have a
GTK-based GUI for configuring your ODBC DSNs, too: run `iodbcadm-gtk`.

### <span id="Just%20get%20me%20connected%21"></span>Just get me connected\!

This is the succinct overview:

Grab the source. Unpack it. Run

    ./configure && nice make && sudo make install

Install an ODBC driver for your backend database. Configure `odbc.ini`
to use this driver. Export the environment variable
<span class="c1">ODBCINI</span> to point to that `odbc.ini`. Run
<span class="c1">iodbctest</span> and attempt to connect. Voila.

### <span id="I%27ve%20got%20this%20linux%20box%20with%20PHP%20and%20Apache..."></span> I've got this linux box with PHP and Apache...

...and you want to connect to SQL Server or MS Access from it. The
overview of the architecture is as follows: `apache` invokes `php` to
handle scripts, `php` is linked against `libiodbc` in order to handle
the `odbc_*` functions in your script, `libiodbc` loads either a native
SQL Server driver for linux or some generic ODBC-proxy for MS Access,
and you're done.

OpenLink produce an *odbc agent* that facilitates the latter sort of
connection.

The [iODBC+PHP+Apache
HOWTO](http://www.iodbc.org/dataspace/doc/iodbc/wiki/iodbcWiki/IODBCPHPHOWTO)
document on this site will guide you through a working set of configure
options for `libiodbc`, `apache`, and `php` in order.

### <span id="What%27s%20a%20libiodbc%20and%20what%20goes%20in%20my%20Driver%3D%20lines%20in%20odbc.ini%3F"></span> What's a libiodbc and what goes in my Driver= lines in odbc.ini?

The ODBC architecture separates the application, the driver-manager and
the driver components, each one calling the next in a chain.

The `libiodbc.so` library only implements a driver manager; you need a
separate driver for each kind of backend database to which you connect,
but your application will at least see one consistent interface across
all of them. If you attempt to use `Driver=libiodbc.so` in the
`odbc.ini`, it will fail.

The `Driver=` parameter should be a full name to a shared-library
implementing the driver for the backend database to which you're
connecting:

    [pglocal]
    Driver     = /usr/local/lib/psqlodbc.so
    Port       = 5432
    ServerName = localhost
    Database   = me
    UserName   = me
    Password   =
    
    [OpenLink]
    Description     = PostgreSQL, over openlink multi-tier
    Driver          = /opt/openlink/bin/oplodbc.so
    ServerType      = PostgreSQL95
    Host            = otherbox
    Database        = me
    Username        = me
    FetchBufferSize = 99

More recent versions of iODBC permit use of `{ }` for quotations and
symbolic names for the driver (referencing the `odbcinst.ini` file),
such as

    Driver = {SQL Server}

Older versions of iODBC implemented neither of these; the `Driver=`
parameter had to be a full path directly to the shared library.

## <span id="Common%20Error%20Messages"></span>Common Error Messages

### <span id="%5BiODBC%5D%5BDriver%20Manager%5DData%20source%20name%20not%20found%20and%20no%20default%20driver%20specified.%20Driver%20could%20not%20be%20loaded%2C%20SQLSTATE%3DIM002"></span> \[iODBC\]\[Driver Manager\]Data source name not found and no default driver specified. Driver could not be loaded, SQLSTATE=IM002

There are several reasons why this message could occur. The best
solution is to trace through what's happening: your application has been
linked against `libiodbc`, which has tried to find an `odbc.ini` file
one way or another - either through the `ODBCINI` environment variable
or the fall-back paths (typically `/etc/odbc.ini`, depending on how it
was compiled). You should check that such a file exists in a suitable
location, and that it is accessible (particularly if your application
runs with different user privileges - such as `apache`/`php` running as
a www-data user).

Additionally, it could be that iODBC has found a suitable `odbc.ini`
file, but none of the file(s) found contain the DSN you've requested.
Check the syntax of your request - is the ODBC connect-string correct,
and does the DSN you're requesting exist? See also the section of this
FAQ entitled *[What's an odbc.ini and what do I put in
it?](#What%27s%20an%20odbc.ini%20and%20what%20do%20I%20put%20in%20it%3F)*

### <span id="%5BiODBC%5D%20%5BDriver%20Manager%5DSpecified%20driver%20could%20not%20be%20loaded"></span> \[iODBC\] \[Driver Manager\]Specified driver could not be loaded

As in the previous error case, there are a few reasons why this could
occur, and thinking through the architecture helps. Your application has
loaded `libiodbc` successfully, and it has found an `odbc.ini` file (or
equivalent through the `ODBCINI` environment variable), and it has found
a DSN within that `odbc.ini` that matches the name requested in your
connection.

However, the driver manager has had problems loading the library
specified in the `Driver=` line of that DSN definition. Either it
doesn't exist, or its permissions are insufficient to allow your
application to load it (it must be readable and executable, and the
directories leading down to it must be executable), or maybe the file is
not a dynamic library -- it could be a static library (a `*.a` file,
except on AIX) -- or is otherwise corrupted. These are all things to
check, or you may be best off reinstalling the driver if all the
permissions check out.

Note also the prior point: the `Driver=` parameter **must** lead to a
shared-library (`*.so`) implementing an ODBC driver for the database to
which you're connecting.

## <span id="Driver-Specific%20Errors"></span>Driver-Specific Errors

### <span id="MyODBC%3A%20%5BTCX%5D%5BMyODBC%5DNo%20DSN%20entered%20%280%29%20SQLSTATE%3DS1000"></span> MyODBC: \[TCX\]\[MyODBC\]No DSN entered (0) SQLSTATE=S1000

This error is raised whenever you attempt to connect to MyODBC using the
`SQLDriverConnect()` function with the `SQL_DRIVER_PROMPT` option.
Normally, `SQL_DRIVER_PROMPT` means the driver should invoke a graphical
dialog to request missing information (`DSN=`, or username and password
if not included); however, MyODBC has no graphical library and does not
distinguish the case that a graphical prompt is unavailable from when
there is insufficient information, so you always see this error message.

`iodbctest` and `iodbctestw` from versions 3.52.1 and 3.52.2 both
request connections using `SQL_DRIVER_PROMPT`, causing this problem with
MyODBC.

The workaround is to edit `iodbctest.c` such that the
`SQLDriverConnect()` and `SQLDriverConnectW()` calls use
`SQL_DRIVER_COMPLETE` instead. This still allows drivers with graphical
setup routines to ask for additional information, but works better with
drivers that have no graphical routines, such as MyODBC. See the
following diff:

    Index: iodbctest.c
    ===================================================================
    RCS file: /opldev/opensource/iODBC/samples/iodbctest.c,v
    retrieving revision 1.22
    retrieving revision 1.21
    diff -u -u -r1.22 -r1.21
    --- iodbctest.c 2005/07/19 10:19:01     1.22
    +++ iodbctest.c 2005/02/15 17:08:13     1.21
    @@ -297,12 +297,12 @@
    #ifdef UNICODE
    strcpy_A2W (wdataSource, (char *) dataSource);
    status = SQLDriverConnectW (hdbc, 0, (SQLWCHAR *) wdataSource, SQL_NTS,
    -      (SQLWCHAR *) outdsn, NUMTCHAR (outdsn), &buflen, SQL_DRIVER_COMPLETE);
    +      (SQLWCHAR *) outdsn, NUMTCHAR (outdsn), &buflen, SQL_DRIVER_PROMPT);
    if (status != SQL_SUCCESS)
    ODBC_Errors ("SQLDriverConnectW");
    #else
    status = SQLDriverConnect (hdbc, 0, (SQLCHAR *) dataSource, SQL_NTS,
    -      (SQLCHAR *) outdsn, NUMTCHAR (outdsn), &buflen, SQL_DRIVER_COMPLETE);
    +      (SQLCHAR *) outdsn, NUMTCHAR (outdsn), &buflen, SQL_DRIVER_PROMPT);
    if (status != SQL_SUCCESS)
    ODBC_Errors ("SQLDriverConnect");
    #endif

This change is included in the iODBC 3.52.3 and later.

## <span id="Segfault%20with%20Perl%20DBD%3A%3AODBC"></span>Segfault with Perl DBD::ODBC

Certain platforms (most notably Debian GNU/Linux 5.0.4 ("Lenny",
currently stable)) ship with version 1.13-5 of Perl's `DBD::ODBC`
module. On 64-bit OS, this has a bug that causes a segfault. The
solution is to upgrade to at least 1.17 (may be found in "Squeeze",
currently the Testing distribution).

## <span id="Tracing%20Application%20Behavior"></span>Tracing Application Behavior

In the above `odbc.ini` snippet, we saw commented-out lines concerning
tracing. These lines would enable us to analyze what ODBC calls the
driver manager sees an application make, with details including
parameters, return states, etc.

To enable this, uncomment the lines in your `odbc.ini`:

    [ODBC]
    Trace = 1 
    TraceFile = /tmp/odbctrace.log 
    Debug = 1 
    DebugFile = /tmp/odbcdebug.log

In iODBC version 3.51.0 and above, the `TraceFile` option now
understands a handful of variables:

    $P        Process ID
    $U        User ID under which the process is currently running
    $T        Timestamp in YYYYMMDDHHMMSS format
    $H        Home directory of the user that started the process

Also, from version 3.52.7 onwards, `TraceFile` now takes an option

    $S        Sequence number

These are case-insensitive. Hence you could specify --

    TraceFile=/tmp/iodbc-$U-$P-$T.log

\-- and it would include your userid, the application process-id, and
the timestamp when ODBC was invoked, in the trace log filename.

### <span id="Tracing%20Application%20Behavior"></span>Tracing Application Behavior

As of release 3.52.5, iODBC has support for File DSNs - where the
connection parameters are stored in a separate file per DSN, under a
standard directory.

To configure these, either use the **FileDSN** tab alongside System and
User DSNs in the iODBC graphical administrator (`iodbcadm-gtk` or the
macOS GUI), or edit files in `/etc/ODBCDataSources/` for yourself.

![](FAQ/iodbcadm-gtk-filedsn.png)

Note that this directory must have suitable permissions for those you
wish to be able to create, edit, and remove files to do so. For example,
`1775` might be suitable - the owner and members of the group owning the
directory can create, remove, and edit their own DSNs, but not those
owned by a different user.

To use a File DSN, replace the `DSN=` parameter in your ODBC connection
string with `FileDSN=`, for example

    iodbctest FileDSN=localvirtuoso;UID=dba;PWD=secret

</div>
