# js-libp2p-crypto

[![](https://img.shields.io/badge/made%20by-Protocol%20Labs-blue.svg?style=flat-square)](http://ipn.io)
[![](https://img.shields.io/badge/project-IPFS-blue.svg?style=flat-square)](http://ipfs.io/)
[![](https://img.shields.io/badge/freenode-%23ipfs-blue.svg?style=flat-square)](http://webchat.freenode.net/?channels=%23ipfs)
[![standard-readme compliant](https://img.shields.io/badge/standard--readme-OK-green.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)
[![Coverage Status](https://coveralls.io/repos/github/libp2p/js-libp2p-crypto/badge.svg?branch=master)](https://coveralls.io/github/libp2p/js-libp2p-crypto?branch=master)
[![Travis CI](https://travis-ci.org/libp2p/js-libp2p-crypto.svg?branch=master)](https://travis-ci.org/libp2p/js-libp2p-crypto)
[![Circle CI](https://circleci.com/gh/libp2p/js-libp2p-crypto.svg?style=svg)](https://circleci.com/gh/libp2p/js-libp2p-crypto)
[![Dependency Status](https://david-dm.org/libp2p/js-libp2p-crypto.svg?style=flat-square)](https://david-dm.org/libp2p/js-libp2p-crypto)
[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/feross/standard)

> Crypto primitives for libp2p in JavaScript

This repo contains the JavaScript implementation of the crypto primitives
needed for libp2p. This is based on this [go implementation](https://github.com/libp2p/go-libp2p-crypto).

## Table of Contents

- [Install](#install)
- [Usage](#usage)
  - [Example](#example)
- [API](#api)
  - [`generateKeyPair(type, bits)`](#generatekeypairtype-bits)
  - [`generateEphemeralKeyPair(curve)`](#generateephemeralkeypaircurve)
  - [`keyStretcher(cipherType, hashType, secret)`](#keystretcherciphertype-hashtype-secret)
  - [`marshalPublicKey(key[, type])`](#marshalpublickeykey-type)
  - [`unmarshalPublicKey(buf)`](#unmarshalpublickeybuf)
  - [`marshalPrivateKey(key[, type])`](#marshalprivatekeykey-type)
  - [`unmarshalPrivateKey(buf)`](#unmarshalprivatekeybuf)
- [Contribute](#contribute)
- [License](#license)

## Install

```sh
npm install --save libp2p-crypto
```

## Usage

### Example

```js
const crypto = require('libp2p-crypto')

var keyPair = crypto.generateKeyPair('RSA', 2048)
```

## API

### `generateKeyPair(type, bits)`

- `type: String`, only `'RSA'` is currently supported
- `bits: Number`

Generates a keypair of the given type and bitsize.

### `generateEphemeralKeyPair(curve)`

- `curve: String`, one of `'P-256'`, `'P-384'`, `'P-521'` is currently supported

Generates an ephemeral public key and returns a function that will compute the shared secret key.

Focuses only on ECDH now, but can be made more general in the future.

Returns an object of the form
```js
{
  key: Buffer,
  genSharedKey: Function
}
```

### `keyStretcher(cipherType, hashType, secret)`

- `cipherType: String`, one of `'AES-128'`, `'AES-256'`, `'Blowfish'`
- `hashType: String`, one of `'SHA1'`, `SHA256`, `SHA512`
- `secret: Buffer`

Generates a set of keys for each party by stretching the shared key.

Returns an object of the form
```js
{
  k1: {
    iv: Buffer,
    cipherKey: Buffer,
    macKey: Buffer
  },
  k2: {
    iv: Buffer,
    cipherKey: Buffer,
    macKey: Buffer
  }
}
```
### `marshalPublicKey(key[, type])`

- `key: crypto.rsa.RsaPublicKey`
- `type: String`, only `'RSA'` is currently supported

Converts a public key object into a protobuf serialized public key.

### `unmarshalPublicKey(buf)`

- `buf: Buffer`

Converts a protobuf serialized public key into its  representative object.

### `marshalPrivateKey(key[, type])`

- `key: crypto.rsa.RsaPrivateKey`
- `type: String`, only `'RSA'` is currently supported

Converts a private key object into a protobuf serialized private key.

### `unmarshalPrivateKey(buf)`

- `buf: Buffer`

Converts a protobuf serialized private key into its  representative object.

## Contribute

Feel free to join in. All welcome. Open an [issue](https://github.com/libp2p/js-libp2p-crypto/issues)!

This repository falls under the IPFS [Code of Conduct](https://github.com/ipfs/community/blob/master/code-of-conduct.md).

[![](https://cdn.rawgit.com/jbenet/contribute-ipfs-gif/master/img/contribute.gif)](https://github.com/ipfs/community/blob/master/contributing.md)

## License

[MIT](LICENSE)
