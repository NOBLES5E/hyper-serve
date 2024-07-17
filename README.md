[![Crates.io](https://img.shields.io/crates/v/hyper-serve)](https://crates.io/crates/hyper-serve)
[![Docs](https://img.shields.io/crates/v/hyper-serve?color=blue&label=docs)](https://docs.rs/hyper-serve/)

# hyper-serve

`hyper-serve` is a fork of the [`axum-server`](https://github.com/programatik29/axum-server) project. It is a hyper server implementation designed to be used with the `axum` framework. This fork aims to continue the development and maintenance of the original project, ensuring compatibility with future `axum` releases and providing high performance and security features.

## Features

- HTTP/1 and HTTP/2
- HTTPS through `rustls`
- High performance through `hyper`
- Using `tower` make service API
- Very good `axum` compatibility. Likely to work with future `axum` releases.

## Usage Example

A simple hello world application can be served like:

```rust
use axum::{routing::get, Router};
use std::net::SocketAddr;

#[tokio::main]
async fn main() {
    let app = Router::new().route("/", get(|| async { "Hello, world!" }));

    let addr = SocketAddr::from(([127, 0, 0, 1], 3000));
    println!("listening on {}", addr);
    hyper_serve::bind(addr)
        .serve(app.into_make_service())
        .await
        .unwrap();
}
```

You can find more examples [here](/examples).

## Minimum Supported Rust Version

`hyper-serve`'s MSRV is 1.63.

## Safety

This crate uses `#![forbid(unsafe_code)]` to ensure everything is implemented in 100% safe Rust.

## License

This project is licensed under the MIT license.
