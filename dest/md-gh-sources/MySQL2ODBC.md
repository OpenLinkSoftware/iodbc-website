<div id="content" class="topic-text" data-wv="http://www.openlinksw.com/Virtuoso/WikiV/" data-vi="http://www.openlinksw.com/virtuoso/xslt/" data-ie="http://www.openlinksw.com/Virtuoso/InclEng/" data-fn2="http://www.w3.org/2004/07/xpath-functions" data-xmlns="http://www.w3.org/1999/xhtml">

<div class="MACRO_TOC">

## Table of Contents

  - [Introduction](#Introduction)

  -   - [What Is It?](#What%20Is%20It%3F)
      - [Why?](#Why%3F)
      - [Benefits](#Benefits)

  - [HOWTO](#HOWTO)

  -   - [Method](#Method)
    
      -   - [Building](#Building)
          - [Deploying](#Deploying)

  - [Download & License](#Download%20%26%20License)

</div>

## <span id="Introduction"></span> Introduction

### <span id="What%20Is%20It%3F"></span> What Is It?

[MySQL2ODBC](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/MySQL2ODBC)
is a library for intercepting MySQL API calls and redirecting them via
ODBC.

### <span id="Why%3F"></span> Why?

Historically the open-source community has produced many useful
applications tied to the LAMP stack (Linux, Apache, MySQL and PHP) or
similar variants. Often, however, the reliance on MySQL as the database
layer of choice has been baked-in with little scope for substituting
another RDBMS.

On the other hand, ODBC has long provided flexible choice of backend
RDBMS - by talking ODBC, an application can switch between PostgreSQL,
MySQL, Oracle, SQL Server, OpenLink Virtuoso and many more at will.

[MySQL2ODBC](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/MySQL2ODBC)
is one way to break free of vendor lock-in and restore
database-independence via ODBC :)

### <span id="Benefits"></span> Benefits

  - Cost-Effectiveness -
    [MySQL2ODBC](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/MySQL2ODBC)
    saves having to rewrite the whole database access layer in a
    potentially large application
  - Database-Independence: Freedom of Choice

## <span id="HOWTO"></span> HOWTO

[MySQL2ODBC](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/MySQL2ODBC)
provides a substitute libmysqlclient library.

### <span id="Method"></span> Method

#### <span id="Building"></span> Building [MySQL2ODBC](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/MySQL2ODBC)

  - Download mysql2odbc-0.99.2.tar.gz
  - unpack it somewhere in your usual source directory tar xvpfz
    mysql2odbc-0.99.2.tar.gz
  - check the options to configure by running `./configure --help` - you
    can choose which ODBC Driver Manager to work with, either unixODBC
    or iODBC
  - ./configure --with-iodbc=/usr/local/iodbc
    --prefix=/usr/local/mysql2odbc
  - make
  - sudo make install

#### <span id="Deploying"></span> Deploying [MySQL2ODBC](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/MySQL2ODBC)

Your application needs to be told to use the
[MySQL2ODBC](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/MySQL2ODBC)
implementation of libmysqlclient in preference to the existing version.
To do this, either

export LD\_LIBRARY\_PATH=/usr/local/mysql2odbc/lib

or

export LD\_PRELOAD=/usr/local/mysql2odbc/lib/libmysqlclient.so

and restart the application. You might want to create a shell-script
wrapper to preserve this.

## <span id="Download%20%26%20License"></span> Download & License

The source can be downloaded from github as a zip archive: [MySQL2ODBC
source
zip](https://github.com/openlink/mysql2odbc/archive/refs/heads/develop.zip).

Alternatively you can clone the repository:

git clone https://github.com/openlink/mysql2odbc.git

The project is licensed under the terms of the GNU [Library General
Public License (LGPL)
v2](https://www.gnu.org/licenses/old-licenses/lgpl-2.0.html).

Patches are welcomed - please either send us a merge request via github
or email the OpenLink iODBC source archive manager at
<iodbc@openlinksw.com>, including documentation. Thank you for your
contributions :)

</div>
