Guidelines for Contributing
===========================

Welcome to the D community and thanks for your interest in contributing!
If this is your first pull request, please read [Contributing to Phobos](https://wiki.dlang.org/Contributing_to_Phobos).
Have a look at [Starting as a Contributor](http://wiki.dlang.org/Starting_as_a_Contributor#Building_D) for build instructions.

Statically linked nature
------------------------

Phobos has some more stringent than average D packages. Most of those are outlined in the aforementioned wiki.
One restriction that is unique to Phobos and druntime is that they are compiled statically and shipped as binaries.
This means you *should not* use the following language features:
- `version (Identifier)`, `debug (Identifier)`, `debug`, or `debug (Integer)` to provide functionalities.
  While those are handy to provide optional feature ([example](https://vibed.org/docs#compile-time-configuration)),
  they can't be used in Phobos.
  However, `version` which are platform-specific (`linux`, `OSX`, `Windows`, `POSIX`) are not affected.
- By extension, `version (unittest)` should not be used (as it slows down compilation).
  Use `version (CoreUnittest)` for unittest utilities that can only be used from within Phobos.
- Library dependencies should be considered carefully.
  Statically linking means locking the user with a specific version of the library,
  which might be incompatible with what the user wants to use, or might bring in an unneeded dependency.
  There are two options to add optional support for a library:
  - One can use lazy loading, see e.g. `std.net.curl`;
  - One can use templated methods which are not instantiated within Phobos;
  In general, bindings to libraries should go in their own package or in [Deimos](https://github.com/D-Programming-Deimos/).
- Usage of other compiler switch that might affect generated binary should also be done carefully.
  For example, using any `-preview` switch that affects mangling would for downstream to use this preview as well,
  while not using means downstream is unlikely to be able to use that specific `-preview`.

More Links
----------

* Fork [on Github](https://github.com/dlang/phobos)
* Use our [Bugzilla bug tracker](https://issues.dlang.org)
* Follow the [D style](http://dlang.org/dstyle.html)
* Participate in [our forum](http://forum.dlang.org/)
* Ask questions on our `#d` IRC channel on freenode.org ([web interface](https://kiwiirc.com/client/irc.freenode.net/d))
* Review Phobos additions in the [Review Queue](http://wiki.dlang.org/Review_Queue).
