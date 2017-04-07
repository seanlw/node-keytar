# keytar - Node module to manage system keychain

[![Build
Status](https://travis-ci.org/atom/node-keytar.svg?branch=master)](https://travis-ci.org/atom/node-keytar)

A native Node module to get, add, replace, and delete passwords in system's keychain. On OS X the passwords are managed by the Keychain, on Linux they are managed by the Secret Service API/libsecret, and on Windows they are managed by Credential Vault.

## Installing

```sh
npm install keytar
```

### On Linux

Currently this library uses `libsecret` so you may need to install it before `npm install`ing.

Depending on your distribution, you will need to run the following command:

* Debian/Ubuntu: `sudo apt-get install libsecret-1-dev`
* Red Hat-based: `sudo yum install libsecret-devel`
* Arch Linux: `sudo pacman -S libsecret`

## Building

  * Clone the repository
  * Run `npm install`
  * Run `npm test` to run the tests

## Docs

```javascript
const keytar = require('keytar')
```

Every function in keytar is asynchronous. You may pass a callback, or you may omit it to return a promise from the function instead. If you pass a callback, the callback will receive any error as the first parameter and the function's "yields" value as the second. If you leave off the callback and receive a promise, the promise will be rejected with any error that occurs or will be resolved with the function's "yields" value.

### getPassword(service, account, [callback])

Get the stored password for the `service` and `account`.

`service` - The string service name.

`account` - The string account name.

Yields the string password or `null` if an entry for the given service and account was not found.

### setPassword(service, account, password, [callback])

Save the `password` for the `service` and `account` to the keychain. Adds a new entry if necessary, or updates an existing entry if one exists.

`service` - The string service name.

`account` - The string account name.

`password` - The string password.

Yields nothing.

### deletePassword(service, account, [callback])

Delete the stored password for the `service` and `account`.

`service` - The string service name.

`account` - The string account name.

Yields `true` if a password was deleted, or `false` if an entry with the given service and account was not found.

### findPassword(service)

Find a password for the `service` in the keychain.

`service` - The string service name.

Yields the string password, or `null` if an entry for the given service and account was not found.
