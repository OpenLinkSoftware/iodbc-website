::: {#content .topic-text wv="http://www.openlinksw.com/Virtuoso/WikiV/" vi="http://www.openlinksw.com/virtuoso/xslt/" ie="http://www.openlinksw.com/Virtuoso/InclEng/" fn2="http://www.w3.org/2004/07/xpath-functions" xmlns="http://www.w3.org/1999/xhtml"}
::: {.MACRO_TOC}
Table of Contents {#table-of-contents .toc}
-----------------

-   [Getting Started](#Getting%20Started)
-   [Bug Fixes](#Bug%20Fixes)
-   [Suggestions](#Suggestions)
-   [Standards Enforcement](#Standards%20Enforcement)
-   [Project Management](#Project%20Management)
-   [Development Standards](#Development%20Standards)
:::

[]{#Getting%20Started}Getting Started
-------------------------------------

-   Download relevant source code release
-   Build and test on desired platforms

Note: If in either one of the steps above you stumble across any
problems/bugs, please contact the OpenLink iODBC source archive manager
at iodbc\@openlinksw.com . Please provide as much information regarding
the type of platform, compiler, compiler flags etc. in your bug report,
we will try to get back in touch with you rapidly.

[]{#Bug%20Fixes}Bug Fixes
-------------------------

If you find a bug and have the know-how to fix it, please create a
\"diff file\" using GNU\'s \"diff\", possibly with \"context\" (diff -c
or diff -u).

If the patch is small, add the patch file as an attachment to your mail
if possible, otherwise tell us where we can pick it up. This will reduce
the turnaround time for new updates etc.

[]{#Suggestions}Suggestions
---------------------------

Suggestions for new features can be discussed with us, through one of
the following forums:

-   Using the Sourceforge.net
    [mailing-lists](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/MailingLists){.wikiword}.
-   Using OpenLink\'s support phpBB [discussion
    forum](http://boards.openlinksw.com/support/viewforum.php?f=4){.absuri}
    for general ODBC questions
-   Direct e-mail to iodbc\@openlinksw.com

Ideas are welcome at all times; ideas accompanied by the code that
demonstrates core concepts are even more welcome.

[]{#Standards%20Enforcement}Standards Enforcement
-------------------------------------------------

This initiative\'s greatest value is the provision of a cross-platform
development interface that conforms to both the Microsoft ODBC and
X/Open SQL CLI data access specifications. Thus, ensure that code
contributions do not compromise this prime objective.

We will adhere to the official Microsoft ODBC and X/Open SQL CLI specs
at all times.

[]{#Project%20Management}Project Management
-------------------------------------------

If you want to contribute news ideas and functionality, please talk to
us on either the
[mailing-lists](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/MailingLists){.wikiword}
or [discussion
forum](http://boards.openlinksw.com/support/viewforum.php?f=4){.absuri}
in advance, as this reduces the chance of development overlaps.

[]{#Development%20Standards}Development Standards
-------------------------------------------------

All iODBC Driver Manager development needs to be done in ANSI C to
ensure the best cross platform compatibility. Code submissions need to
be properly indented (we use the GNU \'indent\' program) and commented
in order to make group development as productive as possible.
:::
