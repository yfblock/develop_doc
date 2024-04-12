# Note

<!-- panels:start -->

<!-- div:title-panel -->

## 2024/4/12

<!-- div:left-panel -->

#### Questions

How to write a simple kernel quickly?

#### Trying

1. I have found some useful cargo subcommand. Such as cargo template. These plugin can help us to generate a simple kernel runtime.[Cargo Generate](https://crates.io/crates/cargo-generate)

2. Maybe another crate named rustflags can help us to find a better way to transfer data to kernel or other crates. [rustflags](https://crates.io/crates/rustflags)

3. Autocfg is a tool to automaticall configure code based oncompiler support. Emmm, it just contains some code snippets that will be used at build time.[AutoCfg](https://crates.io/crates/autocfg)

#### What I did today
Help other engineer to solve a problem of the virtio-drivers' example. The fault reason was it use the latest nightly toolchain.
But rust upgrade the LLVM version t0 18 since nightly-2024-02-13. I think there have a small problem that will impact us in the future.

<!-- div:title-panel -->

## 2024/4/10

<!-- div:left-panel -->

How to separate modules from ByteOS and manage them easily?

1. Design a Github Action to retrieve module info from target's README.md file.
2. Design a Github Action to publish rust-doc and publish crates.io automatically.
3. Separate modules from ByteOS as much as possible.

<!-- div:right-panel -->

retrieve: vt. 检索；取回；检索数据；找回；挽回；索回；扭转颓势

<!-- panels:end -->
