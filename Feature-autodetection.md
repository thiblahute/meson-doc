Meson is designed for high productivity. It tries to do as many things automatically as it possibly can.

CCache
--

[CCache](http://ccache.samba.org/) is a cache system designed to make compiling faster. When you run Meson for the first time for a given project, it checks if CCache is installed. If it is, Meson will use it automatically.

If you do not wish to use CCache for some reason, just specify your compiler with environment variables <tt>CC</tt> and/or <tt>CXX</tt> when first running Meson (remember that once specified the compiler can not be changed). Meson will then use the specified compiler without CCache.

Coverage
--

When doing a code coverage build, Meson will check the existance of binaries <tt>gcovr</tt>, <tt>lcov</tt> and <tt>genhtml</tt>. If the first one is found, it will create targets called *coverage-text* and *coverage-xml*. If the latter two are found, it generates the target *coverage-html*. You can then generate coverage reports just by calling e.g. <tt>ninja coverage-xml</tt>.

Valgrind
--

[Valgrind](http://valgrind.org/) is a multi purpose memory usage checker. If Meson detects Valgrind on the system being run, it will automatically provide a target named *test-valgrind*. This will run each test in the test suite under Valgrind using the default checking options. The output of these tests can be found in the file <tt>meson-private/testlog-valgrind.txt</tt>.

Cppcheck
--

[Cppcheck](http://cppcheck.sourceforge.net/‎) is a tool for detecting errors in C/C++ programs through static analysis. Meson will automatically create a cppcheck target if you have the program installed on your system.

---

[Back to index](Manual).