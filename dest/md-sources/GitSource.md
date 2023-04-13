::: {#content .topic-text wv="http://www.openlinksw.com/Virtuoso/WikiV/" vi="http://www.openlinksw.com/virtuoso/xslt/" ie="http://www.openlinksw.com/Virtuoso/InclEng/" fn2="http://www.w3.org/2004/07/xpath-functions" xmlns="http://www.w3.org/1999/xhtml"}
::: {.MACRO_TOC}
Table of Contents {#table-of-contents .toc}
-----------------

-   [Introduction](#Introduction)
-   [Git Archive Server Access](#Git%20Archive%20Server%20Access)
-   -   [GitHub](#GitHub)
    -   [SourceForge](#SourceForge)

-   [Git Tag-Signing Key](#Git%20Tag-Signing%20Key)
-   [Further Documentation](#Further%20Documentation)
:::

[]{#Introduction} Introduction
------------------------------

Developers who want to actively track progress of the iODBC source code
and contribute bugfixes or enhancements to the project need Git access.

This access requires basic knowledge of git itself; the general layout
of open source and GNU projects; the use of autoconf and automake; and
other things which are beyond the scope of this document.

If you have any questions, please email the \<none\>.

[]{#Git%20Archive%20Server%20Access} Git Archive Server Access
--------------------------------------------------------------

### []{#GitHub}GitHub

For main development, we will publish the iODBC open-source tree to
[GitHub](http://github.com/){.absuri}. We encourage everyone who is
interested in tracking the project to make an account there.

Users who mainly just want to look at the code can use the [GitHub Web
interface](https://github.com/openlink/iODBC){.absuri} or track the
archive by checking out a local copy of the tree, with a command such
as:

    $ git clone git://github.com/openlink/iODBC.git

At this point, you can create your own work-branch based on any
available branch; create bugfixes; commit them to your own branch; and
then use the command `git       format-patch` to generate appropriate
diffs to email to the \<none\>.

Developers are encouraged to fork the project using GitHub; create your
own branches to make enhancements/bugfixes; and then send pull requests
using the excellent GitHub interface, so we can examine and incorporate
those fixes into the master tree for future release.

For more information, please read the [GitHub
Documentation](http://help.github.com/){.absuri} on how to fork a
project, send pull requests, track a project, etc.

### []{#SourceForge}SourceForge

OpenLink will continue to use
[sourceforge.net](http://sourceforge.net/projects/iodbc/){.absuri} to
release source tarballs and certain binaries.

SourceForge also contains the frozen [CVS
Archive](http://virtuoso.cvs.sourceforge.net/viewvc/virtuoso/virtuoso-opensource/){.absuri}
for historical reference, and for completeness, read-only [Git
Archive](http://virtuoso.git.sourceforge.net/git/gitweb.cgi?p=virtuoso/virtuoso-opensource){.absuri}
access will also be available there.

For more information, please see the [SourceForge Git
Documentation](https://sourceforge.net/scm/?type=git&group_id=161622){.absuri}.

[]{#Git%20Tag-Signing%20Key}Git Tag-Signing Key
-----------------------------------------------

To verify signed releases, you should import our Git public GPG key,
either by:

-   running\

                      
        $ gpg --recv-keys 089DE67A

    \

-   or by downloading the attached `089DE67A.asc` file, and running\

                      
        $ gpg --import 089DE67A.asc

    \

-   or by running\

                      
        $ echo '-----BEGIN PGP PUBLIC KEY BLOCK-----

        mQENBE9pILIBCACpRFwsoYwyfswRt7QMWtifJb/L1Zo9955pKyOnnI/vZ2S2uFv0
        OALpyUoR/WhQzIrtmzVYfBSmmBhAr5sh05tcXjFmyulhecAllYfaNAHEYAfgczaj
        7TMYkHOd4xU2dl2PEPpWYaQJ/tuokZICC5BBakpHDN12TUrZTyCe1qEUgJvM6e3A
        8BAwZSB9wbdwhxVwZEbeNYcINsBXL9kc/oy0v61XEIr17n/GS2Lmh533XP97kTz5
        IJhTwrGf3lQUpEYRWptepUI2bnBSO3ZJ8G4x5w4ESP0f+Uw1ihx/yqTmOeeJfvX1
        rhnLF5kOjN8xXtvI4nrYm/ctVtr68A33hjP9ABEBAAG0Q09wZW5MaW5rIFNvZnR3
        YXJlIFNpZ25pbmcgS2V5IChHaXQgdGFncykgPGdpdC5hZG1pbkBvcGVubGlua3N3
        LmNvbT6JAT4EEwECACgFAk9pILICGy8FCQeGH4AGCwkIBwMCBhUIAgkKCwQWAgMB
        Ah4BAheAAAoJEHtptnAIneZ6TJ8IAIytxv4t2umvjWFSOULLLTiQu11WMnYdPWS7
        fMPVznZDpIs9RR1egmj4QAC0x/ImgtRGn3uoebNv2E9WBRYQw+OL4+AnY/y6Grfm
        plkOO/EW3GZYMMWjm6Ih7EhlLooW3Epv1oP8tdikVHKTPl4SiWSPOt1j+W1QyeFO
        7EjWi1zSPL6R0kwqBY/Lpf2SXiiXU40FwoU2J2gPFcWYuBal1Jc3iiBq3hF9W5LZ
        kuJ0D09VXoS6hwc0GkEv2ibFmtBVOsjsjH6N3ENApLT5YK9Pgm2sk5kYXRLDsj1V
        3ojRNFlZbFHr2Hwjwrh0vo9y5XeXUebMu+QPkIQmMeECFkcdl7Y=
        =zD+s
        -----END PGP PUBLIC KEY BLOCK-----
        ' | gpg --import

    \

The fingerprint of this key is [7D6E 3898 F670 9F7A C25C 19D0 7B69 B670
089D E67A]{.c1}.

[]{#Further%20Documentation}Further Documentation
-------------------------------------------------

Please see our [Git
Usage](https://www.iodbc.org/dataspace/iodbc/wiki/iodbcWiki/GitStrategy){.wikiword}
document concerning the usage of branches and tags.

For an introduction to Git, see our [Git Quickstart and
Tips](http://virtuoso.openlinksw.com/dataspace/dav/wiki/Main/GitQuickstartTips){.absuri}
\[virtuoso.openlinksw.com\] guide.
:::
