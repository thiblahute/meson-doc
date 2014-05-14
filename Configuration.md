If there are multiple configuration options, passing them through compiler flags becomes very burdensome. It also makes the configuration settings hard to inspect. To make things easier, Meson supports the generation of configure files. This feature is similar to one found in other build systems such as CMake.

Suppose we have the following Meson snippet:

    conf_data = configuration_data()
    conf_data.set('version', '1.2.3')
    configure_file(input : 'config.h.in', output : 'config.h', configuration : conf_data)

and that the contents of <tt>config.h.in</tt> are

    #define VERSION_STR "@version@"

Meson will then create a file called <tt>config.h</tt> in the corresponding build directory whose contents are the following.

    #define VERSION_STR "1.2.3"

More specifically, Meson will find all strings of the type <tt>@varname@</tt> and replace them with respective values set in <tt>conf_data</tt>. You can use a single <tt>configuration_data</tt> object as many times as you like, but it becomes immutable after the first use. That is, after it has been used once the <tt>set</tt> function becomes unusable and trying to call it causes an error.

For more complex configuration file generation Meson provides a second form. To use it, put a line like this in your configuration file.

    #mesondefine TOKEN

The replacement that happens depends on what the value and type of TOKEN is:

    #define TOKEN     // If TOKEN is set to boolean true.
    #undef TOKEN      // If TOKEN is set to boolean false.
    #define TOKEN 4   // If TOKEN is set to an integer or string value.
    /* undef TOKEN */ // If TOKEN has not been set to any value.

Note that if you want to define a C string, you need to do the quoting yourself like this:

    conf.set(TOKEN, '"value"')

Often you have a boolean value in Meson but need to define the C/C++ token as 0 or 1. Meson provides a convenience function for this use case.

    conf.set10(token, boolean_value)
    # The line above is equivalent to this:
    if boolean_value
      conf.set(token, 1)
    else
      conf.set(token, 0)
    endif

---

[Back to index](Manual).