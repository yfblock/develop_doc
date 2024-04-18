# Note

<!-- panels:start -->


<!-- div:title-panel -->

## 2024/4/18

<!-- div:left-panel -->

#### Trying

How to solve the symbol error in the compile time?

We can define a macro that will generate the boot function and inject the runtime error.

Here is an example.

```rust

boot_entry!(
    entry = crate::main,
    frame_ops = todo!(),   // the type of frame_ops is impl FrameOpsTrait,
    allocator_init = crate::mm::heap::init,
);
```


<!-- div:title-panel -->

## 2024/4/16

<!-- div:left-panel -->

#### Trying 

How to seperate the module from the kernel or ByteOS?

What should I do if I want to write a 

I think we should let kernel to manage the workspace's cargo.toml, because this file will be Override by tool.

<!-- div:title-panel -->

## 2024/4/15

<!-- div:left-panel -->

How to split module from the os?

what should I do if I want to split modules to kernel? Just using kernel tool to download the module info from kernel?

I think I should to write a extend tool to handle this logic.

This tool can use mask.toml or patch.toml to instead of patch.

Reduce the relation between the modules.

```toml

```

What should the tool to do is download the git module to local, and write patch info to kernel.

Is this right?

```toml
# General Denpendencies
[dependencies]

# ByteOS Specific Dependencies
[target.'cfg(target_ps = "ByteOS")'.dependencies]
```

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
