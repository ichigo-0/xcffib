# xcffib [![Build Status](https://travis-ci.org/tych0/xcffib.svg)](https://travis-ci.org/tych0/xcffib)

`xcffib` is intended to be a (mostly) drop-in replacement for `xpyb`. `xpyb`
has an inactive upstream, several memory leaks, is python2 only and doesn't
have pypy support. `xcffib` is a binding which uses
[cffi](https://cffi.readthedocs.org/), which mitigates some of the issues
described above. `xcffib` also builds bindings for all 29 X extensions in 1.10,
whereas `xpyb` (and several other bindings) don't.

## Dependencies

Currently `xcb-types` doesn't run against `xcb-proto` 1.10; there is a hacked
branch available at [tych0/xcb-types](http://github.com/tych0/xcb-types) that
allows you to parse xcb-proto 1.10 mostly correctly. Other than that, you
should be able to install all the deps from hackage or pip.

## Differences

There are lots of differences right now between `xpyb` and `xcffib`, mostly
because `xcffib` isn't done yet :-)

* In general, you should `s/xcb/xcffib/g`
* `xcb.Exception` is spelled `xcffib.XcffibException` and is also a parent of
   all exceptions generated by xcffib.
* `xcb.ConnectException` is gone, it was unused
* `xcffib.ConnectionException` is raised on connection errors
* The `FooError` `BadFoo` duality is gone; it was difficult to understand what
  to actually catch if you wanted to handle an error. Instead, only `FooError`
  remains, which implements both the X error object description and python
  Exception (via inheriting from `xcffib.XcffibException`).

## Why haskell?

Why is the binding generator written in haskell? Because haskell is awesome.

## TODO

* XGE support? (xpyb doesn't implement this either)
