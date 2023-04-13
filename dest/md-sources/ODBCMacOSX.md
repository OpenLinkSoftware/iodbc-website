::: {#content .topic-text wv="http://www.openlinksw.com/Virtuoso/WikiV/" vi="http://www.openlinksw.com/virtuoso/xslt/" ie="http://www.openlinksw.com/Virtuoso/InclEng/" fn2="http://www.w3.org/2004/07/xpath-functions" xmlns="http://www.w3.org/1999/xhtml"}
::: {.MACRO_TOC}
Table of Contents {#table-of-contents .toc}
-----------------

-   [Standard ODBC Architecture](#Standard%20ODBC%20Architecture)
-   -   [Application](#Application)
    -   [Driver Manager](#Driver%20Manager)
    -   [ODBC Drivers](#ODBC%20Drivers)
    -   [Data sources](#Data%20sources)

-   [ODBC Driver Architecture with Driver
    Manager](#ODBC%20Driver%20Architecture%20with%20Driver%20Manager)
-   [ODBC Driver Architecture without Driver
    Manager](#ODBC%20Driver%20Architecture%20without%20Driver%20Manager)
-   [](#)
-   -   [Environment Variables](#Environment%20Variables)
    -   [Setting Environment Variables on
        Darwin](#Setting%20Environment%20Variables%20on%20Darwin)
    -   [Client Libraries](#Client%20Libraries)
    -   [Header Files](#Header%20Files)
    -   [Configuration Files](#Configuration%20Files)
    -   [Administrative Assistants](#Administrative%20Assistants)
    -   [Server Components](#Server%20Components)

-   [Configuring](#Configuring)
-   -   [Configuring Darwin Data Source
        Names](#Configuring%20Darwin%20Data%20Source%20Names)
    -   [The odbc.ini File](#The%20odbc.ini%20File)
    -   [ODBC Data Sources](#ODBC%20Data%20Sources)
    -   [Data Source Specification](#Data%20Source%20Specification)
    -   [The Multi-Tier Administrative
        Assistant](#The%20Multi-Tier%20Administrative%20Assistant)
    -   [Configuring Mac Classic Data Source
        Names](#Configuring%20Mac%20Classic%20Data%20Source%20Names)
    -   [Configuring Mac OS X Data Source
        Names](#Configuring%20Mac%20OS%20X%20Data%20Source%20Names)
    -   [ODBC Data Sources](#ODBC%20Data%20Sources)
    -   [Data Source Specification](#Data%20Source%20Specification)
    -   -   [MS SQL Server Single-Tier drivers recognize these
            specialized
            parameters.](#MS%20SQL%20Server%20Single-Tier%20drivers%20recognize%20these%20specialized%20parameters.)
        -   [](#)
        -   [Oracle Single-Tier drivers recognize these specialized
            parameters.](#Oracle%20Single-Tier%20drivers%20recognize%20these%20specialized%20parameters.)
        -   [](#)

    -   [Aqua GUI ODBC
        Administrators](#Aqua%20GUI%20ODBC%20Administrators)

-   [Developing ODBC Compliant
    Applications](#Developing%20ODBC%20Compliant%20Applications)
-   [](#)
-   [](#)
-   -   [Single-Tier Drivers](#Single-Tier%20Drivers)
    -   [Multi-Tier Drivers](#Multi-Tier%20Drivers)
:::

### []{#Standard%20ODBC%20Architecture} Standard ODBC Architecture

ODBC data access comprises the following, four components:

#### []{#Application} Application

Most end users use ODBC-compliant applications to access their data
stores. ODBC-compliant applications are executables, which issue ODBC
API calls. These API calls are implemented by ODBC drivers that are
customized for use with the data store. These calls enable the
application to connect to the data store and query the data store via
the ODBC driver.

#### []{#Driver%20Manager} Driver Manager

The driver manager is a library, which manages communications between
applications and ODBC drivers. It responds to all ODBC connection
requests made by applications, and it loads the ODBC drivers that are
associated with the requests. Once the drivers are loaded, the driver
manager translates applications\' function calls into the corresponding
ODBC API calls, and it issues these calls to the drivers. When the
applications complete their requests, the driver manager terminates the
connections and unloads the drivers.

Users may encounter the following driver managers on Mac client systems:

  [Platform](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=0&col=1)   [Driver Manager](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=1&col=2)
  ------------------------------------------------------------------------------------------ ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Darwin                                                                                     OpenLink\'s Darwin client installer provides the iODBC driver manager. Users may also encounter unixODBC, mac:ODBC, and other driver managers.
  Mac Classic a/k/a Mac OS 9                                                                 OpenLink\'s Mac Classic client installer provides its own driver manager for this platform. Users may also encounter another driver manager created by Visigenic and maintained by Intersolv, Merant, and Data Direct respectively.
  Mac OS X                                                                                   OpenLink\'s default Mac OS X client installer provides an iODBC frameworks-based driver manager. Apple\'s Jaguar installer provides an iODBC dylibs-based driver manager. Users may also encounter unixODBC, mac:ODBC, and other driver managers.

#### []{#ODBC%20Drivers} ODBC Drivers

ODBC drivers are libraries. These libraries implement ODBC API
functions, which enable applications to speak to databases. Typically,
applications are linked against driver managers, which load the
appropriate driver libraries. However, applications may be linked
directly to drivers. In this instance, driver libraries perform driver
manager library functions.

#### []{#Data%20sources} Data sources

The term data source has two, distinct meanings. First, data source
refers to the actual flat files, spreadsheets, or database management
systems, which store data. Second, data source refers to the collection
of parameters that applications use to establish connections to data
stores. This data source passes a driver name, database name, server
hostname, and other parameters, which are necessary to identify a
database or similar storage entity.

### []{#ODBC%20Driver%20Architecture%20with%20Driver%20Manager} ODBC Driver Architecture with Driver Manager

Figure 1-1 illustrates the default architecture for ODBC connectivity.
The default architecture employs both a driver manager and ODBC drivers.

![Macfig1.jpg](ODBCMacOSX/Macfig1.jpg)

### []{#ODBC%20Driver%20Architecture%20without%20Driver%20Manager} ODBC Driver Architecture without Driver Manager

Figure 1-2 illustrates ODBC connectivity without a driver manager
component. ODBC connectivity is possible, in the absence of a driver
manager, if the client application is linked directly to the ODBC
driver. In some instances, a symbolic link is created, which uses a
driver manager library name to point to an ODBC driver library.

![Macfig2.jpg](ODBCMacOSX/Macfig2.jpg)

###  OpenLink ODBC Driver Architecture

OpenLink Software provides two ODBC driver formats. Use of these drivers
requires knowledge of the following items:

-   Environment Variables
-   Client Libraries
-   Header Files
-   Configuration Files
-   Administrative Assistants
-   Server Components

#### []{#Environment%20Variables}Environment Variables

Environment variables pass the locations of files and directories, which
the operating system or applications need to accomplish tasks. Users do
not need to set environment variables on Mac Classic and Mac OS X
operating systems. Users do need to set environment variables on Darwin.

The following table lists environment variables, which must be set on
Darwin clients.

  [Environment Variable](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=2&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=3&col=2)
  ------------------------------------------------------------------------------------------------------ --------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `CLASSPATH`                                                                                            Passes the full path to OpenLink\'s Java archive (.jar) files. These files comprise the OpenLink JDBC client. This variable is not required for ODBC connectivity.
  `LD_LIBRARY_PATH`                                                                                      Passes the full path to various library directories on Darwin computers. This variable must include the OpenLink /lib sub-directory.
  `ODBCINI`                                                                                              Passes the full path to the odbc.ini file, which resides in the OpenLink /bin sub-directory.
  `ODBCINSTINI`                                                                                          Passes the full path to the odbcinst.ini file, which resides in the OpenLink /bin sub-directory.
  `OPENLINKINI`                                                                                          Passes the full path to the openlink.ini file, which resides in the OpenLink /bin sub-directory.
  `PATH`                                                                                                 Passes the full path to directories, which contain executables. This variable must include the OpenLink /bin sub-directory.

#### []{#Setting%20Environment%20Variables%20on%20Darwin}Setting Environment Variables on Darwin

OpenLink\'s Darwin installers create openlink.sh and openlink.csh files
in the root of the installation. These files contain all the environment
variables, which need to be set for OpenLink client connectivity. Users
must execute these files in the appropriate shell. C shell users may
execute openlink.csh. Bash and Bourne shell users may execute
openlink.sh. Users with different shells are encouraged to switch to C,
Bash, or Bourne before executing the files.

Expert users may set and export the appropriate variables using the
Darwin command line. For example:

    export ODBCINI=/usr/openlink/bin/odbc.ini

Users may also add the variables to their .profiles to insure that the
variables are set at login to their client systems.

#### []{#Client%20Libraries} Client Libraries

OpenLink\'s drivers and iODBC driver manager are library files. Users
will encounter a variety of library file formats and installation locals
on different, client operating systems.

The following table holds a list of common Darwin libraries. Each of
these files appears in the `/lib` sub-directory of the OpenLink client
installation. Click here to see a complete list of OpenLink libraries by
platform.

  [Filename](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=4&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=5&col=2)
  ------------------------------------------------------------------------------------------ ------------------------------------------------------------------------------------------------------------------------
  `libiodbc.la`                                                                              Static, iODBC driver manager library
  `libiodbc.so`                                                                              Shared, iODBC driver manager library. Older, iODBC driver manager libraries are linked to the latest revision
  `libiodbc.so.2`                                                                            Revised, iODBC driver manager library. Older, iODBC driver manager libraries are linked to the latest revision
  `libiodbc.so.2.1.2`                                                                        Revised, iODBC driver manager library. Older, iODBC driver manager libraries are linked to the latest revision
  `mys3 st_lt.la`                                                                            Static, single-threaded MySQL Single-Tier driver
  `mys3_st_lt.so`                                                                            Shared, single-threaded MySQL Single-Tier driver
  `oplodbc.la`                                                                               Static, Multi-Tier ODBC driver
  `oplodbc.so`                                                                               Shared, Multi-Tier ODBC driver. Older, Multi-Tier ODBC driver library files are linked to the latest revision
  `oplodbc.so.1`                                                                             Revised, Multi-Tier ODBC driver library. Older, Multi-Tier ODBC driver library files are linked to the latest revision
  `oplodbc.so.1.0.0`                                                                         Revised, Multi-Tier ODBC driver library. Older, Multi-Tier ODBC driver library files are linked to the latest revision
  `ora81_st_lt.la`                                                                           Static, single-threaded Oracle 8.1.x Single-Tier driver
  `ora81_st_lt.so`                                                                           Shared, single-threaded Oracle 8.1.x Single-Tier driver
  `pgr7_mt_lt.la`                                                                            Static, multi-threaded PostgreSQL Single-Tier driver
  `pgr7_mt_lt.so`                                                                            Shared, multi-threaded PostgreSQL Single-Tier driver
  `pgr7_st_lt.la`                                                                            Static, single-threaded PostgreSQL Single-Tier driver
  `pgr7_st_lt.so`                                                                            Shared, single-threaded PostgreSQL Single-Tier driver
  `sql_st_lt.la`                                                                             Static, single-threaded MS SQLServer Single-Tier driver
  `sql_st_lt.so`                                                                             Shared, single-threaded MS SQLServer Single-Tier driver
  `syb12_st_lt.la`                                                                           Static, single-threaded Sybase Single-Tier driver
  `syb12_st_lt.so`                                                                           Shared, single-threaded Sybase Single-Tier driver

#### []{#Header%20Files} Header Files

OpenLink Software provides a separate iODBC SDK product installer for
Mac Classic and Mac OS X platforms. These installers contain the
`sql.h`, `sqlext.h`, and `sqltypes.h` header files. Developers may use
these files to build ODBC-compliant applications.

#### []{#Configuration%20Files} Configuration Files

OpenLink\'s Darwin-based Single-Tier drivers use the `openlink.ini` file
to obtain database-specific environment variable settings. The
`openlink.ini` file resides in the `/bin` sub-directory of Single-Tier
client installations.

OpenLink\'s Multi-Tier brokers read the `oplrqb.ini` file to resolve
ODBC connection requests and to enforce OpenLink\'s sophisticated,
rule-based security. The `oplrqb.ini` file resides in the `/bin`
sub-directory of OpenLink\'s server components installations.

#### []{#Administrative%20Assistants} Administrative Assistants

OpenLink Software produces two, graphical Administrative Assistants. The
Multi-Tier Administrative Assistant is a web-based GUI, which allows
users to configure all aspects of Multi-Tier connectivity. This
assistant allows users to create Multi-Tier data source names, configure
Multi-Tier Server components, configure rules-based security, and debug
ODBC connectivity problems.

OpenLink Software also produces the independent, HTTP-based iODBC Data
Sources Administrator. This web-based GUI enables users to create and
administer OpenLink and non-OpenLink ODBC data source names using one,
user-friendly interface.

#### []{#Server%20Components} Server Components

OpenLink\'s Multi-Tier drivers implement a client/server connectivity
model. The Multi-Tier client comprises a driver manager and client-side
ODBC driver. The Multi-Tier server component comprises a request broker
and one or more database agents.

The request broker is a generic, listening process. It responds to ODBC
requests made by the Multi-Tier client driver. The broker reviews these
requests and spawns the appropriate database agent. The database agent
is the only portion of the Multi-Tier product portfolio that is written
to a specific CLI. Specifically, the database agent speaks the CLI of
the database to which it is meant to connect. Hence, the agent is able
to submit the SQL request to the database, retrieve its results, and
convey those results to the client application.

### []{#Configuring} Configuring OpenLink Data Source Names

Users must create ODBC data source names to establish connectivity
between client applications and SQL data stores. ODBC data source names
are collections of parameters, which enable the OpenLink driver to
identify and connect to the data store. There are several means, which
users may employ to create ODBC data source names.

#### []{#Configuring%20Darwin%20Data%20Source%20Names}Configuring Darwin Data Source Names

There are three methods, which users may employ to configure Darwin data
source names. Expert users may configure the `odbc.ini` file using
[vi]{.c1} or a similar text editor. Novice users may use the HTTP-Based
iODBC Data Sources Administrator, or they may use the Multi-Tier
Administrative Assistant.

#### []{#The%20odbc.ini%20File} The odbc.ini File

The odbc.ini file appears in the /bin sub-directory of the OpenLink
client installation. Users may open this file with vi or a similar text
editor. The following table describes sections, which users will
encounter in odbc.ini.

  [Section](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=6&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=7&col=2)
  ----------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------
  ODBC Data Sources                                                                         This section names each of the ODBC data sources that appear in the odbc.ini file. It also pairs the appropriate ODBC driver name with the data source name.
  Data Source Specifications                                                                This section lists the actual data source names. Each data source name is composed of a formal name and a parameter list.

#### []{#ODBC%20Data%20Sources}ODBC Data Sources

The ODBC Data Sources section lists the names of the individual data
sources and pairs the names with the appropriate ODBC client driver.
These data sources names are associated with formal data source
specifications, which appear later in the file.

Here is the ODBC Data Sources format:

    [ODBC Data Sources] 
    data_source_name=ODBC_client_driver_name

Here is a sample ODBC Data Sources section with data source names:

    [ODBC Data Sources]
    ora81_lite = OpenLink Oracle 8.1 Lite Driver (multi threaded)
    pgr7_lite = OpenLink PostgreSQL Lite Driver (multi threaded)

#### []{#Data%20Source%20Specification} Data Source Specification

Each \[ODBC Data Sources\] data source name has a corresponding data
source specification. The data source specification lists parameters,
which are necessary to establish the ODBC connection. Here is the
OpenLink data source specification format:

    [data_source_name]
    Driver = driver_path
    ServerType = openlink_domain_alias
    Username = database_username
    Password = database_password
    Database = database_name_or_oracle_sid
    Options = three_tier_or_sockets_connection_parameters
    FetchBufferSize = buffer_size
    ReadOnly = enable_disable_readonly_access_to_database
    DeferLongFetch = enable_disable_deferlongfetch_option
    JetFix = enable_disable_jetfix_option
    Description = data_source_description

Here is a sample data source specification:

    [Oracle]
    Driver = /usr/openlink/lib/ora81_st_lt.sl
    ServerType = Oracle 8.1.x
    Username = scott
    Password = tiger
    Database = ORCL
    Options = 
    FetchBufferSize = 99
    ReadOnly = Yes
    DeferLongFetch = No
    JetFix = No
    Description = Oracle DSN

The following table explains the parameters that appear in the data
source specification sections.

  [Parameter](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=8&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=9&col=2)
  ------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `[Data Source Name]`                                                                        Passes a descriptive data source title. This title must match the title passed under the `[ODBC Data           Sources]` heading.
  `Driver`                                                                                    Passes the full path to the ODBC client driver.
  `ServerType`                                                                                Passes a valid OpenLink domain alias. This domain alias must match a valid domain alias in the Single-Tier `openlink.ini` file or Multi-Tier `oplrqb.ini` file. The drivers use these domain aliases as starting points from which to assess rules, environment variables, and agent binaries to instantiate for connections.
  `Username`                                                                                  Passes a valid database username. If the Multi-Tier `OPSYSLOGIN` parameter is enabled, this parameter passes a valid operating system username.
  `Password`                                                                                  Passes a valid database password. If the Multi-Tier `OPSYSLOGIN` parameter is enabled, this parameter passes a valid operating system password.
  `Database`                                                                                  Passes the name of a database or Oracle SID. Progress users should pass the full path to their databases.
  `Options`                                                                                   Passes Progress SHN sockets parameters. Users may also use the field to pass database native communications parameters to establish three-tier connections. For instance, users may pass Sybase instance names, Oracle aliases, or Ingres vnodes to connect database agents\--through local database native clients\--to remote databases.
  `FetchBufferSize`                                                                           Passes an integer, which represents the number of rows that the driver will return during an individual fetch.
  `ReadOnly`                                                                                  Passes a `Yes` or `No` value to enable or disable `READONLY` access to the data store.
  `DeferLongFetch`                                                                            Passes a `Yes` or `No` value to enable or disable deferred fetching. Deferred fetching causes large, binary objects to be fetched after other, smaller data. This enhances performance.
  `JetFix`                                                                                    Passes a `Yes` or `No` value to enable or disable JetFix. JetFix facilitates translation of data types by Microsoft\'s Jet Engine. This feature is intended primarily for use with Microsoft client applications on Windows.
  `Description`                                                                               Passes a description of the use or nature of the data source name.

The following table explains additional values, which may be added to
Multi-Tier data source name specifications.

  [Parameter](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=10&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=11&col=2)
  -------------------------------------------------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `Protocol`                                                                                   Passes a valid OpenLink network protocol. The default is TCP/IP.
  `Hostname`                                                                                   Passes the hostname or IP address of the machine, which contains the OpenLink request broker.
  `Port`                                                                                       Passes the TCP port on which the request broker listens. This TCP port is associated with the `ListenPort` parameter, and it appears in the `[Protocol TCP]` section of the Multi-Tier Rules Book (`oplrqb.ini`).

OpenLink produces the HTTP-Based iODBC Data Sources Administrator for
Darwin and other platforms. This Web-based administrator is a
stand-alone GUI interface to the iODBC driver manager. It is similar to
the Microsoft ODBC Data Sources Administrator, and it allows users to
create OpenLink and non-OpenLink data source names.

Use the following instructions to create data source names with the
iODBC Data Sources Administrator.

-   cd into the `/bin/w3config` sub-directory of the client\'s OpenLink
    installation.
-   Use a text editor to open the `www_sv.ini` file.
-   Locate the `[Startup]` section.
-   Record the value passed to `HttpPort`. For example:\

                      
        [Startup]
        HttpPort          = 8000

    \

-   Exit the file.
-   cd into the `/bin` sub-directory of the client\'s OpenLink
    installation.
-   Run the following command:\

                      
        ./iodbc-admin-httpd.sh start

    \

-   Open a Web browser.
-   Enter the following URL: `http://localhost:HttpPort_from_www_sv.ini`
-   Expand the following menu items: Client Components Administration
    -\> Data Source Name Configuration -\> Edit Data Sources by Wizard
    -\> Edit ODBC Data Sources.
-   Provide the administrator username and password. Both fields default
    to admin.
-   Click Add.
-   Select the appropriate OpenLink ODBC driver.
-   Click Next.
-   Use setup screens 1 to 5 to provide connection parameters and to
    disable or enable optional features. Figures 1-3 describes
    Single-Tier parameters and options. Figure 1-4 describes Multi-Tier
    parameters and options.

<!-- -->

-   Figure 1-3 - Single-Tier Parameters & Options\*

  [Parameter](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=12&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=13&col=2)
  -------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `Name`                                                                                       Passes a descriptive data source title.
  `Comment`                                                                                    Passes a description of the use or nature of the data source name.
  `Database Name`                                                                              Passes the name of a database or Oracle SID. Progress users should pass the full path to their databases.
  `Server`                                                                                     Passes Progress SHN sockets parameters. Users may also use the field to pass database native communications parameters to establish three-tier connections. For instance, users may pass Sybase instance names, Oracle aliases, or Ingres vnodes to connect database agents\--through local database native clients\--to remote databases.
  `Username`                                                                                   Passes a valid database username. If the Multi-Tier OPSYSLOGIN parameter is enabled, this parameter passes a valid operating system username.
  `Read-only connection`                                                                       Passes a Yes or No value to enable or disable READONLY access to the data store.
  `No Login Dialog Box`                                                                        Enables or disables the login popup box.
  `Defer Fetching of long data`                                                                Passes a Yes or No value to enable or disable deferred fetching. Deferred fetching causes large, binary objects to be fetched after other, smaller data. This enhances performance.
  `Row buffer size`                                                                            Passes an integer, which represents the number of rows that the driver will return during an individual fetch operation.
  `Jet Fix`                                                                                    Passes a Yes or No value to enable or disable JetFix. JetFix facilitates translation of data types by Microsoft\'s Jet Engine. This feature is intended for use with MS Access client applications.
  `Environment`                                                                                Passes a valid OpenLink domain alias. This domain alias must match a valid domain alias in the Single-Tier openlink.ini file. The drivers use these domain aliases as starting points from which to assess rules, environment variables, and agent binaries to instantiate for connections.

-   Note:\* The Server parameter name changes to reflect the database to
    which you are trying to connect. For instance, the setup routine
    will replace Server with Net 8 Service Name, if you choose an Oracle
    Single-Tier driver.

<!-- -->

-   Figure 1-4 - Multi-Tier Parameters & Options\*

  [Parameter](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=14&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=15&col=2)
  -------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Name                                                                                         Passes a descriptive data source title.
  Comment                                                                                      Passes a description of the use or nature of the data source name.
  Domain                                                                                       Passes a valid OpenLink domain alias. This domain alias must match a valid domain alias in the Multi-Tier oplrqb.ini file. The drivers use these domain aliases as starting points from which to assess rules, environment variables, and agent binaries to instantiate for connections.
  Hostname                                                                                     Passes the hostname or IP address of the machine, which contains the OpenLink request broker.
  Port                                                                                         Passes the TCP port, on which the request broker listens. This TCP port is associated with the ListenPort parameter, and it appears in the \[Protocol TCP\] section of the Multi-Tier Rules Book (oplrqb.ini).
  Protocol                                                                                     Passes a valid OpenLink network protocol. The default is TCP/IP.
  Database Name                                                                                Passes the name of a database or Oracle SID. Progress users should pass the full path to their databases.
  Server                                                                                       Passes Progress SHN sockets parameters. Users may also use the field to pass database native communications parameters to establish three-tier connections. For instance, users may pass Sybase instance names, Oracle aliases, or Ingres vnodes to connect database agents\--through local database native clients\--to remote databases.
  Username                                                                                     Passes a valid database username. If the Multi-Tier OPSYSLOGIN parameter is enabled, this parameter passes a valid operating system username.
  Read-only Connection                                                                         Passes a Yes or No value to enable or disable READONLY access to the data store.
  No Login Dialog Box                                                                          Enables or disables login popup box.
  Defer Fetching of long data                                                                  Passes a Yes or No value to enable or disable deferred fetching. Deferred fetching causes large, binary objects to be fetched after other, smaller data. This enhances performance.
  Row buffer size                                                                              Passes an integer, which represents the number of rows that the driver will return during an individual fetch.

-   Note:\* The Server parameter name changes to reflect the database to
    which you are trying to connect. For instance, the setup routine
    will replace Server with Net 8 Service Name, if you choose an Oracle
    domain.

<!-- -->

-   Click the Save button, which appears on the sixth setup screen.
-   Click the Finish button, which appears on the last setup screen.

#### []{#The%20Multi-Tier%20Administrative%20Assistant} The Multi-Tier Administrative Assistant

OpenLink produces the Multi-Tier Administrative Assistant for all server
operating systems, which it supports. This Web-based assistant is
powered by OpenLink\'s server components, and it provides utilities to
configure these components. However, the assistant also provides a GUI
interface to the iODBC driver manager. This interface is similar to the
Microsoft ODBC Data Sources Administrator, and it allows users to create
OpenLink data source names.

Use the following instructions to create data source names with the
Multi-Tier Administrative Assistant.

-   cd into the /bin/w3config sub-directory of the server\'s OpenLink
    installation.
-   Use a text editor to open the www\_sv.ini file.
-   Locate the \[Startup\] section.
-   Record the value passed to HttpPort. For example:\

                      
        [Startup]
        HttpPort          = 8000

    \

-   Exit the file.
-   cd into the /bin sub-directory of the server\'s OpenLink
    installation.
-   Run the following command: oplrqb
-   Open a Web browser.
-   Enter the following URL:\

                      
        http://localhost:HttpPort_from_www_sv.ini

    \

-   Expand the following menu items: Client Components Administration
    -\> Data Source Name Configuration -\> Edit Data Sources by Wizard
    -\> Edit ODBC Data Sources.
-   Provide the administrator username and password. Both fields default
    to admin.
-   Click Add.
-   Select the OpenLink Generic ODBC driver.
-   Click Next.
-   Use setup screens 1 to 5 to provide connection parameters and to
    disable or enable optional features.

Figure 1-5 describes Multi-Tier parameters and options

-   Figure 1-5 - Multi-Tier Parameters & Options\*

  [Parameter](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=16&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=17&col=2)
  -------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Name                                                                                         Passes a descriptive data source title.
  Comment                                                                                      Passes a description of the use or nature of the data source name.
  Domain                                                                                       Passes a valid OpenLink domain alias. This domain alias must match a valid domain alias in the Multi-Tier oplrqb.ini file. The drivers use these domain aliases as starting points from which to assess rules, environment variables, and agent binaries to instantiate for connections.
  Hostname                                                                                     Passes the hostname or IP address of the machine, which contains the OpenLink request broker.
  Port                                                                                         Passes the TCP port, on which the request broker listens. This TCP port is associated with the ListenPort parameter, and it appears in the \[Protocol TCP\] section of the Multi-Tier Rules Book (oplrqb.ini).
  Protocol                                                                                     Passes a valid OpenLink network protocol. The default is TCP/IP.
  Database Name                                                                                Passes the name of a database or Oracle SID. Progress users should pass the full path to their databases.
  Server                                                                                       Passes Progress SHN sockets parameters. Users may also use the field to pass database native communications parameters to establish three-tier connections. For instance, users may pass Sybase instance names, Oracle aliases, or Ingres vnodes to connect database agents\--through local database native clients\--to remote databases.
  Username                                                                                     Passes a valid database username. If the Multi-Tier OPSYSLOGIN parameter is enabled, this parameter passes a valid operating system username.
  Read-only Connection                                                                         Passes a Yes or No value to enable or disable READONLY access to the data store.
  No Login Dialog Box                                                                          Enables or disables login popup box.
  Defer Fetching of long data                                                                  Passes a Yes or No value to enable or disable deferred fetching. Deferred fetching causes large, binary objects to be fetched after other, smaller data. This enhances performance.
  Row buffer size                                                                              Passes an integer, which represents the number of rows that the driver will return during an individual fetch.

-   Note:\* The Server parameter name changes to reflect the database to
    which you are trying to connect. For instance, the setup routine
    will replace Server with Net 8 Service Name, if you choose an Oracle
    domain.

<!-- -->

-   Click the Save button, which appears on the sixth setup screen.
-   Click the Finish button, which appears on the last setup screen.

#### []{#Configuring%20Mac%20Classic%20Data%20Source%20Names}Configuring Mac Classic Data Source Names

OpenLink Software provides Multi-Tier client software for the Mac
Classic operating system. The following instructions will enable users
to create Multi-Tier data source names on Mac Classic.

-   Expand the Apple menu.
-   Expand the Control Panels menu.
-   Select the ODBC Setup PPC menu item.
-   Click on the System DSN, User DSN, or File DSN tab.
-   Click Add.
-   Select the OpenLink Generic ODBC driver.
-   Click Finish.
-   Use the Generic ODBC Setup dialog to provide connection parameters
    and to disable or enable optional features. Figure 1-6 describes
    Multi-Tier parameters and options

<!-- -->

-   Figure 1-6 - Multi-Tier Parameters & Options\*

  [Parameter](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=18&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=19&col=2)
  -------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Name                                                                                         Passes a descriptive data source title.
  Comment                                                                                      Passes a description of the use or nature of the data source name.
  Domain                                                                                       Passes a valid OpenLink domain alias. This domain alias must match a valid domain alias in the Multi-Tier oplrqb.ini file. The drivers use these domain aliases as starting points from which to assess rules, environment variables, and agent binaries to instantiate for connections.
  Hostname                                                                                     Passes the hostname or IP address of the machine, which contains the OpenLink request broker.
  Port                                                                                         Passes the TCP port, on which the request broker listens. This TCP port is associated with the ListenPort parameter, and it appears in the \[Protocol TCP\] section of the Multi-Tier Rules Book (oplrqb.ini).
  Protocol                                                                                     Passes a valid OpenLink network protocol. The default is TCP/IP.
  Database Name                                                                                Passes the name of a database or Oracle SID. Progress users should pass the full path to their databases.
  Server                                                                                       Passes Progress SHN sockets parameters. Users may also use the field to pass database native communications parameters to establish three-tier connections. For instance, users may pass Sybase instance names, Oracle aliases, or Ingres vnodes to connect database agents\--through local database native clients\--to remote databases.
  Username                                                                                     Passes a valid database username. If the Multi-Tier OPSYSLOGIN parameter is enabled, this parameter passes a valid operating system username.
  Read-only Connection                                                                         Passes a Yes or No value to enable or disable READONLY access to the data store.
  No Login Dialog Box                                                                          Enables or disables login popup box.
  Defer Fetching of long data                                                                  Passes a Yes or No value to enable or disable deferred fetching. Deferred fetching causes large, binary objects to be fetched after other, smaller data. This enhances performance.
  Row buffer size                                                                              Passes an integer, which represents the number of rows that the driver will return during an individual fetch.

-   Note:\* The Optional Server parameter name changes to reflect the
    database to which you are trying to connect. For instance, the setup
    routine will replace Server with Net 8 Service Name, if you choose
    an Oracle domain.

<!-- -->

-   Click OK to save your data source name.

#### []{#Configuring%20Mac%20OS%20X%20Data%20Source%20Names}Configuring Mac OS X Data Source Names

There are two methods, which users may employ to configure Mac OS X data
source names. Expert users may configure the ODBC.preference file with
TextEdit or a similar text editor. Novice users may use an Aqua GUI ODBC
Administrator.

-   The ODBC.preference File\*

The ODBC.preference file appears in the /Library/Preferences directory.
Users may open this file with TextEdit or a similar text editor. The
following table describes sections, which users will encounter in
ODBC.preference.

  [Section](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=20&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=21&col=2)
  ------------------------------------------------------------------------------------------ ---------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ODBC Data Sources                                                                          This section names each of the ODBC data sources that appear in the ODBC.preference file. It also pairs the appropriate ODBC driver name with the data source name.
  Data Source Specifications                                                                 This section lists the actual data source names. Each data source name is composed of a formal name and a parameter list.

#### []{#ODBC%20Data%20Sources} ODBC Data Sources

The ODBC Data Sources section lists the names of the individual data
sources and pairs the names with the appropriate ODBC client driver.
These data sources names are associated with formal data source
specifications, which appear later in the file.

Here is the ODBC Data Sources format:

    [ODBC Data Sources]
    data_source_name=ODBC_client_driver_name

Here is a sample ODBC Data Sources section with data source names:

    [ODBC Data Sources]
    ora81_lite = OpenLink Oracle 8.1 Lite Driver (multi threaded)
    pgr7_lite  = OpenLink PostgreSQL Lite Driver (multi threaded)

#### []{#Data%20Source%20Specification} Data Source Specification

Each \[ODBC Data Sources\] data source name has a corresponding data
source specification. The data source specification lists parameters,
which are necessary to establish the ODBC connection. Here is the
OpenLink Multi-Tier data source specification format:

    [data_source_name]
    Driver = driver_path
    Description = data_source_description
    ServerType = openlink_domain_alias
    FetchBufferSize = buffer_size
    Host = hostname_of_machine_which_hosts_OpenLink_server_components
    Port = port_on_which_openlink_broker_listens
    Database = database_name_or_oracle_sid
    Protocol = network_communications_protocol
    Options = three_tier_or_sockets_connection_parameters
    ReadOnly = read_only_flag
    Username = database_username
    Password = database_password
    NoLoginBox = enable_disable_login_dialog_box
    DeferLongFetch = enable_disable_deferlongfetch_option

Here is a sample, Multi-Tier data source specification:

    [Oracle]
    Driver = /usr/openlink/lib/oplodbc.so.1
    Description = Oracle DSN
    ServerType = Oracle 8.1.x
    FetchBufferSize = 99
    Host = localhost
    Port = 5000
    Database = ORCL
    Protocol = TCP/IP
    Options = 
    ReadOnly = Yes
    Username = scott
    Password = tiger
    NoLoginBox = No
    DeferLongFetch = No

The following table explains the parameters that appear in the
Multi-Tier data source specification sections.

  [Parameter](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=22&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=23&col=2)
  -------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Name                                                                                         Passes a descriptive data source title.
  Comment                                                                                      Passes a description of the use or nature of the data source name.
  Domain                                                                                       Passes a valid OpenLink domain alias. This domain alias must match a valid domain alias in the Multi-Tier oplrqb.ini file. The drivers use these domain aliases as starting points from which to assess rules, environment variables, and agent binaries to instantiate for connections.
  Hostname                                                                                     Passes the hostname or IP address of the machine, which contains the OpenLink request broker.
  Port                                                                                         Passes the TCP port, on which the request broker listens. This TCP port is associated with the ListenPort parameter, and it appears in the \[Protocol TCP\] section of the Multi-Tier Rules Book (oplrqb.ini).
  Protocol                                                                                     Passes a valid OpenLink network protocol. The default is TCP/IP.
  Database Name                                                                                Passes the name of a database or Oracle SID. Progress users should pass the full path to their databases.
  Server                                                                                       Passes Progress SHN sockets parameters. Users may also use the field to pass database native communications parameters to establish three-tier connections. For instance, users may pass Sybase instance names, Oracle aliases, or Ingres vnodes to connect database agents\--through local database native clients\--to remote databases.
  Username                                                                                     Passes a valid database username. If the Multi-Tier OPSYSLOGIN parameter is enabled, this parameter passes a valid operating system username.
  Read-only Connection                                                                         Passes a Yes or No value to enable or disable READONLY access to the data store.
  No Login Dialog Box                                                                          Enables or disables login popup box.
  Defer Fetching of long data                                                                  Passes a Yes or No value to enable or disable deferred fetching. Deferred fetching causes large, binary objects to be fetched after other, smaller data. This enhances performance.
  Row buffer size                                                                              Passes an integer, which represents the number of rows that the driver will return during an individual fetch.

All OpenLink Single-Tier drivers recognize a common subset of
specifications parameters. Individual Single-Tier drivers recognize an
additional set of parameters, which are specialized for the database to
which they connect.

Here is a representative Single-Tier data source specification format:

    [data_source_name]
    Driver = driver_path
    Description = data_source_description
    Database =  database_name_or_oracle_sid
    Cursor_Sensitivity = enable_disable_dynamic_cursor_row_version_cache
    FetchBufferSize = buffer_size
    InitialSQL = path_to_script_containing_sql_statements
    UserName = database_username
    Password = database_password
    MaxRows = maximum_number_of_rows_to_return_per_resultset
    NoAutoCommit = enable_disable_autocommit
    NoLoginBox = enable_disable_login_dialog_box
    NoRowsetSizeLimit = enable_disable_norowsetsizelimit
    ReadOnly = enable_disable_read_only_access_to_database
    Options = three_tier_or_sockets_connection_parameters
    DeferLongFetch = enable_disable_deferlongfetch_option

Here is a sample, Single-Tier data source specification:

    [Oracle]
    Driver = /usr/openlink/lib/ora81_st_lt.sl
    Description = Oracle DSN
    Database = ORCL
    Cursor_Sensitivity = Yes
    FetchBufferSize = 99
    InitialSQL = 
    UserName = scott
    Password = tiger
    MaxRows = 
    NoAutoCommit = Yes
    NoLoginBox = No
    NoRowsetSizeLimit = Yes
    ReadOnly = Yes
    Options = 
    DeferLongFetch = No

The following table explains the parameters, which all Single-Tier
drivers recognize.

  [Parameter](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=24&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=25&col=2)
  -------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Data Source Name                                                                             Passes a descriptive data source title. This title must match the title passed under the \[ODBC Data Sources\] heading.
  Driver                                                                                       Passes the full path to the ODBC client driver.
  Description                                                                                  Passes a description of the use or nature of the data source name.
  Cursor\_Sensitivity                                                                          Passes a Yes or No value to enable or disable the row version cache, which is used with dynamic cursors.
  FetchBufferSize                                                                              Passes an integer, which represents the number of rows that the driver will return during individual fetch operations.
  InitialSQL                                                                                   Passes a path to a file containing SQL statements. These statements are issued against the database upon initial connection. InitialSQL scripts usually contain statements, which set ISOLATION levels.
  Username                                                                                     Passes a valid database username.
  Password                                                                                     Passes a valid database password
  MaxRows                                                                                      Passes an integer, which limits the maximum number of rows that may be returned.
  NoAutoCommit                                                                                 Passes a Yes or No value, which enables or disables the driver\'s autocommit behaviour.
  NoLoginBox                                                                                   Passes a Yes or No value to disable or enable the login pop-up box.
  NoRowsetSizeLimit                                                                            Passes a Yes or No value to enable or disable rowset size limits. Default rowset size limits are enforced by the cursor library. These limits prevent the driver from consuming all available memory in the event that rowsets are inordinately large.
  ReadOnly                                                                                     Passes a Yes or No value to enable or disable READONLY access to the data store.
  Options                                                                                      Passes Progress SHN sockets parameters. Users may also use the field to pass database native communications parameters to establish three-tier connections. For instance, users may pass Sybase instance names, Oracle aliases, or Ingres vnodes to connect database agents\--through local database native clients\--to remote databases.
  DeferLongFetch                                                                               Passes a Yes or No value to enable or disable deferred fetching. Deferred fetching causes large, binary objects to be fetched after other, smaller data. This enhances performance.

##### []{#MS%20SQL%20Server%20Single-Tier%20drivers%20recognize%20these%20specialized%20parameters.} MS SQL Server Single-Tier drivers recognize these specialized parameters.

  [Parameter](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=26&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=27&col=2)
  -------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------------
  TDSHost                                                                                      Passes the hostname or IP address of the machine that hosts SQLServer.
  TDSPort                                                                                      Passes the TCP port on which SQLServer listens.
  TDSVersion                                                                                   Passes the TDS Version specification number. Do not alter this value.
  SQLServerCatalog                                                                             Passes Yes to use Microsoft SQLServer implementation of catalog calls. Passes No to use Sybase implementation.

#####  MySQL Single-Tier drivers recognize these specialized parameters.

  [Parameter](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=28&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=29&col=2)
  -------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------
  Disable ODBC transactions                                                                    Disables transaction management. Enforces autocommit for all statements.

##### []{#Oracle%20Single-Tier%20drivers%20recognize%20these%20specialized%20parameters.} Oracle Single-Tier drivers recognize these specialized parameters.

  [Parameter](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=30&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=31&col=2)
  -------------------------------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  OraCatalogs                                                                                  Promotes efficient processing of Oracle catalog calls such as SQLForeignKey() and SQLPrimaryKeys(). The appropriate odbccat\#.sql script must be run before OraCatalogs is enabled. There is one odbccat\#.sql script for each Oracle database version.
  ShowRemarks                                                                                  Retrieves contents of SQLColumns REMARKS field.
  UserTblsFirst                                                                                Causes user tables to appear at beginning of SQLTables() table name listing.
  CountProcParms                                                                               Insures that number of parameters passed by stored procedures matches the number of parameters expected by SQLProcedures.
  OCIPrefetchRows                                                                              Passes an integer value, which represents the number of rows to prefetch.
  OCIPrefetchMemory                                                                            Passes an integer value, which represents the amount of memory to use for prefetch operations.
  OracleDirectory                                                                              Passes the full path to the Oracle home directory.

#####  PostgreSQL Single-Tier drivers recognize these specialized parameters.

  [Parameter](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=32&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=33&col=2)
  -------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------
  Disable ODBC transactions                                                                    Disables transaction management. Enforces autocommit for all statements.

#### []{#Aqua%20GUI%20ODBC%20Administrators} Aqua GUI ODBC Administrators

Users may encounter one of three, Aqua GUI ODBC administrators on Mac OS
X. Users may encounter the ODBC Administrator, the iODBC Administrator,
or Data Direct\'s ODBC Configure. Different driver managers are
installed by different OpenLink install bundles and client applications.

The ODBC Administrator ships with Apple\'s Jaguar installers. Users will
find the ODBC Administrator\'s icon in their /Applications/Utilities
folder. This administrator is an Apple-native interface to the iODBC
dylibs driver manager. Apple dylibs are dynamic shared libraries. One
copy of a .dylib or dynamic library may be shared by multiple
applications simultaneously. These libraries are similar in theory to
Unix dynamic libraries. However, their use and implementation are
different.

The iODBC Administrator ships with OpenLink Software\'s driver
installers. Users will find the iODBC Administrator\'s icon in their
/Applications folder. This administrator is an OpenLink-native interface
to the iODBC frameworks driver manager. Apple frameworks are special
bundles or packages, which contain dynamic shared libraries, header
files, documentation, and other resources that are necessary to use the
library.

The ODBC Configure administrator ships with Filemaker 6. Users will find
the ODBC Configure icon in /Applications/Data Direct ODBC Folder. This
administrator is a Data Direct-native interface to the Data Direct\'s
Carbon-based, CFM driver manager. Carbon is an older, Mac OS application
environment and API, which Apple modified for use with Mac OS X
operating systems. The CFM driver manager is based on Apple\'s CFM
technology. CFM is an abbreviation for Code Fragment Manager. The Code
Fragment Manager loads code fragments (libraries, applications, code,
etc.) and prepares them for execution.

The following instructions will enable users to create OpenLink data
sources using any ODBC administrator.

-   Open the appropriate administrator.
-   Click on the System, User, or File tab.
-   Click Add.
-   Select the appropriate OpenLink Single-Tier or Multi-Tier driver.
-   Click Finish.
-   Use the ODBC Setup dialog to provide connection parameters and to
    disable or enable optional features.

Figure 1-7 describes Multi-Tier parameters and options\*

-   Figure 1-7 - Multi-Tier Parameters & Options\*

  [Parameter](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=34&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=35&col=2)
  -------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Data Source Name                                                                             Passes a descriptive data source title. This title must match the title passed under the \[ODBC Data Sources\] heading.
  Driver                                                                                       Passes the full path to the ODBC client driver.
  Description                                                                                  Passes a description of the use or nature of the data source name.
  Cursor\_Sensitivity                                                                          Passes a Yes or No value to enable or disable the row version cache, which is used with dynamic cursors.
  FetchBufferSize                                                                              Passes an integer, which represents the number of rows that the driver will return during individual fetch operations.
  InitialSQL                                                                                   Passes a path to a file containing SQL statements. These statements are issued against the database upon initial connection. InitialSQL scripts usually contain statements, which set ISOLATION levels.
  Username                                                                                     Passes a valid database username.
  Password                                                                                     Passes a valid database password
  MaxRows                                                                                      Passes an integer, which limits the maximum number of rows that may be returned.
  NoAutoCommit                                                                                 Passes a Yes or No value, which enables or disables the driver\'s autocommit behaviour.
  NoLoginBox                                                                                   Passes a Yes or No value to disable or enable the login pop-up box.
  NoRowsetSizeLimit                                                                            Passes a Yes or No value to enable or disable rowset size limits. Default rowset size limits are enforced by the cursor library. These limits prevent the driver from consuming all available memory in the event that rowsets are inordinately large.
  ReadOnly                                                                                     Passes a Yes or No value to enable or disable READONLY access to the data store.
  Options                                                                                      Passes Progress SHN sockets parameters. Users may also use the field to pass database native communications parameters to establish three-tier connections. For instance, users may pass Sybase instance names, Oracle aliases, or Ingres vnodes to connect database agents\--through local database native clients\--to remote databases.
  DeferLongFetch                                                                               Passes a Yes or No value to enable or disable deferred fetching. Deferred fetching causes large, binary objects to be fetched after other, smaller data. This enhances performance.

\*Note:\* The optional Server parameter name changes to reflect the
database to which you are trying to connect. For instance, the setup
routine will replace Server with Net 8 Service Name, if you choose an
Oracle domain.

Figure 1-8 describes common Single-Tier parameters and options

\*Figure 1-8 - Common Single-Tier Parameters & Options\*

  [Parameter](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=36&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=37&col=2)
  -------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  DSN                                                                                          Passes a descriptive data source title.
  Description                                                                                  Passes a description of the use or nature of the data source name.
  Hostname                                                                                     Passes the hostname or IP address of the machine, which contains the database server.
  Port                                                                                         Passes the TCP port, on which the database server or PostgreSQL postmaster listens.
  Username                                                                                     Passes a valid database username.
  Password                                                                                     Passes a valid database password.
  Row buffer size                                                                              Passes an integer, which represents the number of rows that the driver will return during an individual fetch.
  Hide login dialog                                                                            Enables or disables the login popup box.
  Read only connection                                                                         Enables or disables READONLY access to the data store.
  Database                                                                                     Passes the name of a database or Oracle SID. Progress users should pass the full path to their databases.
  Initialization SQL                                                                           Passes a path to a file containing SQL statements. These statements are issued against the database upon initial connection. InitialSQL scripts usually contain statements, which set ISOLATION levels.
  Max rows override                                                                            Passes an integer, which represents the number of rows that the driver will return during individual fetch operations.
  Disable autocommit                                                                           Enables or disables the driver\'s autocommit behavior.
  Disable rowset size limit                                                                    Enables or disables rowset size limits. Default rowset size limits are enforced by the cursor library. These limits prevent the driver from consuming all available memory in the event that rowsets are inordinately large.
  High cursor sensitivity                                                                      Enables or disables the row version cache, which is used with dynamic cursors.
  Defer Fetching of long data                                                                  Enables or disables deferred fetching. Deferred fetching causes large, binary objects to be fetched after other data. This enhances performance.

Figure 1-9 describes additional, database specific Single-Tier
parameters and options.

-   Figure 1-9 - Database-Specific Single-Tier Parameters & Options\*

  [Parameter](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=38&col=1)   [Description](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCMacOSX?sort=39&col=2)
  -------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------
  Character Set                                                                                MS SQLServer/Sybase
  Enable Microsoft Jet Engine options                                                          MS SQLServer/Sybase
  Language                                                                                     MS SQLServer/Sybase
  Server Type                                                                                  MS SQLServer/Sybase
  Disable ODBC transactions                                                                    MySQL/PostgreSQL
  Count stored procedures parameters                                                           Oracle
  Custom catalog views                                                                         Oracle
  Net Service                                                                                  Oracle
  Net Service name                                                                             Oracle
  OCIPrefetch Memory                                                                           Oracle
  OCIPrefetch Rows                                                                             Oracle
  Oracle directory                                                                             Oracle
  Service name/SID                                                                             Oracle
  Show remarks                                                                                 Oracle
  Use Oracle 8i release 8.0 Compatible Identification                                          Oracle
  User\'s own tables first in SQLTables                                                        Oracle

-   Click OK to save your data source name.

### []{#Developing%20ODBC%20Compliant%20Applications} Developing ODBC Compliant Applications

OpenLink Software\'s Software Development Kits (SDK\'s) provide powerful
tools for Apple applications developers. While Apple SDK\'s provide only
the dylibs format driver manager, OpenLink\'s SDK\'s provide both the
dylibs and frameworks format driver managers. This distinction is
critical. The frameworks format driver manager provides the applications
developer with versatility that is not available with dylibs.

Frameworks bundles contain multiple revisions of the iODBC driver
manager. Moreover, the driver manager library name points to the latest
revision of the component. Therefore, developers do not need to set
environment variables to point to the appropriate file. However,
applications developers can choose to instantiate legacy revisions. In
other words, developers can hard link applications to older driver
managers to access functionality that is not present in recent
revisions.

Finally, OpenLink\'s SDK\'s enable developers to build Classic, Carbon,
and Cocoa native applications. Furthermore, OpenLink\'s SDK\'s assist
developers who need to migrate applications from the Classic API to
Carbon. And, OpenLink aids developers who need to compile applications,
which run on both Classic and Mac OS X. To proceed, developers simply
link their applications against OpenLink\'s iODBC libraries. The
resulting binary issues calls to the iODBC CFM Bridge. This bridge ships
with OpenLink\'s iODBC bundles, and it exists in Classic and OS X
formats. It identifies the correct driver manager format, which to load.

-   macodbc1.jpg:

![macodbc1.jpg](ODBCMacOSX/macodbc1.jpg)

###  OpenLink Driver Objectives

OpenLink Software\'s ODBC data access technologies simplify client and
server computing. These technologies are based on the principle of
interoperability. This principle dictates that one client application
can access diverse, back-end database management systems, without
knowledge of proprietary database protocols. Thereby, this powerful
technology allows application developers to develop, compile, and ship
applications, which speak to any, ODBC-compliant data source. The
application developer does not need to cater to any specific vendor\'s
DBMS. Moreover, application developers do not need to attend to any
specific client/server architecture. The application and DBMS may reside
on one or more machines. These machines may comprise similar or
dissimilar operating systems and hardware.

OpenLink Software\'s ODBC data access technologies meet their
objectives, because they are based on Microsoft\'s ODBC specification.
The specification defines the ability to:

-   Connect and disconnect to ODBC-compliant data sources.
-   Retrieve SQL data from ODBC data sources.
-   Obtain an ODBC driver\'s capabilities and characteristics.
-   Obtain and manipulate ODBC driver options.
-   Prepare and execute SQL statements.
-   Retrieve SQL result sets and process results dynamically.
-   Retrieve result metadata and process metadata dynamically

###  OpenLink Driver Features

OpenLink\'s Single-Tier and Multi-Tier Data Access Drivers provide ODBC
1.x-3.x compliance. The two driver formats also provide the following
features:

#### []{#Single-Tier%20Drivers} Single-Tier Drivers

-   Blistering performance
-   ODBC core, level 1, level 2, and extensions support
-   Client-based scrollable cursor support
-   Mac OS X client access to Microsoft SQL Server, MySQL, Oracle,
    PostgreSQL, and Sybase
-   Support for all network protocols and server operating environments,
    which are supported by the database vendors\' communications
    products.

<!-- -->

-   Note:\* Single-Tier data access is dependent upon client
    installation of the database native communications software. For
    example, Oracle users require a client side installation of Net8.
    Progress users require a client side installation of Progress Client
    Networking. OpenLink\'s drivers for Microsoft SQL Server and Sybase
    are an exception. These drivers contain FreeTDS libraries, which
    enable OpenLink\'s Single-Tier drivers to speak directly to
    Microsoft SQL Server and Sybase databases without Microsoft SQL
    Server\'s NETLIB or Sybase\'s Open Client product.

#### []{#Multi-Tier%20Drivers} Multi-Tier Drivers

-   Blistering performance
-   ODBC core, level 1, level 2, and extensions support
-   Built-in, database-independent communications layer
-   Sophisticated data encryption
-   Concurrent access to heterogeneous ODBC drivers
-   Intelligent metadata information handling
-   Array fetching
-   Network-centric result set management
-   Scrollable cursor support
-   Implementation of scrollable cursors across non-OpenLink ODBC
    drivers
-   Support for all native backend functionality
-   Support for distributed database capabilities of relevant backend
    database engines
-   Implementation of all inter-process communications mechanisms
    supported by relevant database engines. (Sockets, Shared Memory,
    Pipes etc.)
-   Enforcement of query optimizer configurations across all OpenLink
    client components
-   Enforcement of database engine ISOLATION LEVELS across all OpenLink
    client components.
:::
