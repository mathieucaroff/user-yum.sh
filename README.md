# user-yum.sh

A yum &amp; rpm package installer operating at user-privilege.

## Usage

### Installing a package

Downloading one or several package:

```sh
make +screen
make +zsh +tcl
```

Installing all downloaded packages:

```sh
make install
```

### Help to setup

Printing the lines to add to your .rc:

```sh
make environment
```

This will output a block of text like the following (2018-09-29):

```sh
# Setting environment for /home/mc/y
ROOT_D="/home/mc/y"

PATH="$ROOT_D/usr/sbin:$ROOT_D/usr/bin:$ROOT_D/bin:$PATH"

L="/lib:/lib64:/usr/lib:/usr/lib64"
export LD_LIBRARY_PATH="$L:$ROOT_D/usr/lib:$ROOT_D/usr/lib64"
```

Tips: You can source it using process substitution if you like:

```sh
source <(cd user-yum.sh/ && make environment)
```

Remove the root install folder to remove all installed packages.

There is currently no way to remove a package from the directory after running
`make install` so be careful: use backup or use several instances. If you've
just happend to mistype `make +the_wrong_name` you can use `make unload` to
clean the cache (/rpm) and the list of downloaded packages (/dwnldlist).

## Configuration

### Root directory

You should configure the `ROOT_D` value in the Makefile to your liking. The
default is (as of 2018-09-29) (was?):

```sh
ROOT_D := $(shell echo $$HOME)/y
```

### Install flag

You may want to remove the + prefixing the name of the packages to install. If
so, change the `INSTALL_FLAG_PREFIX`, from

```sh
INSTALL_FLAG_PREFIX := +
```

to

```sh
INSTALL_FLAG_PREFIX :=
```