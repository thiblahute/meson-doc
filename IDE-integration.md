Meson has exporters for Visual Studio and XCode, but writing a custom backend for every IDE out there is not a scalable approach. To solve this problem, Meson provides an API that makes it easy for any IDE or build tool to integrate Meson builds and provide an experience comparable to a solution native to the IDE.

The basic tool for this is a script called <tt>mesonintrospect.py</tt>. Some distro packages might not expose this script in the regular path, and in this case you need to execute it from the install directory.

The first thing to do when setting up a Meson project in an IDE is to select the source and build directories. For this example we assume that the source resides in an Eclipse-like directory called <tt>workspace/project</tt> and the build tree is nested inside it as <tt>workscpace/project/build</tt>. First we initialise Meson by running the following command in the source directory.

    meson build

For the remainder of the document we assume that all commands are executed inside the build directory unless otherwise specified.

The first thing you probably want is to get a list of top level targets. For that we use the introspection tool. It comes with extensive command line help so we recommend using that in case problems appear.

    mesonintrospect.py --targets

The JSON formats will not be specified in this document. The easiest way of learning them is to look at sample output from the tool.

Once you have a list of targets, you probably need the list of source files that comprise the target. To get this list for a target, say <tt>exampletarget</tt>, issue the following command.

    mesonintrospect.py --target-files exampletarget

In order to make code completion work, you need the compiler flags for each compilation step. Meson does not provide this itself, but the Ninja tool Meson uses to build does provide it. To find out the compile steps necessary to build target foo, issue the following command.

    ninja -t commands foo

Note that if the target has dependencies (such as generated sources), then the commands for those show up in this list as well, so you need to do some filtering. Alternatively you can grab every command invocation in one go with the command <tt>ninja -t commands all</tt>.

The next thing to display is the list of options that can be set. These include build type and so on. Here's how to extract them.

    mesonintrospect.py --buildoptions

To set the options, use the <tt>mesonconf.py</tt> binary.

Compilation and unit tests are done as usual by running the <tt>ninja</tt> and <tt>ninja test</tt> commands. A JSON formatted result log can be found in <tt>workspace/project/build/meson-logs/testlog.json</tt>.

When these tests fail, the user probably wants to run the failing test in a debugger. To make this as integrated as possible, extract the test test setups with this command.

    mesonintrospect.py --tests

This provides you with all the information needed to run the test: what command to execute, command line arguments and environment variable settings.

---

[Back to index](Manual)