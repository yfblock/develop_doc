# Note

<!-- panels:start -->

<!-- div:title-panel -->

## 2024/5/4

<!-- div:left-panel -->

#### Trying

Use nodejs to parse markdown and deserialize it through markdown-it lib. But it is not a appropriate method. Because markdown's descripte ability is low. The subsititution is TOML、YAML and JSON.

We also can use Kellnr. This is a opensouce crates.io, can publish. https://kellnr.io/documentation#installation


<!-- div:title-panel -->

## 2024/4/29

<!-- div:left-panel -->

#### Discussion

How to improve the system's performance?

Using Rust Async/Await in context will use much time that irq.

If we want to use async, we can use the combination of this.
We can write the context in the top of stack, and use general context switch, when enter kernel privilege, use rust poll to handle async function.
Such as 
```rust
match poll(async move || info!("123")) {
   Poll::pending => switch_context(),
   Poll::Ready(ret) => ret 
};
```

<!-- div:title-panel -->

## 2024/4/29

<!-- div:left-panel -->

#### Discussion

hal with high configuration settins, include stack size, floating point and so on.

#### Trying 

adapt ext4 for byteos, problems.

Q1: Needs riscv64 gc instead of riscv64imac. But riscv64imac is the standard in competition.


<!-- div:title-panel -->

## 2024/4/25

<!-- div:left-panel -->

#### Trying 

Percpu depends on the linker script(.ld), so there will have something wrong if it was written wrong.

Byteos have implmented a simple multicore version based on spin lock. But it's performance reduced by 20 percents when executing the libctest.
I think this is because the spinlock and the locking range are too large. So it often triggers locking.

(Please enable multi-core to recude performance. Please unplug the discrete graphics card to improve performance. LOL)

This situation will be fixed in the future.

<!-- div:title-panel -->

## 2024/4/24

<!-- div:left-panel -->

#### Trying

How to check if git repositories dependencies update ?

```shell
> cargo update SPEC_PACKAGE
```

It can be executed after finishing remove patch, then it can ensure the package was latest version(Just for yourself).

#### Some issues?

When I delete the Cargo.lock to force the cargo to updateb the dependencies to latest version. The build will fail because the fatfs could not find `__log_module_path` in `log`. I found the log verion was upgraded from "0.4.17" to "0.4.21", May be this is a bug. Just record, don't have any motivation to fix it. 


<!-- div:title-panel -->

## 2024/4/23

<!-- div:left-panel -->

#### Trying to support multi core

But it ocurrs the qemu virtio error.
qemu-system-riscv64: virtio: bogus descriptor or out of resources

<!-- div:title-panel -->

## 2024/4/22

<!-- div:left-panel -->

#### Another knowledge

Maybe the thread_local attribute can help us to write the better kernel.

https://github.com/rust-lang/rust/issues/29594

This feature works well for mainstream operating systems.
But it doesn't always work with our operating system.
Maybe we can support this by supporting the ctor and dtor like the rust std does.

https://github.com/rust-lang/rust/blob/7f2fc33da6633f5a764ddc263c769b6b2873d167/library/std/src/sys/pal/xous/thread_local_key.rs#L22

https://github.com/rust-lang/rust/blob/2225ee1b62ff089917434aefd9b2bf509cfa087f/library/std/src/thread/local.rs

https://github.com/rust-lang/rust/issues/28129

https://github.com/rust-lang/rust/issues/74875

https://github.com/crossbeam-rs/crossbeam/blob/master/crossbeam-epoch/src/internal.rs

https://github.com/crossbeam-rs/crossbeam/blob/master/crossbeam-epoch/README.md

https://github.com/rust-lang/rust/pull/10312/files

https://cloud.tencent.com/developer/article/2220168

If we don't do this, we can only alloc a new page and use static generic data types(Can't use alloc).

Some references are here:

https://github.com/dtolnay/inventory/blob/5a50b336f40cd781339118f49daa0cea6cb7f52c/src/lib.rs#L423-L477
https://www.exploit-db.com/papers/13234

I guess that the ctor will be linked at .init_array section.

Tls Data will be filled with .tbss and .tdata.
https://doc.rust-lang.org/beta/unstable-book/compiler-flags/tls-model.html

https://internals.rust-lang.org/t/thread-lifetime-for-tls/13550/7

https://github.com/Amanieu

https://github.com/Amanieu/thread_local-rs

https://docs.rs/thread_local/latest/thread_local/

We can design a new proc-macro that contains the #[thread_local], after that,  drop the memory using ptr::drop_in_place when the thread is existing was possible.

and use linkme to collect it.

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
push to https need authorization manually. The better solution is push to ssh.

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
