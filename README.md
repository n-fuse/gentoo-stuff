Gentoo Linux:

A **source** based (meta) Linux distribution.

- The source code is compiled locally according to the user's preferences
- Precompiled binaries are available for some very large packages and for packages whose source code has not been released

The Gentoo Advantages

- Nearly unlimited flexibility
- Performance
- Rolling Release
- Bleeding Edge Software
- Good Wiki
- Suits for Client and Server and Embedded Devices

Freedom of Choice

- OpenOffice or LibreOffice
- Gnome or KDE or...
- Binary or Open Source GPU drivers
- OpenGL backend (open source or binary)


The advantages reflected by quotes from Gentoo users:

> I don't know when I installed my system from scratch last time

> Forget about OS versions


In many cases it is even possible to have multiple implementations/ versions

Example:

    client6 ~ # eselect
    Usage: eselect <global options> <module name> <module options>

    Global options:
      --brief                   Make output shorter
      --colour=<yes|no|auto>    Enable or disable colour output (default 'auto')

    Built-in modules:
      help                      Display a help message
      usage                     Display a usage message
      version                   Display version information

    Extra modules:
      binutils                  Manage installed versions of sys-devel/binutils
      blas                      Manage installed BLAS implementations
      cblas                     Manage installed CBLAS implementations
      ctags                     Manage /usr/bin/ctags implementations
      editor                    Manage the EDITOR environment variable
      env                       Manage environment variables set in /etc/env.d/
      fontconfig                Manage fontconfig /etc/fonts/conf.d/ symlinks
      java-nsplugin             Manage the Java plugin for Netscape-like Browsers
      java-vm                   Manage the Java system and user VM
      kernel                    Manage the /usr/src/linux symlink
      locale                    Manage the LANG environment variable
      mesa                      Manage the OpenGL driver architecture used by media-libs/mesa
      modules                   Query eselect modules
      news                      Read Gentoo ("GLEP 42") news items
      notify-send               Manage /usr/bin/notify-send implementation
      opencl                    Manage the OpenCL implementation used by your system
      opengl                    Manage the OpenGL implementation used by your system
      pager                     Manage the PAGER environment variable
      php                       Manage php installations
      pinentry                  Manage /usr/bin/pinentry implementation
      postgresql                Manage active PostgreSQL client applications and libraries
      profile                   Manage the make.profile symlink
      python                    Manage Python symlinks
      qtgraphicssystem          Manage the system-wide active Qt Graphics System
      rails                     Manage Ruby on Rails versions
      rc                        Manage /etc/init.d scripts in runlevels
      ruby                      Manage ruby symlinks
      vi                        Manage /usr/bin/vi implementations
      visual                    Manage the VISUAL environment variable
      wxwidgets                 Manage the system default wxWidgets profile.

    client6 ~ # eselect java-vm list
    Available Java Virtual Machines:
      [1]   icedtea-bin-6
      [2]   icedtea-bin-7  system-vm

    client6 ~ # eselect editor list
    Available targets for the EDITOR variable:
      [1]   /bin/nano
      [2]   /usr/bin/ex
      [3]   /usr/bin/vi *
      [ ]   (free form)


Portage

- Gentoo's software Repository
- One of the largest compared to other distros
- Bleeding edge packages
- Overlays -- Add other Repos ran by the community

The meta data is online available via
[http://packages.gentoo.org/](http://packages.gentoo.org/)


Ebuild

- Defines variables and functions used to
  compile and install software from source

USE Flags

- Powerful way to make decisions how software is built
- Config files below `/etc/portage/`
- Main config file defines among others:
    - cflags, ex.: `CFLAGS="-O2 -pipe -march=core2 -fomit-frame-pointer"`
    - Apache Modules
    - global use flags, ex.: `lvm2 bash-completion script spice ncurses qemu vhost-net virt-network vepa macvtap spell ...`
    - The Gentoo mirror(s) to use, ex.: `ftp://ftp-stud.fht-esslingen.de/pub/Mirrors/gentoo/`
- Package specific settings go into: `package.use`, `package.unmask`, `package.accept_keywords`

How to install Software:

1.) Find the right package

    client6 ~ # emerge --search git
    Searching...
    [ Results for search key : git ]
    [ Applications found : 51 ]

    *  app-book/git-magic
          Latest version available: 9999
          Latest version installed: [ Not Installed ]
          Size of files: 0 kB
          Homepage:      http://www-cs-students.stanford.edu/~blynn//gitmagic/
          Description:   A guild to Git
          License:

    *  dev-vcs/gitolite
          Latest version available: 2.3.1
          Latest version installed: [ Not Installed ]
          Size of files: 249 kB
          Homepage:      http://github.com/sitaramc/gitolite
          Description:   Highly flexible server for git directory version tracker
          License:       GPL-2
    [...]

2.1) Check what emerge would do using `--pretend`

    emerge dev-vcs/gitolite --pretend

    These are the packages that would be merged, in order:

    Calculating dependencies... done!
    [ebuild  N     ] perl-core/File-Path-2.90.0
    [ebuild  N     ] virtual/perl-File-Path-2.90.0
    [ebuild  N     ] dev-vcs/gitolite-2.3.1  USE="-contrib -vim-syntax"

2.2) 'emerge' it

   `emerge dev-vcs/gitolite`


Other package management use-cases in the following.

How to remove Packages:

`emerge --unmerge dev-vcs/gitolite`

How to update Packages:

`emerge -u dev-vcs/gitolite`

How to update the entire system:

`emerge -uDN world --pretend --keep-going=y`

- `u`, `--update` → update
- `D`, `--deep` → deep dependency resolving
- `N`, `--newuse` → consider new use flags
- `--keep-going` → Continue as much as possible after an error

Example:

    client6 ~ # emerge -uDN world --pretend

    These are the packages that would be merged, in order:

    Calculating dependencies... done!
    [ebuild     U  ] sys-libs/glibc-2.17 [2.15-r3] USE="-nscd% -suid% -systemtap%"
    [ebuild     U  ] sys-devel/gnuconfig-20130516 [20130111]
    [ebuild     U  ] sys-apps/which-2.20-r1 [2.20]
    [ebuild   R    ] virtual/libiconv-0
    [ebuild     U  ] sys-libs/libseccomp-2.1.1 [2.1.0]
    [ebuild     U  ] app-shells/push-1.6 [1.5]
    [ebuild   R   ~] games-util/steam-games-meta-0-r20131107  USE="-steamgames_painkiller%"
    [ebuild   R    ] virtual/libffi-3.0.11
    [ebuild     U  ] dev-libs/libassuan-2.1.1 [2.1.0]
    [ebuild     U  ] app-emulation/emul-linux-x86-baselibs-20131008-r6 [20130224] ABI_X86="(-32)"
    [ebuild     U  ] app-emulation/emul-linux-x86-compat-20131008 [20130224]
    [ebuild     U  ] app-emulation/emul-linux-x86-db-20131008 [20130224]
    [ebuild     UD ] media-libs/libaacs-0.5.0 [0.6.0]
    [ebuild     U  ] app-admin/logrotate-3.8.7 [3.8.6]
    [ebuild     U  ] sys-apps/debianutils-4.4 [4.3.4]
    [ebuild     U  ] sys-apps/kbd-1.15.5-r1 [1.15.3] USE="pam%*"
    [ebuild     U  ] app-admin/eselect-postgresql-1.2.1 [1.2.0]
    [ebuild  N     ] app-admin/eselect-cdparanoia-0.1
    [ebuild     U  ] virtual/man-0-r1 [0]
    [ebuild     U  ] sys-apps/man-pages-3.55 [3.53]
    [ebuild   R    ] media-plugins/gst-plugins-meta-0.10-r8 [0.10-r8] USE="-vaapi%"
    [ebuild     U  ] x11-misc/xdg-utils-1.1.0_rc1_p20130921 [1.1.0_rc1_p20120319]
    [ebuild   R    ] net-fs/cifs-utils-6.1-r1  USE="ads* (-upcall%*)"
    [ebuild     U  ] net-firewall/iptables-1.4.20 [1.4.16.3]
    [ebuild     U  ] sys-process/procps-3.3.8-r2 [3.3.6] USE="{-test%}"
    [ebuild     U  ] dev-db/mysql-init-scripts-2.0_pre1-r6 [2.0_pre1-r3]
    [ebuild     U  ] sys-fs/fuse-2.9.3 [2.9.2] USE="-examples%"
    [ebuild  N     ] app-crypt/p11-kit-0.13  USE="-debug"
    [ebuild     U  ] sys-fs/ntfs3g-2013.1.13 [2012.1.15-r2] USE="-ntfsdecrypt%"
    [ebuild     U  ] sys-apps/xinetd-2.3.15-r1 [2.3.15]
    [ebuild     U  ] dev-db/sqlite-3.8.2 [3.7.17]
    [ebuild     U  ] dev-libs/boehm-gc-7.2e [7.2d-r1]
    [ebuild     U  ] dev-libs/json-c-0.11 [0.9-r1] USE="-doc%"
    [ebuild  N     ] dev-haskell/primitive-0.5.1.0  USE="-doc -hscolour -profile"
    [ebuild  N     ] dev-haskell/deepseq-1.3.0.1  USE="-doc -hscolour -profile"
    [ebuild     U  ] dev-haskell/alex-3.1.2 [3.0.5]
    [ebuild  N     ] dev-haskell/vector-0.10.0.1  USE="-doc -hscolour -profile"
    [ebuild  N     ] dev-haskell/text-0.11.3.1  USE="-developer -doc -hscolour -profile {-test}"
    [ebuild  N     ] dev-haskell/hashable-1.1.2.5  USE="-doc -hscolour -profile {-test}"
    [ebuild  N     ] dev-haskell/hashtables-1.1.2.1  USE="unsafe-tricks -bounds-checking -debug -doc -hscolour -portable -profile -sse4_1"
    [ebuild     U  ] dev-haskell/gtk2hs-buildtools-0.12.4-r2 [0.12.3.1]
    [ebuild     U  ] dev-haskell/cairo-0.12.4-r1 [0.12.3.1]
    [ebuild     U  ] app-emulation/emul-linux-x86-xlibs-20131008 [20130224] ABI_X86="(-32)"
    [ebuild     U  ] media-gfx/nvidia-cg-toolkit-3.1.0013-r2 [2.1.0017-r1] USE="(multilib%*)"
    [ebuild     U  ] app-emulation/emul-linux-x86-medialibs-20131008-r1 [20130224] ABI_X86="(-32)"
    [ebuild     U  ] app-emulation/emul-linux-x86-soundlibs-20131008-r2 [20130224] USE="-pulseaudio%" ABI_X86="(-32)"
    [ebuild     U  ] app-emulation/emul-linux-x86-sdl-20131008 [20130224]
    [ebuild     U  ] app-emulation/emul-linux-x86-opengl-20131008 [20130224] ABI_X86="(-32)"
    [ebuild     U  ] app-emulation/emul-linux-x86-gtklibs-20131008 [20130224]
    [ebuild     U  ] app-emulation/emul-linux-x86-qtlibs-20131008 [20130224]
    [ebuild     U  ] app-emulation/emul-linux-x86-gstplugins-20131008 [20130224]
    [ebuild     U  ] x11-libs/libXfont-1.4.7 [1.4.6]
    [ebuild     U  ] dev-libs/nspr-4.10.2 [4.10]
    [ebuild     U  ] dev-libs/nss-3.15.4 [3.15.2]
    [ebuild     U  ] dev-lang/perl-5.16.3 [5.12.4-r1]
    [ebuild     U  ] dev-perl/Net-Daemon-0.480.0-r1 [0.480.0]
    [ebuild     U  ] dev-perl/TermReadKey-2.300.200 [2.300.0]
    [ebuild     U  ] dev-perl/DelimMatch-1.06-r1 [1.06]
    [ebuild     U  ] dev-perl/PlRPC-0.202.0-r2 [0.202.0]
    [ebuild     U  ] dev-perl/WWW-RobotRules-6.10.0-r1 [6.10.0]
    [ebuild     U  ] dev-perl/HTTP-Cookies-6.0.1-r1 [6.0.0]
    [ebuild     U  ] dev-perl/HTTP-Negotiate-6.0.1-r1 [6.0.0]
    [ebuild     U  ] sys-apps/help2man-1.43.3 [1.40.11]
    [ebuild     U  ] sys-libs/zlib-1.2.8-r1 [1.2.7] ABI_X86="(64%*) (-32) (-x32)"
    [ebuild     U  ] dev-libs/openssl-1.0.1f [1.0.1e-r1]
    [...]
    [ebuild  NS    ] media-libs/libpng-1.5.17-r15 [1.2.50, 1.5.17-r1] USE="apng (-neon)"
    [blocks b      ] <media-sound/cdparanoia-3.10.2-r5 ("<media-sound/cdparanoia-3.10.2-r5" is blocking app-admin/eselect-cdparanoia-0.1)
    [ebuild     U  ] media-libs/libpng-1.2.50-r1 [1.2.50] ABI_X86="(64%*) (-32) (-x32)"
    [ebuild     U  ] media-libs/faac-1.28-r4 [1.28-r3] ABI_X86="(64%*) (-32) (-x32)"
    [ebuild   R   ~] sys-devel/gettext-0.18.3.1-r1  USE="ncurses%*"
    [ebuild     U  ] virtual/jpeg-0-r2 [0] ABI_X86="(64%*) (-32) (-x32)"
    [ebuild  NS    ] virtual/jpeg-62 [0] ABI_X86="(64) (-32) (-x32)"
    [ebuild  NS    ] dev-lang/python-3.3.3 [2.7.5-r3, 3.2.5-r3] USE="gdbm ipv6 ncurses readline sqlite ssl threads xml -build -doc -examples -hardened -tk -wininst"
    [ebuild     U  ] app-admin/gamin-0.1.10-r1 [0.1.10] ABI_X86="(64%*) (-32) (-x32)"
    [ebuild     U  ] sys-devel/binutils-2.23.2 [2.23.1]
    [blocks b      ] <dev-libs/gobject-introspection-1.36 ("<dev-libs/gobject-introspection-1.36" is blocking dev-libs/glib-2.36.4-r1)
    [blocks b      ] <dev-libs/gobject-introspection-1.36.0 ("<dev-libs/gobject-introspection-1.36.0" is blocking dev-libs/gobject-introspection-common-1.36.0)
    [uninstall     ] dev-lang/vala-0.14.2-r2
    [uninstall     ] dev-lang/vala-0.18.1
    [blocks b      ] <dev-lang/vala-0.20.0 ("<dev-lang/vala-0.20.0" is blocking dev-libs/gobject-introspection-1.36.0-r1)
    [ebuild     U  ] x11-libs/pango-1.34.1 [1.30.1]
    [ebuild     U  ] x11-libs/gdk-pixbuf-2.28.2 [2.26.4]
    [ebuild     U  ] dev-libs/atk-2.8.0 [2.6.0] USE="{-test%}"
    [ebuild  N     ] app-accessibility/at-spi2-core-2.8.0  USE="introspection"
    [ebuild     U  ] net-libs/telepathy-glib-0.20.4 [0.20.1-r1]
    [ebuild  NS    ] dev-python/pygobject-3.8.3 [2.28.6-r53] USE="cairo threads -examples {-test}" PYTHON_TARGETS="python2_7 python3_2 -python2_6 -python3_3"
    [ebuild  N     ] app-accessibility/at-spi2-atk-2.8.1  USE="{-test}"
    [blocks B      ] =media-libs/libpng-1.5*:0 ("=media-libs/libpng-1.5*:0" is blocking media-libs/libpng-1.5.17-r15)

    !!! Multiple package instances within a single package slot have been pulled
    !!! into the dependency graph, resulting in a slot conflict:

    media-libs/libpng:0

      (media-libs/libpng-1.5.17-r1::gentoo, installed) pulled in by
        media-libs/libpng:0/0= required by (x11-libs/cairo-1.12.14-r4::gentoo, installed)
        media-libs/libpng:0/0= required by (kde-base/gwenview-4.11.2-r1::gentoo, installed)
        media-libs/libpng:0/0= required by (dev-python/wxpython-2.8.12.1-r1::gentoo, installed)
        media-libs/libpng:0/0= required by (kde-base/ksplash-4.11.2::gentoo, installed)
        >=media-libs/libpng-1.4:0/0= required by (net-libs/webkit-gtk-1.8.3-r201::gentoo, installed)
        media-libs/libpng:0/0= required by (media-libs/libwebp-0.3.1::gentoo, installed)
        media-libs/libpng:0/0= required by (net-print/cups-filters-1.0.36-r1::gentoo, installed)
        media-libs/libpng:0/0= required by (kde-base/kdelibs-4.11.2-r1::gentoo, installed)
        media-libs/libpng:0/0= required by (media-libs/vigra-1.8.0::gentoo, installed)
        media-libs/libpng:0/0= required by (media-libs/openjpeg-1.5.1::gentoo, installed)
        media-libs/libpng:0/0= required by (dev-qt/qtgui-4.8.5-r1::gentoo, installed)
        media-libs/libpng:0/0= required by (app-text/poppler-0.24.3::gentoo, installed)

      (media-libs/libpng-1.6.8::gentoo, ebuild scheduled for merge) pulled in by
        (no parents that aren't satisfied by other packages in this slot)

    dev-db/sqlite:3

      (dev-db/sqlite-3.8.2::gentoo, ebuild scheduled for merge) pulled in by
        (no parents that aren't satisfied by other packages in this slot)

      (dev-db/sqlite-3.7.17::gentoo, installed) pulled in by
        >=dev-db/sqlite-3.3.8:3[extensions] required by (dev-python/pysqlite-2.6.3::gentoo, installed)

    app-text/poppler:0

      (app-text/poppler-0.24.5::gentoo, ebuild scheduled for merge) pulled in by
        (no parents that aren't satisfied by other packages in this slot)

    (app-text/poppler-0.24.3::gentoo, installed) pulled in by
        >=app-text/poppler-0.16:0/43=[xpdf-headers(+),cxx] required by (app-office/libreoffice-4.1.3.2-r2::gentoo, installed)
        app-text/poppler:0/43=[cxx,jpeg,lcms,tiff,xpdf-headers(+)] required by (net-print/cups-filters-1.0.36-r1::gentoo, installed)
        (and 1 more with the same problems)

    media-libs/harfbuzz:0

    (media-libs/harfbuzz-0.9.12::gentoo, installed) pulled in by
        >=media-libs/harfbuzz-0.9.10:0/0=[icu(+)] required by (app-office/libreoffice-4.1.3.2-r2::gentoo, installed)

    (media-libs/harfbuzz-0.9.23::gentoo, ebuild scheduled for merge) pulled in by
        (no parents that aren't satisfied by other packages in this slot)

    virtual/libffi:0

    (virtual/libffi-3.0.11::gentoo, installed) pulled in by
        (no parents that aren't satisfied by other packages in this slot)

    (virtual/libffi-3.0.11::gentoo, ebuild scheduled for merge) pulled in by
        virtual/libffi[abi_x86_32(-)?,abi_x86_64(-)?,abi_x86_x32(-)?,abi_mips_n32(-)?,abi_mips_n64(-)?,abi_mips_o32(-)?] required by (dev-libs/glib-2.36.4-r1::gentoo, ebuild scheduled for merge)

    virtual/libiconv:0

    (virtual/libiconv-0::gentoo, installed) pulled in by
        (no parents that aren't satisfied by other packages in this slot)

    (virtual/libiconv-0::gentoo, ebuild scheduled for merge) pulled in by
        virtual/libiconv[abi_x86_32(-)?,abi_x86_64(-)?,abi_x86_x32(-)?,abi_mips_n32(-)?,abi_mips_n64(-)?,abi_mips_o32(-)?] required by (dev-libs/glib-2.36.4-r1::gentoo, ebuild scheduled for merge)


    It may be possible to solve this problem by using package.mask to
    prevent one of those packages from being selected. However, it is also
    possible that conflicting dependencies exist such that they are
    impossible to satisfy simultaneously.  If such a conflict exists in
    the dependencies of two different packages, then those packages can
    not be installed simultaneously. You may want to try a larger value of
    the --backtrack option, such as --backtrack=30, in order to see if
    that will solve this conflict automatically.

    For more information, see MASKED PACKAGES section in the emerge man
    page or refer to the Gentoo Handbook.


    * Error: The above package list contains packages which cannot be
    * installed at the same time on the same system.

    (media-libs/libpng-1.5.17-r15::gentoo, ebuild scheduled for merge) pulled in by
        =media-libs/libpng-1.5* required by (mail-client/thunderbird-bin-24.1.1::gentoo, installed)


    For more information about Blocked Packages, please refer to the following
    section of the Gentoo Linux x86 Handbook (architecture is irrelevant):

    http://www.gentoo.org/doc/en/handbook/handbook-x86.xml?full=1#blocked


    The following USE changes are necessary to proceed:
    (see "package.use" in the portage(5) man page for more details)
    # required by app-office/libreoffice-4.1.3.2-r2
    # required by @selected
    # required by @world (argument)
    =media-libs/harfbuzz-0.9.23 icu

Typical Issues:

- Slot conflicts:
  - A package `A` depends on `=xy-1.1.1` but another package `B` requires `>=xy-1.1.2`
  - Two packages that cannot be installed on the system at the same time

- Build Breaks: The build process of a package fails due to
  - GCC crashes
  - Dependency issues discovered during the build process

- Updates of programming languages like perl, haskell etc.
  - Might require many packages to be re-compiled
  - Tools like `perl-cleaner` and `haskell-updater` help in such situations

- Dependent packages are not rebuilt
  - `revdep-rebuild`

Gentoo specific tooling overview:

- `emerge` → package manager
- `eselect` → switch between multiple implementations/ versions of something
- `gcc-config` → manage GCC implementation and profiles
- `java-config` → manage VM implementations etc.
- `eix` → set of utilities for searching and diffing your local portage-tree and overlays using a binary cache
- `equery` → can display package dependencies, metadata, and relate **installed files to packages**
- `dispatch-conf` → tool to manually merge config files of updated packages
- `eclean-pkg` → delete redundant packages from local portage tree
- `eclean-dist` → delete redundant dist files (third party files) from local portage tree
- `webapp-config` → configure webapps installed from portage
- `revdep-rebuild` → reverse dependency scanner and fix tool
- `layman` → overlay manager

Some nice examples of the features provided by these tools in the following.

Recompile the _entire_ system:

`emerge -e world`

List all packages in short that are installed and have `perl` in their dependency variables plus the package itself:

`eix --deps -# -I perl`

List what package the file `/usr/bin/equery` belongs to:

`equery b /usr/bin/equery`

Lazy sync:

`eix-sync`

Does:

- `emerge --sync`
- `eix-update`
- `eix-diff`

See which packages are installed from overlays:

`eix -J`

Is all software on the system managed by Portage?:

No, it does not make sense for everyhting and not everything is available on portage.
The following

- Java based software
- Node JS stuff (has its own package management)
- Web apps in general (some exceptions)


Help resources:

- [The official Wiki](https://wiki.gentoo.org/wiki/Main_Page)
- [Forums](http://forums.gentoo.org/)

Literature:

An up-to-date book written by a Gentoo developer about the Linux OS based on the Gentoo distribution.

[http://swift.siphos.be/linux_sea/](http://swift.siphos.be/linux_sea/)

Qou Vaids?

- Gentoo läuft bereits auf mehr Architekturen als jede andere Distribution
- Weitere sind in Vorbereitung
- Trend zu immer mehr Software, die nur noch im Git existiert
- Bei Gentoo bequem über den Paketmanager zu verwalten
- Live ebuilds
  Pakete, die den Code direkt aus einem git/hg/svn/... Repository beziehen

Was ist von Gentoo nicht zu erwarten?

- Ein offizieller Installer :)
- Sofort überall die neusten Versionen (etwas schwierig bei 200 Entwicklern und 16k Paketen)
- Jemanden, der das Sagen hat

Source:
[Christopher Nguyen](http://www.linuxtag.org/2013/fileadmin/www.linuxtag.org/slides/Chi-Thanh_Christopher_Nguyen_-_Gentoo_Update.e428.odp)
