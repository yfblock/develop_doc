# Note

<!-- panels:start -->

<!-- div:title-panel -->

## 2024/4/20

<!-- div:left-panel -->

#### Another knowledge

Maybe the thread_local attribute can help us to write the better kernel.

https://github.com/rust-lang/rust/issues/29594

This feature can work fine for mainstream operating systems.
But it is now always available for our operating system.
Maybe we can support this by supporting the ctor and dtor like rust std.

https://github.com/rust-lang/rust/blob/7f2fc33da6633f5a764ddc263c769b6b2873d167/library/std/src/sys/pal/xous/thread_local_key.rs#L22



<!-- div:title-panel -->

## 2024/4/20

<!-- div:left-panel -->

Finally, I gound out the reason for crate_interface's born and how to extend it.

This is the doc for rust --extern option.
https://doc.rust-lang.org/nightly/unstable-book/compiler-flags/extern-options.html

We can use this like using the alloc crate. 



like this

```shell
rustc --extern crate_name
```

```plain
   Compiling once_cell v1.18.0
    error[E0463]: can't find crate for `kernel`

    For more information about this error, try `rustc --explain E0463`.
    error: could not compile `cfg-if` (lib) due to previous error
    warning: build failed, waiting for other jobs to finish...
    error: could not compile `static_assertions` (lib) due to previous error
    error: could not compile `bitflags` (lib) due to previous error
    error: could not compile `scopeguard` (lib) due to previous error
    error: could not compile `num_enum` (lib) due to previous error
    error: could not compile `timestamp` (lib) due to previous error
    error: could not compile `downcast-rs` (lib) due to previous error
    error: could not compile `bare-metal` (lib) due to previous error
    error: could not compile `linkme` (lib) due to previous error
    error: could not compile `bitflags` (lib) due to previous error
    error: could not compile `bit_field` (lib) due to previous error
    error: could not compile `once_cell` (lib) due to previous error
    error: could not compile `byteorder` (lib) due to previous error
    error: could not compile `fdt` (lib) due to previous error
    error: could not compile `crossbeam-utils` (lib) due to previous error
    error: could not compile `num-traits` (lib) due to previous error
```

or using env-set to modify environment and pass arguments

https://doc.rust-lang.org/nightly/unstable-book/compiler-flags/env-set.html

maybe feature start is a better choice than link = ".text" or nomangle
https://doc.rust-lang.org/nightly/unstable-book/language-features/start.html#usage-together-with-the-std-crate

no_std thread_local attribute
https://github.com/rust-lang/rust/issues/29594

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

how to push to remote after patch? 
push to https need authorization manually. The better solution is push to ssh

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
