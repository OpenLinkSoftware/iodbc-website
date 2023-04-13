<div id="content" class="topic-text" data-wv="http://www.openlinksw.com/Virtuoso/WikiV/" data-vi="http://www.openlinksw.com/virtuoso/xslt/" data-ie="http://www.openlinksw.com/Virtuoso/InclEng/" data-fn2="http://www.w3.org/2004/07/xpath-functions" data-xmlns="http://www.w3.org/1999/xhtml">

<div class="MACRO_TOC">

## Table of Contents

  - [Introduction](#Introduction)

  - [Releases](#Releases)

  -   - [Latest release: v1.1, April 2,
        2012](#Latest%20release%3A%20v1.1%2C%20April%202%2C%202012)
      - [Previous Release 1.0.0, November 4,
        2005](#Previous%20Release%201.0.0%2C%20November%204%2C%202005)
      - [Previous release: 0.99.21, June 6,
        2004](#Previous%20release%3A%200.99.21%2C%20June%206%2C%202004)

  - [HOWTO](#HOWTO)

  - [Git Access](#Git%20Access)

  - [Bug Fixes](#Bug%20Fixes)

  - [License](#License)

</div>

## <span id="Introduction"></span> Introduction

OpenLink ODBC Bench is an open-source ODBC Benchmarking tool providing
real-time comparative benchmarking for ODBC Drivers, Database Engines,
and Operating Systems combinations. The Benchmarks in this application
are loosely based on the TPC-A and TPC-C standard benchmarks, with
modifications to specifically test the performance of an ODBC Driver
and/or Database Engine in a client/server environment. The benchmark
results can be automatically stored to an ODBC Datasource or XML file
for further analysis and comparisons to be made.

## <span id="Releases"></span> Releases

All releases can be found on the SourceForge.net Project
[File-List](http://sourceforge.net/project/showfiles.php?group_id=90508)
page.

### <span id="Latest%20release%3A%20v1.1%2C%20April%202%2C%202012"></span> Latest release: v1.1, April 2, 2012

This release contains

  - Support for MacOS X 10.5 and 10.6
  - Converted MacOS X UI from NIB for XIB
  - Added initial ReadMe.rtf for Mac OS X 10.5 installer
  - Small bugfixes

Additionally, while files will continue to be hosted on sourceforge for
the time being, the project development hosting has moved to
[Github](https://github.com/openlink/odbc-bench).

Downloads:

  - [source v1.1
    tarball](http://sourceforge.net/projects/odbc-bench/files/odbc-bench/1.1/odbc-bench-1.1.tar.gz/download)
    (Sourceforge)
  - [MacOS X 10.5+
    installer](http://sourceforge.net/projects/odbc-bench/files/odbc-bench/1.1/ODBC-Bench-1.1-MacOSX-10.5-Universal.dmg/download)
    (Sourceforge)

### <span id="Previous%20Release%201.0.0%2C%20November%204%2C%202005"></span> Previous Release 1.0.0, November 4, 2005

This contains these improvements over previous releases:

  - added native Carbon support for MacOS X
  - various stability bug-fixes (concerning memory-allocation and saving
    of XML files)
  - various bug-fixes related to file-system case-sensitivity and
    directories with spaces in the name
  - documentation improvements

### <span id="Previous%20release%3A%200.99.21%2C%20June%206%2C%202004"></span> Previous release: 0.99.21, June 6, 2004

This was the first release of ODBC-Bench on SourceForge.net.

Download the [source
tarball](http://prdownloads.sourceforge.net/odbc-bench/odbc-bench-0.99.21.tar.gz?download)
from sourceforge.

## <span id="HOWTO"></span> HOWTO

[This
document](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/ODBCBenchHOWTO)
walks you through installing and using ODBC Bench.

## <span id="Git%20Access"></span>Git Access

To check out a copy of the Git repository, run

    $ git clone git://github.com/openlink/odbc-bench.git

Related pages:

  - [branching and development
    strategy](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/GitStrategy).
  - [iODBC Git
    Instructions](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/GitSource)
    including GPG keys for tag signing
  - [Quickstart and Tips
    Guide](http://virtuoso.openlinksw.com/dataspace/dav/wiki/Main/GitQuickstartTips)
    (virtuoso.openlinksw.com)

## <span id="Bug%20Fixes"></span> Bug Fixes

If you find a bug and have the know-how to fix it, please create a "diff
file" using GNU's "diff", preferably with "context" (diff -c or diff
-u).

If the patch is small, add the patch file as an attachment to your mail
if possible, otherwise tell us where we can pick it up. This will reduce
the turnaround time for new updates etc.

Patches and new contributions can be submitted as diffs from the current
archive by running the command: <span class="c1">git
format-patch</span>; these may then be emailed to the OpenLink iODBC
source archive manager at iodbc@openlinksw.com to be included the next
distribution. Please provide accompanying documentation on which bugs
are fixed or new features are introduced.

## <span id="License"></span> License

ODBC-Bench is licensed under the terms of the [GNU General Public
License](http://www.gnu.org/licenses/gpl.html) version 2.

</div>
