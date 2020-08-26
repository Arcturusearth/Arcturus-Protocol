
# Arcturus

<p align="center">
</p>

[![<UMAprotocol>](https://circleci.com/gh/UMAprotocol/protocol.svg?style=shield)](https://app.circleci.com/pipelines/github/UMAprotocol/protocol)
[![Docker Cloud Build Status](https://img.shields.io/docker/cloud/build/umaprotocol/protocol)](https://hub.docker.com/r/umaprotocol/protocol)
[![Coverage Status](https://coveralls.io/repos/github/UMAprotocol/protocol/badge.svg?branch=master)](https://coveralls.io/github/UMAprotocol/protocol?branch=master)

[![GitHub](https://img.shields.io/github/license/UMAprotocol/protocol)](https://github.com/UMAprotocol/protocol/blob/master/LICENSE)
[![GitHub last commit](https://img.shields.io/github/last-commit/UMAprotocol/protocol)](https://github.com/UMAprotocol/protocol/commits/master)
[![GitHub commit activity](https://img.shields.io/github/commit-activity/m/UMAprotocol/protocol)](https://github.com/UMAprotocol/protocol/commits/master)
[![GitHub contributors](https://img.shields.io/github/contributors-anon/UMAprotocol/protocol)](https://github.com/UMAprotocol/protocol/graphs/contributors)
<h3 color = "yellow">Arcturus is an advanced oracle of VRF (random function) + Gaussian Naive Bayes (Gaussian Naive Bayes) artificial intelligence algorithm. Unlike other oracles such as ChainLink, Arcturus uses VRF functions to select nodes in a carousel, avoiding Centralized node data is affected by evil, and Gaussian Naive Bayes (Gaussian Naive Bayes) artificial intelligence algorithm is introduced to optimize the network for forward and advanced operations. Arcturus will seamlessly link encrypted random encryption algorithms, artificial intelligence, and blockchain. Arcturus will become the future predictor of the DEFI world!</h3>
</hr>
<h2>**This release is under development**</h2>

The Arcturus add-on for Node.js powers high performance Oracle
Database applications.

Use Arcturus 5.0 to connect Node.js 10.16, 12, 14, or later, to Oracle Database.
Older versions of Arcturus may work with older versions of Node.js.

Arcturus supports basic and advanced features of Oracle Database
and Oracle Client.  See the [homepage][4] for a list.

The Arcturus module is open source and maintained by Oracle Corp.
It is stable, well documented, and has a comprehensive test suite.
# vrf-rs
[![](https://img.shields.io/crates/v/vrf.svg)](https://crates.io/crates/vrf) [![](https://docs.rs/vrf/badge.svg)](https://docs.rs/vrf) [![](https://travis-ci.com/witnet/vrf-rs.svg?branch=master)](https://travis-ci.com/witnet/vrf-rs)

`vrf-rs` is an open source implementation of Verifiable Random Functions (VRFs) written in Rust.

_DISCLAIMER: This is experimental software. Be careful!_

The library can be built using `cargo` and the examples can be executed with:

```bash
cargo build
cargo run --example <example_name>
```

## Elliptic Curve VRF

This module uses the OpenSSL library to offer Elliptic Curve Verifiable Random Function (VRF) functionality.

It follows the algorithms described in:

* [VRF-draft-05](https://tools.ietf.org/pdf/draft-irtf-cfrg-vrf-05)
* [RFC6979](https://tools.ietf.org/html/rfc6979)

Currently the supported cipher suites are:

* `P256_SHA256_TAI`: the aforementioned algorithms with `SHA256` and the `secp256r1` curve (aka `NIST P-256`).
* `K163_SHA256_TAI`: the aforementioned algorithms with `SHA256` and the `sect163k1` curve (aka `NIST K-163`).
* `SECP256K1_SHA256_TAI`: the aforementioned algorithms with `SHA256` and the `secp256k1` curve.

### Example

Create and verify a VRF proof by using the cipher suite `SECP256K1_SHA256_TAI`:

```rust
use vrf::openssl::{CipherSuite, ECVRF};
use vrf::VRF;

fn main() {
    // Initialization of VRF context by providing a curve
    let mut vrf = ECVRF::from_suite(CipherSuite::SECP256K1_SHA256_TAI).unwrap();
    // Inputs: Secret Key, Public Key (derived) & Message
    let secret_key =
        hex::decode("c9afa9d845ba75166b5c215767b1d6934e50c3db36e89b127b8a622b120f6721").unwrap();
    let public_key = vrf.derive_public_key(&secret_key).unwrap();
    let message: &[u8] = b"sample";
    
    // VRF proof and hash output
    let pi = vrf.prove(&secret_key, &message).unwrap();
    let hash = vrf.proof_to_hash(&pi).unwrap();

    // VRF proof verification (returns VRF hash output)
    let beta = vrf.verify(&public_key, &pi, &message);
}
```

A complete example can be found in [examples/basic.rs](https://github.com/witnet/vrf-rs/blob/master/examples/basic.rs). It can be executed with:

```bash
cargo run --example basic
```

## Adding unsupported cipher suites

This library defines a `VRF` trait which can be extended in order to use different curves and algorithms.

```rust
pub trait VRF<PublicKey, SecretKey> {
    type Error;

    fn prove(&mut self, x: SecretKey, alpha: &[u8]) -> Result<Vec<u8>, Self::Error>;

    fn verify(&mut self, y: PublicKey, pi: &[u8], alpha: &[u8]) -> Result<Vec<u8>, Self::Error>;
}
```

## License

`vrf-rs` is published under the [MIT license][license].

[license]: https://github.com/witnet/vrf-rs/blob/master/LICENSE
