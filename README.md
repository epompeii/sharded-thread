# sharded-thread

[![release](https://github.com/Miaxos/json-predicate/actions/workflows/release.yml/badge.svg)](https://github.com/Miaxos/sharded-thread/actions/workflows/release.yml)
[![Crates.io version](https://img.shields.io/crates/v/sharded-thread.svg)](https://crates.io/crates/sharded-thread)
[![dependency status](https://deps.rs/repo/github/miaxos/sharded-thread/status.svg)](https://deps.rs/repo/github/miaxos/sharded-thread)
[![docs.rs docs](https://img.shields.io/badge/docs-latest-blue.svg)](https://docs.rs/sharded-thread)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/miaxos/sharded-thread/compare)


"*Application tail latency is critical for services to meet their latency 
expectations. We have shown that the thread-per-core approach can reduce 
application tail latency of a key-value store by up to 71% compared to baseline 
Memcached running on commodity hardware and Linux.*"[^1]

[^1]: [The Impact of Thread-Per-Core Architecture on Application Tail Latency](https://helda.helsinki.fi/server/api/core/bitstreams/3142abaa-16e3-4ad0-beee-e62add589fc4/content)

## Introduction

This library is mainly made for `io-uring` and monoio. There are no dependency
on the runtime, so you should be able to use it with other runtime and also
without `io-uring`.

The purpose of this library is to have a performant way to send data between
thread when threads are following a `thread per core` architecture. Even if the
aim is to be performant remember it's a core to core passing, (or thread to
thread), which is really slow.

Thanks to [Glommio](https://github.com/DataDog/glommio/) for the inspiration.

## Example

Originally, the library was made when you had multiple thread listening to the
same `TcpStream` and depending on what is sent through the `TcpStream` you might
want to change the thread handling the stream.

<p align="center">
    <img src="./.github/ressources/sharded-thread.drawio.svg" width="60%" />
</p>

You can check some examples in the tests.

## Benchmarks

Those benchmarks are only indicative, they are running in GA. You should run
your own on the targeted hardware.

<p align="center">
<a href="https://bencher.dev/perf/sharded-thread?key=true&reports_per_page=4&branches_per_page=8&testbeds_per_page=8&benchmarks_per_page=8&reports_page=1&branches_page=1&testbeds_page=1&benchmarks_page=1"><img src="https://api.bencher.dev/v0/projects/sharded-thread/perf/img?branches=abb3e39f-486d-45af-924f-3614316b6781&testbeds=63179e4d-88f0-4247-85f4-ad6952282d58&benchmarks=2b3141e3-f3f6-42b7-8209-43381c453c67&measures=0e7c206f-e0e3-4672-be1a-b3820dc2789a&start_time=1702401209000&end_time=1704993221000&title=Benches" title="Benches" alt="Benches for sharded-thread - Bencher" width="60%" /></a>
</p>

## References

- [Glommio example on their sharding](https://github.com/DataDog/glommio/blob/master/examples/sharding.rs)
- [The original monoio issue](https://github.com/bytedance/monoio/issues/213)
- [Sharded Queue - the fastest concurrent collection](https://github.com/ivanivanyuk1993/utility.sharded_queue)

## License

Licensed under either of

- Apache License, Version 2.0, (LICENSE-APACHE or http://www.apache.org/licenses/LICENSE-2.0)
- MIT license (LICENSE-MIT or http://opensource.org/licenses/MIT) at your option.
