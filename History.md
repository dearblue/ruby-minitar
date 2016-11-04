## 0.6 / YYYY-MM-DD

*   Breaking Changes:

    *   Extracted `bin/minitar` into a new gem, `minitar-cli`. No, I am *not*
        going to bump the major version for this. As far as I can tell, few
        people use the command-line utility anyway. (Installing
        `archive-tar-minitar` will install both `minitar` and `minitar-cli`, at
        least until version 1.0.)

*   Enhancements:

    *   Licence change. After speaking with Mauricio Fernández, we have changed
        the licensing of this library to Ruby and Simplified BSD and have
        dropped the GNU GPL license. This takes effect from the 0.6 release.
    *   Printing a deprecation warning for including Archive::Tar to put
        Minitar in the top-level namespace.
    *   Printing a deprecation warning for including Archive::Tar::Minitar into
        a class (Minitar will be a class for version 1.0).
    *   Moved Archive::Tar::PosixHeader to Archive::Tar::Minitar::PosixHeader
        with a deprecation warning. Do not depend on
        Archive::Tar::Minitar::PosixHeader, as it will be moving to
        ::Minitar::PosixHeader in a future release.
    *   Added an alias, ::Minitar, for Archive::Tar::Minitar, opted in with
        `require 'minitar'`. In future releases, this alias will be enabled by
        default, and the Archive::Tar namespace will be removed entirely for
        version 1.0.
    *   Modified the handling of `mtime` in PosixHeader to do an integer
        conversion (#to_i) so that a Time object can be used instead of the
        integer value of the time object.
    *   Writer::RestrictedStream was renamed to Writer::WriteOnlyStream for
        clarity. No alias or deprecation warning was provided for this as it is
        an internal implementation detail.
    *   Writer::BoundedStream was renamed to Writer::BoundedWriteStream for
        clarity. A deprecation warning is provided on first use because a
        BoundedWriteStream may raise a BoundedWriteStream::FileOverflow
        exception.
    *   Writer::BoundedWriteStream::FileOverflow has been renamed to
        Writer::WriteBoundaryOverflow and inherits from StandardError instead
        of RuntimeError. Note that for Ruby 2.0 or higher, an error will be
        raised when specifying Writer::BoundedWriteStream::FileOverflow because
        Writer::BoundedWriteStream has been declared a private constant.
    *   Modified Writer#add_file_simple to accept the data for a
        file in `opts[:data]`. When `opts[:data]` is provided, a stream block
        must not be provided. Improved the documentation for this method.
    *   Modified Writer#add_file to accept `opts[:data]` and transparently call
        Writer#add_file_simple in this case.
    *   Methods that require blocks are no longer required, so the
        Archive::Tar::Minitar::BlockRequired exception has been removed with a
        warning.

*   Bugs:

    *   Fix [#2](https://github.com/halostatue/minitar/issues/2) to handle IO
        streams that are not seekable, such as pipes, STDIN, or STDOUT.
    *   Fix [#3](https://github.com/halostatue/minitar/issues/3) to make the
        test timezone resilient.
    *   Fix [#4](https://github.com/halostatue/minitar/issues/4) for supporting
        the reading of tar files with filenames in the GNU long filename
        extension format. Ported from @atoulme’s fork, originally provided by
        Curtis Sampson.
    *   Fix [#6](https://github.com/halostatue/minitar/issues/6) by making it
        raise the correct error for a long filename with no path components.
    *   Fix [#14](https://github.com/halostatue/minitar/pull/6) provided by
        @kzys should fix Windows detection issues.

*   Development:

    *   Modernized minitar tooling around Hoe.
    *   Added travis and coveralls.

## 0.5.2 / 2008-02-26

* Bugs:
  * Fixed a Ruby 1.9 compatibility error.

## 0.5.1 / 2004-09-27

* Bugs:
  * Fixed a variable name error.

## 0.5.0

* Initial release. Does files and directories. Command does create, extract,
  and list.