This module is a simple generator for [pkg-config](http://pkg-config.freedesktop.org/) files. It has one method.

### generate

The generated file's properties are specified with the following keyword arguments.

- `libraries`, a list of built libraries (usually results of shared_library) that the user needs to link against
- `version`, a string describing the version of this library
- `name`, the name of this library
- `filebase`, the base name to use for the pkg-config file, as an example the value of `libfoo` would produce a pkg-config file called `libfoo.pc`
- `subdirs` which subdirs of `include` should be added to the header search path, for example if you install headers into `${PREFIX}/include/foobar-1`, the correct value for this argument would be `foobar-1`
- `requires` list of strings to put in the `Requires` field
- `requires_private` list of strings to put in the `Requires.private` field
- 'libraries_private` list of strings to put in the `Libraries.private` field