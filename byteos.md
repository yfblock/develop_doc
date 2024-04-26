# ByteOS modules and lines

| module name | Rust Line | description |
| --- | --- | --- |
| kernel | 6444 | 宏内核主要代码逻辑 |
| executor | 256 | 异步内核调度器 |
| logging | 107 | Log初始化配置 |
| allocator | 34 | Rust 内存分配器 |
| arch | 4981 | 架构相关硬件抽象层 |
| arm_gic | 191 | arm 通用中断控制器驱动 |
| arm_pl011 | 65 | arm pl011 串口驱动 |
| crate_interface | 166 | 提供跨组建调用机制 |
| dev_fs | 544 | 设备文件系统 |
| devices| 226 | 设备层，提供设备抽象和设备管理 |
| frame_allocator| 198 | 页分配器 |
| fs | 742 | 文件系统管理 |
| general-plic | 83 | riscv 中断控制器 |
| hal | 62 | 将硬件操作进一步封装，提供更好用的操作 |
| irq_safety | 281 | 提供中断安全锁 |
| kgoldfish-rtc | 56 | rtc 设备驱动 |
| kramdisk | 98 | 基于 RAM 的 disk 设备 |
| kvirtio | 322 | virtio 设备驱动结合层 |
| lost-net-stack | 1366 | 简单的网络协议栈 |
| driver-ns16550a | 69 | ns16550a 驱动 |
| percpu | 579 | CPU 本地数据定义访问 |
| procfs | 176 | 进程文件系统 |
| ramfs | 385 | 内存文件系统 |
| signal | 162 | 提供信号相关定义和操作 |
| sync | 94 | 同步互斥操作 |
| timestamp | 71 | 时间戳操作 |
| vfscore | 292 | 文件系统抽象 |
| driver-k210-sdcard | 565 | k210 sd卡驱动 |
| driver-kcvitek-sd | 58 | cvitek-sd 卡驱动内核结合层 |
| driver-knvme | 109 | nvme 驱动内核结合层 |
| backtrace | 26 | 打印异常调用栈 |
| cv1811-sd | 691 | cvitek-sd 卡通用驱动 |  
| 共计(33) | 19499 | |