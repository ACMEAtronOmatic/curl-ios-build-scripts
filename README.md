Curl iOS build scripts
======================

Automated scripts to build curl for iOS. Supports:

- iPhoneSimulator (i386)
- older iPhones (arm v6)
- newer iPhones/iPads (arm v7)


## Default configuration

The scripts are configured to produce the smallest binary possible, with Curl being configured only to support the HTTP protocol (no FTP, DICT, FILE, etc).

All builds scripts share this configuration, although you can chose to include/exclude HTTPS support.

> **Note**  
>  The recommended build configuration is with HTTPS support using OpenSSL. OpenSSL is smaller and has been integrated with curl since curl's inception.


## Building without HTTPS support

The smallest possible binary you can achieve is by compiling curl without HTTPS support (which removes the dependency on external libs).

You can find the build scripts for curl without HTTPS support on `without-https/` folder.

- **Dependencies:** none
- **Total binary size:** ~900KB (~900KB for libcurl.a)


## Building with HTTPS support via OpenSSL

If you want to generated curl binary to have HTTPS support via OpenSSL (Apache-style license), use the build scripts at `with-https-openssl/` folder.

- **Dependencies:** libssl
- **Total binary size:** ~2.1MB (~900KB for libcurl.a, ~1.2MB for libssl.a)


## Building with HTTPS support via GnuTLS

If you want to generated curl binary to have HTTPS support via GnuTLS (LGPL license), use the build scripts at `with-https-openssl/` folder.

> **Note**  
> These scripts use GnuTLS 2.* rather than 3.*, since 3.* depends on libnettle which in turn depends on libgmp and I couldn't build libgmp for armvX

- **Dependencies:** libgnutls, libgcrypt, libgpg-error
- **Total binary size:** ~8.7MB (~900KB for libcurl.a, ~5.1MB for libgnutls.a, ~2.7MB for libgcrypt.a, ~40K for libgpg-error.a)


## Optimizing for space on your apps

The scripts generate 3 kinds of binaries:

1. One with all the architectures combined (i386, armv6 and armv7);
2. One with just i386, to use on OSX development);
3. One with armvX architectures (without i386), to use only on iPhones/iPads;

For development on iOS, the first one is recommended - allows you to run the app on both the simulator and the physical devices.

When you're about to build the final release (to submit to the app store), you should use the third one - 

> **ProTip™**  
> Use different build targets, and include different variations of the above files in each of them so this process is automatic.


## Acknowledgments

These scripts are based on the excellent work from (x2on)[https://github.com/x2on], with some help from (Bob)[http://stackoverflow.com/questions/9039554/using-libcurl-on-ios-5-as-an-alternative-to-nsurlconnection/9528936#9528936].