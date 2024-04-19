# Questions

## 2024/4/16

#### 关于编写多仓库开发相关脚本：

1. 既然模块之间需要独立，那怎么将模块进行组合？ 写一个 yaml 文件，然后使用脚本下载？还是在 ArceOS 主仓库中保留对分支的信息。
2. 既然模块更新都要及时回到 ArceOS 中，那么怎么保证被别人更新过的模块可以保持对 ArceOS 的兼容性，在 yaml 或者主仓库中保留的是子模块的 commit 的信息，还是永远都保持最新的？
3. 如果一直都保持最新的，那么怎么保证每个人能拿到的 ArceOS 代码都是稳定的（直接带来的影响就是针对训练营），别人更新的模块可能会影响到更多人的使用。如果是只保持commit，那么怎么保证模块都能最快回到 ArceOS 主仓库并进行测试？
4. 多仓库开发的时候怎么记录 commit 信息，是否让多仓库共用一条 commit message，因为是多仓库，是否合适？
5. 模块独立的时候怎么处理模块间的 ".." 依赖，如果独立出去，无法使用 Cargo.toml [workspace.dependencies] 依赖，是否是一个弊端？

#### 关于编写 Cargo 模块化工具的思路

目前 cargo build 工具的缺点，或者说是 Cargo 工具的缺点是，无法有效的处理 features, 且 features 会存在于项目的各个地方，这个时候很难去统一，且不太支持 Rust 已经支持的 --cfg 进行特定的 config 设置，所有的配置几乎都要通过 feature 进行设置，是否可以编写一个新的工具（初步命名为 cargo ebuild），通过设置一个新的配置文件，或者针对 Workspace 的配置文件进行扩充，可以将 cfg 传递到 Rust 代码的每个地方。

1. 配置文件或者扩充 Workspace(Cargo.toml [Workspace])
```toml
[ebuild.cfg]
target_os = "byteos"
cpu = "thead-c906"
drivers = ""
```

甚至可以添加上特定的架构信息和 target 来编译不同的平台

```toml
[ebuild.target.riscv64-qemu.cfg]
cargo-target = "riscv64imac-unknown-none-elf"
cpu = "thead-c906" # Override the cpu config.
```

#### 关于 Cargo [Workspace.dependencies] 的使用

1. 在项目根目录 [Workspace.dependencies] 中可以去写依赖

```toml
[workspace.dependencies]
log = "0.4"
```

2. 然后在各个子模块中使用 

```toml
[dependencies]
log = { workspace = true }
```

[informations https://doc.rust-lang.org/cargo/reference/workspaces.html](https://doc.rust-lang.org/cargo/reference/workspaces.html)


#### 关于在编译期间使用 env 来传递参数

> 这个方案可能不是很优雅

https://github.com/rust-lang/rust/pull/99322/files
Make {integer}::from_str_radix constant #99322
