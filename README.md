# PythonVsRustAWSLambda

Testing the runtime difference between Python and Rust for AWS Lambda.

This repo contains two example Lambdas:
- `pythonLambda/` — Python implementation
- `rustLambda/` — Rust implementation

The Lambdas are intended to be triggered by an S3 event. Note that an S3-triggered invocation can contain multiple records, so the handler typically loops over the incoming event records.

See the full write-up:
https://www.confessionsofadataguy.com/aws-lambdas-python-vs-rust-performance-and-cost-savings/

## What this benchmark does (high level)

At a high level, both Lambdas:
1. Receive an S3 event
2. For each record in the event, read the referenced object
3. Perform the same workload in Python vs Rust
4. Log timing information so the runtimes can be compared

(For exact details, see the implementation in each language folder.)

## Quick start: Rust Lambda build (cargo-lambda)

The Rust Lambda uses `cargo-lambda` to build and package the `bootstrap` binary required for deployment.

Install cargo-lambda (see the cargo-lambda docs for platform-specific instructions), then build the deployment zip:

```bash
cargo lambda build --release --output-format zip
