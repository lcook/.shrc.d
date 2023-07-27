- [About](#about)
    - [Setup](#setup)
     - [Oneliner](#oneliner)
    - [Bootstrapping](#bootstrapping)
- [License](#license)

## About

This repository contains my current MirBSD shell
(mksh) configuration files, structured in such a
way that allows for ease of portability.

While not strictly supported, there is an effort to
maintain backwards compatibility with ksh93, and
as such, should work for the most part. I have not
found any problems whilst using ksh93 with the
provided configuration; this is mostly done by
checking the value of `$KSH_VERSION`—no guarantee
is made outside of this.

Local modifications, as indicated by a `.local`
suffix are intended for personal environments, that
may not be the default options on other systems.

For setting defaults based on the type of underlying
operating-system, place files in host/`$(uname -s)`/,
e.g. `host/Linux/foo-0`. Any corresponding files will
be loaded upon shell initialization.

### Setup

Copy `.mkshrc` to your home directory and create a
symlink to `.kshrc`, whilst ensuring that `~/.shrc.d`
exists too.

```shell
$ cp -fv .mkshrc ~ ; mkdir ~/.shrc.d
$ (cd ~ || return ; ln -sf .mkshrc .kshrc)
```

Lastly, copy the remaining shell configuration over.

```shell
$ cp -frv [0-9]-* host ~/.shrc.d
```

And like that, you are done!

Alternatively, `git clone` this repository into
`~/.shrc.d`, just make sure you have copied
`.mkshrc` and created an accompanying symlink to
`.kshrc` in your home directory.

You can of course just clone to another location
such as `~/.config/mksh` and create a symlink from
`~/.shrc.d`. The choice is up to you.

```shell
$ cd ~ || return
$ ln -sf .config/mksh .shrc.d
$ ln -sf .config/mksh/.mkshrc .mkshrc
$ ln -sf .config/mksh/.mkshrc .kshrc
```

#### Oneliner

```shell
$ git clone git@github.com:lcook/.shrc.d.git ~/.shrc.d;cd ~ && for f in .mkshrc .kshrc;do ln -sf .shrc.d/.mkshrc $f;done||return
```

### Bootstrapping

If, for some reason, you are not able to access
this repository, the setup can be bootstrapped
via an externally provided tar archive, graciously
hosted on freefall (my FreeBSD homepage).

```shell
$ url="https://people.freebsd.org/~lcook/shrc.tar.gz"
```

fetch:
```shell
$ fetch -q -o /dev/stdout $url | tar xfv - -C ~
```

curl:
```shell
$ curl -s -o /dev/stdout $url | tar xfv - -C ~
```

wget:
```shell
$ wget -q -O- $url | tar xfv - -C ~
```

This is entirely for personal usage and does not
include any `.local` files for less baggage. Not
generally recommended.

## License

[BSD 2-Clause](LICENSE)
