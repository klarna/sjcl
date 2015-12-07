ECC.js: simple wrapper around SJCL
====

Based on https://github.com/bitwiseshiftleft/sjcl and https://github.com/jpillora/eccjs.

[![Build Status](https://travis-ci.org/klarna/sjcl.png)](https://travis-ci.org/klarna/sjcl)

## Build
```bash
$ git clone https://github.com/bitwiseshiftleft/sjcl.git
$ cd sjcl
$ ./configure # Requests for extensions go here, e.g. --with-ecc --with-srp
$ make ecc
$ make test  # If any of the tests fail, beware.
```

## Quick Usage

**Encryption and Decryption**

``` js
// Generate (or load) encryption/decryption keys 
var keys = ecc.generate(ecc.ENC_DEC);
// => { dec: "192e35a51dc....", enc: "192037..." }

// A secret message
var plaintext = "hello world!";

// Encrypt message
var cipher = ecc.encrypt(keys.enc, plaintext);
// => {"iv":[1547037338,-736472389,324... }

// Decrypt message
var result = ecc.decrypt(keys.dec, cipher);

console.log(plaintext === result);
// => true
```

**Sign and Verify**

``` js
// Generate (or load) sign/verify keys 
var keys = ecc.generate(ecc.SIG_VER);
// => { sig: "192e35a51dc....", ver: "192037..." }

// An important message
var message = "hello world!";

// Create digital signature
var signature = ecc.sign(keys.sig, message);

// Verify matches the text
var result = ecc.verify(keys.ver, signature, message);

console.log(result); // => true
```

## API

* `ecc.generate(type[, curve = 192])`
* `ecc.encrypt(key, plaintext)`
* `ecc.decrypt(key, cipher)`
* `ecc.sign(key, text[, hash = true])`
* `ecc.verify(key, signature, text[, hash = true])`

Stanford Javascript Crypto Library

Security Advisories
===

* 12.02.2014: the current development version has a paranoia bug in the ecc module. The bug was introduced in commit [ac0b3fe0](https://github.com/bitwiseshiftleft/sjcl/commit/ac0b3fe0) and might affect ecc key generation on platforms without a platform random number generator.

Security Contact
====
Security Mail: sjcl@ovt.me  
OpenPGP-Key Fingerprint: 0D54 3E52 87B4 EC06 3FA9 0115 72ED A6C7 7AAF 48ED  
Keyserver: pool.sks-keyservers.net  
