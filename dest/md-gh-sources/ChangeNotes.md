<div id="content" class="topic-text" data-wv="http://www.openlinksw.com/Virtuoso/WikiV/" data-vi="http://www.openlinksw.com/virtuoso/xslt/" data-ie="http://www.openlinksw.com/Virtuoso/InclEng/" data-fn2="http://www.w3.org/2004/07/xpath-functions" data-xmlns="http://www.w3.org/1999/xhtml">

<div class="MACRO_TOC">

## Table of Contents

  - [2021-06-07 - iODBC Stable Version 3.52.15
    Released](#2021-06-07%20-%20iODBC%20Stable%20Version%203.52.15%20Released)
  - [2021-02-17 - iODBC Stable Version 3.52.14
    Released](#2021-02-17%20-%20iODBC%20Stable%20Version%203.52.14%20Released)
  - [2019-07-23 - iODBC Stable Version 3.52.13
    Released](#2019-07-23%20-%20iODBC%20Stable%20Version%203.52.13%20Released)
  - [2016-07-12 - iODBC Stable Version 3.52.12
    Released](#2016-07-12%20-%20iODBC%20Stable%20Version%203.52.12%20Released)
  - [2016-05-25 - iODBC Internal Version 3.52.11
    Released](#2016-05-25%20-%20iODBC%20Internal%20Version%203.52.11%20Released)
  - [2015-02-12 - iODBC Stable Version 3.52.10
    Released](#2015-02-12%20-%20iODBC%20Stable%20Version%203.52.10%20Released)
  - [2014-04-15 - iODBC Stable Version 3.52.9
    Released](#2014-04-15%20-%20iODBC%20Stable%20Version%203.52.9%20Released)
  - [2012-03-27 - iODBC Stable Version 3.52.8
    Released](#2012-03-27%20-%20iODBC%20Stable%20Version%203.52.8%20Released)
  - [2009-09-11 - iODBC Stable Version 3.52.7
    Released](#2009-09-11%20-%20iODBC%20Stable%20Version%203.52.7%20Released)
  - [2007-01-05 - iODBC Stable Version 3.52.6
    Released](#2007-01-05%20-%20iODBC%20Stable%20Version%203.52.6%20Released)
  - [2006-01-27 - iODBC Stable Version 3.52.5
    Released](#2006-01-27%20-%20iODBC%20Stable%20Version%203.52.5%20Released)
  - [2005-11-07 - iODBC Stable Version 3.52.4
    Released](#2005-11-07%20-%20iODBC%20Stable%20Version%203.52.4%20Released)
  - [2005-02-07 - iODBC Stable Version 3.52.3
    Released](#2005-02-07%20-%20iODBC%20Stable%20Version%203.52.3%20Released)
  - [2004-02-28 - iODBC Version 3.52.2 Source
    Released](#2004-02-28%20-%20iODBC%20Version%203.52.2%20Source%20Released)
  - [2003-09-08 - iODBC Version 3.52.1 Source
    Released](#2003-09-08%20-%20iODBC%20Version%203.52.1%20Source%20Released)
  - [2003-08-22 - iODBC Version 3.51.2 Source
    Released](#2003-08-22%20-%20iODBC%20Version%203.51.2%20Source%20Released)
  - [2002-04-29 - iODBC Version 3.51.1 Source
    Released](#2002-04-29%20-%20iODBC%20Version%203.51.1%20Source%20Released)
  - [2003-08-22 - iODBC Version 3.51.0 Source
    Released](#2003-08-22%20-%20iODBC%20Version%203.51.0%20Source%20Released)
  - [2002-04-29 - iODBC 3.0.6 Source
    Release](#2002-04-29%20-%20iODBC%203.0.6%20Source%20Release)
  - [2001-06-12 - iODBC 3.0.5 Source
    Release](#2001-06-12%20-%20iODBC%203.0.5%20Source%20Release)
  - [2000-08-25 - iODBC 3.0.4 Source
    Release](#2000-08-25%20-%20iODBC%203.0.4%20Source%20Release)
  - [2000-08-09 - iODBC 3.0.3 Source
    Release](#2000-08-09%20-%20iODBC%203.0.3%20Source%20Release)
  - [2000-08-09 - iODBC 3.0.3 Linux Binary
    Release](#2000-08-09%20-%20iODBC%203.0.3%20Linux%20Binary%20Release)
  - [2000-02-01 - iODBC Development Version 3.0.2
    Release](#2000-02-01%20-%20iODBC%20Development%20Version%203.0.2%20Release)
  - [2000-01-28 - iODBC Development Version 3.0.1
    Release](#2000-01-28%20-%20iODBC%20Development%20Version%203.0.1%20Release)
  - [1999-12-16 - iODBC Development Version 3.0.0
    Release](#1999-12-16%20-%20iODBC%20Development%20Version%203.0.0%20Release)

</div>

## <span id="2021-06-07%20-%20iODBC%20Stable%20Version%203.52.15%20Released"></span> 2021-06-07 - iODBC Stable Version 3.52.15 Released

  - Added support for macOS Big Sur (11.x) on Apple Silicon using a
    universal build
  - Fixed title to show CPU architecture used
  - Fixed length of error message buffer
  - Removed support for Mac OS X Snow Leopard (10.6) and older
  - Removed deprecated `iODBCcfmbridge` for PPC
  - Upgraded iODBC build to use recent versions of Xcode
      - Minimum Xcode version is set to Xcode 8.0
      - Minimum macOS deployment target is OS X Mavericks (10.9)
      - Migrated dialogs and `plist` files
      - Migrated translation support

Please continue sending your suggestions, questions and/or patches to
the Archive Maintainer at iodbc@openlinksw.com

## <span id="2021-02-17%20-%20iODBC%20Stable%20Version%203.52.14%20Released"></span> 2021-02-17 - iODBC Stable Version 3.52.14 Released

  - Fixed: `SQLSetEnvAttr` doesn't return `SQL_SUCCESS` for option
    `SQL_ATTR_APP_UNICODE_TYPE`
  - Fixed: issue with switching ODBC driver to best supported Unicode
    codepage
  - Fixed: misprint in `SQLBrowseConnect`
  - Fixed: `SQLGetConnectOption returned wrong value for
    SQL_CURRENT_QUALIFIER`
  - Fixed: mixing calls to `SQLFetchScroll` with `SQLFetch`
  - Fixed: Misc Unicode issues

## <span id="2019-07-23%20-%20iODBC%20Stable%20Version%203.52.13%20Released"></span> 2019-07-23 - iODBC Stable Version 3.52.13 Released

  - Added extra validation for `SQLAllocHandle (SQL_HANDLE_DESC, ...)`
  - Added GCC `__attribute__` for checking format string
  - Added missing define `SQL_CONVERT_GUID`
  - Fixed issue using heap after free in `SQLConnect_internal`
  - Fixed issue with global mutex in `SQLError`, `SQLGetDiagRec`, and
    `SQLGetDiagField`
  - Fixed `SQLSetStmtAttr` to cache the correct values for
    `SQL_ATTR_ROW_ARRAY_SIZE` and `SQL_ATTR_ROW_BIND_TYPE`
  - Fixed format specifiers and some casts to fix trace output
  - Fixed missing check for section in `SQLGetPrivateProfileString`
  - Fixed non-void function needs to return a value
  - Fixed issue in Mac Cocoa code
  - Fixed iODBC apps/frameworks `CFBundleGetInfoString` attribute
  - Fixes an issue where build fails on Alpine
  - Fixed package versioning
  - Fixed small memory leaks

## <span id="2016-07-12%20-%20iODBC%20Stable%20Version%203.52.12%20Released"></span> 2016-07-12 - iODBC Stable Version 3.52.12 Released

  - Added new Cocoa based dialogs for Mac OS X to allow 64-bit
    applications to use the standard Login and Setup dialogs from the
    `iODBCinst` framework
  - Added 64-bit version of the iODBC Administrator to configure and
    test DSNs on drivers that are only available in 64-bit format
  - Fixed User DSN support for recent versions of Microsoft Excel and
    Query on macOS
  - Documentation fixes

## <span id="2016-05-25%20-%20iODBC%20Internal%20Version%203.52.11%20Released"></span> 2016-05-25 - iODBC Internal Version 3.52.11 Released

  - Added `xcodebuild` option for OS X El Capitan (10.11)
  - Added support for x86\_64 to iODBC Demo
  - Fix crash ODBCdemo - error message overwrite stack data
  - Fix iODBCdemo issue with UID/PWD values
  - Fixed crash in iODBC DM on push of "Test" button when 64-bit ODBC
    driver is used
  - Fixed crash when `create_dsnsetup` fails to load the window
  - Fixed crash when passing an empty connect string with no window
    handle
  - Fixed `iODBCadm` and `iODBCdrvproxy` Development build errors on OS
    X
  - Fixed `iODBCdrvproxy` XIBs not compiling to NIBs on OS X
  - Fixed issue in `SQLGetInfo`
  - Fixed issue with Xcode 7.2.1 on OS X Yosemite (10.10)
  - Fixed use only major.minor of macOS version to configure flags

## <span id="2015-02-12%20-%20iODBC%20Stable%20Version%203.52.10%20Released"></span> 2015-02-12 - iODBC Stable Version 3.52.10 Released

  - Fixed issue with `~/Library/ODBC/odbc[inst].ini` on macOS
  - Added build support for macOS 10.10
  - Updated iODBC Administrator
  - Updated iODBC Demo
  - Fixed string truncation in Unicode \<-\> Ansi conversion on some API
    calls

## <span id="2014-04-15%20-%20iODBC%20Stable%20Version%203.52.9%20Released"></span> 2014-04-15 - iODBC Stable Version 3.52.9 Released

  - Added support for building on recent versions of Mac OS X
  - Fixed warnings from `autoconf`/`automake`
  - Fixed infinite loop in connection pool
  - Fixed compiler warnings
  - Fixed build dependency for `make -jX`
  - Fixed check for Unicode driver
  - Fixed issue calling `SQLCancel` from other thread
  - Fixed `SQLInstallDriverEx` when driver is readonly

## <span id="2012-03-27%20-%20iODBC%20Stable%20Version%203.52.8%20Released"></span> 2012-03-27 - iODBC Stable Version 3.52.8 Released

  - Added support for Mac OS X 10.7
  - Added Mac OS X build files to ignore list
  - Added initial `.gitignore`
  - Added more files to ignore
  - Converted build rules to compile the UI from new `.xib` files
  - Converted old `.nib` format to `.xib` format
  - Fixed list of files to be distributed
  - Fixed problem installing `CFMSupport`
  - Updated version of iODBC Demo to 1.1

## <span id="2009-09-11%20-%20iODBC%20Stable%20Version%203.52.7%20Released"></span> 2009-09-11 - iODBC Stable Version 3.52.7 Released

  - Added iODBC Graphical Administrator for Mac OS X
  - Added iODBC CFM Bridge
  - Added resizable windows and dialogs for GTK+
  - Added option in `tracefile` for sequence number (`$S`)
  - Added additional translations between ANSI and Unicode
  - Fixed if tracefile gets too big, continue in new tracefile
  - Fixed unload bug due to wrong pointer deref
  - Fixed Connection Pooling UI
  - Fixed checking `odbc_ver` on connect handle
  - Fixed packaging of runtime only libraries
  - Fixed porting issues
  - Fixed documentation

## <span id="2007-01-05%20-%20iODBC%20Stable%20Version%203.52.6%20Released"></span> 2007-01-05 - iODBC Stable Version 3.52.6 Released

  - Added support for GTK+ 2.x
  - Fixed long mutex lock on connect
  - Fixed problems with `SQLBrowseConnect`
  - Fixed missing functions in export list
  - Fixed core dump when checking for driver odbc version
  - Fixed allocation error in `SQLDescribeCol`
  - Fixed rpm specification for RedHat
  - Fixed porting problems on FreeBSD, OpenBSD and OSF
  - Use `SQLFetchScroll` in `iodbctest`

## <span id="2006-01-27%20-%20iODBC%20Stable%20Version%203.52.5%20Released"></span> 2006-01-27 - iODBC Stable Version 3.52.5 Released

  - Added support for File DSN
  - Added support for Connection Pooling
  - Added check for tracefile size
  - Call ODBC 2.x functions in driver if application uses ODBC 2.x only
    calls
  - Fixed problem parsing driver result in `SQLSetStmtAttr`
  - Fixed source code readability
  - Fixed bug in overwriting driver name
  - Fixed check for `/Library/ODBC` for Mac OS X
  - Fixed prototypes
  - Rewrote bootstrap script and configure summary
  - Use `localtime_r` in tracing when available
  - Fixed build issues with Mac OS X
  - Small code cleanups and fixes

## <span id="2005-11-07%20-%20iODBC%20Stable%20Version%203.52.4%20Released"></span> 2005-11-07 - iODBC Stable Version 3.52.4 Released

  - Added support for Mac OS X 10.4 Universal kit (ppc, ppc64, and i386)
  - Removed dependency between `iodbc` and `iodbcinst` shared libraries
  - Cleanups to the build process particularly on MacOS X
  - Clarification on LGPL license conditions
  - Bugfix: error on subsequent `SQLExecute` statements
  - Fixed problem building 64-bit GUI components
  - Fixed problem determining which compiler to use on AIX
  - Enabled `SHLIB_PATH` on HP/UX
  - Fixed problem using `#` as comment in `odbc.ini` file
  - Disabled `--disable-odbc3` flag
  - Small code cleanups and fixes

## <span id="2005-02-07%20-%20iODBC%20Stable%20Version%203.52.3%20Released"></span> 2005-02-07 - iODBC Stable Version 3.52.3 Released

  - Added support for DSN-less connections
  - Added timestamp to `ENTER`/`EXIT` lines in trace file
  - Added build support for AIX 5.x, HP/UX 11.23 IA\_64
  - Added build support for Mac OS X 10.3 (32-bit) and 10.4 (32-bit +
    64-bit)
  - Fixed problem with `SQLDriverConnect (SQL_DRIVER_PROMPT)` if no
    setup dialog had been registered
  - Fixed symbol-clash between Oracle Instant client and iODBC on Mac OS
    X
  - Various small build fixes
  - Various stability bug-fixes

## <span id="2004-02-28%20-%20iODBC%20Version%203.52.2%20Source%20Released"></span> 2004-02-28 - iODBC Version 3.52.2 Source Released

  - Added tracing option for root without overwriting existing files
  - Added `PORT.OpenLink` script
  - Added special `iodbc-config` script for Mac OS X framework build
  - Fixed problem starting/stopping tracing
  - Fixed `SQLSetConnectAttr` to return `SQL_SUCCESS_WITH_INFO` if
    driver cannot handle option set before connect time
  - Fixed `SQLInfo` to use `pcbInfoValue` if present
  - Fixed `NULL` pointer problem in GTK choose driver dialog
  - Fixed problem with C++ prototypes with older 32-bit code
  - Fixed locking problem with `SQLAllocEnv`/`SQLAllocHandle`
  - Fixed tracefile name expansion
  - Fixed problem running `bootstrap.sh` on machines without GTK
  - Fixed problem installing code in temp directory for packaging
  - Fixed problem calling `SQLGetDiagRec` on uninitialized handles in
    `iodbctest` program
  - Link `iodbctest` program with static `iodbc` libraries

## <span id="2003-09-08%20-%20iODBC%20Version%203.52.1%20Source%20Released"></span> 2003-09-08 - iODBC Version 3.52.1 Source Released

  - Added support for new ODBC 3.52 specification for 64-bit
    environments
  - Added support for `SQLGetEnvAttr(SQL_ATTR_WCHAR_SIZE)` extension
  - Added missing Mac OS X build files
  - Added script to symlink Mac OS X framework into `/usr/local/iODBC`
    to allow traditional GNU configurable packages to use the same
    version of iODBC
  - Added new layer to driver loading to prevent memory leaks when
    drivers cannot be physically unloaded
  - Added man pages for `iodbc-config`, `iodbctest`, and `iodbcadm-gtk`
  - Added header file `iodbcunix.h` for portability
  - Enhanced tracing for `SQLGetFunctions`, `SQLColAttribute`
  - Fixed `NULL` pointer problem when connection failed
  - Fixed initialization problem with `SQLGetPrivateProfileString`
  - Fixed export Unicode and ANSI names of ODBC functions in `libiodbc`
  - Fixed `SQLSetScrollOption` emulation
  - Fixed tracing for `SQLSetDescRec`
  - Fixed rpm build issue with RedHat 9
  - Fixed Mac OS X install problem
  - Fixed Mac OS X build dependency on Carbon libraries
  - Fixed HP/UX shared library name handling
  - Fixed handling of UTF-8 sequences
  - Fixed compiler warnings
  - Small code cleanups and fixes

## <span id="2003-08-22%20-%20iODBC%20Version%203.51.2%20Source%20Released"></span> 2003-08-22 - iODBC Version 3.51.2 Source Released

  - Added support for installation layouts for different distributions,
    e.g., `--with-layout=RedHat`
  - Added support for Mac OS X 10.3 (Panther)
  - Added support for creating `libodbc.so` symlink
  - Added more ODBC 3.x calls to `iodbctest.c` program
  - Added `SQLRowCount` for SQL `UPDATE`/`DELETE` statements in
    `iodbctest.c`
  - Fixed build problem with older `make` programs
  - Fixed bug in state handling `SQLCloseCursor`
  - Fixed driver statement allocation problem
  - Fixed double free in statement handle
  - Fixed problem tracing variable length strings and binary data
  - Use `snprintf` when available to guard against buffer overruns
  - Small documentation fixes

## <span id="2002-04-29%20-%20iODBC%20Version%203.51.1%20Source%20Released"></span> 2002-04-29 - iODBC Version 3.51.1 Source Released

  - Release of GTK-based Administrator component
  - Improved API tracing functionality (improvement is trace
    granularity)
  - New `SQLDrivers()` API implementation
  - Upgrade to `libtool-1.4.3`
  - Reworked SRPM `.spec-file` to aid co-existence with other managers
  - Improved ./configure and GTK support for FreeBSD and MacOS X
  - Reinstated `libiodbc.so` dependency on `libiodbcinst.so`
  - State-transition fixes for
    `SQLFetch`/`SQLExecDirect`/`SQLMoreResults`
  - Tidied ini-file- and connection-string-parsing functions
  - Added a `README.CVS`
  - Symbol-clash removal

## <span id="2003-08-22%20-%20iODBC%20Version%203.51.0%20Source%20Released"></span> 2003-08-22 - iODBC Version 3.51.0 Source Released

  - Unicode support
  - Updated ODBC tracing support
  - Updated threading model
  - Improved graphical Administration (GTK) interface
  - General Bug fixes

## <span id="2002-04-29%20-%20iODBC%203.0.6%20Source%20Release"></span> 2002-04-29 - iODBC 3.0.6 Source Release

  - Mac OS X support
  - Portability fixes
  - Small bug fixes

## <span id="2001-06-12%20-%20iODBC%203.0.5%20Source%20Release"></span> 2001-06-12 - iODBC 3.0.5 Source Release

  - Portability fixes
  - Small bug fixes
  - CVS archive integration

## <span id="2000-08-25%20-%20iODBC%203.0.4%20Source%20Release"></span> 2000-08-25 - iODBC 3.0.4 Source Release

  - This release was a source release only.

## <span id="2000-08-09%20-%20iODBC%203.0.3%20Source%20Release"></span> 2000-08-09 - iODBC 3.0.3 Source Release

  - Full source code for GTK GUI based iODBC Administrator for
    interactive administration of ODBC DSNs

## <span id="2000-08-09%20-%20iODBC%203.0.3%20Linux%20Binary%20Release"></span> 2000-08-09 - iODBC 3.0.3 Linux Binary Release

  - GTK GUI based iODBC Administrator for interactive administration of
    ODBC DSNs

## <span id="2000-02-01%20-%20iODBC%20Development%20Version%203.0.2%20Release"></span> 2000-02-01 - iODBC Development Version 3.0.2 Release

  - `SQLGetData` returned `SQLSTATE 24000` error as internal
    `SQLNumResultCols` call deadlocked
  - `SQLDatasources` argument check was wrong

## <span id="2000-01-28%20-%20iODBC%20Development%20Version%203.0.1%20Release"></span> 2000-01-28 - iODBC Development Version 3.0.1 Release

  - Added code to make Driver Manager thread safe
  - Added code to call non thread-safe drivers from thread safe
    applications
  - Small bug fixes and code cleanups

## <span id="1999-12-16%20-%20iODBC%20Development%20Version%203.0.0%20Release"></span> 1999-12-16 - iODBC Development Version 3.0.0 Release

  - ODBC 3.x support and the ODBC 3.x to 2.x translation layer
  - Support for more platforms including Mac OS X (Rhapsody)
  - Small bug fixes and code cleanups

</div>
