::: {#content .topic-text wv="http://www.openlinksw.com/Virtuoso/WikiV/" vi="http://www.openlinksw.com/virtuoso/xslt/" ie="http://www.openlinksw.com/Virtuoso/InclEng/" fn2="http://www.w3.org/2004/07/xpath-functions" xmlns="http://www.w3.org/1999/xhtml"}
::: {.MACRO_TOC}
Table of Contents {#table-of-contents .toc}
-----------------

-   [Disclaimer](#Disclaimer)
-   [ODBC Overview](#ODBC%20Overview)
-   [Preface](#Preface)
-   [Compiling PHP with linked iODBC Driver Manager as an Apache shared
    module](#Compiling%20PHP%20with%20linked%20iODBC%20Driver%20Manager%20as%20an%20Apache%20shared%20module)
-   [Building Apache](#Building%20Apache)
-   [Compiling PHP](#Compiling%20PHP)
-   [Restarting Apache](#Restarting%20Apache)
-   [Checking your PHP
    installation](#Checking%20your%20PHP%20installation)
-   [Environment Variable concerns](#Environment%20Variable%20concerns)
-   [Sample PHP script](#Sample%20PHP%20script)
-   [Concerns and Improvements](#Concerns%20and%20Improvements)
-   [References](#References)
:::

[]{#Disclaimer}Disclaimer
-------------------------

The following is a HOWTO document for installing PHP with iODBC as an
Apache module on Linux or Unix. Feel free to criticize, suggest
modifications, or ask further questions. It is currently maintained by
Tim Haynes of Openlink Software (`iodbc@openlinksw.com`).

Prerequisites include basic Unix familiarity, such as creating
directories and users, using an editor, etc.

This HOWTO is intended to assist in connecting `php`/`apache` to back
end databases via ODBC in a development environment and should not take
the place of thorough testing before deployment on a production system.

[]{#ODBC%20Overview} ODBC Overview
----------------------------------

ODBC (Open Database Connectivity) is an operating system- and
database-independent communication API that allows a client application
(productivity tool, other database, web page, custom application, etc.)
to communicate via standards-based function calls to a backend database
without relying on that vendor\'s proprietary communication protocols.

ODBC connections involve an application, driver manager, driver, and
database. The driver manager under Microsoft Windows platforms is the
ODBC Control Panel. The driver manager registers a set of ODBC driver
connection parameters called a Data Source Name (DSN). An application
looks to the driver manager for a DSN, and then passes the connection
parameters specified in the DSN to the appropriate driver, which makes
the connection. Under non-Windows platforms you may need to install a
Driver Manager.

iODBC is an Open Source Driver Manager maintained by OpenLink Software.
It is released under a dual LGPL / BSD license.

[]{#Preface} Preface
--------------------

You will also need an ODBC Driver and Database to complete the
architecture.

If you need ODBC drivers to connect to a third-party database on the
same or another machine, [OpenLink ODBC
Drivers](http://uda.openlinksw.com/odbc/){.absuri} are available, and
may be [downloaded for free
trial](https://shop.openlinksw.com/license_generator/uda/){.absuri}.

The [Virtuoso database](http://virtuoso.openlinksw.com/){.absuri} may
also be [downloaded for free
trial](https://shop.openlinksw.com/license_generator/virtuoso/){.absuri}.

Support with downloading, installing, configuring, and testing these
OpenLink products may be obtained through the [OpenLink Community
Space](http://community.openlinksw.com/){.absuri}.

[]{#Compiling%20PHP%20with%20linked%20iODBC%20Driver%20Manager%20as%20an%20Apache%20shared%20module} Compiling PHP with linked iODBC Driver Manager as an Apache shared module
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

The process is fairly straightforward. You will need to be a user who
has sufficient privileges to perform all of these steps as well. Root
privileges can be obtained by typing `su root` and entering your root
password, but be forewarned that you can easily destroy your system as
`root`. If you use root privileges, please do so on a test machine.

Set up a build location, and get the latest builds of
[iODBC](http://www.iodbc.org/){.absuri},
[Apache](http://httpd.apache.org/){.absuri}, and
[PHP](http://www.php.net/){.absuri}.

Set some environment variables:

    export LD_LIBRARY_PATH=/usr/local/src/odbcsdk/lib:$LD_LIBRARY_PATH

\- this tells the compiler where to find the driver manager.

If you prefer to statically link iODBC then remove or rename
`libiodbc.so` from the above path, and `libiodbc.a` will be statically
linked instead.

[]{#Building%20Apache} Building Apache
--------------------------------------

We build `apache` with support for dynamic modules and APXS:

    cd httpd-1.3.*
    ./configure --prefix=/usr/local/apache --enable-module=so --enable-mods-shared=[list of modules]
    nice make && su root -c 'make install'

Choose the list of modules to go with whatever you expect to be loading
from your `httpd.conf` (or similar). Among other things, authentication,
dav (in the case of Apache 2.x), ssl, virtualhosting, user-tracking,
spelling-correction, proxying, SSI, fine control of MIME data, etc. \--
these are all configurable at this time.

After a while, Apache should finish compiling and install itself into
`/usr/local/apache/`.

[]{#Compiling%20PHP} Compiling PHP
----------------------------------

Unpack the PHP sources with a command like \--

    tar xvpfj php-4.3.2.tar.bz2

\-- and change into the resultant directory.

Note: if you are using iodbc-3.51.0, this will expose a problem in
PHP\'s configure script whereby it assumes the only library required is
`-liodbc`, when it should be calling \"`iodbc-config --libs`\" to
determine the `LDFLAGS` required. This causes a `debug.log` to be
created as PHP is configured, and while it may build seemingly to
completion, the resultant PHP library will give unresolved symbol
errors, and apache will fail to start. [This
patch](IODBCPHPHOWTO/php-configure-iodbc.diff){.c1} can be applied to
PHP\'s `./configure` script to avoid the problem.

PHP needs to be configured with a pointer both to Apache that you
installed earlier, and to the ODBC SDK (`iodbc` directory):

    bash$ ./configure --prefix=$HOME/php5 \
    --enable-discard-path \
    --with-layout=GNU \
    --with-openlink=/usr/local/openlink/odbcsdk \
    --enable-experimental-zts \
    --with-regex=php \
    --enable-experimental-zts  \
    --enable-debug  \
    --enable-calendar \
    --with-iodbc=/usr/local/openlink/odbcsdk  \
    --without-mysql \
    --disable-sockets \
    --disable-cli \
    --with-apxs=/usr/local/apache/sbin/apxs \
    --enable-embed=share{,d}

    bash$ nice make
    bash$ su root -c 'make install'

The process of installing here will invoke `apxs`, Apache\'s utility for
making installation of modules an awful lot easier. This should also
include making minor changes to your `httpd.conf` (so to be safe, back
it up first) - namely these:

    LoadModule php5_module    extramodules/libphp5.so

and

    AddModule mod_php5.c

Also, the following should be set:

    AddType  application/x-httpd-php         .php .php4 .php3 .phtml   
    AddType  application/x-httpd-php-source  .phps

[]{#Restarting%20Apache} Restarting Apache
------------------------------------------

Use the command:

    /usr/local/apache/sbin/apachectl start

to start apache.

Should it fail to start, you\'ll be best off checking `logs/error_log`
to see why it failed: there are a multitude of possible configuration
errors, from typos, through failure to access files to which it should
have permission, processes already using the socket configured for
listening, and more.

[]{#Checking%20your%20PHP%20installation} Checking your PHP installation
------------------------------------------------------------------------

Create a simple PHP starter script, e.g., `info.php`, containing nothing
but the line:

    <?php phpinfo(); ?>

Ensure that the permissions are acceptable - `644` (owner read+write,
everyone else read-only) should suffice.

Put it in your `htdocs/` directory, or somewhere else accessible under
your webserver configuration (e.g., `~/public_html/`).

Point your browser to <http://localhost/info.php> to see all PHP\'s
configuration information.

[]{#Environment%20Variable%20concerns} Environment Variable concerns
--------------------------------------------------------------------

There are two files that your ODBC-using PHP scripts must be able to
access:

\* `libiodbc.so` - PHP requires this to be in the list of directories
searched, so if you export `LD_LIBRARY_PATH` either before starting
`apache`, or using the `SetEnv` directive in `httpd.conf`, it should be
able to access the driver manager.

\* `odbc.ini` - this is accessed by the driver manager, `libiodbc.so`,
and contains a list of all your DSNs and their connect info, etc. In
order to find this, iODBC uses the `ODBCINI` environment variable, or
failing that it will search `/etc/odbc.ini` or `~/.odbc.ini` instead.
You can either export this in `httpd.conf`, or before Apache starts, or
from within your PHP script itself with the `setenv()` function call.

[]{#Sample%20PHP%20script} Sample PHP script
--------------------------------------------

The following script effects a connection to a database
(`Local Virtuoso Demo` is the default DSN), and either executes a query
or lists tables present in that database.

    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"> 

    <html>
    <head>
    <title>OpenLink Virtuoso test of ODBC access through PHP hosting</title>
    <link type="text/css" rel="STYLESHEET" 
    media="ALL" href="../../tutorial.css" />
    </head>

    <body>
    <h1>Testing ODBC connectivity from PHP hosted within Virtuoso</h1>

    <hr />

    <?php
    # set global variables based on the form thing - see `register global
    # variables' and PHP security updates
    $query=$_POST['query'];
    $uid=$_POST['uid'];
    $passwd=$_POST['passwd'];
    $listtables=$_POST['listtables'];
    $DSN=$_POST['DSN'];
    $exec=$_POST['exec'];
    ?>

    <p>Enter the parameters for your query here:</p>

    <form action="odbc-sample.php" method="post"> 
    <div> 
    <span class="caption">DSN</span> 
    <input type="text" name="DSN" value="<?php
    print ($DSN<>"")?$DSN:"Local Virtuoso Demo"
    ?>" /> 

    <span class="caption">UserID</span>
    <input type="text" name="uid" value="<?php print ($uid<>"")?$uid:"demo" ?>" />

    <span class="caption">Password</span>
    <input type="password" name="passwd" value="<?php print ($passwd<>"")?$passwd:"demo"?>" />
    </div>

    <div>
    <span class="caption">Query</span> 
    <input type="text" name="query" value="<?php
    print ($query<>"")?$query:"select top 100 * from Demo..Customers"
    ?>" /> 
    </div>
    <div>
    <input type="submit" name="exec" value="Execute query" />
    or
    <input type="submit" name="listtables" value="List Tables" />
    </div>
    </form>

    <hr />

    <?php
    if($query<>"" && $DSN<>"" && $exec!=NULL) {

    print "<h2>Results:</h2>
    ";
    print "<p>Connecting... ";
    $handle=odbc_connect ("$DSN", "$uid", "$passwd");

    if(!$handle) {
    print "<p>Uh-oh! Failure to connect to DSN [$DSN]: <br />";
    odbc_errormsg();
    }
    else {
    print "done</p>
    ";
    $resultset=odbc_exec ($handle, "$query");
    odbc_result_all($resultset, "border=2");
    odbc_close($handle);
    }
    }

    if($listtables!=NULL) {
    print "<h2>List of tables</h2>";
    print "<p>Connecting... ";
    $handle=odbc_connect ("$DSN", "$uid", "$passwd");
    print "done</p>
    ";

    if(!$handle) {
    print "<p>Uh-oh! Failure to connect to DSN [$DSN]: <br />";
    odbc_errormsg();
    }
    else {
    $resultset=odbc_tables($handle);
    odbc_result_all($resultset, "border=2");
    odbc_close($handle);
    }
    }
    ?>
    </body>
    </html>

[]{#Concerns%20and%20Improvements} Concerns and Improvements
------------------------------------------------------------

Historically, iODBC has not been fully supported in PHP. We made a patch
addressing these issues:

-   ODBC 3.52 datatypes are now used, to comply with ODBC64 spec on
    Win64 and 64-bit \*nix platforms
-   Enabled use of `SQLDriverConnect()`, array fetching, and other
    advanced PHP API functions
-   Made the static cursor model the default (instead of dynamic), to
    speed up advanced drivers. The cursor model can be selected by a
    setting in `php.ini`.

This patch has been incorporated into PHP around version 5.2.11 and
above.

To use this patch with older versions of PHP, first download it:
`iodbc-php5.diff`

Second, apply it using `patch(1)`:

    bash$ tar xvfpj php-5.2.5.tar.bz2
    php-5.2.5/
    php-5.2.5/ext/
    php-5.2.5/ext/gd/
    php-5.2.5/ext/gd/gd.c
    php-5.2.5/ext/gd/gd_ctx.c
    ...
    bash$ patch -p0 < ../iodbc-php5.diff
    patching file ext/odbc/php_odbc.c
    Hunk #26 succeeded at 1644 (offset 1 line).
    Hunk #27 succeeded at 1715 (offset 1 line).
    Hunk #28 succeeded at 1777 (offset 1 line).
    Hunk #29 succeeded at 1863 (offset 1 line).
    Hunk #47 succeeded at 3603 (offset 1 line).
    patching file ext/odbc/php_odbc.h
    patching file ext/odbc/php_odbc_includes.h

You can now resume the build process from the \"`./configure`\" step
above.

[]{#References} References
--------------------------

-   PHP on macOS [installation
    instructions](http://www.php.net/manual/en/install.macosx.php){.absuri}
-   [iODBC.org](http://www.iodbc.org){.absuri}
-   History of [ODBC on
    Unix](http://www.iodbc.org/odbcstory.htm){.absuri}
-   [PHP main site](http://www.php.net/support.php){.absuri}
-   [OpenLink Software](http://www.openlinksw.com/){.absuri}
    -   [Community Space](http://community.openlinksw.com/){.absuri}
    -   [Support Center and Case
        System](http://support.openlinksw.com/){.absuri}
:::
