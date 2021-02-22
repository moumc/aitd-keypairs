# aitd-keypairs [![NPM](https://img.shields.io/npm/v/aitd-keypairs.svg)](https://npmjs.org/package/aitd-keypairs) [![Build Status](https://img.shields.io/travis/aitd/aitd-keypairs/master.svg)](https://travis-ci.org/aitd/aitd-keypairs) ![Codecov](https://img.shields.io/codecov/c/github/aitd/aitd-keypairs)

An implementation of AITD Ledger keypairs & wallet generation using
[elliptic](https://github.com/indutny/elliptic) which supports rfc6979 and
eddsa deterministic signatures.

[![NPM](https://nodei.co/npm/aitd-keypairs.png)](https://www.npmjs.org/package/aitd-keypairs)

## API Methods

```
generateSeed({entropy?: Array<integer>, algorithm?: string}) -> string
```
Generate a seed that can be used to generate keypairs. Entropy can be provided as an array of bytes expressed as integers in the range 0-255. If provided, it must be 16 bytes long (additional bytes are ignored). If not provided, entropy will be automatically generated. The "algorithm" defaults to "ecdsa-secp256k1", but can also be set to "ed25519". The result is a seed encoded in base58, starting with "s".

```
deriveKeypair(seed: string) -> {privateKey: string, publicKey: string}
```
Derive a public and private key from a seed. The keys are represented as 33-byte hexadecimal strings.

```
sign(messageHex: string, privateKey: string) -> string
```
Sign an arbitrary hex-encoded message with a private key. Returns the signature as a hexadecimal string.

```
verify(messageHex: string, signature: string, publicKey: string) -> boolean
```
Verify a signature for a given hex-encoded message and public key. Returns true if the signature is valid, false otherwise.

```
deriveAddress(publicKey: string) -> string
```
Derive an AITD Ledger classic address from a public key.

```
deriveNodeAddress(publicKey: string) -> string
```
Derive a node address from a public key.


## Generate a random AITD Ledger address

```
const seed = generateSeed();
const keypair = deriveKeypair(seed);
const address = deriveAddress(keypair.publicKey);
```
