This page lists functions and methods available in Meson scripts. For more in-depth documentation on how to use them, refer to the [manual](Manual).

## Functions ##

### executable ###

Creates a new executable. The first argument specifies its name and the remaining positional arguments define the source files to use.

Executable supports the following keyword arguments.

- <tt>install</tt>, when set to true, this executable should be installed
- <tt>link_with</tt>, one or more shared or static libraries (built by this project) that this target should be linked with
- <tt>&lt;languagename&gt;_pch</tt> precompiled header fire to use for the given language
- <tt>&lt;languagename&gt;_args</tt> compiler flags to use for the given language
- <tt>link_args</tt> flags to use during linking
- <tt>link_depends</tt> an extra file that the link step depends on such as a symbol visibility map
- <tt>include_directories</tt> one or more objects created with the <tt>include_directories</tt> function
- <tt>dependencies</tt> one or more objects created with <tt>dependency</tt> or <tt>find_library</tt>
- <tt>gui_app</tt> when set to true flags this target as a GUI application on platforms where this makes a difference (e.g. Windows)
- <tt>extra_files</tt> are not used for the build itself but are shown as source files in IDEs that group files by targets (such as Visual Studio)
- <tt>install_rpath</tt> a string to set the target's rpath to after install (but *not* before that)

### message ###

This function prints its argument to stdout.

### project ###

The first argument to this function must be a string defining the name of this project. It must be followed by one or more programming languages that the project uses. Supported values for languages are <tt>c</tt>, <tt>cpp</tt> (for <tt>C++</tt>), <tt>objc</tt>, <tt>objcpp</tt>, <tt>fortran</tt>, <tt>java</tt>, <tt>cs</tt> (for <tt>C#</tt>) and <tt>vala</tt>.
