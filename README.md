tibitset
---

A simple bitset container for Rust, meant to be a replacement for `HashSet`

Please read the [API documentation here](https://docs.rs/tibitset/)

[![build\_status](https://github.com/bestouff/tibitset/workflows/Continuous%20integration/badge.svg?branch=master)](https://github.com/bestouff/tibitset/actions)
[![crates](https://img.shields.io/crates/v/tibitset.svg)](https://crates.io/crates/tibitset)

# Philosophy

This crate is a fork from [fixedbitset](https://crates.io/crates/fixedbitset) with added genericity over its
bit indexing type. It is the same idea like [TiVec](https://crates.io/crates/typed-index-collections) is for `Vec`,
a collection which you can use with a custom index type which is not `usize`.
It's also a nearly-drop-in replacement for `HashSet` which you can use when you have a limited index space
with mostly full collections.

# Usage

```toml
[dependencies]
tibitset = "0.1"
```

```rust
use tibitset::TiBitSet;
use std::convert::TryInto;

struct CustomIndex(pub u16);

impl From<usize> for CustomIndex {
    fn from(value: usize) -> Self {
        CustomIndex(value.try_into().expect("value too large to fit u16"))
    }
}
impl Into<usize> for CustomIndex {
    fn into(self) -> usize {
        self.0.into()
    }
}

let fb: TiBitSet::<CustomIndex>::with_capacity(10);
fb.set(CustomIndex(2), true);
assert!(!fb.contains(CustomIndex(1)));
assert!(fb.contains(CustomIndex(2)));
```


# License

Dual-licensed to be compatible with the Rust project.

Licensed under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0)
 or the [MIT license](https://opensource.org/licenses/MIT),
 at your option. This file may not be copied, modified, or distributed except
according to those terms.
