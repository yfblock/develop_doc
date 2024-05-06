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

## ext4 iozone benchmark

iozone automatic measurements
        Iozone: Performance Test of File I/O
                Version $Revision: 3.506 $
                Compiled for 64 bit mode.
                Build: linux

        Contributors:William Norcott, Don Capps, Isom Crawford, Kirby Collins
                     Al Slater, Scott Rhine, Mike Wisner, Ken Goss
                     Steve Landherr, Brad Smith, Mark Kelly, Dr. Alain CYR,
                     Randy Dunlap, Mark Montague, Dan Million, Gavin Brebner,
                     Jean-Marc Zucconi, Jeff Blomberg, Benny Halevy, Dave Boone,
                     Erik Habbinga, Kris Strecker, Walter Wong, Joshua Root,
                     Fabrice Bacchella, Zhenghua Xue, Qin Li, Darren Sawyer,
                     Vangel Bojaxhi, Ben England, Vikentsi Lapa,
                     Alexey Skidanov, Sudhir Kumar.

        Run began: Thu Jan  1 00:00:01 1970

        Auto Mode
        Record Size 1 kB
        File size set to 4096 kB
        Command line used: iozone -a -r 1k -s 4m
        Output is in kBytes/sec
        Time Resolution = 0.000021 seconds.
        Processor cache size set to 1024 kBytes.
        Processor cache line size set to 32 bytes.
        File stride size set to 17 * record size.
                                                                    random    random      bkwd     record     stride                          
              kB  reclen    write    rewrite      read    reread      read     write      read    rewrite       read    fwrite  frewrite     fread   freread
            4096       1       269      3114      3206      3277      2843      2477      2716       2588       2800      2969      2965      1812      1840

iozone test complete.
iozone throughput write/read measurements
        Iozone: Performance Test of File I/O
                Version $Revision: 3.506 $
                Compiled for 64 bit mode.
                Build: linux

        Contributors:William Norcott, Don Capps, Isom Crawford, Kirby Collins
                     Al Slater, Scott Rhine, Mike Wisner, Ken Goss
                     Steve Landherr, Brad Smith, Mark Kelly, Dr. Alain CYR,
                     Randy Dunlap, Mark Montague, Dan Million, Gavin Brebner,
                     Jean-Marc Zucconi, Jeff Blomberg, Benny Halevy, Dave Boone,
                     Erik Habbinga, Kris Strecker, Walter Wong, Joshua Root,
                     Fabrice Bacchella, Zhenghua Xue, Qin Li, Darren Sawyer,
                     Vangel Bojaxhi, Ben England, Vikentsi Lapa,
                     Alexey Skidanov, Sudhir Kumar.

        Run began: Thu Jan  1 00:00:38 1970

        Record Size 1 kB
        File size set to 1024 kB
        Command line used: iozone -t 4 -i 0 -i 1 -r 1k -s 1m
        Output is in kBytes/sec
        Time Resolution = 0.000024 seconds.
        Processor cache size set to 1024 kBytes.
        Processor cache line size set to 32 bytes.
        File stride size set to 17 * record size.
        Throughput test with 4 processes
        Each process writes a 1024 kByte file in 1 kByte records

        Children see throughput for  4 initial writers  =     221.13 kB/sec
        Parent sees throughput for  4 initial writers   =     217.22 kB/sec
        Min throughput per process                      =      55.10 kB/sec
        Max throughput per process                      =      55.64 kB/sec
        Avg throughput per process                      =      55.28 kB/sec
        Min xfer                                        =    1004.00 kB

        Children see throughput for  4 rewriters        =    2727.58 kB/sec
        Parent sees throughput for  4 rewriters         =    2656.88 kB/sec
        Min throughput per process                      =     676.38 kB/sec
        Max throughput per process                      =     686.08 kB/sec
        Avg throughput per process                      =     681.89 kB/sec
        Min xfer                                        =     995.00 kB

        Children see throughput for  4 readers          =    2791.46 kB/sec
        Parent sees throughput for  4 readers           =    2718.09 kB/sec
        Min throughput per process                      =     692.09 kB/sec
        Max throughput per process                      =     702.73 kB/sec
        Avg throughput per process                      =     697.86 kB/sec
        Min xfer                                        =     998.00 kB

        Children see throughput for 4 re-readers        =    2740.10 kB/sec
        Parent sees throughput for 4 re-readers         =    2668.06 kB/sec
        Min throughput per process                      =     674.56 kB/sec
        Max throughput per process                      =     690.79 kB/sec
        Avg throughput per process                      =     685.02 kB/sec
        Min xfer                                        =     995.00 kB



iozone test complete.
iozone throughput random-read measurements
        Iozone: Performance Test of File I/O
                Version $Revision: 3.506 $
                Compiled for 64 bit mode.
                Build: linux

        Contributors:William Norcott, Don Capps, Isom Crawford, Kirby Collins
                     Al Slater, Scott Rhine, Mike Wisner, Ken Goss
                     Steve Landherr, Brad Smith, Mark Kelly, Dr. Alain CYR,
                     Randy Dunlap, Mark Montague, Dan Million, Gavin Brebner,
                     Jean-Marc Zucconi, Jeff Blomberg, Benny Halevy, Dave Boone,
                     Erik Habbinga, Kris Strecker, Walter Wong, Joshua Root,
                     Fabrice Bacchella, Zhenghua Xue, Qin Li, Darren Sawyer,
                     Vangel Bojaxhi, Ben England, Vikentsi Lapa,
                     Alexey Skidanov, Sudhir Kumar.

        Run began: Thu Jan  1 00:01:18 1970

        Record Size 1 kB
        File size set to 1024 kB
        Command line used: iozone -t 4 -i 0 -i 2 -r 1k -s 1m
        Output is in kBytes/sec
        Time Resolution = 0.000022 seconds.
        Processor cache size set to 1024 kBytes.
        Processor cache line size set to 32 bytes.
        File stride size set to 17 * record size.
        Throughput test with 4 processes
        Each process writes a 1024 kByte file in 1 kByte records

        Children see throughput for  4 initial writers  =    2708.63 kB/sec
        Parent sees throughput for  4 initial writers   =    2605.94 kB/sec
        Min throughput per process                      =     671.39 kB/sec
        Max throughput per process                      =     686.56 kB/sec
        Avg throughput per process                      =     677.16 kB/sec
        Min xfer                                        =     993.00 kB

        Children see throughput for  4 rewriters        =    2736.45 kB/sec
        Parent sees throughput for  4 rewriters         =    2664.79 kB/sec
        Min throughput per process                      =     676.89 kB/sec
        Max throughput per process                      =     690.14 kB/sec
        Avg throughput per process                      =     684.11 kB/sec
        Min xfer                                        =     998.00 kB

        Children see throughput for 4 random readers    =    2576.12 kB/sec
        Parent sees throughput for 4 random readers     =    2528.03 kB/sec
        Min throughput per process                      =     641.72 kB/sec
        Max throughput per process                      =     647.10 kB/sec
        Avg throughput per process                      =     644.03 kB/sec
        Min xfer                                        =    1019.00 kB

        Children see throughput for 4 random writers    =    2482.72 kB/sec
        Parent sees throughput for 4 random writers     =    2431.47 kB/sec
        Min throughput per process                      =     618.66 kB/sec
        Max throughput per process                      =     622.14 kB/sec
        Avg throughput per process                      =     620.68 kB/sec
        Min xfer                                        =    1017.00 kB



iozone test complete.
iozone throughput read-backwards measurements
        Iozone: Performance Test of File I/O
                Version $Revision: 3.506 $
                Compiled for 64 bit mode.
                Build: linux

        Contributors:William Norcott, Don Capps, Isom Crawford, Kirby Collins
                     Al Slater, Scott Rhine, Mike Wisner, Ken Goss
                     Steve Landherr, Brad Smith, Mark Kelly, Dr. Alain CYR,
                     Randy Dunlap, Mark Montague, Dan Million, Gavin Brebner,
                     Jean-Marc Zucconi, Jeff Blomberg, Benny Halevy, Dave Boone,
                     Erik Habbinga, Kris Strecker, Walter Wong, Joshua Root,
                     Fabrice Bacchella, Zhenghua Xue, Qin Li, Darren Sawyer,
                     Vangel Bojaxhi, Ben England, Vikentsi Lapa,
                     Alexey Skidanov, Sudhir Kumar.

        Run began: Thu Jan  1 00:01:45 1970

        Record Size 1 kB
        File size set to 1024 kB
        Command line used: iozone -t 4 -i 0 -i 3 -r 1k -s 1m
        Output is in kBytes/sec
        Time Resolution = 0.000023 seconds.
        Processor cache size set to 1024 kBytes.
        Processor cache line size set to 32 bytes.
        File stride size set to 17 * record size.
        Throughput test with 4 processes
        Each process writes a 1024 kByte file in 1 kByte records

        Children see throughput for  4 initial writers  =    2706.70 kB/sec
        Parent sees throughput for  4 initial writers   =    2603.90 kB/sec
        Min throughput per process                      =     670.85 kB/sec
        Max throughput per process                      =     683.33 kB/sec
        Avg throughput per process                      =     676.68 kB/sec
        Min xfer                                        =     996.00 kB

        Children see throughput for  4 rewriters        =    2718.23 kB/sec
        Parent sees throughput for  4 rewriters         =    2647.63 kB/sec
        Min throughput per process                      =     675.74 kB/sec
        Max throughput per process                      =     684.57 kB/sec
        Avg throughput per process                      =     679.56 kB/sec
        Min xfer                                        =     995.00 kB

        Children see throughput for 4 reverse readers   =    2574.60 kB/sec
        Parent sees throughput for 4 reverse readers    =    2525.85 kB/sec
        Min throughput per process                      =     640.72 kB/sec
        Max throughput per process                      =     647.44 kB/sec
        Avg throughput per process                      =     643.65 kB/sec
        Min xfer                                        =    1021.00 kB



iozone test complete.
iozone throughput stride-read measurements
        Iozone: Performance Test of File I/O
                Version $Revision: 3.506 $
                Compiled for 64 bit mode.
                Build: linux

        Contributors:William Norcott, Don Capps, Isom Crawford, Kirby Collins
                     Al Slater, Scott Rhine, Mike Wisner, Ken Goss
                     Steve Landherr, Brad Smith, Mark Kelly, Dr. Alain CYR,
                     Randy Dunlap, Mark Montague, Dan Million, Gavin Brebner,
                     Jean-Marc Zucconi, Jeff Blomberg, Benny Halevy, Dave Boone,
                     Erik Habbinga, Kris Strecker, Walter Wong, Joshua Root,
                     Fabrice Bacchella, Zhenghua Xue, Qin Li, Darren Sawyer,
                     Vangel Bojaxhi, Ben England, Vikentsi Lapa,
                     Alexey Skidanov, Sudhir Kumar.

        Run began: Thu Jan  1 00:02:06 1970

        Record Size 1 kB
        File size set to 1024 kB
        Command line used: iozone -t 4 -i 0 -i 5 -r 1k -s 1m
        Output is in kBytes/sec
        Time Resolution = 0.000022 seconds.
        Processor cache size set to 1024 kBytes.
        Processor cache line size set to 32 bytes.
        File stride size set to 17 * record size.
        Throughput test with 4 processes
        Each process writes a 1024 kByte file in 1 kByte records

        Children see throughput for  4 initial writers  =    2712.90 kB/sec
        Parent sees throughput for  4 initial writers   =    2608.20 kB/sec
        Min throughput per process                      =     672.43 kB/sec
        Max throughput per process                      =     688.58 kB/sec
        Avg throughput per process                      =     678.23 kB/sec
        Min xfer                                        =     993.00 kB

        Children see throughput for  4 rewriters        =    2712.27 kB/sec
        Parent sees throughput for  4 rewriters         =    2642.98 kB/sec
        Min throughput per process                      =     668.45 kB/sec
        Max throughput per process                      =     686.30 kB/sec
        Avg throughput per process                      =     678.07 kB/sec
        Min xfer                                        =     995.00 kB

        Children see throughput for 4 stride readers    =    2536.98 kB/sec
        Parent sees throughput for 4 stride readers     =    2488.88 kB/sec
        Min throughput per process                      =     628.38 kB/sec
        Max throughput per process                      =     640.56 kB/sec
        Avg throughput per process                      =     634.24 kB/sec
        Min xfer                                        =    1019.00 kB



iozone test complete.
iozone throughput fwrite/fread measurements
        Iozone: Performance Test of File I/O
                Version $Revision: 3.506 $
                Compiled for 64 bit mode.
                Build: linux

        Contributors:William Norcott, Don Capps, Isom Crawford, Kirby Collins
                     Al Slater, Scott Rhine, Mike Wisner, Ken Goss
                     Steve Landherr, Brad Smith, Mark Kelly, Dr. Alain CYR,
                     Randy Dunlap, Mark Montague, Dan Million, Gavin Brebner,
                     Jean-Marc Zucconi, Jeff Blomberg, Benny Halevy, Dave Boone,
                     Erik Habbinga, Kris Strecker, Walter Wong, Joshua Root,
                     Fabrice Bacchella, Zhenghua Xue, Qin Li, Darren Sawyer,
                     Vangel Bojaxhi, Ben England, Vikentsi Lapa,
                     Alexey Skidanov, Sudhir Kumar.

        Run began: Thu Jan  1 00:02:27 1970

        Record Size 1 kB
        File size set to 1024 kB
        Command line used: iozone -t 4 -i 6 -i 7 -r 1k -s 1m
        Output is in kBytes/sec
        Time Resolution = 0.000022 seconds.
        Processor cache size set to 1024 kBytes.
        Processor cache line size set to 32 bytes.
        File stride size set to 17 * record size.
        Throughput test with 4 processes
        Each process writes a 1024 kByte file in 1 kByte records

        Children see throughput for  4 fwriters         =    2756.04 kB/sec
        Parent sees throughput for  4 fwriters          =    2664.81 kB/sec
        Min throughput per process                      =     688.52 kB/sec
        Max throughput per process                      =     689.71 kB/sec
        Avg throughput per process                      =     689.01 kB/sec
        Min xfer                                        =    1024.00 kB

        Children see throughput for  4 freaders         =    1601.22 kB/sec
        Parent sees throughput for  4 freaders          =    1570.42 kB/sec
        Min throughput per process                      =     396.39 kB/sec
        Max throughput per process                      =     404.33 kB/sec
        Avg throughput per process                      =     400.31 kB/sec
        Min xfer                                        =    1024.00 kB



iozone test complete.
iozone throughput pwrite/pread measurements
        Iozone: Performance Test of File I/O
                Version $Revision: 3.506 $
                Compiled for 64 bit mode.
                Build: linux

        Contributors:William Norcott, Don Capps, Isom Crawford, Kirby Collins
                     Al Slater, Scott Rhine, Mike Wisner, Ken Goss
                     Steve Landherr, Brad Smith, Mark Kelly, Dr. Alain CYR,
                     Randy Dunlap, Mark Montague, Dan Million, Gavin Brebner,
                     Jean-Marc Zucconi, Jeff Blomberg, Benny Halevy, Dave Boone,
                     Erik Habbinga, Kris Strecker, Walter Wong, Joshua Root,
                     Fabrice Bacchella, Zhenghua Xue, Qin Li, Darren Sawyer,
                     Vangel Bojaxhi, Ben England, Vikentsi Lapa,
                     Alexey Skidanov, Sudhir Kumar.

        Run began: Thu Jan  1 00:02:42 1970

        Record Size 1 kB
        File size set to 1024 kB
        Command line used: iozone -t 4 -i 9 -i 10 -r 1k -s 1m
        Output is in kBytes/sec
        Time Resolution = 0.000022 seconds.
        Processor cache size set to 1024 kBytes.
        Processor cache line size set to 32 bytes.
        File stride size set to 17 * record size.
        Throughput test with 4 processes
        Each process writes a 1024 kByte file in 1 kByte records

        Children see throughput for 4 pwrite writers    =    2784.67 kB/sec
        Parent sees throughput for 4 pwrite writers     =    2674.93 kB/sec
        Min throughput per process                      =     692.80 kB/sec
        Max throughput per process                      =     704.93 kB/sec
        Avg throughput per process                      =     696.17 kB/sec
        Min xfer                                        =     997.00 kB

        Children see throughput for 4 pread readers     =    2881.96 kB/sec
        Parent sees throughput for 4 pread readers      =    2803.07 kB/sec
        Min throughput per process                      =     712.16 kB/sec
        Max throughput per process                      =     727.76 kB/sec
        Avg throughput per process                      =     720.49 kB/sec
        Min xfer                                        =    1000.00 kB



iozone test complete.
iozone throughtput pwritev/preadv measurements
        Iozone: Performance Test of File I/O
                Version $Revision: 3.506 $
                Compiled for 64 bit mode.
                Build: linux

        Contributors:William Norcott, Don Capps, Isom Crawford, Kirby Collins
                     Al Slater, Scott Rhine, Mike Wisner, Ken Goss
                     Steve Landherr, Brad Smith, Mark Kelly, Dr. Alain CYR,
                     Randy Dunlap, Mark Montague, Dan Million, Gavin Brebner,
                     Jean-Marc Zucconi, Jeff Blomberg, Benny Halevy, Dave Boone,
                     Erik Habbinga, Kris Strecker, Walter Wong, Joshua Root,
                     Fabrice Bacchella, Zhenghua Xue, Qin Li, Darren Sawyer,
                     Vangel Bojaxhi, Ben England, Vikentsi Lapa,
                     Alexey Skidanov, Sudhir Kumar.

        Run began: Thu Jan  1 00:03:01 1970

        Selected test not available on the version.
        Record Size 1 kB
        File size set to 1024 kB
        Command line used: iozone -t 4 -i 11 -i 12 -r 1k -s 1m
        Output is in kBytes/sec
        Time Resolution = 0.000022 seconds.
        Processor cache size set to 1024 kBytes.
        Processor cache line size set to 32 bytes.
        File stride size set to 17 * record size.
        Throughput test with 4 processes
        Each process writes a 1024 kByte file in 1 kByte records

        Children see throughput for  4 initial writers  =    2729.33 kB/sec
        Parent sees throughput for  4 initial writers   =    2624.44 kB/sec
        Min throughput per process                      =     678.35 kB/sec
        Max throughput per process                      =     691.02 kB/sec
        Avg throughput per process                      =     682.33 kB/sec
        Min xfer                                        =     997.00 kB

        Children see throughput for  4 rewriters        =    2755.24 kB/sec
        Parent sees throughput for  4 rewriters         =    2681.20 kB/sec
        Min throughput per process                      =     681.65 kB/sec
        Max throughput per process                      =     692.73 kB/sec
        Avg throughput per process                      =     688.81 kB/sec
        Min xfer                                        =     997.00 kB



iozone test complete.