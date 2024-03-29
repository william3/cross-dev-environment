<html>
<body>

<div id="navigation">
<h1>Cross platform</h1>

    <ul>
        <li><a href="#introduction"     >Introduction</a></li>
        <li><a href="#screenshots"      >Screenshots</a></li>
        <li><a href="#tutorial"         >Tutorial</a></li>
        <li><a href="#download"         >Download</a></li>
        <li><a href="http://lists.nongnu.org/mailman/listinfo/mingw-cross-env-list">Mailing List</a></li>
    </ul>
    <ul>
        <li><a href="#requirements"     >Requirements</a></li>
        <li><a href="#usage"            >Usage</a></li>
        <li><a href="#packages"         >List of Packages</a></li>
        <li><a href="#creating-packages">Creating Packages</a></li>
        <li><a href="#copyright"        >Copyright</a></li>
        <li><a href="#history"          >History</a></li>
    </ul>
    <ul>
        <li><a href="#see-also"         >See also</a></li>
        <li><a href="#used-by"          >Used by</a></li>
    </ul>
</div>

<div class="section">
<h2 id="introduction">Introduction</h2>

    <p>
    Set of make commands and patches to cross-compile hundreds of packages for windows. This project is a fork of the MXE project. It allows you to have :
    <ul>
      <li>the mingw.org 32 bit repository (the one maintained by MXE)</li>
      <li>mingw-w64 32/64 bit repository</li>
    </ul>
    </p>
	<p>
    The MXE project has a great community and works well for the "mingw.org 32 bit" repository. The cross-platform project is experimental and allows you to commit your work when it suits the MXE system (Makefile, *.mk files, patches) but does not fit the mingw.org main repository.
    </p>
    <p>
    This project aims to be integrated in MXE in the futur. Please visit http://mxe.cc/ for more information on MXE.
    </p>
    <p>
    MXE (M cross environment) is a Makefile that
    compiles a cross compiler and cross compiles
    many free libraries such as SDL and Qt. Thus,
    it provides a nice cross compiling environment
    for various target platforms, which
    </p>

    <ul>
    <li>
        is designed to
        <a href="#requirements">run on any Unix system</a>
    </li>
    <li>
        is easy to adapt and to extend
    </li>
    <li>
        builds
        <a href="#packages">many free libraries</a>
        in addition to the cross compiler
    </li>
    <li>
        can also
        <a href="#usage">build just a subset</a>
        of the packages,
        and automatically builds their dependencies
    </li>
    <li>
        downloads all needed packages
        and verifies them by their checksums
    </li>
    <li>
        is able to update the version numbers of all packages automatically
    </li>
    <li>
        directly uses source packages,
        thus ensuring the whole build mechanism is transparent
    </li>
    <li>
        allows inter-package and intra-package
        <a href="#usage">parallel builds</a>
        whenever possible
    </li>
    <li>
        is already
        <a href="#used-by">used by several projects</a>
    </li>
    </ul>
</div>

<div class="section">
<h2 id="screenshots">Screenshots</h2>

    <p>
    Cross compiling
    <a href="http://www.xs4all.nl/~thebeez/4tH/">4tH</a>:
    </p>
    <a href="doc/screenshot-4th-compile.png"><img src="doc/screenshot-4th-compile-small.png" alt="4th-compile"></a>

    <p>
    and running it:
    </p>
    <a href="doc/screenshot-4th-run.png"><img src="doc/screenshot-4th-run-small.png" alt="4th-run"></a>
</div>

<div class="section">
<h2 id="tutorial">Tutorial</h2>

    <h3>Step 1: Download and Unpack</h3>

    <p>
    First, you should ensure that your system meets
    MXE's
    <a href="#requirements">requirements</a>.
    You will almost certainly have to install some stuff.
    </p>

    <p>
    When everything is fine, download the
    <a href="#download">current stable version</a>:
    </p>
    <pre>git clone -b stable https://github.com/mxe/mxe.git</pre>

    <p>
    If you don't mind installing it in your home directory,
    just skip the following step and go straight to step 3.
    </p>

    <h3>Step 2: System-wide Installation (optional)</h3>

    <p>
    Now you should save any previous installation
    of the MXE.
    Assuming you've installed it under
    /opt/mxe (any other directory will do as well),
    you should execute the following commands:
    </p>
    <pre>su
mv /opt/mxe /opt/mxe.old
exit</pre>

    <p>
    Then you need to transfer the entire directory to its definitive location.
    We will assume again you use /opt/mxe,
    but feel free to use any other directory if you like.
    </p>
    <pre>su
mv mxe /opt/mxe
exit</pre>

    <p>
    We're almost done.
    Just change to your newly created directory and get going:
    </p>
    <pre>cd /opt/mxe</pre>

    <h3>Step 3: Build MXE</h3>

    <p>
    Enter the directory where you've downloaded the MXE.
    Now it depends on what you actually want &ndash; or need.
    </p>

    <p>
    If you choose to enter:
    </p>
    <pre>make</pre>
    <p>
    you're in for a long wait,
    because it compiles
    <a href="#packages">a lot of packages</a>.
    On the other hand it doesn't require any intervention,
    so you're free to do whatever you like
    &ndash; like watch a movie or go for a night on the town.
    When it's done you'll find that you've installed
    a very capable Win32 cross compiler onto your system.
    </p>

    <p>
    If you only need the most basic tools you can also use:
    </p>
    <pre>make gcc</pre>
    <p>
    and add any additional packages you need later on.
    You can also supply a host of packages on the
    <a href="#usage">command line</a>,
    e.g.:
    </p>
    <pre>make gtk lua libidn</pre>
    <p>
    You'll always end up with a consistent cross compiling environment.
    </p>

    <p>
    After you're done it just needs a little post-installation.
    </p>

    <h3>Step 4: Environment Variables</h3>

    <p>
    Edit your .bashrc script in order to change $PATH:
    </p>
    <pre>export PATH=/<em>where MXE is installed</em>/usr/bin:$PATH</pre>

    <p>
    In case you are using custom $PKG_CONFIG_PATH entries,
    you can add separate entries for cross builds:
    </p>
    <pre>export PKG_CONFIG_PATH="<em>entries for native builds</em>"</pre>
    <pre>export PKG_CONFIG_PATH_i686_pc_mingw32="<em>entries for MXE builds</em>"</pre>
    <p>
    Remember to use i686-pc-mingw32-pkg-config
    instead of pkg-config for cross builds.
    The Autotools do that automatically for you.
    </p>

    <p>
    Note that any other compiler related environment variables
    (like $CC, $LDFLAGS, etc.)
    may spoil your compiling pleasure,
    so be sure to delete or disable those.
    </p>

    <p>
    Congratulations!
    You're ready to cross compile anything you like.
    </p>

    <h3>Step 5a: Cross compile your Project (Autotools)</h3>

    <p>
    If you use the
    <a href="http://www.lrde.epita.fr/~adl/autotools.html">Autotools</a>,
    all you have to do is:
    </p>
    <pre>./configure --host=i686-pc-mingw32
make</pre>

    <p>
    If you build a library, you might also want to enforce a static build:
    </p>
    <pre>./configure --host=i686-pc-mingw32 --enable-static --disable-shared
make</pre>

    <p>
    Don't worry about a warning like this:
    </p>
    <pre>configure: WARNING: If you wanted to set the --build type, don't use --host.
If a cross compiler is detected then cross compile mode will be used.</pre>
    <p>
    Everything will be just fine.
    </p>

    <h3>Step 5b: Cross compile your Project (CMake)</h3>

    <p>
    If you have a
    <a href="http://www.cmake.org/">CMake</a> project,
    you can use the provided toolchain file:
    </p>
    <pre>cmake ... -DCMAKE_TOOLCHAIN_FILE=/<em>where MXE is installed</em>/usr/i686-pc-mingw32/share/cmake/mingw-cross-env-conf.cmake</pre>

    <h3>Step 5c: Cross compile your Project (Qt)</h3>

    <p>
    If you have a
    <a href="http://qt.nokia.com/">Qt</a> application,
    all you have to do is:
    </p>
    <pre>i686-pc-mingw32-qmake
make</pre>
    <p>
    If you are using Qt plugins
    such as the svg or ico image handlers,
    you should also have a look at the
    <a href="http://qt.nokia.com/doc/plugins-howto.html#static-plugins">Qt documentation about static plugins</a>.
    </p>
    <p>
    Note the sql drivers (-qt-sql-*)
    and the image handlers for jpeg, tiff, gif and mng
    are built-in, <em>not</em> plugins.
    </p>

    <h3>Step 5d: Cross compile your Project (Makefile)</h3>

    <p>
    If you have a handwritten Makefile,
    you probably will have to make a few adjustments to it:
    </p>
    <pre>CC=$(CROSS)gcc
LD=$(CROSS)ld
AR=$(CROSS)ar
PKG_CONFIG=$(CROSS)pkg-config</pre>
    <p>
    You may have to add a few others, depending on your project.
    </p>

    <p>
    Then, all you have to do is:
    </p>
    <pre>make CROSS=i686-pc-mingw32-</pre>
    <p>
    That's it!
    </p>

    <h3>Step 5e: Cross compile your Project (OSG)</h3>

    <p>
    Using static OpenSceneGraph libraries requires a few changes to your source.
    The graphics subsystem and all plugins required by your application must be
    referenced explicitly. Use a code block like the following:
    </p>
    <pre>#ifdef OSG_LIBRARY_STATIC
USE_GRAPHICSWINDOW()
USE_OSGPLUGIN(&lt;plugin1&gt;)
USE_OSGPLUGIN(&lt;plugin2&gt;)
...
#endif</pre>
    <p>
    Look at <code>examples/osgstaticviewer/osgstaticviewer.cpp</code> in the
    OpenSceneGraph source distribution for an example. This example can be
    compiled with the following command:
    </p>
    <pre>i686-pc-mingw32-g++ \
    -o osgstaticviewer.exe examples/osgstaticviewer/osgstaticviewer.cpp \
    `i686-pc-mingw32-pkg-config --cflags openscenegraph-osgViewer openscenegraph-osgPlugins` \
    `i686-pc-mingw32-pkg-config --libs openscenegraph-osgViewer openscenegraph-osgPlugins`</pre>
    <p>
    The <code>i686-pc-mingw32-pkg-config</code> command from MXE will
    automatically add <code>-DOSG_LIBRARY_STATIC</code> to your compiler flags.
    </p>

    <h3>Further Steps</h3>

    <p>
    If you need further assistance,
    feel free to join the
    <a href="http://lists.nongnu.org/mailman/listinfo/mingw-cross-env-list">project mailing list</a>
    where you'll get in touch with
    the MXE developers
    and other users.
    </p>
</div>

<div class="section">
<div id="latest-release"></div>
<div id="development"></div>
<h2 id="download">Download</h2>

    <p>
    To obtain the current stable version, run:
    </p>

    <pre>git clone -b stable https://github.com/mxe/mxe.git</pre>

    <p>
    The development version can be obtained by:
    </p>

    <pre>git clone -b master https://github.com/mxe/mxe.git</pre>

    <p>
    To retrieve updates, run:
    </p>

    <pre>git pull</pre>

    <p>
    You can also browse the
    <a href="https://github.com/mxe/mxe">web repository</a>.
    </p>

    <p>
    In addition,
    feel free to join the
    <a href="http://lists.nongnu.org/mailman/listinfo/mingw-cross-env-list">project mailing list</a>
    and to <a href="#creating-packages">propose new packages</a>.
    </p>

    <h3>For Committers</h3>

    <p>
    The following <code>.git/config</code> settings ensure
    that the stable branch will always be pushed to the
    <code>gh-pages</code> branch in addition to the
    <code>stable</code> branch,
    thus ensuring the website will always stay in sync:
    </p>
    <pre>[remote "origin"]
        url = git@github.com:mxe/mxe.git
        fetch = +refs/heads/*:refs/remotes/origin/*
        push = refs/heads/master:refs/heads/master
        push = refs/heads/stable:refs/heads/stable
        push = refs/heads/stable:refs/heads/gh-pages
[branch "master"]
        remote = origin
        merge = refs/heads/master
[branch "stable"]
        remote = origin
        merge = refs/heads/stable</pre>

    <h3>Branch Concept</h3>

    <p>
    For the sake of simplicity, there are just two
    branches, "master" and "stable". Although it might
    seem obvious, here's an overview of the types of
    changes that go into each branch:
    </p>

    <ul class="compact-list">
        <li>
            Any change of a build script goes into "master".
        </li>
        <li>
            Any package upgrade goes into "master".
        </li>
        <li>
            Any documentation upgrade that refers to a feature
            not present in stable goes into "master".
        </li>
        <li>
            Anything else that doesn't affect the build goes
            into "stable".
        </li>
        <li>
            Any non-critical improvement to the main Makefile
            goes into "stable".
        </li>
        <li>
            Any improvement in the package download URLs or
            package version recognition goes into "stable".
        </li>
        <li>
            When in doubt, "master" is used rather than "stable".
        </li>
        <li>
            After a successful testing phase, the whole "master"
            branch will be merged into "stable" (fast-forward).
        </li>
    </ul>
</div>

<div class="section">
<h2 id="requirements">Requirements</h2>

    <p>
    Mingw-cross-env requires a recent Unix system where
    all components as stated in the table below
    are installed.
    Detailed instructions are available for:
    </p>

    <ul class="compact-list">
        <li><a href="#requirements-debian">Debian</a></li>
        <li><a href="#requirements-fedora">Fedora</a></li>
        <li><a href="#requirements-freebsd">FreeBSD</a></li>
        <li><a href="#requirements-frugalware">Frugalware</a></li>
        <li><a href="#requirements-gentoo">Gentoo</a></li>
        <li><a href="#requirements-macos">Mac OS X</a></li>
        <li><a href="#requirements-opensuse">openSUSE</a></li>
    </ul>

    <table class="requirements">
    <tr>
        <td><a href="http://www.gnu.org/software/autoconf/">Autoconf</a></td>
        <td>≥ 2.64</td>
    </tr>
    <tr>
        <td><a href="http://sources.redhat.com/automake/">Automake</a></td>
        <td>≥ 1.10</td>
    </tr>
    <tr>
        <td><a href="http://www.gnu.org/software/bash/">Bash</a></td>
        <td></td>
    </tr>
    <tr>
        <td><a href="http://www.gnu.org/software/bison/">Bison</a></td>
        <td></td>
    </tr>
    <tr>
        <td><a href="http://www.bzip.org/">Bzip2</a></td>
        <td></td>
    </tr>
    <tr>
        <td><a href="http://www.cmake.org/">CMake</a></td>
        <td>≥ 2.8.0</td>
    </tr>
    <tr>
        <td><a href="http://flex.sourceforge.net/">Flex</a></td>
        <td>≥ 2.5.31</td>
    </tr>
    <tr>
        <td><a href="http://gcc.gnu.org/">GCC</a> (gcc, g++)</td>
        <td></td>
    </tr>
    <tr>
        <td><a href="http://git-scm.com/">Git</a></td>
        <td>≥ 1.7</td>
    </tr>
    <tr>
        <td><a href="http://www.gnu.org/s/gettext/">GNU Gettext</a></td>
        <td></td>
    </tr>
    <tr>
        <td><a href="http://www.gnu.org/software/make/">GNU Make</a></td>
        <td>≥ 3.81</td>
    </tr>
    <tr>
        <td><a href="http://www.gnu.org/software/sed/">GNU Sed</a></td>
        <td></td>
    </tr>
    <tr>
        <td><a href="http://freedesktop.org/wiki/Software/intltool/">Intltool</a></td>
        <td>≥ 0.40</td>
    </tr>
    <tr>
        <td><a href="http://en.wikipedia.org/wiki/C_standard_library">LibC</a> for 32-bit</td>
        <td></td>
    </tr>
    <tr>
        <td><a href="http://www.gnu.org/software/libtool/">Libtool</a></td>
        <td>≥ 2.2</td>
    </tr>
    <tr>
        <td><a href="http://www.openssl.org/">OpenSSL</a>-dev</td>
        <td></td>
    </tr>
    <tr>
        <td><a href="http://www.gnu.org/software/patch/">Patch</a></td>
        <td></td>
    </tr>
    <tr>
        <td><a href="http://www.perl.org/">Perl</a></td>
        <td></td>
    </tr>
    <tr>
        <td><a href="http://search.cpan.org/dist/XML-Parser/Parser.pm">Perl XML::Parser</a></td>
        <td></td>
    </tr>
    <tr>
        <td><a href="http://pkg-config.freedesktop.org/">Pkg-config</a></td>
        <td>≥ 0.16</td>
    </tr>
    <tr>
        <td><a href="http://www.scons.org/">SCons</a></td>
        <td>≥ 0.98</td>
    </tr>
    <tr>
        <td><a href="http://www.info-zip.org/UnZip.html">UnZip</a></td>
        <td></td>
    </tr>
    <tr>
        <td><a href="http://www.gnu.org/software/wget/">Wget</a></td>
        <td></td>
    </tr>
    <tr>
        <td><a href="http://tukaani.org/xz/">XZ Utils</a></td>
        <td></td>
    </tr>
    <tr>
        <td><a href="http://www.tortall.net/projects/yasm/">Yasm</a></td>
        <td></td>
    </tr>
    </table>

    <h3 id="requirements-debian">Debian (GNU/kFreeBSD &amp; GNU/Linux)</h3>

    <!-- http://www.debian.org/distrib/packages#search_packages -->
    <pre>aptitude install -R autoconf automake bash bison bzip2 \
                    cmake flex gettext git g++ intltool \
                    libtool libltdl-dev openssl libssl-dev \
                    libxml-parser-perl make patch perl \
                    pkg-config scons sed unzip wget \
                    xz-utils yasm</pre>

    <p>
    On 64-bit Debian, install also:
    </p>
    <pre>aptitude install -R g++-multilib</pre>

    <h3 id="requirements-fedora">Fedora</h3>

    <!-- https://admin.fedoraproject.org/pkgdb/ -->
    <pre>yum install autoconf automake bash bison bzip2 cmake \
            flex gcc-c++ gettext git intltool make sed \
            libtool openssl-devel patch perl pkgconfig \
            scons yasm unzip wget xz</pre>

    <p>
    On 64-bit Fedora,
    there are <a href="#open-issue-nsis">open issues with the NSIS package</a>.
    </p>

    <h3 id="requirements-freebsd">FreeBSD</h3>

    <!-- http://www.freshports.org/ -->
    <pre>pkg_add -r automake111 autoconf268 bash bison cmake \
           flex gettext git gmake gsed intltool libtool \
           openssl patch perl p5-XML-Parser pkg-config \
           scons unzip wget yasm</pre>

    <p>
    Ensure that /usr/local/bin precedes /usr/bin in your $PATH:
    </p>
    <p>
    For C style shells, edit .cshrc
    </p>
    <pre>setenv PATH /usr/local/bin:$PATH</pre>
    <p>
    For Bourne shells, edit .profile
    </p>
    <pre>export PATH = /usr/local/bin:$PATH</pre>
    <p>
    On 64-bit FreeBSD,
    there are <a href="#open-issue-nsis">open issues with the NSIS package</a>.
    </p>

    <h3 id="requirements-frugalware">Frugalware</h3>

    <!-- http://www.frugalware.org/packages -->
    <pre>pacman-g2 -S autoconf automake bash bzip2 bison cmake \
             flex gcc gettext git intltool make sed libtool \
             openssl patch perl perl-xml-parser pkgconfig \
             scons unzip wget xz xz-lzma yasm</pre>

    <p>
    On 64-bit Frugalware,
    there are <a href="#open-issue-nsis">open issues with the NSIS package</a>.
    </p>

    <h3 id="requirements-gentoo">Gentoo</h3>

    <!-- http://packages.gentoo.org/ -->
    <pre>emerge sys-devel/autoconf sys-devel/automake \
       app-shells/bash sys-devel/bison app-arch/bzip2 \
       dev-util/cmake sys-devel/flex sys-devel/gcc \
       sys-devel/gettext dev-vcs/git \
       dev-util/intltool sys-devel/make sys-apps/sed \
       sys-devel/libtool dev-libs/openssl sys-devel/patch \
       dev-lang/perl dev-perl/XML-Parser \
       dev-util/pkgconfig dev-util/scons app-arch/unzip \
       net-misc/wget app-arch/xz-utils dev-lang/yasm</pre>

    <h3 id="requirements-macos">Mac OS X</h3>

    <p>
    Install
    <a href="http://developer.apple.com/xcode/">Xcode 4</a>
    and
    <a href="http://www.macports.org/">MacPorts</a>,
    then run:
    </p>
    <!-- http://www.macports.org/ports.php -->
    <pre>sudo port install autoconf automake bison cmake flex \
                  gettext git-core gsed intltool libtool \
                  openssl p5-xml-parser pkgconfig scons \
                  wget xz yasm</pre>
    <p>
    Mac OS X versions ≤ 10.6 are no longer supported.
    </p>

    <h3 id="requirements-opensuse">openSUSE</h3>

    <!-- http://software.opensuse.org/113/en -->
    <pre>zypper install -R autoconf automake bash bison bzip2 \
                  cmake flex gcc-c++ gettext-tools git \
                  intltool libtool make openssl \
                  libopenssl-devel patch perl \
                  perl-XML-Parser pkg-config scons \
                  sed unzip wget xz yasm</pre>

    <p>
    On 64-bit openSUSE, install also:
    </p>
    <pre>zypper install -R gcc-32bit glibc-devel-32bit \
                  libgcc46-32bit libgomp46-32bit \
                  libstdc++46-devel-32bit</pre>

    <h3 id="open-issue-nsis">Open Issues with NSIS</h3>

    <p>
    The NSIS package contains some native tools that are
    currently 32-bit only. In order to build these on a
    64-bit system, multi-lib support must be enabled in the
    compiler toolchain. However, not all operating systems
    support this.
    </p>
    <p>
    Since no other packages depend on it, the remainder of
    MXE can be successfully built by simply specifying
    an empty build rule:
    </p>
    <pre>make nsis_BUILD=</pre>
</div>

<div class="section">
<h2 id="usage">Usage</h2>

    <p>
    All build commands also download the packages if necessary.
    </p>
    <p>
    In a BSD userland, substitute "make" with "gmake".
    </p>
    <dl class="usage">

    <dt>make</dt>

        <dd>
        build all packages,
        non-parallel
        </dd>

    <dt>make gcc</dt>

        <dd>
        build a minimal useful set of packages,
        i.e. the cross compilers
        and the most basic packages,
        non-parallel
        </dd>

    <dt>make foo bar</dt>

        <dd>
        build packages "foo", "bar" and their dependencies,
        non-parallel
        </dd>

    <dt>make foo bar -j 4 JOBS=2</dt>

        <dd>
        build packages "foo", "bar" and their dependencies,
        where up to 4 packages are build in parallel,
        each with up to 2 compiler processes running in parallel
        </dd>

    <dt>make check-requirements</dt>

        <dd>
        check most of the
        <a href="#requirements">requirements</a>
        if necessary
        &ndash; executed automatically
        before building packages
        </dd>

    <dt>make download</dt>

        <dd>
        download all packages,
        non-parallel,
        such that subsequent builds work without internet access
        </dd>

    <dt>make download-foo download-bar</dt>

        <dd>
        download packages "foo", "bar" and their dependencies,
        non-parallel
        </dd>

    <dt>make download-foo download-bar -j 4</dt>

        <dd>
        download packages "foo", "bar" and their dependencies,
        where up to 4 packages are downloaded in parallel
        </dd>

    <dt>make clean</dt>

        <dd>
        remove all package builds
        &ndash; use with caution!
        </dd>

    <dt>make clean-pkg</dt>

        <dd>
        remove all unused package files,
        handy after a successful update
        </dd>

    <dt>make update</dt>

        <dd>
        for internal use only!
        &ndash;
        update the version numbers of all packages,
        download the new versions and note their checksums
        </dd>

    <dt>make cleanup-style</dt>

        <dd>
        for internal use only!
        &ndash;
        cleanup coding style
        </dd>

    </dl>
</div>

<div class="section">
<h2 id="packages">List of Packages</h2>

    <p>
    See something missing? Feel free to <a href="#creating-packages">create a new package</a>.
    </p>
    <p>
    mingw.org
    </p>
    <table id="package-list">
    <tr>
        <td id="mingw.org-agg-package">agg</td>
        <td id="agg-version">2.5</td>
        <td id="agg-website"><a href="http://www.antigrain.com/">Anti-Grain Geometry</a></td>
    </tr>
    <tr>
        <td id="mingw.org-atk-package">atk</td>
        <td id="atk-version">2.2.0</td>
        <td id="atk-website"><a href="http://www.gtk.org/">ATK</a></td>
    </tr>
    <tr>
        <td id="mingw.org-atkmm-package">atkmm</td>
        <td id="atkmm-version">2.22.6</td>
        <td id="atkmm-website"><a href="http://www.gtkmm.org/">ATKmm</a></td>
    </tr>
    <tr>
        <td id="mingw.org-aubio-package">aubio</td>
        <td id="aubio-version">0.3.2</td>
        <td id="aubio-website"><a href="http://www.aubio.org/">aubio</a></td>
    </tr>
    <tr>
        <td id="mingw.org-bfd-package">bfd</td>
        <td id="bfd-version">2.22</td>
        <td id="bfd-website"><a href="http://www.gnu.org/software/binutils/">Binary File Descriptor library</a></td>
    </tr>
    <tr>
        <td id="mingw.org-binutils-package">binutils</td>
        <td id="binutils-version">2.22</td>
        <td id="binutils-website"><a href="http://www.gnu.org/software/binutils/">GNU Binutils</a></td>
    </tr>
    <tr>
        <td id="mingw.org-blas-package">blas</td>
        <td id="blas-version">1</td>
        <td id="blas-website"><a href="http://www.netlib.org/blas/">blas</a></td>
    </tr>
    <tr>
        <td id="mingw.org-boost-package">boost</td>
        <td id="boost-version">1.49.0</td>
        <td id="boost-website"><a href="http://www.boost.org/">Boost C++ Library</a></td>
    </tr>
    <tr>
        <td id="mingw.org-bzip2-package">bzip2</td>
        <td id="bzip2-version">1.0.6</td>
        <td id="bzip2-website"><a href="http://www.bzip.org/">bzip2</a></td>
    </tr>
    <tr>
        <td id="mingw.org-cairo-package">cairo</td>
        <td id="cairo-version">1.10.2</td>
        <td id="cairo-website"><a href="http://cairographics.org/">cairo</a></td>
    </tr>
    <tr>
        <td id="mingw.org-cairomm-package">cairomm</td>
        <td id="cairomm-version">1.10.0</td>
        <td id="cairomm-website"><a href="http://cairographics.org/cairomm/">cairomm</a></td>
    </tr>
    <tr>
        <td id="mingw.org-cblas-package">cblas</td>
        <td id="cblas-version">1</td>
        <td id="cblas-website"><a href="http://www.netlib.org/blas/">cblas</a></td>
    </tr>
    <tr>
        <td id="mingw.org-cgal-package">cgal</td>
        <td id="cgal-version">4.0</td>
        <td id="cgal-website"><a href="http://www.cgal.org/">cgal</a></td>
    </tr>
    <tr>
        <td id="mingw.org-cppunit-package">cppunit</td>
        <td id="cppunit-version">1.12.1</td>
        <td id="cppunit-website"><a href="http://apps.sourceforge.net/mediawiki/cppunit/">CppUnit</a></td>
    </tr>
    <tr>
        <td id="mingw.org-cunit-package">cunit</td>
        <td id="cunit-version">2.1-2</td>
        <td id="cunit-website"><a href="http://cunit.sourceforge.net/">cunit</a></td>
    </tr>
    <tr>
        <td id="mingw.org-curl-package">curl</td>
        <td id="curl-version">7.25.0</td>
        <td id="curl-website"><a href="http://curl.haxx.se/libcurl/">cURL</a></td>
    </tr>
    <tr>
        <td id="mingw.org-dbus-package">dbus</td>
        <td id="dbus-version">1.5.12</td>
        <td id="dbus-website"><a href="http://dbus.freedesktop.org/">dbus</a></td>
    </tr>
    <tr>
        <td id="mingw.org-dcmtk-package">dcmtk</td>
        <td id="dcmtk-version">3.6.0</td>
        <td id="dcmtk-website"><a href="http://dicom.offis.de/dcmtk.php.en">DCMTK</a></td>
    </tr>
    <tr>
        <td id="mingw.org-devil-package">devil</td>
        <td id="devil-version">1.7.8</td>
        <td id="devil-website"><a href="http://openil.sourceforge.net/">DevIL</a></td>
    </tr>
    <tr>
        <td id="mingw.org-eigen-package">eigen</td>
        <td id="eigen-version">2.0.17</td>
        <td id="eigen-website"><a href="http://eigen.tuxfamily.org/">eigen</a></td>
    </tr>
    <tr>
        <td id="mingw.org-exiv2-package">exiv2</td>
        <td id="exiv2-version">0.22</td>
        <td id="exiv2-website"><a href="http://www.exiv2.org/">Exiv2</a></td>
    </tr>
    <tr>
        <td id="mingw.org-expat-package">expat</td>
        <td id="expat-version">2.1.0</td>
        <td id="expat-website"><a href="http://expat.sourceforge.net/">Expat XML Parser</a></td>
    </tr>
    <tr>
        <td id="mingw.org-faad2-package">faad2</td>
        <td id="faad2-version">2.7</td>
        <td id="faad2-website"><a href="http://www.audiocoding.com/">faad2</a></td>
    </tr>
    <tr>
        <td id="mingw.org-ffmpeg-package">ffmpeg</td>
        <td id="ffmpeg-version">0.10.2</td>
        <td id="ffmpeg-website"><a href="http://www.ffmpeg.org/">ffmpeg</a></td>
    </tr>
    <tr>
        <td id="mingw.org-fftw-package">fftw</td>
        <td id="fftw-version">3.3.1</td>
        <td id="fftw-website"><a href="http://www.fftw.org/">fftw</a></td>
    </tr>
    <tr>
        <td id="mingw.org-file-package">file</td>
        <td id="file-version">5.11</td>
        <td id="file-website"><a href="http://www.darwinsys.com/file/">file</a></td>
    </tr>
    <tr>
        <td id="mingw.org-flac-package">flac</td>
        <td id="flac-version">1.2.1</td>
        <td id="flac-website"><a href="http://www.xiph.org/ogg/">FLAC</a></td>
    </tr>
    <tr>
        <td id="mingw.org-fltk-package">fltk</td>
        <td id="fltk-version">1.3.0</td>
        <td id="fltk-website"><a href="http://www.fltk.org/">FLTK</a></td>
    </tr>
    <tr>
        <td id="mingw.org-fontconfig-package">fontconfig</td>
        <td id="fontconfig-version">2.9.0</td>
        <td id="fontconfig-website"><a href="http://fontconfig.org/">fontconfig</a></td>
    </tr>
    <tr>
        <td id="mingw.org-freeglut-package">freeglut</td>
        <td id="freeglut-version">2.8.0</td>
        <td id="freeglut-website"><a href="http://freeglut.sourceforge.net/">freeglut</a></td>
    </tr>
    <tr>
        <td id="mingw.org-freeimage-package">freeimage</td>
        <td id="freeimage-version">3.15.3</td>
        <td id="freeimage-website"><a href="http://freeimage.sourceforge.net/">FreeImage</a></td>
    </tr>
    <tr>
        <td id="mingw.org-freetds-package">freetds</td>
        <td id="freetds-version">0.91</td>
        <td id="freetds-website"><a href="http://www.freetds.org/">FreeTDS</a></td>
    </tr>
    <tr>
        <td id="mingw.org-freetype-package">freetype</td>
        <td id="freetype-version">2.4.9</td>
        <td id="freetype-website"><a href="http://freetype.sourceforge.net/">freetype</a></td>
    </tr>
    <tr>
        <td id="mingw.org-fribidi-package">fribidi</td>
        <td id="fribidi-version">0.19.2</td>
        <td id="fribidi-website"><a href="http://fribidi.org/">FriBidi</a></td>
    </tr>
    <tr>
        <td id="mingw.org-ftgl-package">ftgl</td>
        <td id="ftgl-version">2.1.3~rc5</td>
        <td id="ftgl-website"><a href="http://sourceforge.net/projects/ftgl/">ftgl</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gc-package">gc</td>
        <td id="gc-version">7.1</td>
        <td id="gc-website"><a href="http://www.hpl.hp.com/personal/Hans_Boehm/gc/">gc</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gcc-package">gcc</td>
        <td id="gcc-version">4.7.0</td>
        <td id="gcc-website"><a href="http://gcc.gnu.org/">GCC</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gcc-gmp-package">gcc-gmp</td>
        <td id="gcc-gmp-version">5.0.4</td>
        <td id="gcc-gmp-website"><a href="http://www.gmplib.org/">GMP for GCC</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gcc-mpc-package">gcc-mpc</td>
        <td id="gcc-mpc-version">0.9</td>
        <td id="gcc-mpc-website"><a href="http://www.multiprecision.org/">MPC for GCC</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gcc-mpfr-package">gcc-mpfr</td>
        <td id="gcc-mpfr-version">3.1.0</td>
        <td id="gcc-mpfr-website"><a href="http://www.mpfr.org/">MPFR for GCC</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gd-package">gd</td>
        <td id="gd-version">2.0.35</td>
        <td id="gd-website"><a href="http://www.libgd.org/">GD  (without support for xpm)</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gdal-package">gdal</td>
        <td id="gdal-version">1.9.0</td>
        <td id="gdal-website"><a href="http://www.gdal.org/">GDAL</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gdb-package">gdb</td>
        <td id="gdb-version">7.4</td>
        <td id="gdb-website"><a href="http://www.gnu.org/software/gdb/">gdb</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gdk-pixbuf-package">gdk-pixbuf</td>
        <td id="gdk-pixbuf-version">2.22.1</td>
        <td id="gdk-pixbuf-website"><a href="http://www.gdk-pixbuf.org/">GDK-pixbuf</a></td>
    </tr>
    <tr>
        <td id="mingw.org-geos-package">geos</td>
        <td id="geos-version">3.3.3</td>
        <td id="geos-website"><a href="http://trac.osgeo.org/geos/">GEOS</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gettext-package">gettext</td>
        <td id="gettext-version">0.18.1.1</td>
        <td id="gettext-website"><a href="http://www.gnu.org/software/gettext/">gettext</a></td>
    </tr>
    <tr>
        <td id="mingw.org-giflib-package">giflib</td>
        <td id="giflib-version">4.1.6</td>
        <td id="giflib-website"><a href="http://sourceforge.net/projects/libungif/">giflib</a></td>
    </tr>
    <tr>
        <td id="mingw.org-glew-package">glew</td>
        <td id="glew-version">1.7.0</td>
        <td id="glew-website"><a href="http://glew.sourceforge.net/">GLEW</a></td>
    </tr>
    <tr>
        <td id="mingw.org-glib-package">glib</td>
        <td id="glib-version">2.28.8</td>
        <td id="glib-website"><a href="http://www.gtk.org/">GLib</a></td>
    </tr>
    <tr>
        <td id="mingw.org-glibmm-package">glibmm</td>
        <td id="glibmm-version">2.28.2</td>
        <td id="glibmm-website"><a href="http://www.gtkmm.org/">GLibmm</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gmp-package">gmp</td>
        <td id="gmp-version">5.0.4</td>
        <td id="gmp-website"><a href="http://www.gmplib.org/">GMP</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gnutls-package">gnutls</td>
        <td id="gnutls-version">3.0.18</td>
        <td id="gnutls-website"><a href="http://www.gnu.org/software/gnutls/">GnuTLS</a></td>
    </tr>
    <tr>
        <td id="mingw.org-graphicsmagick-package">graphicsmagick</td>
        <td id="graphicsmagick-version">1.3.14</td>
        <td id="graphicsmagick-website"><a href="http://www.graphicsmagick.org/">GraphicsMagick</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gsl-package">gsl</td>
        <td id="gsl-version">1.14</td>
        <td id="gsl-website"><a href="http://www.gnu.org/software/gsl/">GSL</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gsoap-package">gsoap</td>
        <td id="gsoap-version">2.8.8</td>
        <td id="gsoap-website"><a href="http://gsoap2.sourceforge.net/">gSOAP</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gst-plugins-base-package">gst-plugins-base</td>
        <td id="gst-plugins-base-version">0.10.35</td>
        <td id="gst-plugins-base-website"><a href="http://gstreamer.freedesktop.org/">gst-plugins-base</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gst-plugins-good-package">gst-plugins-good</td>
        <td id="gst-plugins-good-version">0.10.30</td>
        <td id="gst-plugins-good-website"><a href="http://gstreamer.freedesktop.org/">gst-plugins-good</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gstreamer-package">gstreamer</td>
        <td id="gstreamer-version">0.10.35</td>
        <td id="gstreamer-website"><a href="http://gstreamer.freedesktop.org/">gstreamer</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gta-package">gta</td>
        <td id="gta-version">1.0.2</td>
        <td id="gta-website"><a href="http://gta.nongnu.org/">gta</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gtk2-package">gtk2</td>
        <td id="gtk2-version">2.24.4</td>
        <td id="gtk2-website"><a href="http://www.gtk.org/">GTK+</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gtkglext-package">gtkglext</td>
        <td id="gtkglext-version">1.2.0</td>
        <td id="gtkglext-website"><a href="http://gtkglext.sourceforge.net/">GtkGLExt</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gtkglextmm-package">gtkglextmm</td>
        <td id="gtkglextmm-version">1.2.0</td>
        <td id="gtkglextmm-website"><a href="http://gtkglext.sourceforge.net/">GtkGLExtmm</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gtkmm2-package">gtkmm2</td>
        <td id="gtkmm2-version">2.24.0</td>
        <td id="gtkmm2-website"><a href="http://www.gtkmm.org/">GTKMM</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gtksourceview-package">gtksourceview</td>
        <td id="gtksourceview-version">2.10.5</td>
        <td id="gtksourceview-website"><a href="http://projects.gnome.org/gtksourceview/">GTKSourceView</a></td>
    </tr>
    <tr>
        <td id="mingw.org-gtksourceviewmm2-package">gtksourceviewmm2</td>
        <td id="gtksourceviewmm2-version">2.10.1</td>
        <td id="gtksourceviewmm2-website"><a href="http://projects.gnome.org/gtksourceviewmm/">GtkSourceViewmm</a></td>
    </tr>
    <tr>
        <td id="mingw.org-guile-package">guile</td>
        <td id="guile-version">1.8.7</td>
        <td id="guile-website"><a href="http://www.gnu.org/software/guile/">GNU Guile</a></td>
    </tr>
    <tr>
        <td id="mingw.org-id3lib-package">id3lib</td>
        <td id="id3lib-version">3.8.3</td>
        <td id="id3lib-website"><a href="http://id3lib.sourceforge.net/">id3lib</a></td>
    </tr>
    <tr>
        <td id="mingw.org-ilmbase-package">ilmbase</td>
        <td id="ilmbase-version">1.0.2</td>
        <td id="ilmbase-website"><a href="http://www.openexr.com/">IlmBase</a></td>
    </tr>
    <tr>
        <td id="mingw.org-imagemagick-package">imagemagick</td>
        <td id="imagemagick-version">6.7.2-7</td>
        <td id="imagemagick-website"><a href="http://www.imagemagick.org/">ImageMagick</a></td>
    </tr>
    <tr>
        <td id="mingw.org-jasper-package">jasper</td>
        <td id="jasper-version">1.900.1</td>
        <td id="jasper-website"><a href="http://www.ece.uvic.ca/~mdadams/jasper/">JasPer</a></td>
    </tr>
    <tr>
        <td id="mingw.org-jpeg-package">jpeg</td>
        <td id="jpeg-version">8d</td>
        <td id="jpeg-website"><a href="http://www.ijg.org/">jpeg</a></td>
    </tr>
    <tr>
        <td id="mingw.org-json-c-package">json-c</td>
        <td id="json-c-version">0.9</td>
        <td id="json-c-website"><a href="http://oss.metaparadigm.com/json-c/">json-c</a></td>
    </tr>
    <tr>
        <td id="mingw.org-lame-package">lame</td>
        <td id="lame-version">3.99</td>
        <td id="lame-website"><a href="http://lame.sourceforge.net/">lame</a></td>
    </tr>
    <tr>
        <td id="mingw.org-lapack-package">lapack</td>
        <td id="lapack-version">3.4.0</td>
        <td id="lapack-website"><a href="http://www.netlib.org/lapack/">lapack</a></td>
    </tr>
    <tr>
        <td id="mingw.org-lcms-package">lcms</td>
        <td id="lcms-version">2.3</td>
        <td id="lcms-website"><a href="http://www.littlecms.com/">lcms</a></td>
    </tr>
    <tr>
        <td id="mingw.org-lcms1-package">lcms1</td>
        <td id="lcms1-version">1.19</td>
        <td id="lcms1-website"><a href="http://www.littlecms.com/">lcms1</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libarchive-package">libarchive</td>
        <td id="libarchive-version">3.0.3</td>
        <td id="libarchive-website"><a href="http://code.google.com/p/libarchive/">Libarchive</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libass-package">libass</td>
        <td id="libass-version">0.10.0</td>
        <td id="libass-website"><a href="http://code.google.com/p/libass/">libass</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libcroco-package">libcroco</td>
        <td id="libcroco-version">0.6.2</td>
        <td id="libcroco-website"><a href="http://www.freespiders.org/projects/libcroco/">Libcroco</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libdnet-package">libdnet</td>
        <td id="libdnet-version">1.11</td>
        <td id="libdnet-website"><a href="http://libdnet.sourceforge.net/">libdnet</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libevent-package">libevent</td>
        <td id="libevent-version">2.0.18</td>
        <td id="libevent-website"><a href="http://libevent.org/">libevent</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libffi-package">libffi</td>
        <td id="libffi-version">3.0.10</td>
        <td id="libffi-website"><a href="http://sourceware.org/libffi/">libffi</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libgcrypt-package">libgcrypt</td>
        <td id="libgcrypt-version">1.5.0</td>
        <td id="libgcrypt-website"><a href="ftp://ftp.gnupg.org/gcrypt/libgcrypt/">libgcrypt</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libgee-package">libgee</td>
        <td id="libgee-version">0.5.0</td>
        <td id="libgee-website"><a href="http://live.gnome.org/Libgee">libgee</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libgeotiff-package">libgeotiff</td>
        <td id="libgeotiff-version">1.3.0</td>
        <td id="libgeotiff-website"><a href="http://trac.osgeo.org/geotiff/">GeoTiff</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libgnurx-package">libgnurx</td>
        <td id="libgnurx-version">2.5.1</td>
        <td id="libgnurx-website"><a href="http://sourceforge.net/projects/mingw/files/UserContributed/regex/">libgnurx</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libgomp-package">libgomp</td>
        <td id="libgomp-version">4.7.0</td>
        <td id="libgomp-website"><a href="http://gcc.gnu.org/projects/gomp/">GCC-libgomp</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libgpg_error-package">libgpg_error</td>
        <td id="libgpg_error-version">1.10</td>
        <td id="libgpg_error-website"><a href="ftp://ftp.gnupg.org/gcrypt/libgpg-error/">libgpg-error</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libgsasl-package">libgsasl</td>
        <td id="libgsasl-version">1.6.1</td>
        <td id="libgsasl-website"><a href="http://www.gnu.org/software/gsasl/">Libgsasl</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libgsf-package">libgsf</td>
        <td id="libgsf-version">1.14.22</td>
        <td id="libgsf-website"><a href="http://ftp.gnome.org/pub/gnome/sources/libgsf/">libgsf</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libharu-package">libharu</td>
        <td id="libharu-version">2.2.1</td>
        <td id="libharu-website"><a href="http://libharu.org/">libharu</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libiberty-package">libiberty</td>
        <td id="libiberty-version">2.22</td>
        <td id="libiberty-website"><a href="http://gcc.gnu.org/onlinedocs/libiberty/">libiberty</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libical-package">libical</td>
        <td id="libical-version">0.48</td>
        <td id="libical-website"><a href="http://freeassociation.sourceforge.net/">libical</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libiconv-package">libiconv</td>
        <td id="libiconv-version">1.14</td>
        <td id="libiconv-website"><a href="http://www.gnu.org/software/libiconv/">libiconv</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libidn-package">libidn</td>
        <td id="libidn-version">1.24</td>
        <td id="libidn-website"><a href="http://www.gnu.org/software/libidn/">Libidn</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libircclient-package">libircclient</td>
        <td id="libircclient-version">1.6</td>
        <td id="libircclient-website"><a href="http://sourceforge.net/projects/libircclient/">libircclient</a></td>
    </tr>
    <tr>
        <td id="mingw.org-liblo-package">liblo</td>
        <td id="liblo-version">0.26</td>
        <td id="liblo-website"><a href="http://liblo.sourceforge.net/">liblo</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libmad-package">libmad</td>
        <td id="libmad-version">0.15.1b</td>
        <td id="libmad-website"><a href="http://www.underbit.com/products/mad/">libmad</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libmikmod-package">libmikmod</td>
        <td id="libmikmod-version">3.2.0-beta2</td>
        <td id="libmikmod-website"><a href="http://mikmod.raphnet.net/">libMikMod</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libmng-package">libmng</td>
        <td id="libmng-version">1.0.10</td>
        <td id="libmng-website"><a href="http://www.libmng.com/">libmng</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libntlm-package">libntlm</td>
        <td id="libntlm-version">1.3</td>
        <td id="libntlm-website"><a href="http://www.nongnu.org/libntlm/">Libntlm</a></td>
    </tr>
    <tr>
        <td id="mingw.org-liboauth-package">liboauth</td>
        <td id="liboauth-version">0.9.6</td>
        <td id="liboauth-website"><a href="http://liboauth.sourceforge.net/">liboauth</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libodbc++-package">libodbc++</td>
        <td id="libodbc++-version">0.2.5</td>
        <td id="libodbc++-website"><a href="http://libodbcxx.sourceforge.net/">libodbc++</a></td>
    </tr>
    <tr>
        <td id="mingw.org-liboil-package">liboil</td>
        <td id="liboil-version">0.3.17</td>
        <td id="liboil-website"><a href="http://liboil.freedesktop.org/">liboil</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libpano13-package">libpano13</td>
        <td id="libpano13-version">2.9.18_rc2</td>
        <td id="libpano13-website"><a href="http://panotools.sourceforge.net/">libpano13</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libpaper-package">libpaper</td>
        <td id="libpaper-version">1.1.24+nmu1</td>
        <td id="libpaper-website"><a href="http://packages.debian.org/unstable/libpaper1">libpaper</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libpng-package">libpng</td>
        <td id="libpng-version">1.5.10</td>
        <td id="libpng-website"><a href="http://www.libpng.org/">libpng</a></td>
    </tr>
    <tr>
        <td id="mingw.org-librsvg-package">librsvg</td>
        <td id="librsvg-version">2.36.0</td>
        <td id="librsvg-website"><a href="http://librsvg.sourceforge.net/">librsvg</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libsamplerate-package">libsamplerate</td>
        <td id="libsamplerate-version">0.1.8</td>
        <td id="libsamplerate-website"><a href="http://www.mega-nerd.com/SRC/">libsamplerate</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libshout-package">libshout</td>
        <td id="libshout-version">2.2.2</td>
        <td id="libshout-website"><a href="http://www.icecast.org/">libshout</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libsigc++-package">libsigc++</td>
        <td id="libsigc++-version">2.2.10</td>
        <td id="libsigc++-website"><a href="http://libsigc.sourceforge.net/">libsigc++</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libsndfile-package">libsndfile</td>
        <td id="libsndfile-version">1.0.25</td>
        <td id="libsndfile-website"><a href="http://www.mega-nerd.com/libsndfile/">libsndfile</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libssh2-package">libssh2</td>
        <td id="libssh2-version">1.4.1</td>
        <td id="libssh2-website"><a href="http://www.libssh2.org">libssh2</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libtool-package">libtool</td>
        <td id="libtool-version">2.4.2</td>
        <td id="libtool-website"><a href="http://www.gnu.org/software/libtool/">GNU Libtool</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libunistring-package">libunistring</td>
        <td id="libunistring-version">0.9.3</td>
        <td id="libunistring-website"><a href="http://www.gnu.org/software/libunistring/">libunistring</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libusb-package">libusb</td>
        <td id="libusb-version">1.2.6.0</td>
        <td id="libusb-website"><a href="http://libusb-win32.sourceforge.net/">LibUsb</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libvpx-package">libvpx</td>
        <td id="libvpx-version">1.0.0</td>
        <td id="libvpx-website"><a href="http://code.google.com/p/webm/">vpx</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libxml++-package">libxml++</td>
        <td id="libxml++-version">2.35.2</td>
        <td id="libxml++-website"><a href="http://libxmlplusplus.sourceforge.net/">libxml2</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libxml2-package">libxml2</td>
        <td id="libxml2-version">2.7.8</td>
        <td id="libxml2-website"><a href="http://www.xmlsoft.org/">libxml2</a></td>
    </tr>
    <tr>
        <td id="mingw.org-libxslt-package">libxslt</td>
        <td id="libxslt-version">1.1.26</td>
        <td id="libxslt-website"><a href="http://xmlsoft.org/XSLT/">libxslt</a></td>
    </tr>
    <tr>
        <td id="mingw.org-llvm-package">llvm</td>
        <td id="llvm-version">3.0</td>
        <td id="llvm-website"><a href="http://llvm.org/">llvm</a></td>
    </tr>
    <tr>
        <td id="mingw.org-lua-package">lua</td>
        <td id="lua-version">5.1.4</td>
        <td id="lua-website"><a href="http://www.lua.org/">Lua</a></td>
    </tr>
    <tr>
        <td id="mingw.org-lzo-package">lzo</td>
        <td id="lzo-version">2.06</td>
        <td id="lzo-website"><a href="http://www.oberhumer.com/opensource/lzo/">lzo</a></td>
    </tr>
    <tr>
        <td id="mingw.org-matio-package">matio</td>
        <td id="matio-version">1.3.4</td>
        <td id="matio-website"><a href="http://sourceforge.net/projects/matio/">matio</a></td>
    </tr>
    <tr>
        <td id="mingw.org-mingw-utils-package">mingw-utils</td>
        <td id="mingw-utils-version">0.4-1</td>
        <td id="mingw-utils-website"><a href="http://www.mingw.org/">MinGW Utilities</a></td>
    </tr>
    <tr>
        <td id="mingw.org-mingwrt-package">mingwrt</td>
        <td id="mingwrt-version">3.20</td>
        <td id="mingwrt-website"><a href="http://www.mingw.org/">MinGW Runtime</a></td>
    </tr>
    <tr>
        <td id="mingw.org-mpfr-package">mpfr</td>
        <td id="mpfr-version">3.1.0</td>
        <td id="mpfr-website"><a href="http://www.mpfr.org/">mpfr</a></td>
    </tr>
    <tr>
        <td id="mingw.org-muparser-package">muparser</td>
        <td id="muparser-version">1.34</td>
        <td id="muparser-website"><a href="http://muparser.sourceforge.net/">muParser</a></td>
    </tr>
    <tr>
        <td id="mingw.org-mxml-package">mxml</td>
        <td id="mxml-version">2.7</td>
        <td id="mxml-website"><a href="http://www.minixml.org/">Mini-XML</a></td>
    </tr>
    <tr>
        <td id="mingw.org-nettle-package">nettle</td>
        <td id="nettle-version">2.4</td>
        <td id="nettle-website"><a href="http://www.lysator.liu.se/~nisse/nettle/">nettle</a></td>
    </tr>
    <tr>
        <td id="mingw.org-nsis-package">nsis</td>
        <td id="nsis-version">2.46</td>
        <td id="nsis-website"><a href="http://nsis.sourceforge.net/">NSIS</a></td>
    </tr>
    <tr>
        <td id="mingw.org-ogg-package">ogg</td>
        <td id="ogg-version">1.3.0</td>
        <td id="ogg-website"><a href="http://www.xiph.org/ogg/">OGG</a></td>
    </tr>
    <tr>
        <td id="mingw.org-old-package">old</td>
        <td id="old-version">0.17</td>
        <td id="old-website"><a href="http://blitiri.com.ar/p/old/">old</a></td>
    </tr>
    <tr>
        <td id="mingw.org-openal-package">openal</td>
        <td id="openal-version">1.14</td>
        <td id="openal-website"><a href="http://kcat.strangesoft.net/openal.html">openal</a></td>
    </tr>
    <tr>
        <td id="mingw.org-opencore-amr-package">opencore-amr</td>
        <td id="opencore-amr-version">0.1.2</td>
        <td id="opencore-amr-website"><a href="http://opencore-amr.sourceforge.net/">opencore-amr</a></td>
    </tr>
    <tr>
        <td id="mingw.org-opencsg-package">opencsg</td>
        <td id="opencsg-version">1.3.2</td>
        <td id="opencsg-website"><a href="http://www.opencsg.org/">opencsg</a></td>
    </tr>
    <tr>
        <td id="mingw.org-openexr-package">openexr</td>
        <td id="openexr-version">1.7.0</td>
        <td id="openexr-website"><a href="http://www.openexr.com/">OpenEXR</a></td>
    </tr>
    <tr>
        <td id="mingw.org-openscenegraph-package">openscenegraph</td>
        <td id="openscenegraph-version">3.0.1</td>
        <td id="openscenegraph-website"><a href="http://www.openscenegraph.org/">OpenSceneGraph</a></td>
    </tr>
    <tr>
        <td id="mingw.org-openssl-package">openssl</td>
        <td id="openssl-version">1.0.1</td>
        <td id="openssl-website"><a href="http://www.openssl.org/">openssl</a></td>
    </tr>
    <tr>
        <td id="mingw.org-pango-package">pango</td>
        <td id="pango-version">1.29.3</td>
        <td id="pango-website"><a href="http://www.pango.org/">Pango</a></td>
    </tr>
    <tr>
        <td id="mingw.org-pangomm-package">pangomm</td>
        <td id="pangomm-version">2.28.2</td>
        <td id="pangomm-website"><a href="http://www.pango.org/">Pangomm</a></td>
    </tr>
    <tr>
        <td id="mingw.org-pcre-package">pcre</td>
        <td id="pcre-version">8.30</td>
        <td id="pcre-website"><a href="http://www.pcre.org/">PCRE</a></td>
    </tr>
    <tr>
        <td id="mingw.org-pdcurses-package">pdcurses</td>
        <td id="pdcurses-version">3.4</td>
        <td id="pdcurses-website"><a href="http://pdcurses.sourceforge.net/">PDcurses</a></td>
    </tr>
    <tr>
        <td id="mingw.org-pdflib_lite-package">pdflib_lite</td>
        <td id="pdflib_lite-version">7.0.5</td>
        <td id="pdflib_lite-website"><a href="http://www.pdflib.com/download/free-software/pdflib-lite-7/">PDFlib Lite</a></td>
    </tr>
    <tr>
        <td id="mingw.org-pfstools-package">pfstools</td>
        <td id="pfstools-version">1.8.5</td>
        <td id="pfstools-website"><a href="http://pfstools.sourceforge.net/">pfstools</a></td>
    </tr>
    <tr>
        <td id="mingw.org-physfs-package">physfs</td>
        <td id="physfs-version">2.0.2</td>
        <td id="physfs-website"><a href="http://icculus.org/physfs/">physfs</a></td>
    </tr>
    <tr>
        <td id="mingw.org-pixman-package">pixman</td>
        <td id="pixman-version">0.25.2</td>
        <td id="pixman-website"><a href="http://cairographics.org/">pixman</a></td>
    </tr>
    <tr>
        <td id="mingw.org-plotmm-package">plotmm</td>
        <td id="plotmm-version">0.1.2</td>
        <td id="plotmm-website"><a href="http://plotmm.sourceforge.net/">PlotMM</a></td>
    </tr>
    <tr>
        <td id="mingw.org-plotutils-package">plotutils</td>
        <td id="plotutils-version">2.6</td>
        <td id="plotutils-website"><a href="http://www.gnu.org/software/plotutils/">plotutils</a></td>
    </tr>
    <tr>
        <td id="mingw.org-poco-package">poco</td>
        <td id="poco-version">1.4.3p1</td>
        <td id="poco-website"><a href="http://pocoproject.org/">POCO C++ Libraries</a></td>
    </tr>
    <tr>
        <td id="mingw.org-popt-package">popt</td>
        <td id="popt-version">1.16</td>
        <td id="popt-website"><a href="http://freshmeat.net/projects/popt/">popt</a></td>
    </tr>
    <tr>
        <td id="mingw.org-portaudio-package">portaudio</td>
        <td id="portaudio-version">19_20071207</td>
        <td id="portaudio-website"><a href="http://www.portaudio.com/">portaudio</a></td>
    </tr>
    <tr>
        <td id="mingw.org-postgresql-package">postgresql</td>
        <td id="postgresql-version">9.1.3</td>
        <td id="postgresql-website"><a href="http://www.postgresql.org/">PostgreSQL</a></td>
    </tr>
    <tr>
        <td id="mingw.org-proj-package">proj</td>
        <td id="proj-version">4.8.0</td>
        <td id="proj-website"><a href="http://trac.osgeo.org/proj/">proj</a></td>
    </tr>
    <tr>
        <td id="mingw.org-pthreads-package">pthreads</td>
        <td id="pthreads-version">2-8-0</td>
        <td id="pthreads-website"><a href="http://sourceware.org/pthreads-win32/">Pthreads-w32</a></td>
    </tr>
    <tr>
        <td id="mingw.org-qjson-package">qjson</td>
        <td id="qjson-version">0.7.1</td>
        <td id="qjson-website"><a href="http://qjson.sourceforge.net/">QJson</a></td>
    </tr>
    <tr>
        <td id="mingw.org-qt-package">qt</td>
        <td id="qt-version">4.8.1</td>
        <td id="qt-website"><a href="http://qt.nokia.com/">Qt</a></td>
    </tr>
    <tr>
        <td id="mingw.org-qwtplot3d-package">qwtplot3d</td>
        <td id="qwtplot3d-version">0.2.7</td>
        <td id="qwtplot3d-website"><a href="http://qwtplot3d.sourceforge.net/">QwtPlot3D</a></td>
    </tr>
    <tr>
        <td id="mingw.org-readline-package">readline</td>
        <td id="readline-version">6.2</td>
        <td id="readline-website"><a href="http://tiswww.case.edu/php/chet/readline/rltop.html">Readline</a></td>
    </tr>
    <tr>
        <td id="mingw.org-sdl-package">sdl</td>
        <td id="sdl-version">1.2.15</td>
        <td id="sdl-website"><a href="http://www.libsdl.org/">SDL</a></td>
    </tr>
    <tr>
        <td id="mingw.org-sdl_image-package">sdl_image</td>
        <td id="sdl_image-version">1.2.12</td>
        <td id="sdl_image-website"><a href="http://www.libsdl.org/projects/SDL_image/">SDL_image</a></td>
    </tr>
    <tr>
        <td id="mingw.org-sdl_mixer-package">sdl_mixer</td>
        <td id="sdl_mixer-version">1.2.12</td>
        <td id="sdl_mixer-website"><a href="http://www.libsdl.org/projects/SDL_mixer/">SDL_mixer</a></td>
    </tr>
    <tr>
        <td id="mingw.org-sdl_net-package">sdl_net</td>
        <td id="sdl_net-version">1.2.8</td>
        <td id="sdl_net-website"><a href="http://www.libsdl.org/projects/SDL_net/">SDL_net</a></td>
    </tr>
    <tr>
        <td id="mingw.org-sdl_pango-package">sdl_pango</td>
        <td id="sdl_pango-version">0.1.2</td>
        <td id="sdl_pango-website"><a href="http://sdlpango.sourceforge.net/">SDL_Pango</a></td>
    </tr>
    <tr>
        <td id="mingw.org-sdl_sound-package">sdl_sound</td>
        <td id="sdl_sound-version">1.0.3</td>
        <td id="sdl_sound-website"><a href="http://icculus.org/SDL_sound/">SDL_sound</a></td>
    </tr>
    <tr>
        <td id="mingw.org-sdl_ttf-package">sdl_ttf</td>
        <td id="sdl_ttf-version">2.0.11</td>
        <td id="sdl_ttf-website"><a href="http://www.libsdl.org/projects/SDL_ttf/">SDL_ttf</a></td>
    </tr>
    <tr>
        <td id="mingw.org-smpeg-package">smpeg</td>
        <td id="smpeg-version">0.4.5+cvs20030824</td>
        <td id="smpeg-website"><a href="http://icculus.org/smpeg/">smpeg</a></td>
    </tr>
    <tr>
        <td id="mingw.org-speex-package">speex</td>
        <td id="speex-version">1.2rc1</td>
        <td id="speex-website"><a href="http://www.speex.org/">Speex</a></td>
    </tr>
    <tr>
        <td id="mingw.org-sqlite-package">sqlite</td>
        <td id="sqlite-version">3071100</td>
        <td id="sqlite-website"><a href="http://www.sqlite.org/">SQLite</a></td>
    </tr>
    <tr>
        <td id="mingw.org-suitesparse-package">suitesparse</td>
        <td id="suitesparse-version">3.7.0</td>
        <td id="suitesparse-website"><a href="http://www.cise.ufl.edu/research/sparse/SuiteSparse/">SuiteSparse</a></td>
    </tr>
    <tr>
        <td id="mingw.org-t4k_common-package">t4k_common</td>
        <td id="t4k_common-version">0.1.1</td>
        <td id="t4k_common-website"><a href="http://tux4kids.alioth.debian.org/">t4k_common</a></td>
    </tr>
    <tr>
        <td id="mingw.org-taglib-package">taglib</td>
        <td id="taglib-version">1.7.1</td>
        <td id="taglib-website"><a href="http://developer.kde.org/~wheeler/taglib.html">TagLib</a></td>
    </tr>
    <tr>
        <td id="mingw.org-theora-package">theora</td>
        <td id="theora-version">1.1.1</td>
        <td id="theora-website"><a href="http://theora.org/">Theora</a></td>
    </tr>
    <tr>
        <td id="mingw.org-tiff-package">tiff</td>
        <td id="tiff-version">4.0.1</td>
        <td id="tiff-website"><a href="http://www.remotesensing.org/libtiff/">LibTIFF</a></td>
    </tr>
    <tr>
        <td id="mingw.org-tinyxml-package">tinyxml</td>
        <td id="tinyxml-version">2.6.2</td>
        <td id="tinyxml-website"><a href="http://sourceforge.net/projects/tinyxml/">tinyxml</a></td>
    </tr>
    <tr>
        <td id="mingw.org-tre-package">tre</td>
        <td id="tre-version">0.8.0</td>
        <td id="tre-website"><a href="http://laurikari.net/tre/">TRE</a></td>
    </tr>
    <tr>
        <td id="mingw.org-vigra-package">vigra</td>
        <td id="vigra-version">1.8.0</td>
        <td id="vigra-website"><a href="http://hci.iwr.uni-heidelberg.de/vigra">vigra</a></td>
    </tr>
    <tr>
        <td id="mingw.org-vmime-package">vmime</td>
        <td id="vmime-version">0.9.1</td>
        <td id="vmime-website"><a href="http://vmime.sourceforge.net/">VMime</a></td>
    </tr>
    <tr>
        <td id="mingw.org-vorbis-package">vorbis</td>
        <td id="vorbis-version">1.3.2</td>
        <td id="vorbis-website"><a href="http://www.vorbis.com/">Vorbis</a></td>
    </tr>
    <tr>
        <td id="mingw.org-vtk-package">vtk</td>
        <td id="vtk-version">5.8.0</td>
        <td id="vtk-website"><a href="http://www.vtk.org/">vtk</a></td>
    </tr>
    <tr>
        <td id="mingw.org-w32api-package">w32api</td>
        <td id="w32api-version">3.17</td>
        <td id="w32api-website"><a href="http://www.mingw.org/">MinGW Windows API</a></td>
    </tr>
    <tr>
        <td id="mingw.org-winpcap-package">winpcap</td>
        <td id="winpcap-version">4_1_2</td>
        <td id="winpcap-website"><a href="http://www.winpcap.org/">WinPcap</a></td>
    </tr>
    <tr>
        <td id="mingw.org-wt-package">wt</td>
        <td id="wt-version">3.2.0</td>
        <td id="wt-website"><a href="http://witty.sourceforge.net/">Wt</a></td>
    </tr>
    <tr>
        <td id="mingw.org-wxwidgets-package">wxwidgets</td>
        <td id="wxwidgets-version">2.8.12</td>
        <td id="wxwidgets-website"><a href="http://www.wxwidgets.org/">wxWidgets</a></td>
    </tr>
    <tr>
        <td id="mingw.org-x264-package">x264</td>
        <td id="x264-version">20111018-2245</td>
        <td id="x264-website"><a href="http://www.videolan.org/developers/x264.html">x264</a></td>
    </tr>
    <tr>
        <td id="mingw.org-xerces-package">xerces</td>
        <td id="xerces-version">3.1.1</td>
        <td id="xerces-website"><a href="http://xerces.apache.org/xerces-c/">Xerces-C++</a></td>
    </tr>
    <tr>
        <td id="mingw.org-xine-lib-package">xine-lib</td>
        <td id="xine-lib-version">1.1.20.1</td>
        <td id="xine-lib-website"><a href="http://www.xine-project.org/">xine-lib</a></td>
    </tr>
    <tr>
        <td id="mingw.org-xmlwrapp-package">xmlwrapp</td>
        <td id="xmlwrapp-version">0.6.3</td>
        <td id="xmlwrapp-website"><a href="http://sourceforge.net/projects/xmlwrapp/">xmlwrapp</a></td>
    </tr>
    <tr>
        <td id="mingw.org-xvidcore-package">xvidcore</td>
        <td id="xvidcore-version">1.3.2</td>
        <td id="xvidcore-website"><a href="http://www.xvid.org/">xvidcore</a></td>
    </tr>
    <tr>
        <td id="mingw.org-xz-package">xz</td>
        <td id="xz-version">5.0.3</td>
        <td id="xz-website"><a href="http://tukaani.org/xz/">XZ</a></td>
    </tr>
    <tr>
        <td id="mingw.org-zlib-package">zlib</td>
        <td id="zlib-version">1.2.6</td>
        <td id="zlib-website"><a href="http://zlib.net/">zlib</a></td>
    </tr>
    <tr>
        <td id="mingw.org-zziplib-package">zziplib</td>
        <td id="zziplib-version">0.13.59</td>
        <td id="zziplib-website"><a href="http://zziplib.sourceforge.net/">ZZIPlib</a></td>
    </tr>
    </table>
    <p>
    mingw-w64
    </p>
    <table id="package-list">
    <tr>
        <td id="mingw-w64-agg-package">agg</td>
        <td id="agg-version">2.5</td>
        <td id="agg-website"><a href="http://www.antigrain.com/">Anti-Grain Geometry</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-atk-package">atk</td>
        <td id="atk-version">2.2.0</td>
        <td id="atk-website"><a href="http://www.gtk.org/">ATK</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-atkmm-package">atkmm</td>
        <td id="atkmm-version">2.22.6</td>
        <td id="atkmm-website"><a href="http://www.gtkmm.org/">ATKmm</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-aubio-package">aubio</td>
        <td id="aubio-version">0.3.2</td>
        <td id="aubio-website"><a href="http://www.aubio.org/">aubio</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-bfd-package">bfd</td>
        <td id="bfd-version">2.22</td>
        <td id="bfd-website"><a href="http://www.gnu.org/software/binutils/">Binary File Descriptor library</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-binutils-package">binutils</td>
        <td id="binutils-version">2.22</td>
        <td id="binutils-website"><a href="http://www.gnu.org/software/binutils/">GNU Binutils</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-blas-package">blas</td>
        <td id="blas-version">1</td>
        <td id="blas-website"><a href="http://www.netlib.org/blas/">blas</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-boost-package">boost</td>
        <td id="boost-version">1.49.0</td>
        <td id="boost-website"><a href="http://www.boost.org/">Boost C++ Library</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-bzip2-package">bzip2</td>
        <td id="bzip2-version">1.0.6</td>
        <td id="bzip2-website"><a href="http://www.bzip.org/">bzip2</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-cairo-package">cairo</td>
        <td id="cairo-version">1.10.2</td>
        <td id="cairo-website"><a href="http://cairographics.org/">cairo</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-cairomm-package">cairomm</td>
        <td id="cairomm-version">1.10.0</td>
        <td id="cairomm-website"><a href="http://cairographics.org/cairomm/">cairomm</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-cblas-package">cblas</td>
        <td id="cblas-version">1</td>
        <td id="cblas-website"><a href="http://www.netlib.org/blas/">cblas</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-cgal-package">cgal</td>
        <td id="cgal-version">4.0</td>
        <td id="cgal-website"><a href="http://www.cgal.org/">cgal</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-cppunit-package">cppunit</td>
        <td id="cppunit-version">1.12.1</td>
        <td id="cppunit-website"><a href="http://apps.sourceforge.net/mediawiki/cppunit/">CppUnit</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-cunit-package">cunit</td>
        <td id="cunit-version">2.1-2</td>
        <td id="cunit-website"><a href="http://cunit.sourceforge.net/">cunit</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-curl-package">curl</td>
        <td id="curl-version">7.25.0</td>
        <td id="curl-website"><a href="http://curl.haxx.se/libcurl/">cURL</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-dbus-package">dbus</td>
        <td id="dbus-version">1.5.12</td>
        <td id="dbus-website"><a href="http://dbus.freedesktop.org/">dbus</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-dcmtk-package">dcmtk</td>
        <td id="dcmtk-version">3.6.0</td>
        <td id="dcmtk-website"><a href="http://dicom.offis.de/dcmtk.php.en">DCMTK</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-devil-package">devil</td>
        <td id="devil-version">1.7.8</td>
        <td id="devil-website"><a href="http://openil.sourceforge.net/">DevIL</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-eigen-package">eigen</td>
        <td id="eigen-version">2.0.17</td>
        <td id="eigen-website"><a href="http://eigen.tuxfamily.org/">eigen</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-exiv2-package">exiv2</td>
        <td id="exiv2-version">0.22</td>
        <td id="exiv2-website"><a href="http://www.exiv2.org/">Exiv2</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-expat-package">expat</td>
        <td id="expat-version">2.1.0</td>
        <td id="expat-website"><a href="http://expat.sourceforge.net/">Expat XML Parser</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-faad2-package">faad2</td>
        <td id="faad2-version">2.7</td>
        <td id="faad2-website"><a href="http://www.audiocoding.com/">faad2</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-ffmpeg-package">ffmpeg</td>
        <td id="ffmpeg-version">0.10.2</td>
        <td id="ffmpeg-website"><a href="http://www.ffmpeg.org/">ffmpeg</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-fftw-package">fftw</td>
        <td id="fftw-version">3.3.1</td>
        <td id="fftw-website"><a href="http://www.fftw.org/">fftw</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-file-package">file</td>
        <td id="file-version">5.11</td>
        <td id="file-website"><a href="http://www.darwinsys.com/file/">file</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-flac-package">flac</td>
        <td id="flac-version">1.2.1</td>
        <td id="flac-website"><a href="http://www.xiph.org/ogg/">FLAC</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-fltk-package">fltk</td>
        <td id="fltk-version">1.3.0</td>
        <td id="fltk-website"><a href="http://www.fltk.org/">FLTK</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-fontconfig-package">fontconfig</td>
        <td id="fontconfig-version">2.9.0</td>
        <td id="fontconfig-website"><a href="http://fontconfig.org/">fontconfig</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-freeglut-package">freeglut</td>
        <td id="freeglut-version">2.8.0</td>
        <td id="freeglut-website"><a href="http://freeglut.sourceforge.net/">freeglut</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-freeimage-package">freeimage</td>
        <td id="freeimage-version">3.15.3</td>
        <td id="freeimage-website"><a href="http://freeimage.sourceforge.net/">FreeImage</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-freetds-package">freetds</td>
        <td id="freetds-version">0.91</td>
        <td id="freetds-website"><a href="http://www.freetds.org/">FreeTDS</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-freetype-package">freetype</td>
        <td id="freetype-version">2.4.9</td>
        <td id="freetype-website"><a href="http://freetype.sourceforge.net/">freetype</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-fribidi-package">fribidi</td>
        <td id="fribidi-version">0.19.2</td>
        <td id="fribidi-website"><a href="http://fribidi.org/">FriBidi</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-ftgl-package">ftgl</td>
        <td id="ftgl-version">2.1.3~rc5</td>
        <td id="ftgl-website"><a href="http://sourceforge.net/projects/ftgl/">ftgl</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gc-package">gc</td>
        <td id="gc-version">7.1</td>
        <td id="gc-website"><a href="http://www.hpl.hp.com/personal/Hans_Boehm/gc/">gc</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gcc-package">gcc</td>
        <td id="gcc-version">4.7.0</td>
        <td id="gcc-website"><a href="http://gcc.gnu.org/">GCC</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gcc-core-package">gcc-core</td>
        <td id="gcc-core-version">4.7.0</td>
        <td id="gcc-core-website"><a href="http://gcc.gnu.org/">GCC</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gcc-package">gcc</td>
        <td id="gcc-version">4.7.0</td>
        <td id="gcc-website"><a href="http://gcc.gnu.org/">GCC</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gd-package">gd</td>
        <td id="gd-version">2.0.35</td>
        <td id="gd-website"><a href="http://www.libgd.org/">GD  (without support for xpm)</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gdal-package">gdal</td>
        <td id="gdal-version">1.9.0</td>
        <td id="gdal-website"><a href="http://www.gdal.org/">GDAL</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gdb-package">gdb</td>
        <td id="gdb-version">7.4</td>
        <td id="gdb-website"><a href="http://www.gnu.org/software/gdb/">gdb</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gdk-pixbuf-package">gdk-pixbuf</td>
        <td id="gdk-pixbuf-version">2.22.1</td>
        <td id="gdk-pixbuf-website"><a href="http://www.gdk-pixbuf.org/">GDK-pixbuf</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-geos-package">geos</td>
        <td id="geos-version">3.3.3</td>
        <td id="geos-website"><a href="http://trac.osgeo.org/geos/">GEOS</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gettext-package">gettext</td>
        <td id="gettext-version">0.18.1.1</td>
        <td id="gettext-website"><a href="http://www.gnu.org/software/gettext/">gettext</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-giflib-package">giflib</td>
        <td id="giflib-version">4.1.6</td>
        <td id="giflib-website"><a href="http://sourceforge.net/projects/libungif/">giflib</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-glew-package">glew</td>
        <td id="glew-version">1.7.0</td>
        <td id="glew-website"><a href="http://glew.sourceforge.net/">GLEW</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-glib-package">glib</td>
        <td id="glib-version">2.28.8</td>
        <td id="glib-website"><a href="http://www.gtk.org/">GLib</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-glibmm-package">glibmm</td>
        <td id="glibmm-version">2.28.2</td>
        <td id="glibmm-website"><a href="http://www.gtkmm.org/">GLibmm</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gmp-package">gmp</td>
        <td id="gmp-version">5.0.4</td>
        <td id="gmp-website"><a href="http://www.gmplib.org/">GMP</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gnutls-package">gnutls</td>
        <td id="gnutls-version">3.0.18</td>
        <td id="gnutls-website"><a href="http://www.gnu.org/software/gnutls/">GnuTLS</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-graphicsmagick-package">graphicsmagick</td>
        <td id="graphicsmagick-version">1.3.14</td>
        <td id="graphicsmagick-website"><a href="http://www.graphicsmagick.org/">GraphicsMagick</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gsl-package">gsl</td>
        <td id="gsl-version">1.14</td>
        <td id="gsl-website"><a href="http://www.gnu.org/software/gsl/">GSL</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gsoap-package">gsoap</td>
        <td id="gsoap-version">2.8.8</td>
        <td id="gsoap-website"><a href="http://gsoap2.sourceforge.net/">gSOAP</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gst-plugins-base-package">gst-plugins-base</td>
        <td id="gst-plugins-base-version">0.10.35</td>
        <td id="gst-plugins-base-website"><a href="http://gstreamer.freedesktop.org/">gst-plugins-base</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gst-plugins-good-package">gst-plugins-good</td>
        <td id="gst-plugins-good-version">0.10.30</td>
        <td id="gst-plugins-good-website"><a href="http://gstreamer.freedesktop.org/">gst-plugins-good</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gstreamer-package">gstreamer</td>
        <td id="gstreamer-version">0.10.35</td>
        <td id="gstreamer-website"><a href="http://gstreamer.freedesktop.org/">gstreamer</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gta-package">gta</td>
        <td id="gta-version">1.0.2</td>
        <td id="gta-website"><a href="http://gta.nongnu.org/">gta</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gtk2-package">gtk2</td>
        <td id="gtk2-version">2.24.4</td>
        <td id="gtk2-website"><a href="http://www.gtk.org/">GTK+</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gtkglext-package">gtkglext</td>
        <td id="gtkglext-version">1.2.0</td>
        <td id="gtkglext-website"><a href="http://gtkglext.sourceforge.net/">GtkGLExt</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gtkglextmm-package">gtkglextmm</td>
        <td id="gtkglextmm-version">1.2.0</td>
        <td id="gtkglextmm-website"><a href="http://gtkglext.sourceforge.net/">GtkGLExtmm</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gtkmm2-package">gtkmm2</td>
        <td id="gtkmm2-version">2.24.0</td>
        <td id="gtkmm2-website"><a href="http://www.gtkmm.org/">GTKMM</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gtksourceview-package">gtksourceview</td>
        <td id="gtksourceview-version">2.10.5</td>
        <td id="gtksourceview-website"><a href="http://projects.gnome.org/gtksourceview/">GTKSourceView</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-gtksourceviewmm2-package">gtksourceviewmm2</td>
        <td id="gtksourceviewmm2-version">2.10.1</td>
        <td id="gtksourceviewmm2-website"><a href="http://projects.gnome.org/gtksourceviewmm/">GtkSourceViewmm</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-guile-package">guile</td>
        <td id="guile-version">1.8.7</td>
        <td id="guile-website"><a href="http://www.gnu.org/software/guile/">GNU Guile</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-mingw-w64-crt-package">mingw-w64-crt</td>
        <td id="mingw-w64-crt-version">2.0.1</td>
        <td id="mingw-w64-crt-website"><a href="http://mingw-w64.sourceforge.net/">mingw-w64-crt</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-mingw-w64-headers-package">mingw-w64-headers</td>
        <td id="mingw-w64-headers-version">2.0.1</td>
        <td id="mingw-w64-headers-website"><a href="http://mingw-w64.sourceforge.net/">mingw-w64-headers</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-id3lib-package">id3lib</td>
        <td id="id3lib-version">3.8.3</td>
        <td id="id3lib-website"><a href="http://id3lib.sourceforge.net/">id3lib</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-ilmbase-package">ilmbase</td>
        <td id="ilmbase-version">1.0.2</td>
        <td id="ilmbase-website"><a href="http://www.openexr.com/">IlmBase</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-imagemagick-package">imagemagick</td>
        <td id="imagemagick-version">6.7.2-7</td>
        <td id="imagemagick-website"><a href="http://www.imagemagick.org/">ImageMagick</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-jasper-package">jasper</td>
        <td id="jasper-version">1.900.1</td>
        <td id="jasper-website"><a href="http://www.ece.uvic.ca/~mdadams/jasper/">JasPer</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-jpeg-package">jpeg</td>
        <td id="jpeg-version">8d</td>
        <td id="jpeg-website"><a href="http://www.ijg.org/">jpeg</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-json-c-package">json-c</td>
        <td id="json-c-version">0.9</td>
        <td id="json-c-website"><a href="http://oss.metaparadigm.com/json-c/">json-c</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-lame-package">lame</td>
        <td id="lame-version">3.99</td>
        <td id="lame-website"><a href="http://lame.sourceforge.net/">lame</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-lapack-package">lapack</td>
        <td id="lapack-version">3.4.0</td>
        <td id="lapack-website"><a href="http://www.netlib.org/lapack/">lapack</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-lcms-package">lcms</td>
        <td id="lcms-version">2.3</td>
        <td id="lcms-website"><a href="http://www.littlecms.com/">lcms</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-lcms1-package">lcms1</td>
        <td id="lcms1-version">1.19</td>
        <td id="lcms1-website"><a href="http://www.littlecms.com/">lcms1</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libarchive-package">libarchive</td>
        <td id="libarchive-version">3.0.3</td>
        <td id="libarchive-website"><a href="http://code.google.com/p/libarchive/">Libarchive</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libass-package">libass</td>
        <td id="libass-version">0.10.0</td>
        <td id="libass-website"><a href="http://code.google.com/p/libass/">libass</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libcroco-package">libcroco</td>
        <td id="libcroco-version">0.6.2</td>
        <td id="libcroco-website"><a href="http://www.freespiders.org/projects/libcroco/">Libcroco</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libdnet-package">libdnet</td>
        <td id="libdnet-version">1.11</td>
        <td id="libdnet-website"><a href="http://libdnet.sourceforge.net/">libdnet</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libevent-package">libevent</td>
        <td id="libevent-version">2.0.18</td>
        <td id="libevent-website"><a href="http://libevent.org/">libevent</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libffi-package">libffi</td>
        <td id="libffi-version">3.0.10</td>
        <td id="libffi-website"><a href="http://sourceware.org/libffi/">libffi</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libgcrypt-package">libgcrypt</td>
        <td id="libgcrypt-version">1.5.0</td>
        <td id="libgcrypt-website"><a href="ftp://ftp.gnupg.org/gcrypt/libgcrypt/">libgcrypt</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libgee-package">libgee</td>
        <td id="libgee-version">0.5.0</td>
        <td id="libgee-website"><a href="http://live.gnome.org/Libgee">libgee</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libgeotiff-package">libgeotiff</td>
        <td id="libgeotiff-version">1.3.0</td>
        <td id="libgeotiff-website"><a href="http://trac.osgeo.org/geotiff/">GeoTiff</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libgnurx-package">libgnurx</td>
        <td id="libgnurx-version">2.5.1</td>
        <td id="libgnurx-website"><a href="http://sourceforge.net/projects/mingw/files/UserContributed/regex/">libgnurx</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libgomp-package">libgomp</td>
        <td id="libgomp-version">4.7.0</td>
        <td id="libgomp-website"><a href="http://gcc.gnu.org/projects/gomp/">GCC-libgomp</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libgpg_error-package">libgpg_error</td>
        <td id="libgpg_error-version">1.10</td>
        <td id="libgpg_error-website"><a href="ftp://ftp.gnupg.org/gcrypt/libgpg-error/">libgpg-error</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libgsasl-package">libgsasl</td>
        <td id="libgsasl-version">1.6.1</td>
        <td id="libgsasl-website"><a href="http://www.gnu.org/software/gsasl/">Libgsasl</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libgsf-package">libgsf</td>
        <td id="libgsf-version">1.14.22</td>
        <td id="libgsf-website"><a href="http://ftp.gnome.org/pub/gnome/sources/libgsf/">libgsf</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libharu-package">libharu</td>
        <td id="libharu-version">2.2.1</td>
        <td id="libharu-website"><a href="http://libharu.org/">libharu</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libiberty-package">libiberty</td>
        <td id="libiberty-version">2.22</td>
        <td id="libiberty-website"><a href="http://gcc.gnu.org/onlinedocs/libiberty/">libiberty</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libical-package">libical</td>
        <td id="libical-version">0.48</td>
        <td id="libical-website"><a href="http://freeassociation.sourceforge.net/">libical</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libiconv-package">libiconv</td>
        <td id="libiconv-version">1.14</td>
        <td id="libiconv-website"><a href="http://www.gnu.org/software/libiconv/">libiconv</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libidn-package">libidn</td>
        <td id="libidn-version">1.24</td>
        <td id="libidn-website"><a href="http://www.gnu.org/software/libidn/">Libidn</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libircclient-package">libircclient</td>
        <td id="libircclient-version">1.6</td>
        <td id="libircclient-website"><a href="http://sourceforge.net/projects/libircclient/">libircclient</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-liblo-package">liblo</td>
        <td id="liblo-version">0.26</td>
        <td id="liblo-website"><a href="http://liblo.sourceforge.net/">liblo</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libmad-package">libmad</td>
        <td id="libmad-version">0.15.1b</td>
        <td id="libmad-website"><a href="http://www.underbit.com/products/mad/">libmad</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libmikmod-package">libmikmod</td>
        <td id="libmikmod-version">3.2.0-beta2</td>
        <td id="libmikmod-website"><a href="http://mikmod.raphnet.net/">libMikMod</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libmng-package">libmng</td>
        <td id="libmng-version">1.0.10</td>
        <td id="libmng-website"><a href="http://www.libmng.com/">libmng</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libntlm-package">libntlm</td>
        <td id="libntlm-version">1.3</td>
        <td id="libntlm-website"><a href="http://www.nongnu.org/libntlm/">Libntlm</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-liboauth-package">liboauth</td>
        <td id="liboauth-version">0.9.6</td>
        <td id="liboauth-website"><a href="http://liboauth.sourceforge.net/">liboauth</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libodbc++-package">libodbc++</td>
        <td id="libodbc++-version">0.2.5</td>
        <td id="libodbc++-website"><a href="http://libodbcxx.sourceforge.net/">libodbc++</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-liboil-package">liboil</td>
        <td id="liboil-version">0.3.17</td>
        <td id="liboil-website"><a href="http://liboil.freedesktop.org/">liboil</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libpano13-package">libpano13</td>
        <td id="libpano13-version">2.9.18_rc2</td>
        <td id="libpano13-website"><a href="http://panotools.sourceforge.net/">libpano13</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libpaper-package">libpaper</td>
        <td id="libpaper-version">1.1.24+nmu1</td>
        <td id="libpaper-website"><a href="http://packages.debian.org/unstable/libpaper1">libpaper</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libpng-package">libpng</td>
        <td id="libpng-version">1.5.10</td>
        <td id="libpng-website"><a href="http://www.libpng.org/">libpng</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-librsvg-package">librsvg</td>
        <td id="librsvg-version">2.36.0</td>
        <td id="librsvg-website"><a href="http://librsvg.sourceforge.net/">librsvg</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libsamplerate-package">libsamplerate</td>
        <td id="libsamplerate-version">0.1.8</td>
        <td id="libsamplerate-website"><a href="http://www.mega-nerd.com/SRC/">libsamplerate</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libshout-package">libshout</td>
        <td id="libshout-version">2.2.2</td>
        <td id="libshout-website"><a href="http://www.icecast.org/">libshout</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libsigc++-package">libsigc++</td>
        <td id="libsigc++-version">2.2.10</td>
        <td id="libsigc++-website"><a href="http://libsigc.sourceforge.net/">libsigc++</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libsndfile-package">libsndfile</td>
        <td id="libsndfile-version">1.0.25</td>
        <td id="libsndfile-website"><a href="http://www.mega-nerd.com/libsndfile/">libsndfile</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libssh2-package">libssh2</td>
        <td id="libssh2-version">1.4.1</td>
        <td id="libssh2-website"><a href="http://www.libssh2.org">libssh2</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libtool-package">libtool</td>
        <td id="libtool-version">2.4.2</td>
        <td id="libtool-website"><a href="http://www.gnu.org/software/libtool/">GNU Libtool</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libunistring-package">libunistring</td>
        <td id="libunistring-version">0.9.3</td>
        <td id="libunistring-website"><a href="http://www.gnu.org/software/libunistring/">libunistring</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libusb-package">libusb</td>
        <td id="libusb-version">1.2.6.0</td>
        <td id="libusb-website"><a href="http://libusb-win32.sourceforge.net/">LibUsb</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libvpx-package">libvpx</td>
        <td id="libvpx-version">1.0.0</td>
        <td id="libvpx-website"><a href="http://code.google.com/p/webm/">vpx</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libxml++-package">libxml++</td>
        <td id="libxml++-version">2.35.2</td>
        <td id="libxml++-website"><a href="http://libxmlplusplus.sourceforge.net/">libxml2</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libxml2-package">libxml2</td>
        <td id="libxml2-version">2.7.8</td>
        <td id="libxml2-website"><a href="http://www.xmlsoft.org/">libxml2</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-libxslt-package">libxslt</td>
        <td id="libxslt-version">1.1.26</td>
        <td id="libxslt-website"><a href="http://xmlsoft.org/XSLT/">libxslt</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-llvm-package">llvm</td>
        <td id="llvm-version">3.0</td>
        <td id="llvm-website"><a href="http://llvm.org/">llvm</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-lua-package">lua</td>
        <td id="lua-version">5.1.4</td>
        <td id="lua-website"><a href="http://www.lua.org/">Lua</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-lzo-package">lzo</td>
        <td id="lzo-version">2.06</td>
        <td id="lzo-website"><a href="http://www.oberhumer.com/opensource/lzo/">lzo</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-matio-package">matio</td>
        <td id="matio-version">1.3.4</td>
        <td id="matio-website"><a href="http://sourceforge.net/projects/matio/">matio</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-mingw-utils-package">mingw-utils</td>
        <td id="mingw-utils-version">0.4-1</td>
        <td id="mingw-utils-website"><a href="http://www.mingw-w64/">MinGW Utilities</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-mpfr-package">mpfr</td>
        <td id="mpfr-version">3.1.0</td>
        <td id="mpfr-website"><a href="http://www.mpfr.org/">mpfr</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-muparser-package">muparser</td>
        <td id="muparser-version">1.34</td>
        <td id="muparser-website"><a href="http://muparser.sourceforge.net/">muParser</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-mxml-package">mxml</td>
        <td id="mxml-version">2.7</td>
        <td id="mxml-website"><a href="http://www.minixml.org/">Mini-XML</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-nettle-package">nettle</td>
        <td id="nettle-version">2.4</td>
        <td id="nettle-website"><a href="http://www.lysator.liu.se/~nisse/nettle/">nettle</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-nsis-package">nsis</td>
        <td id="nsis-version">2.46</td>
        <td id="nsis-website"><a href="http://nsis.sourceforge.net/">NSIS</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-ocaml-core-package">ocaml</td>
        <td id="ocaml-core-version">3.12.1</td>
        <td id="ocaml-core-website"><a href="http://caml.inria.fr/">ocaml</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-ocaml-findlib-package">ocaml-findlib</td>
        <td id="ocaml-findlib-version">1.2.8</td>
        <td id="ocaml-findlib-website"><a href="http://download.camlcity.org/">findlib</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-ocaml-flexdll-package">ocaml-flexdll</td>
        <td id="ocaml-flexdll-version">0.11</td>
        <td id="ocaml-flexdll-website"><a href="http://alain.frisch.fr/">flexdll</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-ocaml-lablgtk2-package">ocaml-lablgtk2</td>
        <td id="ocaml-lablgtk2-version">2.14.2</td>
        <td id="ocaml-lablgtk2-website"><a href="http://forge.ocamlcore.org/">lablgtk2</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-ogg-package">ogg</td>
        <td id="ogg-version">1.3.0</td>
        <td id="ogg-website"><a href="http://www.xiph.org/ogg/">OGG</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-old-package">old</td>
        <td id="old-version">0.17</td>
        <td id="old-website"><a href="http://blitiri.com.ar/p/old/">old</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-openal-package">openal</td>
        <td id="openal-version">1.14</td>
        <td id="openal-website"><a href="http://kcat.strangesoft.net/openal.html">openal</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-opencore-amr-package">opencore-amr</td>
        <td id="opencore-amr-version">0.1.2</td>
        <td id="opencore-amr-website"><a href="http://opencore-amr.sourceforge.net/">opencore-amr</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-opencsg-package">opencsg</td>
        <td id="opencsg-version">1.3.2</td>
        <td id="opencsg-website"><a href="http://www.opencsg.org/">opencsg</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-openexr-package">openexr</td>
        <td id="openexr-version">1.7.0</td>
        <td id="openexr-website"><a href="http://www.openexr.com/">OpenEXR</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-openscenegraph-package">openscenegraph</td>
        <td id="openscenegraph-version">3.0.1</td>
        <td id="openscenegraph-website"><a href="http://www.openscenegraph.org/">OpenSceneGraph</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-openssl-package">openssl</td>
        <td id="openssl-version">1.0.1</td>
        <td id="openssl-website"><a href="http://www.openssl.org/">openssl</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-pango-package">pango</td>
        <td id="pango-version">1.29.3</td>
        <td id="pango-website"><a href="http://www.pango.org/">Pango</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-pangomm-package">pangomm</td>
        <td id="pangomm-version">2.28.2</td>
        <td id="pangomm-website"><a href="http://www.pango.org/">Pangomm</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-pcre-package">pcre</td>
        <td id="pcre-version">8.30</td>
        <td id="pcre-website"><a href="http://www.pcre.org/">PCRE</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-pdcurses-package">pdcurses</td>
        <td id="pdcurses-version">3.4</td>
        <td id="pdcurses-website"><a href="http://pdcurses.sourceforge.net/">PDcurses</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-pdflib_lite-package">pdflib_lite</td>
        <td id="pdflib_lite-version">7.0.5</td>
        <td id="pdflib_lite-website"><a href="http://www.pdflib.com/download/free-software/pdflib-lite-7/">PDFlib Lite</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-pfstools-package">pfstools</td>
        <td id="pfstools-version">1.8.5</td>
        <td id="pfstools-website"><a href="http://pfstools.sourceforge.net/">pfstools</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-physfs-package">physfs</td>
        <td id="physfs-version">2.0.2</td>
        <td id="physfs-website"><a href="http://icculus.org/physfs/">physfs</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-pixman-package">pixman</td>
        <td id="pixman-version">0.25.2</td>
        <td id="pixman-website"><a href="http://cairographics.org/">pixman</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-plotmm-package">plotmm</td>
        <td id="plotmm-version">0.1.2</td>
        <td id="plotmm-website"><a href="http://plotmm.sourceforge.net/">PlotMM</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-plotutils-package">plotutils</td>
        <td id="plotutils-version">2.6</td>
        <td id="plotutils-website"><a href="http://www.gnu.org/software/plotutils/">plotutils</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-poco-package">poco</td>
        <td id="poco-version">1.4.3p1</td>
        <td id="poco-website"><a href="http://pocoproject.org/">POCO C++ Libraries</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-popt-package">popt</td>
        <td id="popt-version">1.16</td>
        <td id="popt-website"><a href="http://freshmeat.net/projects/popt/">popt</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-portaudio-package">portaudio</td>
        <td id="portaudio-version">19_20071207</td>
        <td id="portaudio-website"><a href="http://www.portaudio.com/">portaudio</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-postgresql-package">postgresql</td>
        <td id="postgresql-version">9.1.3</td>
        <td id="postgresql-website"><a href="http://www.postgresql.org/">PostgreSQL</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-proj-package">proj</td>
        <td id="proj-version">4.8.0</td>
        <td id="proj-website"><a href="http://trac.osgeo.org/proj/">proj</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-pthreads-package">pthreads</td>
        <td id="pthreads-version">2-8-0</td>
        <td id="pthreads-website"><a href="http://sourceware.org/pthreads-win32/">Pthreads-w32</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-qjson-package">qjson</td>
        <td id="qjson-version">0.7.1</td>
        <td id="qjson-website"><a href="http://qjson.sourceforge.net/">QJson</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-qt-package">qt</td>
        <td id="qt-version">4.8.1</td>
        <td id="qt-website"><a href="http://qt.nokia.com/">Qt</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-qwtplot3d-package">qwtplot3d</td>
        <td id="qwtplot3d-version">0.2.7</td>
        <td id="qwtplot3d-website"><a href="http://qwtplot3d.sourceforge.net/">QwtPlot3D</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-readline-package">readline</td>
        <td id="readline-version">6.2</td>
        <td id="readline-website"><a href="http://tiswww.case.edu/php/chet/readline/rltop.html">Readline</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-sdl-package">sdl</td>
        <td id="sdl-version">1.2.15</td>
        <td id="sdl-website"><a href="http://www.libsdl.org/">SDL</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-sdl_image-package">sdl_image</td>
        <td id="sdl_image-version">1.2.12</td>
        <td id="sdl_image-website"><a href="http://www.libsdl.org/projects/SDL_image/">SDL_image</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-sdl_mixer-package">sdl_mixer</td>
        <td id="sdl_mixer-version">1.2.12</td>
        <td id="sdl_mixer-website"><a href="http://www.libsdl.org/projects/SDL_mixer/">SDL_mixer</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-sdl_net-package">sdl_net</td>
        <td id="sdl_net-version">1.2.8</td>
        <td id="sdl_net-website"><a href="http://www.libsdl.org/projects/SDL_net/">SDL_net</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-sdl_pango-package">sdl_pango</td>
        <td id="sdl_pango-version">0.1.2</td>
        <td id="sdl_pango-website"><a href="http://sdlpango.sourceforge.net/">SDL_Pango</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-sdl_sound-package">sdl_sound</td>
        <td id="sdl_sound-version">1.0.3</td>
        <td id="sdl_sound-website"><a href="http://icculus.org/SDL_sound/">SDL_sound</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-sdl_ttf-package">sdl_ttf</td>
        <td id="sdl_ttf-version">2.0.11</td>
        <td id="sdl_ttf-website"><a href="http://www.libsdl.org/projects/SDL_ttf/">SDL_ttf</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-smpeg-package">smpeg</td>
        <td id="smpeg-version">0.4.5+cvs20030824</td>
        <td id="smpeg-website"><a href="http://icculus.org/smpeg/">smpeg</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-speex-package">speex</td>
        <td id="speex-version">1.2rc1</td>
        <td id="speex-website"><a href="http://www.speex.org/">Speex</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-sqlite-package">sqlite</td>
        <td id="sqlite-version">3071100</td>
        <td id="sqlite-website"><a href="http://www.sqlite.org/">SQLite</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-suitesparse-package">suitesparse</td>
        <td id="suitesparse-version">3.7.0</td>
        <td id="suitesparse-website"><a href="http://www.cise.ufl.edu/research/sparse/SuiteSparse/">SuiteSparse</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-t4k_common-package">t4k_common</td>
        <td id="t4k_common-version">0.1.1</td>
        <td id="t4k_common-website"><a href="http://tux4kids.alioth.debian.org/">t4k_common</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-taglib-package">taglib</td>
        <td id="taglib-version">1.7.1</td>
        <td id="taglib-website"><a href="http://developer.kde.org/~wheeler/taglib.html">TagLib</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-theora-package">theora</td>
        <td id="theora-version">1.1.1</td>
        <td id="theora-website"><a href="http://theora.org/">Theora</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-tiff-package">tiff</td>
        <td id="tiff-version">4.0.1</td>
        <td id="tiff-website"><a href="http://www.remotesensing.org/libtiff/">LibTIFF</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-tinyxml-package">tinyxml</td>
        <td id="tinyxml-version">2.6.2</td>
        <td id="tinyxml-website"><a href="http://sourceforge.net/projects/tinyxml/">tinyxml</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-tre-package">tre</td>
        <td id="tre-version">0.8.0</td>
        <td id="tre-website"><a href="http://laurikari.net/tre/">TRE</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-vigra-package">vigra</td>
        <td id="vigra-version">1.8.0</td>
        <td id="vigra-website"><a href="http://hci.iwr.uni-heidelberg.de/vigra">vigra</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-vmime-package">vmime</td>
        <td id="vmime-version">0.9.1</td>
        <td id="vmime-website"><a href="http://vmime.sourceforge.net/">VMime</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-vorbis-package">vorbis</td>
        <td id="vorbis-version">1.3.2</td>
        <td id="vorbis-website"><a href="http://www.vorbis.com/">Vorbis</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-vtk-package">vtk</td>
        <td id="vtk-version">5.8.0</td>
        <td id="vtk-website"><a href="http://www.vtk.org/">vtk</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-winpcap-package">winpcap</td>
        <td id="winpcap-version">4_1_2</td>
        <td id="winpcap-website"><a href="http://www.winpcap.org/">WinPcap</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-wt-package">wt</td>
        <td id="wt-version">3.2.0</td>
        <td id="wt-website"><a href="http://witty.sourceforge.net/">Wt</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-wxwidgets-package">wxwidgets</td>
        <td id="wxwidgets-version">2.8.12</td>
        <td id="wxwidgets-website"><a href="http://www.wxwidgets.org/">wxWidgets</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-x264-package">x264</td>
        <td id="x264-version">20111018-2245</td>
        <td id="x264-website"><a href="http://www.videolan.org/developers/x264.html">x264</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-xerces-package">xerces</td>
        <td id="xerces-version">3.1.1</td>
        <td id="xerces-website"><a href="http://xerces.apache.org/xerces-c/">Xerces-C++</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-xine-lib-package">xine-lib</td>
        <td id="xine-lib-version">1.1.20.1</td>
        <td id="xine-lib-website"><a href="http://www.xine-project.org/">xine-lib</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-xmlwrapp-package">xmlwrapp</td>
        <td id="xmlwrapp-version">0.6.3</td>
        <td id="xmlwrapp-website"><a href="http://sourceforge.net/projects/xmlwrapp/">xmlwrapp</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-xvidcore-package">xvidcore</td>
        <td id="xvidcore-version">1.3.2</td>
        <td id="xvidcore-website"><a href="http://www.xvid.org/">xvidcore</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-xz-package">xz</td>
        <td id="xz-version">5.0.3</td>
        <td id="xz-website"><a href="http://tukaani.org/xz/">XZ</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-zlib-package">zlib</td>
        <td id="zlib-version">1.2.6</td>
        <td id="zlib-website"><a href="http://zlib.net/">zlib</a></td>
    </tr>
    <tr>
        <td id="mingw-w64-zziplib-package">zziplib</td>
        <td id="zziplib-version">0.13.59</td>
        <td id="zziplib-website"><a href="http://zziplib.sourceforge.net/">ZZIPlib</a></td>
    </tr>
    </table>
</div>

<div class="section">
<h2 id="creating-packages">Guidelines for Creating Packages</h2>

    <ol>
    <li>
        <p>
        The package should be a
        <a href="http://www.gnu.org/philosophy/free-sw.html">free</a>
        <a href="http://www.debian.org/social_contract#guidelines">software</a>
        <a href="http://www.opensource.org/osd.html">library</a>
        that is really used by one of your applications.
        </p>

        <p>
        BTW, we're always curious about the applications people are porting.
        We maintain a
        <a href="#used-by">list of projects</a>
        which use MXE.
        No matter whether your project is free or proprietary
        &ndash; as long as it has its own website,
        we'd be happy to link to it.
        </p>

        <p>
        Also, feel free to link to us. :-)
        </p>
    </li>

    <li>
        <p>
        Grep through the <code>src/*.mk</code> files
        to find a project that is most similar to yours.
        (Really, <code>grep</code> is your friend here.)
        </p>

        <p>
        For instance,
        when adding a GNU library,
        you should take a package like
        <a href="https://github.com/mxe/mxe/blob/master/src/gettext.mk">gettext.mk</a>
        or
        <a href="https://github.com/mxe/mxe/blob/master/src/libiconv.mk">libiconv.mk</a>
        as the base of your work.
        When using a SourceForge project,
        you could start with a copy of
        <a href="https://github.com/mxe/mxe/blob/master/src/xmlwrapp.mk">xmlwrapp.mk</a>.
        And so on.
        </p>
    </li>

    <li>
        <p>
        Adjust the comments,
        fill in the <code>$(PKG)_*</code> fields.
        </p>

        <p>
        Be especially careful with the <code>$(PKG)_DEPS</code> section.
        The easiest way to get the dependencies right
        is to start with a minimal setup.
        That is,
        initialize MXE with <code>make gcc</code> only,
        then check whether your package builds successfully.
        </p>

        <p>
        Always list the dependency on <code>gcc</code> explicitly:
        </p>
        <pre>$(PKG)_DEPS     := gcc ...</pre>
    </li>

    <li>
        <p>
        Write your <code>$(PKG)_BUILD</code>.
        If your library has a <code>./configure</code> script,
        enable/disable all dependency libraries explicitly
        via "<code>--enable-*</code>" and "<code>--disable-*</code>" options.
        </p>
    </li>

    <li>
        <p>
        You might also have to provide a patch for it.
        In that case, have a look at other patches such as
        <a href="https://github.com/mxe/mxe/blob/master/src/sdl-2-fix-dinput.patch">sdl-2-fix-dinput.patch</a>.
        In particular, each patch file should be named as:
        </p>
        <pre>PACKAGE-PATCHNUMBER-DESCRIPTION.patch</pre>
        <p>
        and should start with:
        </p>
        <pre>This file is part of MXE.
See index.html for further information.

This patch has been taken from:
https://...</pre>
        <p>
        where the URL points to the
        bugtracker entry,
        mailing list entry or
        website
        you took the patch from.
        </p>

        <p>
        If you created the patch yourself,
        please offer it to the upstream project first,
        and point to <em>that</em> URL,
        using the same wording:
        "This patch has been taken from:".
        </p>

        <p>
        Depending on the feedback you get from the upstream project,
        you might want to improve your patch.
        </p>
    </li>

    <li>
        <p>
        If you find some time,
        please provide a minimal test program for it.
        It should be
        simple,
        stand alone and
        should work unmodified for many (all?) future versions of the library.
        Test programs are named as:
        </p>
        <pre>PACKAGE-test.c</pre>
        or
        <pre>PACKAGE-test.cpp</pre>
        <p>
        depending on whether it is a C or C++ library.
        To get a clue,
        please have a look at existing test programs such as
        <a href="https://github.com/mxe/mxe/blob/master/src/sdl-test.c">sdl-test.c</a>.
        </p>

        <p>
        At the very end of your <code>*.mk</code> file
        you should build the test program in a generic way,
        using strict compiler flags.
        The last few lines of
        <a href="https://github.com/mxe/mxe/blob/master/src/sdl.mk">sdl.mk</a>
        will give you a clue.
        </p>
    </li>

    <li>
        <p>
        You could also try to provide a <code>$(PKG)_UPDATE</code> section.
        However, that requires some experience and "feeling" for it.
        So it is perfectly okay if you leave the <code>$(PKG)_UPDATE</code> section empty.
        We'll fill that in for you.
        It's a funny exercise.
        </p>
    </li>

    <li>
        <p>
        Check that you don't have "dirty stuff" in your <code>*.mk</code> files,
        such as TAB characters or trailing spaces at lines endings.
        Have a look at random <code>*.mk</code> files
        to get a feeling for the coding style.
        </p>

        <p>
        The same holds for your test program.
        </p>

        <p>
        However, patch files should always appear
        in the same coding style as the files they are patching.
        </p>

        <p>
        Finally, in your <code>$(PKG)_BUILD</code> section,
        please check that you use our portability variables:
        </p>
        <table class="translation">
            <tr><td><code>bash</code></td>      <td>&rarr;</td><td><code>$(SHELL)</code></td></tr>
            <tr><td><code>install</code></td>   <td>&rarr;</td><td><code>$(INSTALL)</code></td></tr>
            <tr><td><code>libtool</code></td>   <td>&rarr;</td><td><code>$(LIBTOOL)</code></td></tr>
            <tr><td><code>libtoolize</code></td><td>&rarr;</td><td><code>$(LIBTOOLIZE)</code></td></tr>
            <tr><td><code>make</code></td>      <td>&rarr;</td><td><code>$(MAKE)</code></td></tr>
            <tr><td><code>patch</code></td>     <td>&rarr;</td><td><code>$(PATCH)</code></td></tr>
            <tr><td><code>sed</code></td>       <td>&rarr;</td><td><code>$(SED)</code></td></tr>
        </table>
    </li>

    <li>
        <p>
        Check whether everything runs fine.
        If you have some trouble,
        don't hesitate to ask on the
        <a href="http://lists.nongnu.org/mailman/listinfo/mingw-cross-env-list">mailing list</a>,
        providing your <code>*.mk</code> file so far.
        </p>
    </li>

    <li>
        <p>
        Propose your final <code>*.mk</code> file to the mailing list.
        Don't forget to tell us
        if there are some pieces in your <code>*.mk</code> file
        you feel unsure about.
        We'll then have a specific look at those parts,
        which avoids trouble for you and us in the future.
        </p>
    </li>
    </ol>
</div>

<div class="section">
<h2 id="copyright">Copyright © <span class="years">2007–2012</span></h2>

    <ul id="authors-list" class="compact-list">
    <li>Volker Grabsch</li>
    <li>Mark Brand</li>
    <li>Tony Theodore</li>
    <li><a href="https://www.ohloh.net/p/mxe/contributors">... and many other contributors</a></li>
    </ul>

    <p>(contact via the
       <a href="http://lists.nongnu.org/mailman/listinfo/mingw-cross-env-list">project mailing list</a>)</p>

    <p>
    Permission is hereby granted, free of charge, to any person obtaining
    a copy of this software and associated documentation files (the
    "Software"), to deal in the Software without restriction, including
    without limitation the rights to use, copy, modify, merge, publish,
    distribute, sublicense, and/or sell copies of the Software, and to
    permit persons to whom the Software is furnished to do so, subject
    to the following conditions:
    </p>

    <p>
    The above copyright notice and this permission notice shall be
    included in all copies or substantial portions of the Software.
    </p>

    <p>
    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
    EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
    MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
    IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
    CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
    TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
    SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
    </p>
</div>

<div class="section">
<h2 id="history">History</h2>

    <dl>

    <dt>2012-04-12 &ndash; Release <span id="latest-version">2.22</span></dt>
    <dd>
        <p>
        <a href="http://mxe.cc/#download">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.22">Changelog</a>
        </p>

        <p>
        The project has been
        <a href="http://lists.nongnu.org/archive/html/mingw-cross-env-list/2012-03/msg00101.html">renamed</a>
        from
        mingw-cross-env (MinGW cross compiling environment)
        to
        MXE (M&nbsp;cross&nbsp;environment).
        </p>

        <p>
        The release tarballs have been replaced with a <a href="#download">Git checkout</a>.
        </p>

        <p>
        Most packages were updated to their latest version.
        </p>

        <p>
        New packages are supported:
        agg, cgal, eigen, file, gta, json-c, libgnurx, libharu,
        libircclient, libssh2, libxml++, llvm, lzo, mpfr, nettle,
        opencsg, qjson, qwtplot3d, vtk, and wt.
        </p>
    </dd>

    <dt>2011-06-07 &ndash; Release 2.21</dt>
    <dd>
        <p>
        <a href="https://bitbucket.org/vog/mingw-cross-env/downloads/mingw-cross-env-2.21.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.21">Changelog</a>
        </p>

        <p>
        Minor bugfixes in several packages.
        </p>

        <p>
        Almost all packages are updated to their latest version.
        </p>

        <p>
        Packages gtkmm and gtksourceviewmm have been renamed to gtkmm2 and gtksourceviewmm2.
        </p>

        <p>
        New packages are supported:
        libass, poco, and t4k_common.
        </p>
    </dd>

    <dt>2011-04-05 &ndash; Release 2.20</dt>
    <dd>
        <p>
        <a href="https://bitbucket.org/vog/mingw-cross-env/downloads/mingw-cross-env-2.20.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.20">Changelog</a>
        </p>

        <p>
        This release fixes a download error caused by the pixman project
        (a sudden change of their URL scheme without proper redirects).
        <a href="http://www.w3.org/Provider/Style/URI">That sort of thing should never happen!</a>
        </p>
    </dd>

    <dt>2011-03-19 &ndash; Release 2.19</dt>
    <dd>
        <p>
        <a href="https://bitbucket.org/vog/mingw-cross-env/downloads/mingw-cross-env-2.19.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.19">Changelog</a>
        </p>

        <p>
        The download mechanisms are improved.
        </p>

        <p>
        A CMake toolchain file is provided
        to simplify cross-compiling projects which use CMake.
        </p>

        <p>
        Support for Debian/Lenny is dropped.
        </p>

        <p>
        Package gtk is renamed to gtk2.
        </p>

        <p>
        Almost all packages are updated to their latest version.
        </p>

        <p>
        New packages are supported:
        dbus, graphicsmagick, libical, liboauth, physfs, and vigra.
        </p>

        <p>
        Note for <code>boost::filesystem</code> users:
        <a href="http://beta.boost.org/doc/libs/1_46_1/libs/filesystem/v3/doc/index.htm">Version 3 is a major revision</a>
        and now the default in 1.46.
        </p>
    </dd>

    <dt>2010-12-15 &ndash; Release 2.18</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.18.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.18">Changelog</a>
        </p>

        <p>
        This release fixes a checksum error caused by the atkmm project
        (a sudden change of their current source tarball).
        <a href="http://www.w3.org/Provider/Style/URI">That sort of thing should never happen!</a>
        </p>
    </dd>

    <dt>2010-12-11 &ndash; Release 2.17</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.17.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.17">Changelog</a>
        </p>

        <p>
        This release provides some improvements of the build system
        such as an automatic check for most of the requirements.
        </p>

        <p>
        All packages are updated to their latest version.
        </p>

        <p>
        New packages are supported:
        bfd, blas, cblas, dcmtk, ftgl, lapack, lcms1,
        mingw-utils, mxml, suitesparse and tinyxml.
        </p>
    </dd>

    <dt>2010-10-27 &ndash; Release 2.16</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.16.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.16">Changelog</a>
        </p>

        <p>
        This release provides lots of improvements to
        the build system as well as the documentation.
        </p>

        <p>
        Support for OpenSolaris is dropped.
        </p>

        <p>
        Almost all packages are updated to their latest version.
        </p>

        <p>
        Many new packages are supported:
        atkmm, cairomm, cunit, faac, faad2, ffmpeg, gdk-pixbuf, glibmm,
        gtkglextmm, gtkmm, gtksourceview, gtksourceviewmm, imagemagick,
        lame, libiberty, libsigc++, libvpx, matio, openal, opencore-amr,
        pangomm, pfstools, plotmm, sdl_sound and x264.
        </p>
    </dd>

    <dt>2010-06-16 &ndash; Release 2.15</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.15.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.15">Changelog</a>
        </p>

        <p>
        This release fixes download errors caused by the Qt project
        (a sudden change of their current source tarball).
        </p>

        <p>
        Almost all packages are updated to their latest version.
        </p>
    </dd>

    <dt>2010-06-08 &ndash; Release 2.14</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.14.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.14">Changelog</a>
        </p>

        <p>
        This release fixes download errors caused by the MinGW project
        (a sudden change of their URL scheme without proper redirects).
        <a href="http://www.w3.org/Provider/Style/URI">That sort of thing should never happen!</a>
        </p>

        <p>
        Almost all packages are updated to their latest version.
        </p>

        <p>
        New packages are supported:
        libarchive, libgee and xvidcore.
        </p>
    </dd>

    <dt>2010-05-31 &ndash; Release 2.13</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.13.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.13">Changelog</a>
        </p>

        <p>
        This release switches back from TDM to the official GCC,
        thus supporting the current GCC&nbsp;4.5.
        </p>

        <p>
        The set of DirectX headers is improved and more complete.
        </p>

        <p>
        The deadlock issues with Pthreads-w32 are fixed.
        </p>

        <p>
        A static build of GDB is provided,
        i.e. a standalone "gdb.exe"
        that doesn't require any extra DLLs.
        </p>

        <p>
        More packages are backed by test programs.
        </p>

        <p>
        Many "sed hacks" are replaced by proper portability patches.
        </p>

        <p>
        Almost all packages are updated to their latest version.
        </p>

        <p>
        Many new packages are supported:
        fribidi, gc, gdb, gmp, gsl, gst-plugins-base, gst-plugins-good,
        gstreamer, gtkglext, guile, libcroco, libffi, liboil, libpaper,
        libshout, libunistring and xine-lib.
        </p>
    </dd>

    <dt>2010-02-21 &ndash; Release 2.12</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.12.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.12">Changelog</a>
        </p>

        <p>
        This release fixes some minor build issues,
        and contains a first small set of test programs
        to check the package builds.
        </p>

        <p>
        The build rules are simplified
        by calling generators like Autotools and Flex,
        instead of patching the generated files.
        </p>

        <p>
        Almost all packages are updated to their latest version.
        </p>

        <p>
        Many new packages are supported:
        aubio, devil, directx, exiv2, fftw, freeimage, gsoap,
        id3lib, liblo, libpano13, librsvg, libsamplerate,
        muparser, openscenegraph, portaudio and sdl_pango.
        </p>
    </dd>

    <dt>2010-02-20 &ndash; Release 2.11</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.11.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.11">Changelog</a>
        </p>

        <p>
        This release contains a packaging bug.
        Please use release 2.12 instead.
        </p>
    </dd>

    <dt>2009-12-23 &ndash; Release 2.10</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.10.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.10">Changelog</a>
        </p>

        <p>
        This release adds support for many new packages:
        flac, libmad, libsndfile, sdl_net, speex, postgresql,
        freetds, openssl, plotutils, taglib, lcms, freeglut,
        xerces and zziplib.
        </p>

        <p>
        Almost all packages are updated to their latest version.
        </p>

        <p>
        In addition to the libraries
        some command line tools such as psql.exe are built, too.
        </p>

        <p>
        The placements of logfiles, as well as many other build details, have been improved.
        </p>
    </dd>

    <dt>2009-10-24 &ndash; Release 2.9</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.9.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.9">Changelog</a>
        </p>

        <p>
        This release adds support for Qt, VMime and libmng.
        </p>

        <p>
        The target triplet is updated to i686-pc-mingw32.
        </p>

        <p>
        OpenMP support is enabled in GCC.
        </p>

        <p>
        Almost all packages are updated to their latest version.
        </p>
    </dd>

    <dt>2009-09-11 &ndash; Release 2.8</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.8.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.8">Changelog</a>
        </p>

        <p>
        This release comes with a better look &amp; feel
        by providing a highlevel overview of the build process.
        </p>

        <p>
        The detailed build messages are stored into
        separate log files for each package,
        so parallel builds don't intermix them anymore.
        </p>

        <p>
        The download URLs of SourceForge packages
        are adjusted to ensure that
        the selected SourceForge mirror is really used
        and not circumvalented via HTTP redirects to other mirrors.
        </p>

        <p>
        Almost all packages are updated to their latest version.
        </p>

        <p>
        The whole mingw-cross-env project has moved to
        <a href="https://savannah.nongnu.org/">Savannah</a>.
        So all URIs have changed,
        but the old URIs
        redirect to the new locations seamlessly.
        </p>

        <p>
        Everyone is invited to join the freshly created
        <a href="http://lists.nongnu.org/mailman/listinfo/mingw-cross-env-list">project mailing list</a>.
        </p>
    </dd>

    <dt>2009-08-11 &ndash; Release 2.7</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.7.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.7">Changelog</a>
        </p>

        <p>
        This release
        provides an improved version recognition
        for SourceForge packages.
        SourceForge changed their page layout
        in a way that makes it much harder
        to identify the current version of a package.
        </p>

        <p>
        Additionally,
        almost all packages are updated to their latest version.
        </p>
    </dd>

    <dt>2009-06-19 &ndash; Release 2.6</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.6.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.6">Changelog</a>
        </p>

        <p>
        This release contains some portability fixes
        which allow it to run on a wider range of systems
        such as Frugalware.
        </p>

        <p>
        The documentation and website are completely revised.
        </p>

        <p>
        New packages such as
        CppUnit, libUsb, NSIS, Popt, SQLite and Theora
        are supported.
        </p>

        <p>
        Almost all packages are updated to their latest version.
        </p>

        <p>
        A new command "make download" is implemented.
        </p>
    </dd>

    <dt>2009-04-06 &ndash; Release 2.5</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.5.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.5">Changelog</a>
        </p>

        <p>
        This release fixes a download error caused by the MinGW project.
        They suddenly changed the names of their source tarballs.
        <a href="http://www.w3.org/Provider/Style/URI">That sort of thing should never happen!</a>
        </p>

        <p>
        This release also contains some bugfixes
        which allow it to run on a wider range of systems.
        </p>

        <p>
        All downloaded files are now
        verified by their SHA-1 checksums.
        </p>

        <p>
        New versions of various packages are supported.
        </p>
    </dd>

    <dt>2009-03-08 &ndash; Release 2.4</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.4.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.4">Changelog</a>
        </p>

        <p>
        This release provides many new libraries such as
        wxWidgets, GTK+ and OpenEXR.
        </p>

        <p>
        In addition, new versions of various packages
        are supported.
        </p>
    </dd>

    <dt>2009-02-09 &ndash; Release 2.3</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.3.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.3">Changelog</a>
        </p>

        <p>
        This release fixes some serious build problems on FreeBSD and MacOS-X.
        </p>

        <p>
        The Makefile has a new target "clean-pkg"
        and allows to be called from a separate build directory
        via "make -f .../Makefile".
        </p>

        <p>
        Some new versions of the packages are supported,
        especially GCC-4.3 by switching from MinGW GCC to
        <a href="http://www.tdragon.net/recentgcc/">TDM-GCC</a>.
        </p>
    </dd>

    <dt>2009-01-31 &ndash; Release 2.2<dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.2.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.2">Changelog</a>
        </p>

        <p>
        This release fixes some minor build problems.
        </p>

        <p>
        It also supports some new packages and
        some newer versions of the already supported packages.
        </p>

        <p>
        Parallelization is now disabled by default.
        </p>
    </dd>

    <dt>2008-12-13 &ndash; Release 2.1</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.1.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.1">Changelog</a>
        </p>

        <p>
        This release fixes a download error caused by the GDAL project.
        They suddenly changed their download URLs.
        <a href="http://www.w3.org/Provider/Style/URI">That sort of thing should never happen!</a>
        </p>

        <p>
        In addition, some newer versions of various packages are supported.
        </p>

        <p>
        There is also a small compatibility fix for OS X.
        </p>
    </dd>

    <dt>2008-11-10 &ndash; Release 2.0</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.0.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/2.0">Changelog</a>
        </p>

        <p>
        The shell script has been rewritten as Makefile
        and supports partial builds and parallel builds.
        </p>

        <p>
        As usual,
        this release also supports some new packages and
        some newer versions of the already supported packages.
        </p>
    </dd>

    <dt>2008-01-11 &ndash; Release 1.4</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-1.4.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/1.4">Changelog</a>
        </p>

        <p>
        This release now includes a tutorial by Hans Bezemer
        and has improved compile options of FLTK.
        As usual, it supports some newer versions of the libraries.
        </p>

        <p>
        At the <a href="http://www.fefe.de/nowindows/">request of its author</a>,
        libowfat is no longer supported from this release on.
        </p>

        <p>
        The script now uses a specific SourceForge mirror
        instead of randomly chosen ones,
        because the download phase
        often stumbled on some very slow mirrors.
        </p>
    </dd>

    <dt>2007-12-23 &ndash; Release 1.3</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-1.3.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/1.3">Changelog</a>
        </p>

        <p>
        A sudden change in the download URLs of GEOS
        made the automatic download fail.
        <a href="http://www.w3.org/Provider/Style/URI">Such changes should never happen!</a>
        But it happened,
        and this quick release is an attempt to limit the damage.
        </p>

        <p>
        This release also supports some newer versions of the libraries
        including support for fontconfig-2.5.0.
        </p>
    </dd>

    <dt>2007-12-13 &ndash; Release 1.2</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-1.2.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/1.2">Changelog</a>
        </p>

        <p>
        This release is a switch from gcc-3 to gcc-4.
        It also supports a new library and
        some newer versions of the already supported libraries.
        </p>
    </dd>

    <dt>2007-07-24 &ndash; Release 1.1</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-1.1.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/1.1">Changelog</a>
        </p>

        <p>
        This release is the result of the public attention the release 1.0 got.
        It contains many improvements suggested by its first users,
        and adds support for many new libraries.
        </p>

        <p>
        Thanks to Rocco Rutte who contributed many code snippets.
        </p>
    </dd>

    <dt>2007-06-19 &ndash; Release 1.0</dt>
    <dd>
        <p>
        <a href="http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-1.0.tar.gz">Download</a> |
        <a href="http://hg.savannah.nongnu.org/hgweb/mingw-cross-env/log/1.0">Changelog</a>
        </p>

        <p>
        This first release has been created in a 7-day-sprint.
        </p>
    </dd>

    <dt>2007-06-12 &ndash; Project start</dt>
    <dd>
    </dd>

    </dl>
</div>

<div class="section">
<h2 id="see-also">See also</h2>

    <h3>This project</h3>

    <ul class="compact-list">
    <li>
        <a href="http://mxe.cc/">Website</a>
    </li>
    <li>
        <a href="https://github.com/mxe/mxe">Entry on GitHub</a>
    </li>
    <li>
        <a href="https://www.ohloh.net/p/mxe">Entry on Ohloh</a>
    </li>
    <li>
        <a href="http://freshmeat.net/projects/mingw_cross_env">Entry on Freshmeat</a>
    </li>
    <li>
        <a href="http://savannah.nongnu.org/projects/mingw-cross-env">Entry on Savannah</a>
    </li>
    <li>
        <a href="http://lists.debian.org/debian-embedded/2007/06/msg00007.html">First release anouncement</a>
        and the discussion around it
    </li>
    </ul>

    <h3>Related projects</h3>

    <ul>
    <li>
        <a href="http://download.opensuse.org/repositories/windows:/mingw:/win32/SLE_11/noarch/">openSUSE MinGW packages</a>
        <br>
        win32 cross compiling packages by openSUSE
    </li>
    <li>
        <a href="https://admin.fedoraproject.org/pkgdb/acls/list/**mingw**">Fedora MinGW packages</a>
        <br>
        win32 cross compiling packages by Fedora
    </li>
    <li>
        <a href="http://www.sandroid.org/imcross/">IMCROSS</a>
        <br>
        another project with similar goal
    </li>
    <li>
        <a href="http://packages.debian.org/stable/devel/mingw32">mingw32 Debian package</a>
        <br>
        bare win32 cross compiler
    </li>
    <li>
        <a href="http://gnuwin32.sourceforge.net/">GnuWin32</a>
        <br>
        win32 ports of many free software packages
    </li>
    <li>
        <a href="http://www.libsdl.org/extras/win32/cross/README.txt">MinGW cross-compiler build script</a>
        <br>
        old script provided by the
        <a href="http://www.libsdl.org/">SDL project</a>
    </li>
    </ul>

    <h3>Related articles</h3>

    <ul>
    <li>
        <a href="http://thebeezspeaks.blogspot.com/2009/04/cross-compilers-new-wave.html">Cross compilers, the new wave</a>
        <br>
        appeared on
        <a href="http://lxer.com/module/newswire/view/118868">LXer</a>
        and
        <a href="http://www.linuxtoday.com/developer/2009041501335RVSWDV">Linux Today</a>
    </li>
    <li>
        <a href="http://wiki.njh.eu/Cross_Compiling_for_Win32">Cross Compiling for Win32</a>
        <br>
        overview of win32 cross compiling
    </li>
    <li>
        <a href="http://www.mingw.org/wiki/LinuxCrossMinGW">MinGW cross compiler for Linux build environment</a>
        <br>
        official tutorial of the
        <a href="">MinGW project</a>
    </li>
    <li>
        <a href="http://wiki.wxwidgets.org/Cross-Compiling_Under_Linux#Cross-compiling_under_Linux_for_MS_Windows">Cross-compiling under Linux for MS Windows</a>
        <br>
        old tutorial provided by the
        <a href="http://www.wxwidgets.org/">wxWidgets project</a>
    </li>
    </ul>
</div>

<div class="section">
<h2 id="used-by">Projects which use MXE</h2>

    <ul class="compact-list">
    <li>
        <a href="http://toppler.sourceforge.net/">Tower Toppler</a>
    </li>
    <li>
        <a href="http://pushover.sourceforge.net/">Pushover</a>
    </li>
    <li>
        <a href="http://www.xs4all.nl/~thebeez/4tH/">The 4tH Compiler</a>
    </li>
    <li>
        <a href="http://springrts.com/">Spring RTS</a>
    </li>
    <li>
        <a href="http://ph.on.things.free.fr/projects/ube/">Ube</a>
    </li>
    <li>
        <a href="http://marathon.sourceforge.net/">Marathon Aleph One</a>
    </li>
    <li>
        <a href="http://sourceforge.net/projects/aorta/">Aorta</a>
    </li>
    <li>
        <a href="http://msmtp.sourceforge.net/">msmtp</a>
    </li>
    <li>
        <a href="http://mpop.sourceforge.net/">mpop</a>
    </li>
    <li>
        <a href="http://cvtool.sourceforge.net/">cvtool</a>
    </li>
    <li>
        <a href="http://tux4kids.alioth.debian.org/tuxmath/">Tux Math</a>
    </li>
    <li>
        <a href="http://tux4kids.alioth.debian.org/tuxtype/">Tux Typing</a>
    </li>
    <li>
        <a href="http://gcompris.net/">GCompris</a>
    </li>
    <li>
        <a href="http://www.nongnu.org/gta/">Generic Tagged Arrays</a>
    </li>
    <li>
        <a href="http://qtads.sourceforge.net/">QTads</a>
    </li>
    <li>
        <a href="http://ufoai.ninex.info/">UFO: Alien Invasion</a>
    </li>
    <li>
        <a href="http://www.pokerth.net/">PokerTH</a>
    </li>
    <li>
        <a href="http://www.tug.org/texworks/">TeXworks</a>
    </li>
    <li>
        <a href="http://bino.nongnu.org/">Bino</a>
    </li>
    <li>
        <a href="http://www.ros.org/wiki/eros">Eros</a>
    </li>
    <li>
        <a href="http://www.bunkus.org/videotools/mkvtoolnix/">MKVToolNix</a>
    </li>
    <li>
        <a href="http://www.openscad.org/">OpenSCAD</a>
    </li>
    <li>
        <a href="http://wz2100.net/">Warzone 2100</a>
    </li>
    <li>
        <a href="http://lightspark.github.com/">Lightspark</a>
    </li>
    <li>
        <a href="http://ifwiki.org/index.php/Hugor">Hugor</a>
    </li>
    </ul>
</div>

</body>
</html>
