# freemobile-smsapi

A Bash API for Free Mobile notification service

![Stable version](https://img.shields.io/badge/stable-1.0.2-blue.svg)
[![BSD-3 license](https://img.shields.io/badge/license-BSD--3--Clause-428F7E.svg)](https://tldrlegal.com/license/bsd-3-clause-license-%28revised%29)

*freemobile-smsapi* is a Bash library which allows to use Free Mobile SMS notification service.

## Free Mobile SMS notification service

To be able to use Free Mobile SMS notification service, you must have:

 * Subscribed a mobile line with [Free Mobile](https://mobile.free.fr) operator.

   It's on this line SMS will be sent.

 * Enable SMS notification service.

  This will give you an authentication key.

With your Free Mobile login and the authentication key you have all information to use this library.

## Library files

This library is composed of two files:

 * `/etc/freemobile-smsapi/freemobile-smsapi.conf.src`

	*The configuration file*

 * `/usr/lib/freemobile-smsapi/freemobile-smsapi.bash.src`

	*The library*

Both are located inside the directory **freemobile-smsapi** which allows to build a Debian package.

## Configuration file

Configuration file: `/etc/freemobile-smsapi/freemobile-smsapi.conf.src` is in fact a file which is sourced by the Bash library.

Thus syntax is the Bash one and is composed of the following variables:

| Name | Meaning                                |
|:-----|:---------------------------------------|
| USER | Free Mobile login                      |
| PASS | Authentication key associated to login |

Example:

```bash
# Free Mobile login
USER="12345678"
# Authentication key associated to login
PASS="1a2B3c4D5e6F7g"
```

## HOW TO

### Use

To use the library there are only two steps:

1. Source the library:
```bash
. /usr/lib/freemobile-smsapi/freemobile-smsapi.bash.src
```
2. Call the function to send a SMS:
```bash
callFreeMobileSmsApi "My first SMS"
```

In this example *My first SMS* will be sent to the phone number associated with the Free Mobile account defined in the configuration file.

Exit code will be `0` in case of success, `1` otherwise.

## Create Debian package

You can create the Debian package with the following commands:

```bash
# Move to the repository directory
cd /github/freemobile-smsapi/repository/path
# Generate the Debian package
sudo dpkg-deb --build freemobile-smsapi
# Update the package name following Debian convention
VERSION=$(grep "Version" freemobile-smsapi/DEBIAN/control | cut -d ' ' -f 2)
ARCH=$(grep "Architecture" freemobile-smsapi/DEBIAN/control | cut -d ' ' -f 2)
mv freemobile-smsapi.deb freemobile-smsapi_${VERSION}_${ARCH}.deb
```
