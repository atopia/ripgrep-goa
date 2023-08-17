ripgrep-goa - Goa project to run ripgrep on Genode
==================================================

This implements a little demo repository to run [ripgrep](https://github.com/BurntSushi/ripgrep) on the [Genode OS Framework](https://genode.org/) with the [Goa](https://github.com/genodelabs/goa/) tool.

Testing
-------

On x86_64 Linux, first install Rust's [rustup](https://github.com/rust-lang/rustup/) toolchain manager by a method of your choosing and follow these steps on x86_64 Linux to try it out:
```
$ rustup toolchain install stable-x86_64-unknown-linux-gnu
$ rustup target add x86_64-unknown-freebsd
$ git clone https://github.com/genodelabs/goa
$ export PATH="$PATH:$(pwd)/goa/bin"
$ git clone https://github.com/atopia/ripgrep-goa
$ goa run -C ripgrep-goa
```

The run was successful if it prints the following lines:
```
[init -> ripgrep-goa] 3:            say hello to Genode!
[init] child "ripgrep-goa" exited with exit value 0
```

Limitations
-----------
* The build has been tested with version 1.73.0 of the Rust toolchain on Sculpt OS release 23.10 and may fail to compile with future versions due to incompatibilities with the Genode OS port of FreeBSD's C library.
* Running *rg* on Genode may lead to runtime warnings or errors, especially when extending the example to more complex scenarios. For example, the [runtime](pkg/ripgrep-goa/runtime) passes the `--no-mmap` switch to `rg` to suppress an error message because the used Inline file system does not support *mmap(3)*.
