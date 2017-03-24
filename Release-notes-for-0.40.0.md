**Preliminary, 0.40.0 has not been released yet**

# New features

## Outputs of generators can be used in custom targets in the VS backend

This has been possible with the Ninja backend for a long time but now the Visual Studio backend works too.

## `compute_int` method in the compiler objects

This method can be used to evaluate the value of an expression. As an example:

    cc = meson.get_compiler('c')
    two = cc.compute_int('1 + 1') # A very slow way of adding two numbers.

## Visual Studio 2017 support

There is now a VS2017 backend as well as a generic VS backend that autodetects the currently active VS version.

## More

Add here as they are merged to master.
