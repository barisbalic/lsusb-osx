# lsbusb-osx

This is a rough port of `lsusb` from the [usbutils](https://github.com/gregkh/usbutils) package.  It's taken from v007 as this was the last readily compatible version, and it drops the `devices` and `tree` flags/options as they rely on `sysfs` which doesn't exist in OSX.

In fact, there's probably little use to this package, but it's teaching me a few things.

I've left the original `AUTHORS`, `NEWS` and `CHANGELOG` files in place to avoid discrediting anyone.

## Installation

...well this should be available through [homebrew](http://brew.sh/) soon, for now if you want to install it you will need to build it.  See below.


## Building

I know basically nothing about C++ and it's tooling.  I'm trying to stick reasonably closely to the existing build process for `usbutils`, so we're going to need to install a few things...

### Dependencies

You will need to install `autotools`, `autoconf` and `libusb`.  If you don't have [homebrew](http://brew.sh/) installed, then start with that.

```bash
  $ brew install automake
  $ brew install autoconf
  $ brew install libusb
```

### Configuring

There are a number of steps, as long as they occur in the right order everything else falls into place.  I believe the reason it's so convoluted is that the generated files add platform/system independence, but I really can't tell.  I could add a script to do this automatically, but I feel like there's something to be gained from seeing the chain.

```bash
  $ aclocal
  $ autoheader
  $ automake --add-missing
  $ autoconf
  $ ./configure
  $ make
  $ make install
```

- `aclocal` generates some automake macros used in the automake files.
- `autoheader` will generate the config.h header.
- `automake --add-missing` will then process `automake.am` and generate `automake.in`.
- `autoconf` processes `configure.ac` and any files specified for inclusion and generates your `configure` script.
- Everything from that point on is vanilla.


## Documentation

Like all good command-line tools, it's built in, and provides man-pages!

```bash
  $ lsusb --help
  $ lsusb ?
```

## Roadmap

The 0.8x family of `usbutils` releases make use of a different byte-ordering library that moans when pushing out information about Hubs.  I'd like to work out why and fix it.

Sometime after version 0.8x the project moves to using `libudev` to provide vendor/device information for USB IDs.  In this project we'll continue to use the [linux-usb](http://www.linux-usb.org/usb.ids) list directly, so an upgrade to match 0.9x is unlikely.

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## License

See [LICENSE][] for details.

[license]: LICENSE.md
