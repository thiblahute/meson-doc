By default Meson will not install anything. Build targets can be installed by tagging them as installable in the definition.

    project('install', 'c')
    shared_library('mylib', 'libfile.c', install : true)

There is usually no need to specify install paths or the like. Meson will automatically install it to the standards-conforming location. In this particular case the executable is installed to the <tt>bin</tt> subdirectory of the install prefix. However if you wish to override the install dir, you can do that with the <tt>install_dir</tt> argument.

    executable('prog', 'prog.c', install : true, install_dir : 'my/special/dir')

Other install commands are the following.

    headers('header.h', subdir : 'projname') # -> include/projname/header.h
    man('foo.1') # -> share/man/man1/foo.1.gz
    data('progname', sources : 'datafile.cat') # -> share/progname/datafile.dat

## Custom install behaviour ##

Sometimes you need to do more than just install basic targets. Meson makes this easy by allowing you to specify a custom script to execute at install time. As an example, here is a script that generates an empty file in a custom directory.

    #!/bin/sh

    mkdir "${DESTDIR}/${MESON_INSTALL_PREFIX}/mydir"
    touch "${DESTDIR}/${MESON_INSTALL_PREFIX}/mydir/file.dat"

As you can see, Meson sets up some environment variables to help you write your script (<tt>DESTDIR</tt> is not set by Meson, it is inherited from the outside environment). In addition to the install prefix, Meson also sets the variables <tt>MESON_SOURCE_ROOT</tt> and <tt>MESON_BUILD_ROOT</tt>.

Telling Meson to run this script at install time is a one-liner.

    meson.set_install_script('myscript.sh')

The argument is the name of the script file relative to the current subdirectory.

---

[Back to index](Manual).