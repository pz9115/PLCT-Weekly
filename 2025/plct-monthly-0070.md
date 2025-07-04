# PLCT 开源进展·第 70 期·2025 年 5 月汇总

## 卷首语

5月是劳动的季节，也有收获的喜悦。PLCT实验室的一系列长期的开源努力，在多个开源项目上都实现了阶段性的突破。中旬的 RISC-V 欧洲峰会，PLCT实验室资助了 2 名伙伴赴法国展示 RuyiSDK 等开源成果。下旬，雄安新区围绕 RISC-V 组织了两天的高级别会议，打造「RISC-V 之城」的口号也被提出。高校方面，在合肥工业大学、中国科学技术大学、大连理工大学分别举办了「开源之夏」和 RISC-V 走进高校的活动。一系列高校活动火热的展开了。

今年是 PLCT Lab 充满挑战的一年：既面临着周期性的人员调整，又怀着进一步深入国际开源治理的雄心。同时，在学术领域，PLCT Lab 也开始了新的尝试。希望在不久的将来，PLCT的伙伴和实习生同学们，可以在一些微小的地方，突破人类的知识边界。

## 本期亮点

PLCT实验室的亮点产出通过「RuyiSDK」微信公众号（ID：RuyiSDK）和英文网站提供更新服务：

- https://plctlab.org/en/news/

为了减少冗余工作量，已经在微信公众号推送的中文信息默认不再搬运。

## RuyiSDK IDE
1. RuyiSDK IDE 插件开发：
   - 发布插件 [V0.0.4](https://github.com/ruyisdk/ruyisdk-eclipse-plugins/releases/tag/v0.0.4) 版本：
      - 优化：插件工程调整及规范化：
      - 新增ruyi包管理器：
         - ide启动时自动ruyi安装检测：根据安装情况、版本情况进入对应向导界面；
         - 实现安装向导：根据实际环境情况进入ruyi安装/ruyi更新先导，按照向导界面引导完成ruyi的安装和版本更新；以及ruyi安装路径、软件源、遥测模式的设置，以及ruyi软件索引更新，全流程；
         - 提供 “ RuyiSDK > Ruyi Installation” 菜单项目，手动启动ruyi安装检测
      - 新增 RuyiSDK 配置面板 (Windows > Preferences > RuyiSDK) ：
         - 提供 “ Windows > Preferences > RuyiSDK > Ruyi Config ” 配置项：提供ruyi启动自动检测设置、安装路径设置、软件源设置、遥测模式设置等基本配置选项；
         - 提供 “ Windows > Preferences > RuyiSDK > Device Manage ” 配置项：提供RISC-V开发板的新增、修改、删除、设为默认设备等功能；
   - 发布插件 [V0.0.5](https://github.com/ruyisdk/ruyisdk-eclipse-plugins/releases/tag/v0.0.5) 版本：
      - ruyi 插件优化：
         - 针对 ruyi 安装向导中下载进度条不能达到100%的问题进行了修复；
         - 删除 ruyi 安装向导中将 ruyi 加入到 path 路径的设定和步骤，改为使用 ruyi 绝对路径；
      - 新增软件包资源管理插件：
         - 通过树状结构分类展示软件包资源，并通过 checkbox 状态表示软件包资源的下载状态；
         - 实现对所勾选软件包的批量下载；
         - 支持打开软件包资源的本地缓存等路径，方便查看缓存文件；
2. RuyiSDK IDE 正在招聘插件开发实习生，详情参考 [J159 RuyiSDK IDE 开发实习生](https://github.com/lazyparser/weloveinterns/blob/master/open-internships.md) ，欢迎有兴趣的小伙伴加入。

## RuyiSDK 包管理器

项目地址：https://github.com/ruyisdk/ruyi

5 月份 RuyiSDK 包管理器发布了 2 个新版本：0.33.0、0.34.0，对应
RuyiSDK 整体的 0.33 与 0.34 两个正式版本。您可移步
[GitHub Releases][GitHub Releases] 或 [ISCAS 镜像源][iscas]下载体验。

[GitHub Releases]: https://github.com/ruyisdk/ruyi/releases/tag/0.34.0
[iscas]: https://mirror.iscas.ac.cn/ruyisdk/ruyi/tags/0.34.0/

本月的主要变更如下：

Release Engineering 与工程化方面：

* 重构了 `ruyi` 命令行工具的入口点和 `ruyi` 的日志处理方式，消除了大部分全局量的使用，以便后续 RuyiSDK 生态的其他 Python 组件复用 `ruyi` 的功能。
* `ruyi admin format-manifest` 会保留文件头部和尾部的注释了。

`ruyi` 包管理器命令行工具方面：

* 将设备安装器的数据源迁移到了实体数据库，以降低维护成本、避免频繁更新时潜在的合并冲突等。
* 支持了部分解包 `tar` 归档文件，以适应个别厂商在其官方渠道将多个软件打成一个包分发的做法。
* 允许用 `ruyi venv --extra-commands-from` 为虚拟环境提供额外的与目标元组（target tuple）无关的命令，如特定厂商的刷写工具等。
* 遥测功能更新：
    * 当用户在终端首次运行 `ruyi` 时，现在会一次性询问用户是否允许立即上传安装信息。
    * 修复了 `ruyi` 的命令转发模式下遥测事件未被记录的问题。
    * 支持在软件源级别记录软件包的安装动作，以便第一方或第三方软件源的维护者们了解其软件的使用情况。

RuyiSDK 软件源方面：

* 软件源格式更新：
    * 明确了官方软件源的 ID 为 `ruyisdk`，以便后续与第三方源和谐共存。
    * 术语更新：将那些指代非标准行为的"flavor"重命名为了"quirk"。
    * 为支持软件包声明其含有的可执行命令，为 `binary` 元数据新增了 `commands` 可选字段。
    * 为支持 `tar` 归档文件的部分解包，为 `distfile` 元数据新增了 `prefixes_to_unpack` 可选字段。
* 完善了设备支持：
    * 新增支持了 Milk-V Meles 的 16G RAM 型号，支持 RevyOS 系统。
    * `board-image/revyos-sipeed-lpi4a`: 更新了 Sipeed LicheePi 4A 的 RevyOS 镜像版本至 20250420，修复了 20250323 版本的信息。
    * 将 Milk-V Duo 系列设备的 1.0.7 版本的 "Python" 镜像与非 "Python" 镜像调换了名称。
* 新增软件包：
    * `board-util/wlink`: 社区独立实现的 WCH-Link 刷写与调试工具。
    * `source/wch-ch32v103-evt`: WCH CH32V103 EVT 官方代码示例包。
    * `source/wch-ch32v20x-evt`: WCH CH32V20x EVT 官方代码示例包。
    * `source/wch-ch32v307-evt`: WCH CH32V30x & CH32V317 EVT 官方代码示例包。
    * `toolchain/gnu-wch-mrs-toolchain-gcc12-bin`: WCH MounRiver Studio (MRS) 工具链的官方 2.1.0 版本，其中的 GCC 12.x 工具链。仅支持 x86\_64 架构。
    * `toolchain/gnu-wch-mrs-toolchain-gcc8-bin`: WCH MounRiver Studio (MRS) 工具链的官方 2.1.0 版本，其中的 GCC 8.x 工具链。仅支持 x86\_64 架构。
* 更新软件包：
    * `toolchain/gnu-plct-xthead`: 采用玄铁官方源码、由 PLCT 构建的玄铁工具链的 3.1.0 版本，GCC 版本为 14.1.1。
* 实体数据库更新：
    * 设备实体定义更新：设备型号变体现已被拆分为单独实体类型 `device-variant` 了。
    * 新增了"设备适用系统信息"实体 `image-combo`。
    * 新增了 WCH 微架构、CPU 的实体定义。
    * 修正了 WCH 开发板的 CPU 信息。
* 插件系统更新：
    * 新增了初步的 RISC-V 32 位配置文件支持。
* 修复了一些软件包声明的格式错误。
* 弃用了旧版设备安装器支持，该支持将于 RuyiSDK 0.35 移除。

RuyiSDK 服务端组件方面:

* 新增了官方软件源的新闻条目阅读 API。
* 新增了按版本号查询 RuyiSDK 版本发行注记的 API。
* 将官方软件源当前目录结构下的所有子目录都纳入了下载量统计范围。
* 改进了服务容器的构建方式。

欢迎试用或来上游围观；您的需求是我们迭代开发的目标和动力。您也可以亲自参与
RuyiSDK 软件的打包与分发工作：目前您可以直接在 GitHub 上查看、修改我们的[部分打包脚本](https://github.com/ruyisdk/ruyici)与[软件源仓库](https://github.com/ruyisdk/packages-index)。今后，按照本年度的开发计划，我们也将支持有权的第三方贡献者通过程序化的方式上传软件包、系统镜像等分发文件，以便利打包工作。

## V8 / Chromium

Chromium:

- [sysroot_creator: add riscv64 support](https://chromium-review.googlesource.com/c/chromium/src/+/6574317)
- [reversion_glibc: add riscv64 support](https://chromium-review.googlesource.com/c/chromium/src/+/6574441)
- [\[Sysroot\] Build and upload riscv64 sysroot](https://chromium-review.googlesource.com/c/chromium/src/+/6603953)
- [Add clang triple for riscv64 linux](https://chromium-review.googlesource.com/c/chromium/src/+/6585073)
- [cpuinfo: enable for riscv64 linux](https://chromium-review.googlesource.com/c/chromium/src/+/6597694)
- [xnnpack: enable riscv64 support](https://chromium-review.googlesource.com/c/chromium/src/+/6597834)
- [highway: add riscv RVV to BROKEN_TARGETS](https://chromium-review.googlesource.com/c/chromium/src/+/6583376)
- [Add riscv64 to GetCurrentCpuArchitecture](https://chromium-review.googlesource.com/c/chromium/src/+/6584974)

## Spidermonkey / Firefox

一般都是风平浪静。欢迎对 Firefox 开发感兴趣的同学来实习。

## OpenJDK

1. Authored/Co-authored JDK-mainline PRs:
- https://github.com/openjdk/jdk/pull/23739 (8342382: Implementation of JEP G1: Improve Application Throughput with a More Efficient Write-Barrier)
- https://github.com/openjdk/jdk/pull/24048 (8352011: RISC-V: Two IR tests fail after JDK-8351662)
- https://github.com/openjdk/jdk/pull/24123 (8352477: RISC-V: Print warnings when unsupported intrinsics are enabled)

2. Reviewed JDK-mainline PRs:
- https://github.com/openjdk/jdk/pull/25252 (8356159: RISC-V: Add Zabha)
- https://github.com/openjdk/jdk/pull/25253 (8357056: RISC-V: Asm fixes - load/store width)
- https://github.com/openjdk/jdk/pull/23030 (8347405: MergeStores with reverse bytes order value)
- https://github.com/openjdk/jdk/pull/23985 (8351662: [Test] RISC-V: enable bunch of IR test)
- https://github.com/openjdk/jdk/pull/23963 (8318220: RISC-V: C2 ReverseI)
- https://github.com/openjdk/jdk/pull/24096 (8320997: RISC-V: C2 ReverseV)
- https://github.com/openjdk/jdk/pull/24008 (8351861: RISC-V: add simple assert at arrays_equals_v)
- https://github.com/openjdk/jdk/pull/24015 (8351876: RISC-V: enable and fix some float round tests)
- https://github.com/openjdk/jdk/pull/24081 (8352159: RISC-V: add more zfa support)
- https://github.com/openjdk/jdk/pull/24094 (8352218: RISC-V: Zvfh requires RVV)
- https://github.com/openjdk/jdk/pull/24027 (8351902: RISC-V: Several tests fail after JDK-8351145)
- https://github.com/openjdk/jdk/pull/24119 (8352423: RISC-V: simplify DivI/L ModI/L)
- https://github.com/openjdk/jdk/pull/24138 (8352529: RISC-V: enable loopopts tests)
- https://github.com/openjdk/jdk/pull/24161 (8352597: [IR Framework] test bug: TestNotCompilable.java fails on product build)
- https://github.com/openjdk/jdk/pull/24157 (8352615: [Test] RISC-V: TestVectorizationMultiInvar.java fails on riscv64 without rvv support)
- https://github.com/openjdk/jdk/pull/24182 (8352673: RISC-V: Vector can't be turned on with -XX:+UseRVV)

## Go
1. Authored/Co-authored Go-mainline CLs:
- 647596: runtime: unify C -> Go ABI transitions on riscv64 | https://go-review.googlesource.com/c/go/+/647596
- all: add race support for riscv64 | https://github.com/mengzhuo/go/commit/a1b9b0d4faae07a31c599e00ee73aa6b4f882068 
https://github.com/golang/go/issues/64345
- 659175: cmd/link: generate proper attributes for riscv profile | https://go-review.googlesource.com/c/go/+/659175
- 657036: internal/bytealg: vector implementation of count 1 byte for riscv64 | https://go-review.googlesource.com/c/go/+/657036 
- 663778: cmd/asm, cmd/internal/obj: add zvbb/zvbc/zvkb for riscv64 | https://go-review.googlesource.com/c/go/+/663778
- 664155: cmd/asm, cmd/internal/obj: add crypto algorithm suites for riscv64 | https://go-review.googlesource.com/c/go/+/664155
- 664375: cpu: add crypto extensions detection for riscv64 | https://go-review.googlesource.com/c/sys/+/664375
- 663675: cmd/internal/obj: add crypto extension for riscv64 | https://go-review.googlesource.com/c/go/+/663675

2. Reviewed Go-mainline CLs:
- 652717: doc, cmd/internal/obj/riscv: document the riscv64 assembler | https://go-review.googlesource.com/c/go/+/652717 
- 646736: internal/bytealg: vector implementation of equal for riscv64 | https://go-review.googlesource.com/c/go/+/646736
- 646737: internal/bytealg: vector implementation of compare for riscv64 | https://go-review.googlesource.com/c/go/+/646737
- 670876: riscv64: add support for RVV 1.0 instructions | https://go-review.googlesource.com/c/arch/+/670876
- 670875: riscv64: fix the path to the RISC-V extensions in spec.go | https://go-review.googlesource.com/c/arch/+/670875

## OpenCV

## GNU Toolchain

GCC15.1.0已正式发布，包含RVV自动向量化特性，已同步更新GCC与Binutils至RUYISDK中
- https://github.com/ruyisdk/riscv-gcc/tree/15.1.0
- https://github.com/ruyisdk/riscv-binutils/tree/binutils-2.45

RISC-V Profiles RV20/22/23已合入上游
- https://patchwork.sourceware.org/project/gcc/patch/20250510123003.3901726-1-jiawei@iscas.ac.cn/
- https://patchwork.sourceware.org/project/gcc/patch/20250510123003.3901726-2-jiawei@iscas.ac.cn/
- https://patchwork.sourceware.org/project/binutils/patch/20250511133819.442839-1-jiawei@iscas.ac.cn/
- https://patchwork.sourceware.org/project/binutils/patch/20250511133819.442839-2-jiawei@iscas.ac.cn/

提交了Sha扩展支持，已合入上游
- https://patchwork.sourceware.org/project/gcc/patch/20250513035521.654554-1-jiawei@iscas.ac.cn/
- https://patchwork.sourceware.org/project/binutils/patch/20250508105005.3030397-1-jiawei@iscas.ac.cn/

提交了Shlcofideleg扩展支持,仍在review中
- https://patchwork.sourceware.org/project/gcc/patch/20250527073234.843408-1-jiawei@iscas.ac.cn/
- https://patchwork.sourceware.org/project/binutils/patch/20250527073242.843514-1-jiawei@iscas.ac.cn/

支持了priv-1.13特权寄存器规范
- https://patchwork.sourceware.org/project/binutils/patch/20250509022245.483271-1-jiawei@iscas.ac.cn/

优化了Bitmanip中指令组合，将 bclr+binv 结合为 bset 指令
- https://patchwork.sourceware.org/project/gcc/patch/20250528102325.3183637-1-jiawei@iscas.ac.cn/

与Rivosinc协作，支持了Smcdeleg与Ssccfg扩展
- https://patchwork.sourceware.org/project/binutils/patch/20250521130609.542862-1-jiawei@iscas.ac.cn/

向FFmpeg社区提交了建议开启-ftree-vectorize自动向量化的patch
- https://patchwork.ffmpeg.org/project/ffmpeg/patch/20250521061750.54882-1-jiawei@iscas.ac.cn/

更新了RISC-V ISA Manual草案中关于 Smcsrind/Sscsrind/Smcntrpmf扩展的寄存器描述
- https://github.com/riscv/riscv-isa-manual/pull/2044
- https://github.com/riscv/riscv-isa-manual/pull/2045

更新了RISC-V Toolchain conventions中Profiles的格式规范
- https://github.com/riscv-non-isa/riscv-toolchain-conventions/pull/36

添加了Pointer Masking扩展支持到gcc中
- https://patchwork.sourceware.org/project/gcc/patch/20250512091924.28368-1-chendongyan@isrc.iscas.ac.cn/

修复了回归测试中发现的一些错误
- https://patchwork.sourceware.org/project/gcc/patch/20250529015926.142801-1-shihua@iscas.ac.cn/
- https://patchwork.sourceware.org/project/gcc/patch/20250519071712.9952-1-chendongyan@isrc.iscas.ac.cn/
- https://patchwork.sourceware.org/project/gcc/patch/20250522031601.117067-1-chendongyan@isrc.iscas.ac.cn/

## LLVM Team
- upstream：
  - [RISCV]Add zihintpause LLVM/Clang intrinsic: [#139519] (https://github.com/llvm/llvm-project/pull/139519)
  - [InstCombine] Fix frexp(frexp(x)) -> frexp(x) fold [#138837](https://github.com/llvm/llvm-project/pull/138837) issue [#138819](https://github.com/llvm/llvm-project/issues/138819)
  - [RISCV] Add 2^N + 2^M expanding pattern for mul [#137954](https://github.com/llvm/llvm-project/pull/137954)
  - [CIR] Cleanup support for C functions [#136854](https://github.com/llvm/llvm-project/pull/136854) issue [#130200](https://github.com/llvm/llvm-project/issues/130200)
  - [RISCV][MC] Add support for Q extension [#139369](https://github.com/llvm/llvm-project/pull/139369) issue [#130217](https://github.com/llvm/llvm-project/issues/130217)
  - [RISCV][MC] Add Q support for Zfa [#139508](https://github.com/llvm/llvm-project/pull/139508)
  - [RISCV][Scheduler] Add scheduler definitions for the Q extension [#139495](https://github.com/llvm/llvm-project/pull/139495)
  - [RISCV] Expand constant multiplication for targets without M extension [#137195](https://github.com/llvm/llvm-project/pull/137195)
  - [RISCV][Scheduler] Add scheduling definitions for 128-bit Zfa instructions [#140003](https://github.com/llvm/llvm-project/pull/140003)
  - [RISCV][Scheduler] Split UnsupportedSchedZfa by other fp extensions [#140186](https://github.com/llvm/llvm-project/pull/140186)
  - [NFC][RISCV] Add more test cases for multiplication [#139195](https://github.com/llvm/llvm-project/pull/139195)
  - [NFC][RISCV] Pre-commit tests for RVI constant multiplication expansion [#139200](https://github.com/llvm/llvm-project/pull/139200)
  - [NFC] Cleanup dead code in LoadStoreVectorizer.cpp [#139211](https://github.com/llvm/llvm-project/pull/139211)
  - [mlir][NFC] Use llvm::sort [#140261](https://github.com/llvm/llvm-project/pull/140261)
  - [Flang][OpenMP] fix crash on sematic error in atomic capture clause [#140710](https://github.com/llvm/llvm-project/pull/140710)

- ruyisdk-llvm-project:
  - xtheadvector: [Clang][XTHeadVector] fix vector integer widening multiply intrinsics: https://github.com/ruyisdk/llvm-project/pull/154
  - xtheadvector: [Clang][XTHeadVector] fix vector integer divide intrinsics: https://github.com/ruyisdk/llvm-project/pull/155
  - xtheadvector: [Clang][XTHeadVector] fix vector single-width integer multiply-add intrinsics: https://github.com/ruyisdk/llvm-project/pull/156
  - xtheadvector: [Clang][XTHeadVector] fix vector widening integer multiply-add intrinsics: https://github.com/ruyisdk/llvm-project/pull/157

## MLIR

### Buddy Compiler

- Buddy Compiler 主页地址 - https://buddy-compiler.github.io/
- Buddy Compiler As A Service (Buddy CAAS) - https://buddy.isrc.ac.cn/
- Buddy Compiler 开源之夏 2025 正在报名阶段，欢迎申报 - https://summer-ospp.ac.cn/org/orgdetail/8d995d4c-b188-4690-9a53-c022dc7c19e3?lang=zh

**buddy-mlir**

- [midend] Add the vectorization pass for the batchmatmul_transpsoe_b operation.
- [examples] Update pass pipeline for Stable Diffusion example.
- [midend] Add batchmatmul vectorization pass.

## eBPF

- Merge GPU related code into bpftime [PR](https://github.com/eunomia-bpf/bpftime/pull/400)
- Add benchmark scripts and code for OSDI artifact evaluation [PR](https://github.com/eunomia-bpf/bpftime/pull/398) [PR](https://github.com/eunomia-bpf/bpftime/pull/399)  [PR](https://github.com/eunomia-bpf/bpftime/pull/391)  [PR](https://github.com/eunomia-bpf/bpftime/pull/390)
- Implement bpf_get_stackid [PR](https://github.com/eunomia-bpf/bpftime/pull/394)
- Add simple attach impl to provide simpler way to register some basic attach impls [PR](https://github.com/eunomia-bpf/bpftime/pull/393)
- Add a cuda tutorial [repo](https://github.com/eunomia-bpf/basic-cuda-tutorial)
- Add a cupti tutorial [repo](https://github.com/eunomia-bpf/cupti-tutorial)
  

## Box64

- ksco

  - [\[DYNAREC\] Fixed a prefix typo in dynarec dump](https://github.com/ptitSeb/box64/pull/2693)
  - [\[WOW64\] Improved RIP handling on INT n](https://github.com/ptitSeb/box64/pull/2692)
  - [\[DYNAREC\] Ported 37ed49cb to RV64 and LA64](https://github.com/ptitSeb/box64/pull/2690)
  - [\[WOW64\] Print banner at startup](https://github.com/ptitSeb/box64/pull/2685)
  - [\[WOW64\] Added support for cosim](https://github.com/ptitSeb/box64/pull/2683)
  - [\[WOW64\] Added more missing pieces and the interpreter works](https://github.com/ptitSeb/box64/pull/2682)
  - [\[WOW64\][ENV] Clean up a bit](https://github.com/ptitSeb/box64/pull/2681)
  - [\[ARM64_DYNAREC\] Small optim to modreg CMPXCHG](https://github.com/ptitSeb/box64/pull/2680)
  - [\[WOW64\] Supported logging to stdout](https://github.com/ptitSeb/box64/pull/2679)
  - [\[ARM64_DYNAREC\] Fixed a warning](https://github.com/ptitSeb/box64/pull/2678)
  - [\[DYNAREC\] Fixed expected return address in bridged native call](https://github.com/ptitSeb/box64/pull/2677)
  - [\[RV64_DYNAREC\] Fixed regression introduced in #2669](https://github.com/ptitSeb/box64/pull/2676)
  - [\[CMAKE\] Fixed dependency issues introduced recently](https://github.com/ptitSeb/box64/pull/2673)
  - [\[RV64_DYNAREC\] Removed useless zero-ups in some emit_* functions](https://github.com/ptitSeb/box64/pull/2672)
  - [\[RV64_DYNAREC\] Added more opcodes to printer](https://github.com/ptitSeb/box64/pull/2671)
  - [\[RV64_DYNAREC\] Improved ret_to_epilog with xtheadmemidx](https://github.com/ptitSeb/box64/pull/2670)
  - [\[RV64_DYNAREC\] Minor nativeflags optim to LEA and CMOVcc opcodes](https://github.com/ptitSeb/box64/pull/2669)
  - [\[RV64_DYNAREC\] Improved emit_pf with Zbb](https://github.com/ptitSeb/box64/pull/2665)
  - [\[RV64_DYNAREC\] Optimized CLZ macro with xtheadbb](https://github.com/ptitSeb/box64/pull/2664)
  - [\[RV64_DYNAREC\] Optimized some opcodes with xtheadbb](https://github.com/ptitSeb/box64/pull/2663)
  - [\[CMAKE\] Removed the hard dependency between dynarec and main executable to speed up build](https://github.com/ptitSeb/box64/pull/2662)
  - [Added -k option to kill all box64 instances](https://github.com/ptitSeb/box64/pull/2661)
  - [\[RV64_DYNAREC\] Enable nativeflags optimization for more patterns](https://github.com/ptitSeb/box64/pull/2659)
  - [\[RV64_DYNAREC\] Fixed a typo in 66 F0 0F LOCK CMPXCHG opcode](https://github.com/ptitSeb/box64/pull/2658)
  - [Reprint env configs when special libraries detected](https://github.com/ptitSeb/box64/pull/2657)
  - [\[RV64_DYNAREC\] Implemented unaligned path for LOCK INC/DEC opcodes](https://github.com/ptitSeb/box64/pull/2656)
  - [\[DYNAREC\] Removed unnecessary volatile metadata barriers](https://github.com/ptitSeb/box64/pull/2653)
  - [\[RV64_DYNAREC\] Fixed more potential scratch register conflicts](https://github.com/ptitSeb/box64/pull/2652)
  - [\[RV64_DYNAREC\] Improved POPCNT and fixed some scratch conflicts](https://github.com/ptitSeb/box64/pull/2651)
  - [\[RV64\] Improved vendor extension detection to avoid conflicts (for #2645)](https://github.com/ptitSeb/box64/pull/2648)
  - [\[RV64_DYNAREC\] Enabled native flags optimization for SETcc opcodes](https://github.com/ptitSeb/box64/pull/2640)
  - [\[RV64_DYNAREC\] Added F2 0F F0 LDDQU opcode for vector](https://github.com/ptitSeb/box64/pull/2639)
  - [\[DYNAREC\] Fixed alternate address testing when retrieving dynablock](https://github.com/ptitSeb/box64/pull/2638)
  - [\[RV64_DYNAREC\] Added more opcodes for vector](https://github.com/ptitSeb/box64/pull/2637)
  - [\[DYNAREC\] More minor changes to missing VEX prefixed opcodes](https://github.com/ptitSeb/box64/pull/2636)
  - [\[RV64_DYNAREC\] Added and optimized some SSE/MMX opcodes](https://github.com/ptitSeb/box64/pull/2635)
  - [\[RV64_DYNAREC\] Fixed a typo introduced lately](https://github.com/ptitSeb/box64/pull/2634)
  - [\[DOCS\] Align usage.json and env.h](https://github.com/ptitSeb/box64/pull/2633)
  - [\[RV64_DYNAREC\] Added more mmx opcodes](https://github.com/ptitSeb/box64/pull/2630)
  - [\[RV64_DYNAREC\] Added more mmx opcodes](https://github.com/ptitSeb/box64/pull/2629)
  - [\[RV64_DYNAREC\] Added more mmx opcodes](https://github.com/ptitSeb/box64/pull/2627)
  - [\[RV64_DYNAREC\] Added more mmx opcodes](https://github.com/ptitSeb/box64/pull/2626)
  - [\[CI\] Check WOW64 build in the CI](https://github.com/ptitSeb/box64/pull/2623)
  - [\[GDBJIT\] Added a new option to register debuginfo only after trapped into signalhandler](https://github.com/ptitSeb/box64/pull/2614)
  - [\[ENV\] Refactored file-mapping handling](https://github.com/ptitSeb/box64/pull/2612)
  - [\[DYNAREC\] Use PE volatile metadata in dynarec](https://github.com/ptitSeb/box64/pull/2610)
  - [Added a simple PE loaded dedicated for volatileMetadata](https://github.com/ptitSeb/box64/pull/2607)


## DynamoRIO

## coreboot for riscv

本期没有新的进展。

## openocd

本期没有新的进展。

## opensbi

 - 添加工具链的堆栈保护支持。[1](https://lists.infradead.org/pipermail/opensbi/2025-May/008429.html)
 - 为冻结的RPMI规格更新代码。[1](https://lists.infradead.org/pipermail/opensbi/2025-May/008440.html)
 - 在pmu代码中通过cbase/cmask标识counter，添加错误处理代码阻止cmask为0。[1](https://lists.infradead.org/pipermail/opensbi/2025-May/008448.html)
 - 禁止低特权等级对 CY/IR 的访问以避免侧信道攻击。[1](https://lists.infradead.org/pipermail/opensbi/2025-May/008450.html)
 - 在sbi_dbtr.c中优化saddr的mapping操作。[1](https://lists.infradead.org/pipermail/opensbi/2025-May/008454.html)
 - 添加编译选项移除绝对路径。[1](https://lists.infradead.org/pipermail/opensbi/2025-May/008458.html)
 - 修正dtbr共享内存的内存布局。[1](https://lists.infradead.org/pipermail/opensbi/2025-May/008535.html)
 - 把SSE callbacks的中断委托设置移动到register_cb/unregister_cb。[1](https://lists.infradead.org/pipermail/opensbi/2025-May/008469.html)
 - 改进设置menvcfg.pmm字段的方法，添加有效值的检测。[1](https://lists.infradead.org/pipermail/opensbi/2025-May/008517.html)
 - 修正sbi_hsm_hart_start的逻辑bug，opensbi通过两个计数器判断设备是在等待中断还是进掉电，在热启动路径上有一个hsm等待的操作为了节能可能进入了掉电模式，但两个计数器值不相同的情况，这会导致核心无法被唤醒。[1](https://lists.infradead.org/pipermail/opensbi/2025-May/008534.html)
 - 修正update_triggers,匹配最新的规格。[1](https://lists.infradead.org/pipermail/opensbi/2025-May/008546.html)

## u-boot

本期没有新的进展。

## RevyOS (Debian for Xuantie)

### Debian
本月在社区是配合 debci team 及 [reproduce-build team](https://reproduce.debian.net/riscv64/)
维护 riscv64 基础设施， 其中后者期望赶在 Trixie 发布之前完成对 riscv64 的 reproduced.

以下是外部可见links:

* https://salsa.debian.org/go-team/packages/opensnitch/-/merge_requests/5 [opensnith MR closed]
* https://tracker.debian.org/news/1643172/accepted-ananta-115-1-source-into-unstable/ [ananta upload]
* http://vimer.7766.org:63015/qt6-webengine/6-6-2/debs/ [qt6-webengine 6.6.2]
* https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=1104825 [mame ftbfs riscv64]
* https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=1104895 [ haskell-charsetdetect-ae support rv64]
* https://salsa.debian.org/debian/strace/-/merge_requests/22 [merged strace MR]
* https://www.eclipse.org/lists/epp-dev/msg06990.html [eclipse +1 test]
* https://salsa.debian.org/ci-team/debian-ci-config/-/merge_requests/32 [update nodes]
* https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=1105847 [piuparts flaky tests on rv64]
* https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=1105906 [valgrind support rv64 wishlist]
* https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=1106130 [python-tornado ftbfs on rv64]
* https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=1106292 [unblock upload]
* https://salsa.debian.org/ocaml-team/lem/-/tree/debian/master/debian?ref_type=heads [lem update]
* https://salsa.debian.org/vimerbf-guest/sail-ocaml/-/tree/debian/main?ref_type=heads [add lean backend]
* https://salsa.debian.org/vimerbf-guest/sail-riscv/-/tree/debian/main/debian?ref_type=heads [sail-riscv update]
* https://github.com/yuzibo/mkimg-xuantie/tree/rv-learning [Debian image for licheepi4A]


### RedleafOS
* 本月初步适配 [nanhu v3](https://mp.weixin.qq.com/s/qhduTnP23mxreoh8NId0UQ?poc_token=HK32P2ijilvv18PDrrAXI2pudmtBgpMTMaDneYdz).
* 更多优化及适配正在进行中.

### 桂香伟
### debian package patches
forgejo-cli:https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=1105023  
matrix-synapse:https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=1105140  
forgejo-cli: https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=1106150  
### upstream
synapse:https://github.com/element-hq/synapse/pull/18430

## RT-Thread

RTT upstream:

- [bsp: k230: add hwtimer support][rtt-10346]
- [bsp: k230: use utest asset api][rtt-10344]
- [Doxygen: move device/driver under to components][rtt-10336]
- [bsp: k230: add watchdog support][rtt-10331]
- [bsp: k230: fix kconfig warnings][rtt-10325]
- [bsp: k230: support sdio][rtt-10295]
- [bsp: k230: improve cleanup][rtt-10291]
- [bsp: k230: add flashsd script][rtt-10289]
- [bsp: k230: use sysctl to reboot the board][rtt-10288]
- [bsp: k230: add sysctl driver][rtt-10281]
- [MAINTAINERS: add myself as owner of bsp/cvitek & bsp/k230][rtt-10278]
- [bsp: k230: add hardlock driver][rtt-10277]
- [MAINTAINERS: add myself as owner of documentation][rtt-10272]
- [MAINTAINERS: sort entries with tag in alphabetical][rtt-10269]
- [bsp: k230: eliminate warnings for kconfig][rtt-10245]
- [[RFC] [utest] Add audio driver test framework][rtt-10243]

[rtt-10346]:https://github.com/RT-Thread/rt-thread/pull/10346
[rtt-10344]:https://github.com/RT-Thread/rt-thread/pull/10344
[rtt-10336]:https://github.com/RT-Thread/rt-thread/pull/10336
[rtt-10331]:https://github.com/RT-Thread/rt-thread/pull/10331
[rtt-10325]:https://github.com/RT-Thread/rt-thread/pull/10325
[rtt-10295]:https://github.com/RT-Thread/rt-thread/pull/10295
[rtt-10291]:https://github.com/RT-Thread/rt-thread/pull/10291
[rtt-10289]:https://github.com/RT-Thread/rt-thread/pull/10289
[rtt-10288]:https://github.com/RT-Thread/rt-thread/pull/10288
[rtt-10281]:https://github.com/RT-Thread/rt-thread/pull/10281
[rtt-10278]:https://github.com/RT-Thread/rt-thread/pull/10278
[rtt-10277]:https://github.com/RT-Thread/rt-thread/pull/10277
[rtt-10272]:https://github.com/RT-Thread/rt-thread/pull/10272
[rtt-10269]:https://github.com/RT-Thread/rt-thread/pull/10269
[rtt-10245]:https://github.com/RT-Thread/rt-thread/pull/10245
[rtt-10243]:https://github.com/RT-Thread/rt-thread/pull/10243

RTT Package Tool:

- [differ return code for sdcard][rttpkgtool-9]

[rttpkgtool-9]:https://github.com/plctlab/rttpkgtool/pull/9

## PLCT罗云翔测试团队

（包含 SAIL 和 ACT 测试部分）

1. 完成RuyiSDK v0.33多平台测试，产出测试报告
2. 操作系统支持矩阵新增了megrez RockOS支持，openCloudOS桌面首次进入操作系统支持矩阵
3. Sail-RISCV和编译工具链提交了等19个PR
4. 参加2025年RISC-V欧洲峰会，讲解入选的2篇海报和进行学术交流。
5. 参加2025年中国科学院软件研究所公众科学日活动，演示和互动PLCT在RISC-V编译工具链、操作系统和应用生态方面的贡献，展示物超过15个。

### 1. RuyiSDK

#### 1.1 RuyiSDK测试

- [RuyiSDK 测试策略和测试报告](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/README.md)

  - [RuyiSDK v0.33测试报告](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/README.md)
        
    - [LPi4A openEuler 23.09 测试报告](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_LicheePi4A_openEuler23.09_riscv64_测试结果.md)

    - [LPi4A openEuler 24.03 测试报告](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_LicheePi4A_openEuler24.03_riscv64_测试结果.md)

    - [LPi4A RevyOS 测试报告](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_LicheePi4A_RevyOS_riscv64_测试结果.md)
    
    - [RevyOS riscv64 测试结果](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_RevyOS_riscv64_测试结果.md)
    
    - [Archlinux riscv64 测试结果](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_Archlinux_riscv64_测试结果.md)
    
    - [Archlinux x86\_64 测试结果](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_Archlinux_x86_64_测试结果.md)
    
    - [Debian sid riscv64 测试结果](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_Debiansid_riscv64_测试结果.md)
    
    - [Deepin23 x86_64 测试报告](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_Deepin23_x86_64_测试结果.md)
    
    - [Deepin 23 riscv64 测试报告](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_Deepin23_riscv64_测试结果.md)
  
    - [Fedora39 x86\_64 测试报告](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_Fedora39_x86_64_测试结果.md)
    
    - [Fedora38 riscv64 测试结果](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_Fedora38_riscv64_测试结果.md)
    
    - [QEMU Ubuntu22.04 x86\_64 测试报告](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_Ubuntu22.04_x86_64_测试结果.md)
    
    - [Ubuntu22.04 riscv64 测试结果](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_QEMU_Ubuntu22.04_riscv64_测试结果.md)
    
    - [Ubuntu24.04 x86\_64 测试报告](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514//RUYI_包管理_Ubuntu24.04_x86_64_测试结果.md)
    
    - [Ubuntu24.04 riscv64 测试结果](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_Ubuntu24.04_riscv64_测试结果.md)
    
    - [openEuler23.09 riscv64 测试报告](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_openEuler23.09_riscv64_测试结果.md)
    
    - [openEuler23.09 x86\_64 测试结果](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_openEuler23.09_x86_64_测试结果.md)
    
    - [openEuler24.03 riscv64 测试报告](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_openEuler24.03_riscv64_测试结果.md)
    
    - [openEuler24.03 x86\_64 测试结果](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_openEuler24.03_x86_64_测试结果.md)
    
    - [Debian12 aarch64 测试结果](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_Debian12_aarch64_测试结果.md)
    
    - [Debian12 x86\_64 测试结果](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_Debian12_x86_64_测试结果.md)
    
    - [Gentoo Linux x86\_64 测试结果](https://gitee.com/yunxiangluo/ruyisdk-test/blob/master/20250514/RUYI_包管理_Gentoo_x86_64_测试结果.md)
  
    - 本版本新增 1 个 issue（已修复）：
      - [ruyi device provision 调用 fastboot 镜像刷写步骤异常 #297](https://github.com/ruyisdk/ruyi/issues/297)
      - Box64 WPS 无法运行，并提交issue：
      [#2650](https://github.com/ptitSeb/box64/issues/2650) 
    - 资源：
      - [本版本 litester 测试程序](https://github.com/weilinfox/ruyi-litester/tree/bbd4fb24b11802f1079c99680338daa1a09eb1dc)
      - [本版本自动化调度程序](https://github.com/weilinfox/ruyi-reimu/tree/ce05926b26fe13e6a5ce5d20897309a55a211108)
  
  - [ruyi 0.32.0 加入packages-index 到 support-matrix, upstream 的检查](https://gitee.com/weilinfox/ruyisdk-test/pulls/5)

  - RuyiSDK IDE v0.0.4 测试

    测试重点：

    1. 本地没有ruyi时：启动时自动检测并进入安装向导  
    2. 本地有ruyi，版本不是最新时，启动时自动进入更新向导（也是安装，但是界面信息不同）  
    3. ruyi配置项的测试

    上面三项均正常执行；

    [演示视频](https://github.com/Cyl18/plct_working/blob/7b4225bde47ee7191f2e42e63369bfef0770e471/month6/files/2025-05-16%2020-04-52.mp4)

    内容为：
    1. ide启动自动检测ruyi，并展示ruyi安装向导安装ruyi过程；
    2. 在ide中打开一个terminal窗口，执行ruyi install 安装工具链（milkv duo的）
    3. 导入Helloworld/demosum工程代码
    4. 配置工具链并编译
    5. 远程执行程序

#### 1.2 RuyiSDK 测试工具开发
- ruyi: 
  尝试为其添加 bash/zsh completion支持（仍在进行） [#301](https://github.com/ruyisdk/ruyi/pull/301)

- ruyi-packaging
  - [Add multithreading, current version check, Fix type mismatch in OpenEulerLpi4aChecker #13](https://github.com/ruyisdk/ruyi-packaging/pull/13)
  - [Update DB #14](https://github.com/ruyisdk/ruyi-packaging/pull/14)
  - [Implement gen\_report and update file structure #15](https://github.com/ruyisdk/ruyi-packaging/pull/15)
  - [Remove test flag #16](https://github.com/ruyisdk/ruyi-packaging/pull/16)
  - [Manually fix revyos version 20250323 of sipeed-lpi4a #73](https://github.com/ruyisdk/packages-index/pull/73)
  - [Bump RevyOS image to version 20250420 for LicheePi 4A #74](https://github.com/ruyisdk/packages-index/pull/74)
  - [Swap buildroot-sdk-milkv-{duo,duo256m} and buildroot-sdk-milkv-{duo,duo256m}-python v1.0.7 image #75](https://github.com/ruyisdk/packages-index/pull/75)
  - [Manually fix RevyOS version 20250123 and 20250323 for Milkv Meles #76](https://github.com/ruyisdk/packages-index/pull/76)
  - [board-image/revyos-milkv-meles: fix old version and add new versions #76](https://github.com/ruyisdk/packages-index/pull/76)
  - [board-image/buildroot-sdk-milkv-duos-sd: add image version Duo-V1.1.1, Duo-V1.1.2, v1.1.4 and fix v1.1.3, v2.0.0 #77](https://github.com/ruyisdk/packages-index/pull/77)
  - [board-image/buildroot-sdk-milkv-duos-sd: add upstream\_version metadata for old versions #78](https://github.com/ruyisdk/packages-index/pull/78)
  - [board-image/buildroot-sdk-milkv-duo: add some old image version and f… #79](https://github.com/ruyisdk/packages-index/pull/79)
  - [board-image/buildroot-sdk-milkv-duo256: add some old image version and fix new image version #80](https://github.com/ruyisdk/packages-index/pull/80)
  - [ruyi-packaging/#13](https://github.com/ruyisdk/ruyi-packaging/pull/13) 添加多线程检查, 当前版本检查, 修复 OpenEulerLpi4aChecker 中的类型不匹配
  - [ruyi-packaging/#14](https://github.com/ruyisdk/ruyi-packaging/pull/14) 更新 DB
  - [ruyi-packaging/#15](https://github.com/ruyisdk/ruyi-packaging/pull/15) 实现 gen_report 并更新文件结构
  - [ruyi-packaging/#16](https://github.com/ruyisdk/ruyi-packaging/pull/16) 移除 Test flag

- ruyi-litester
  - [ruyi-litester/#11](https://github.com/weilinfox/ruyi-litester/pull/11)修改到ruyi help的工作

  - [ruyi-litester/#10](https://github.com/weilinfox/ruyi-litester/pull/10)完善对ruyi list/ruyi admin/ruyi install三个命令的子命令的测试

#### 1.3 RuyiSDK网站

- [pages: add github releases download to total download #117](https://github.com/ruyisdk/ruyisdk-website/pull/117)

- [pages: fetch ruyi download link with ruyi backend api #118](https://github.com/ruyisdk/ruyisdk-website/pull/118)

- [pages: fix download page ReleaseProvider context #119](https://github.com/ruyisdk/ruyisdk-website/pull/119)

- [pages: update i18n ruyi download page with ruyi backend api #121](https://github.com/ruyisdk/ruyisdk-website/pull/121)

- [pages: use blured slide news background #123](https://github.com/ruyisdk/ruyisdk-website/pull/123)

- [docs: fetch ruyi download link with ruyi backend api #125](https://github.com/ruyisdk/ruyisdk-website/pull/125)

- [pages: remove meetup page #131](https://github.com/ruyisdk/ruyisdk-website/pull/131)

- [pages: fix news show link #132](https://github.com/ruyisdk/ruyisdk-website/pull/132)

- [pages: add open internship to footer #136](https://github.com/ruyisdk/ruyisdk-website/pull/136)

- [docs: fetch ruyi download link in translations and update contents #126](https://github.com/ruyisdk/ruyisdk-website/pull/126)

- [Updated homepage with new content #128](https://github.com/ruyisdk/ruyisdk-website/pull/128)

- [beautify homepage & add demoboardpages & fix some statistic pages bugs #115](https://github.com/ruyisdk/ruyisdk-website/pull/115)

- [docs: update English version #120](https://github.com/ruyisdk/ruyisdk-website/pull/120)

- [docs: update English version #122](https://github.com/ruyisdk/ruyisdk-website/pull/122)

- ruyisdk-website 关闭 8 个 issue
    - [需要找到专人检查维护 俄语 页面，否则需要隐藏起来更新不及时的俄语页面 #24](https://github.com/ruyisdk/ruyisdk-website/issues/24)
    - [需要找到专人检查维护 日语 页面，否则需要隐藏起来更新不及时的俄语页面 #25](https://github.com/ruyisdk/ruyisdk-website/issues/25)
    - [移动端网页适配 #64](https://github.com/ruyisdk/ruyisdk-website/issues/64)
    - [[BUG] 部分设备点击数据统计按钮会无反应 #65](https://github.com/ruyisdk/ruyisdk-website/issues/65)
    - [[需求] 更新页面内容 #72](https://github.com/ruyisdk/ruyisdk-website/issues/72)
    - [[需求] 更新页面布局 #73](https://github.com/ruyisdk/ruyisdk-website/issues/73)
    - [[优化] 移动端 数据统计页面 #109](https://github.com/ruyisdk/ruyisdk-website/issues/109)
    - [Ruyi包管理器-安装部分 跨域访问导致报错 #130](https://github.com/ruyisdk/ruyisdk-website/issues/130)

- ruyisdk-website 新开 1 个 issue
    - [官网多语言支持情况 #134](https://github.com/ruyisdk/ruyisdk-website/issues/134)

- [Design and implement the new Homepage](https://github.com/ruyisdk/ruyisdk-website/pull/128)

  - Initial version of new homepage
  - New component MainDisplay for visual attraction and animated ruyi operations
  - New component RuyiInLive for community link and stats
  - New NewsShowcase for display Ruyi News

- [Pull #138](https://github.com/ruyisdk/ruyisdk-website/pull/138)
  - Updated native RuyiInLive chart for better scrolling handling and performance
  - RuyiInLive chart with better visuals(bolder bars, in-bar commands, no digits)
  - Unified Button animation
  - Relative sizing for MainDisplay, RuyiInLive and SlideNews, use `rem` instead
  - New Social account link for mobile visitors
  - Add translation & Minor improvements
 
#### 1.4 RuyiSDK文档

- wechat-articles 
    - [Add update of ruyisdk.org #152](https://github.com/ruyisdk/wechat-articles/pull/152)

- docs 
    - [Updates to installation.md and packages.md #83](https://github.com/ruyisdk/docs/pull/83)

#### 1.5 RuyiSDK技术分享

- 参加 RISC-V 欧洲峰会，提供现场照片，记录展品内容，张贴和介绍海报
- [RISC-V 欧洲峰会微信文章](https://mp.weixin.qq.com/s/wx7IwcPNIkk_u_J5LT3j4A)
- [RISC-V 欧洲峰会微信文章](https://mp.weixin.qq.com/s/hUnChz2EH5qzvVxTRHw-HQ)
- [欧洲峰会见闻](https://gitlab.inuyasha.love/weilinfox/plct-working/-/blob/master/Done/Month23/欧洲峰会见闻.docx)
- [2025年RISC-V欧洲峰会游记](https://gitlab.inuyasha.love/weilinfox/plct-working/-/blob/master/Done/Month23/2025年RISC-V欧洲峰会游记.docx)
- 第 102 次东亚时区双周会，补充和参会介绍“RISC-V 德语社区的同步与八卦”部分
- RISC-V Infra 分享[欧洲峰会见闻](https://gitlab.inuyasha.love/weilinfox/plct-working/-/blob/master/Done/Month23/欧洲峰会见闻.pptx)
- 玄铁课程介绍录音 [Intro 内容](https://gitlab.inuyasha.love/weilinfox/plct-working/-/blob/master/Done/Month23/Intro.md)
- 协助完成 5 月 23 日的 RuyiSDK Office Hours 演示准备
  
#### 1.6 实习生考核

- 新实习生面试考核 [Marco 面试考核](https://gitlab.inuyasha.love/weilinfox/plct-working/-/blob/master/Done/Month23/Macro.md)
- 新实习生面试 [Marco 面试](https://gitlab.inuyasha.love/weilinfox/plct-working/-/blob/master/Done/Month23/Macro-update.md)
  
### 2. 操作系统支持矩阵

#### 2.1 开发板操作系统支持测试
- [Star64/Ubuntu: fix typo](https://github.com/ruyisdk/support-matrix/pull/285)
- [Duo/Alpine: Bump to 3.21.3](https://github.com/ruyisdk/support-matrix/pull/286)
- [Megrez/RockOS: Bump to 20250423](https://github.com/ruyisdk/support-matrix/pull/287)
- [Pioneer/openCloudOS: Bump to main repo version](https://github.com/ruyisdk/support-matrix/pull/289)
- [LicheePi4A8+32G: Add Arch Linux](https://github.com/ruyisdk/support-matrix/pull/290)
- [Add ArchLinux test reports for Mars.](https://github.com/ruyisdk/support-matrix/pull/291)
- [Meles/RevyOS: Bump to 20250420](https://github.com/ruyisdk/support-matrix/pull/292)
- [Add Pine64 Ox64](https://github.com/ruyisdk/support-matrix/pull/293)
- [Update RV-STAR](https://github.com/ruyisdk/support-matrix/pull/294)
- [Add new Board HengShanPi and it's RT-Thread test report.](https://github.com/ruyisdk/support-matrix/pull/295)
- [Add Alpine test report for Mars and fix typos.](https://github.com/ruyisdk/support-matrix/pull/296)
- [Update Ubuntu 24.04.02 test report for Nezha.](https://github.com/ruyisdk/support-matrix/pull/297)
- [Update: ESP32C2, ESP32H2, ESP32C6 test reports](https://github.com/ruyisdk/support-matrix/pull/298)
- [LicheeRV_Dock: update ubuntu to 25.04](https://github.com/ruyisdk/support-matrix/pull/299)
- [Metadata: fix wrong sys metadata](https://github.com/ruyisdk/support-matrix/pull/300)
- [LiP4A_8_32: Add NixOS and Slackware](https://github.com/ruyisdk/support-matrix/pull/301)
- [MusePi Pro: Init board and add systems](https://github.com/ruyisdk/support-matrix/pull/303)
- [Add new board OrangePi RV with OpenWRT and Ubuntu LTS test report and…](https://github.com/ruyisdk/support-matrix/pull/304)
- [Metadata: Add cpu_arch, fill-in all vendor and board_variant](https://github.com/ruyisdk/support-matrix/pull/305)
- [Mars: add Armbian and DietPi test report; Fix some typos.](https://github.com/ruyisdk/support-matrix/pull/306)
- [Add Premier P550 & Megrez test report on Deepin](https://github.com/ruyisdk/support-matrix/pull/309)
- [DuoS: dump Debian to 1.6.23](https://github.com/ruyisdk/support-matrix/pull/310)
- [Duo 256M: update Debian 13.0 test report and fix some typos.](https://github.com/ruyisdk/support-matrix/pull/311)
- [megrez: RockOS: update to 20250423](https://github.com/ruyisdk/support-matrix/pull/288)（完成实际启动测试部分）
- [Pioneer/OpenCloudOS: Add desktop](https://github.com/ruyisdk/support-matrix/pull/302)（完成实际启动测试部分）
- Meles/Revyos：更新至最新版 [#292](https://github.com/ruyisdk/support-matrix/pull/292)
- Pioneer/openCloudOS: 更新桌面结果 [#302](https://github.com/ruyisdk/support-matrix/pull/302)
- Muse Pi Pro: 新增板子 [#303](https://github.com/ruyisdk/support-matrix/pull/303)
  - 系统： Bianbu
  - 系统：openEuler
- 为所有板子添加了 vendor board_variant 和 cpu_arch三个字段 [#305](https://github.com/ruyisdk/support-matrix/pull/305)
  - 收集目前所有板子的微架构和对应的march
- [Add Pine64 Ox64](https://github.com/ruyisdk/support-matrix/pull/293)
- [Update RV-STAR](https://github.com/ruyisdk/support-matrix/pull/294)
- [Update Pine64 Oz64/Star64/Pinecone](https://github.com/ruyisdk/support-matrix/pull/307)
- LiP4A8+32
  - Nix & Slackware & ArchLinux
  - https://github.com/ruyisdk/support-matrix/pull/290
  - https://github.com/ruyisdk/support-matrix/pull/301
- DuoS
  - FreeRTOS + Debian
  - https://github.com/ruyisdk/support-matrix/pull/283
  - https://github.com/ruyisdk/support-matrix/pull/310
- [Add ESP32C6 ESP32C6 ESP32H2 test report.](https://github.com/ruyisdk/support-matrix/pull/298)
- [update NeZha D1H gcc 14.2 gcc upstream report.](https://github.com/QA-Team-lo/ruyisdk-gnu-tests/pull/7)
- [Update ESP32P4 test report and fix metadata errors #312.](https://github.com/ruyisdk/support-matrix/pull/312)
- [Update ESP32P4 test report and fix metadata errors #312.](https://github.com/ruyisdk/support-matrix/pull/312)
- [Metadata: fix wrong sys metadata](https://github.com/ruyisdk/support-matrix/pull/300) : 修复支持矩阵部分测试报告无法跳转
- [LicheeRV_Dock: update ubuntu to 25.04](https://github.com/ruyisdk/support-matrix/pull/299) : 测试并更新 LicheeRV Dock @ Ubuntu 25.04 
- [291](https://github.com/ruyisdk/support-matrix/pull/291)
  - Add ArchLinux test reports for Mars.
- [295](https://github.com/ruyisdk/support-matrix/pull/295)
  - Add new Board HengShanPi.
  - Add RT-Thread test report for HengShanPi.
- [296](https://github.com/ruyisdk/support-matrix/pull/296)
  - Add Alpine test report for Mars.
  - Fix some typos.
- [297](https://github.com/ruyisdk/support-matrix/pull/297)
  - Update Ubuntu 24.04.02 test report for Nezha.
- [304](https://github.com/ruyisdk/support-matrix/pull/304)
  - Add new board OrangePi RV2.
  - Add OpenWRT test report for OrangePi RV2.
  - Add Ubuntu LTS test report for OrangePi RV2.
  - Fix some typos.
- [306](https://github.com/ruyisdk/support-matrix/pull/306)
  - Add Armbian test report for Mars.
  - Add DietPi test report for Mars.
  - Fix some typos.
- [313](https://github.com/ruyisdk/support-matrix/pull/313)
  - Add irradium test report for Maes.
  - Add openKylin test report for Mars.
  - Add openSUSE test reports for Mars.
- [314](https://github.com/ruyisdk/support-matrix/pull/314)
  - Add irradium test report for OrangePi RV2.
- [315](https://github.com/ruyisdk/support-matrix/pull/314)
  - Add irradium test report for LicheePi 4A (CFT).
  
#### 2.2 操作系统支持矩阵Web UI

- [x] BUG: matrix 部分测试报告无法跳转
- [x] matrix: 不同系统比较(去掉其他行/列)
- [x] matrix: 首列背景色
- [x] matrix: 不同系统比较(添加去掉重复选项)
- [x] matrix: 比较仅限示表内有数据的开发板
- [x] 外部需求: 首页: 搜索栏搜索操作系统
- [x] matrix: 支持状态解释
  
#### 2.3 操作系统支持矩阵测试开发

- lintestor 重构、实现模板测试系统

- 支持基于模板直出报告和 summary.md 总结报告、有断言、变量、引用能力

  - [feat: Implement template reference system for test templates](https://github.com/255doesnotexist/lintestor/commit/79d9bb0)
  - [feat: enhance template parser to support multiple assertions and improve attribute extraction](https://github.com/255doesnotexist/lintestor/commit/5754828)

- lintstor 实现测试步骤断言能力

  - [feat: Enhance assertion types and parser functionality](https://github.com/255doesnotexist/lintestor/commit/9bc36d6)
  - [feat: enhance template parsing with detailed logging and error handling](https://github.com/255doesnotexist/lintestor/commit/47688b6)
  - [fix: update test reports with correct execution timestamps and enhance variable extraction patterns](https://github.com/255doesnotexist/lintestor/commit/01783c)

- lintestor 模板变量系统 PoC

  - [feat: update test reports with new execution timestamps and output formatting](https://github.com/255doesnotexist/lintestor/commit/2032daf)

- 测试用模板新增

  - [feat: add comprehensive test reports and enhance report aggregation logic](https://github.com/255doesnotexist/lintestor/commit/dd2e969)

- CLI 参数重构到 cli_args.rs 中

  - [feat(v0.2.0): Enhance CLI argument handling and add report aggregation features](https://github.com/255doesnotexist/lintestor/commit/7254553)

- 大量关于新模板机制的解析和适配代码

  - [refactor: bunch of new templates adapts](https://github.com/255doesnotexist/lintestor/commit/526d9fb)

- 重构测试脚本管理器，为管理测试模板准备

  - [Refactor test script management to use templates](https://github.com/255doesnotexist/lintestor/commit/e7fb624)

- 利用重写的 TestExecutor 封装统一了测试行为

  - [feat: Implement unified test execution logic with TestExecutor](https://github.com/255doesnotexist/lintestor/commit/551603c)

- 将 lintestor 原本的比较局限限定的 [发行版, 包] 对应测试概念改为 [测试目标, 测试单元] 概念，保持兼容性但应用范围更广

  - [refactor: distro -> target, package -> unit](https://github.com/255doesnotexist/lintestor/commit/9fe79d8)

- lintestor 现已支持在 BPI-F3 (K1) 上的 ruyisdk-gnu-toolchain 的自动化测试，可以实现全自动直出报告（[测试模板](https://github.com/255doesnotexist/lintestor/blob/ruyisdk-gnu-tests/devices/k1/gnu-upstream/README.test.md) | [测试报告](https://github.com/255doesnotexist/lintestor/blob/ruyisdk-gnu-tests/reports/readme_k1.toml.report.md)）

- lintestor 实现原生串口测试能力，不再依赖 boardtest（并允许超时时长配置以人类友好方式书写）

  * [feat: serial testing_type prototype, and timeout now support humanserde format (Ns...)](https://github.com/255doesnotexist/lintestor/commit/9550de5)

- 跨模板变量引用修复

  - [chore: fix reference template tests](https://github.com/255doesnotexist/lintestor/commit/6d3b155)

  - [feat: add metadata.custom_fields to the input](https://github.com/255doesnotexist/lintestor/commit/8bfddff)

- 现在模板支持引用标准输入输出的 summary 变量，而不是输出全文

  - [feat: support (stdout/stderr)_summary variables](https://github.com/255doesnotexist/lintestor/commit/7061221)
  - [Merge remote-tracking branch 'refs/remotes/origin/ruyisdk-gnu-tests' into ruyisdk-gnu-tests](https://github.com/255doesnotexist/lintestor/commit/cc1d868)

- 模板代码块在最终渲染后的报告中不再展示 attributes

  - [feat: remove attr strs in rendered CodeBlocks](https://github.com/255doesnotexist/lintestor/commit/c150916)

- 标题块因有独特隐式划分依赖层级作用，从文本块中单独提出自成一个内容块类型

  - [feat: split heading block from text block, and appends more infos](https://github.com/255doesnotexist/lintestor/commit/8af4e18)

- 自动机解析模板变量时如果变量名中有换行符则不认为是一个有效的变量标识符

  - [fix: ignore variable if the inner id got \n or \r exists](https://github.com/255doesnotexist/lintestor/commit/032c7f6)

  - [feat: metadata vars name change, replace unit_version in tests](https://github.com/255doesnotexist/lintestor/commit/c2524f6)
  - [feat: replace unit_version_command with static unit_version (indicates the test template unit version)](https://github.com/255doesnotexist/lintestor/commit/6611ce0)

- 自动机解析 attributes 时支持解析列表

  - [feat: allow ListValue when parsing attributes string in fsm](https://github.com/255doesnotexist/lintestor/commit/a04b728)

  - [feat: implement step status.execution/assertion variable](https://github.com/255doesnotexist/lintestor/commit/f3b5f1f)

- 引用当前模板变量时，允许忽略当前模板名

  - [feat: support auto completion for abbv first::second -> current_template_id::first::second](https://github.com/255doesnotexist/lintestor/commit/e84d87d)

- 使得父内容块隐式依赖子模板内容块

  - [feat: make parent blocks implicitly depends_on child blocks](https://github.com/255doesnotexist/lintestor/commit/2328cb8)

- 重写 attributes 解析器，使用手搓的自动机

  - [feat: propose a simple fsm for parsing attr strings, remove old 0.1.6 based intergration tests](https://github.com/255doesnotexist/lintestor/commit/13c02cd)

- 解析 attributes 时采用更鲁棒的正则表达式，但是正则表达式无法严格匹配提取正则表达式自己，后弃用这种解析方式

  - [fix: take more robust regex for attr matching, which fix assertion extracting](https://github.com/255doesnotexist/lintestor/commit/d79b93b)

- 确认测试步输出块可在 k1 上正常渲染测试结果

  - [chore: just to confirm output block are ok on k1 testing](https://github.com/255doesnotexist/lintestor/commit/73e65be)

- 在最终输出报告中清理一些块的 attributes

  - [fix: clean markdown markup robustly](https://github.com/255doesnotexist/lintestor/commit/54ea658)

- 修复一些变量唯一标识符不匹配的问题

  - [feat: enhance summary and result ID handling (fixes the issue that sometimes output block cannot found the result it refers to)](https://github.com/255doesnotexist/lintestor/commit/0f0e3e9)

- 重构与代码清理

  - [refactor: Clean up unused code and improve variable management in multiple modules](https://github.com/255doesnotexist/lintestor/commit/7c29c6b)

- 变量管理器支持处理命名空间（跨模板引用）

  - [feat: Enhance VariableManager with namespace handling and template ID registration](https://github.com/255doesnotexist/lintestor/commit/7523daa)
  - [refactor: Clean up code structure and improve variable management in template processing](https://github.com/255doesnotexist/lintestor/commit/b096fa1)

- 修改 metadata 中引用模板的写法

  - [fix: metadata reference/as not match with path/namespace](https://github.com/255doesnotexist/lintestor/commit/c646656)

- 实现基于测试步的测试批运行器，以及大量原有代码重构

  - [refactor: Implement Step-based batch executor, and bunch of other improvements](https://github.com/255doesnotexist/lintestor/commit/f69d7de)

- [lintestor code review](https://github.com/255doesnotexist/lintestor/pull/96)重构和代码优化工作：

- [refactor: remove obsolete code and re-enable integration test](https://github.com/255doesnotexist/lintestor/pull/96/commits/72b11e546cae412adda52c9ad445ffbc1b9d31b2)

- [refactor: remove obsolete code and unused imports](https://github.com/255doesnotexist/lintestor/pull/96/commits/ad89ca0d090736899ab51ca86442a86078bc95e0)

- [refactor: remove unused summary and aggregation](https://github.com/255doesnotexist/lintestor/pull/96/commits/14fa0f8277c1fe179f2a3084a954aa429bfb3f25)

- [refactor: fill in error handling for template functions](https://github.com/255doesnotexist/lintestor/pull/96/commits/f49211133ce457539bd97c9ce99982be392ec7e6)

- [refactor: remove useless functions](https://github.com/255doesnotexist/lintestor/pull/96/commits/75b17b464d70dd20455edffc7fb02c6808473dd6)

- [refactor: make clippy happy](https://github.com/255doesnotexist/lintestor/pull/96/commits/818c17ebeed0a85fa143ddf7e431f3822f0f41ae)

- [refactor(connection/ssh): use Default for param initialization](https://github.com/255doesnotexist/lintestor/pull/96/commits/ef05b23d76333122be013f380503da52de5e3e80)

- [feat: remove newline in stdout/err summary](https://github.com/255doesnotexist/lintestor/commit/3d032e8)

- [chore: update more complex k1 report](https://github.com/255doesnotexist/lintestor/commit/293e3f5)

- [fix: output block re should match whole block](https://github.com/255doesnotexist/lintestor/commit/7896d9e)

- [feat: when continue_on_error set, we get a pause](https://github.com/255doesnotexist/lintestor/commit/5d34d6c)

- [feat: now extraction will try to extract variable from both (stdout/stderr)](https://github.com/255doesnotexist/lintestor/commit/f356632)
- [feat: add connection pool to reduce remote connection overhead](https://github.com/255doesnotexist/lintestor/commit/d782bfb)
- [feat: early tell user ghost deps](https://github.com/255doesnotexist/lintestor/commit/b95bdca)
- [feat: make output support stream attr](https://github.com/255doesnotexist/lintestor/commit/44242f5)
- [feat: output block re expansion](https://github.com/255doesnotexist/lintestor/commit/c66adb3)
- [feat: add stream attr for OutputBlock, could be 'stdout' / 'stderr' / 'both'](https://github.com/255doesnotexist/lintestor/commit/3749f4f)
- [feat: add metadata.target_description variable](https://github.com/255doesnotexist/lintestor/commit/428017f)
- [feat: add name, description parsing at TargetConfig, and TemplateMetadata now got TargetConfig instead of PathBuf](https://github.com/255doesnotexist/lintestor/commit/ec7188e)
- [feat: allow overwrite previous var value](https://github.com/255doesnotexist/lintestor/commit/81535a1)

- ruyisdk-gnu-tests 分支更新与优化
  - [chore: add k1 plct tests for test](https://github.com/255doesnotexist/lintestor/commit/3787fcc)

- ruyisdk-gnu-tests/lintestor-templates 分支加了更 fancy 一点的模板
  - [feat: K1 initial version lintestor-templates](https://github.com/QA-Team-Io/ruyisdk-gnu-tests/commit/40beaf2)

#### 2.4 会议和技术分享
- https://github.com/ruyisdk/wechat-articles/pull/149
- https://github.com/ruyisdk/wechat-articles/pull/156

#### 2.5 操作系统支持矩阵设备维护

- 内部 Infra 日常维护
    - 电源更换
    - 上架 K230，为 https://github.com/ruyisdk/ruyisdk/issues/2 做准备
    - https://radiata.kevinmx.top   
  - 
- 其它线下事务处理
  
#### 2.6 实习生考核

- 甲辰计划联合招聘

### 3. SAIL和ACT

#### 3.1 SAIL和ACT开发

- SAIL/ACT
  - [PR](https://github.com/riscv/sail-riscv/pull/930) Fix build failure due to plat_enable_htif signature mismatch
  - [PR](https://github.com/riscv/sail-riscv/pull/970) Fix printf in first party test
  - [PR](https://github.com/rems-project/sail/pull/1312) Add --sail_config flag for sail compiler
  - [PR](https://github.com/rems-project/sail/pull/1313) Enhance AST printing for better debugging
  - [PR](https://github.com/rems-project/sail/pull/1314) Enhance fmt for Index
  - [PR](https://github.com/rems-project/sail/pull/1325) Add test case for mapping
  - [#904](https://github.com/riscv/sail-riscv/pull/904) : 适配Sail-RISCV Zicsr扩展为可配置
  - [#752](https://github.com/riscv/sail-riscv/pull/752) : 为Sail-RISCV 添加Zvkned扩展，并添加可配置选项
  - [#807](https://github.com/riscv/sail-riscv/pull/807) : 为Sail-RISCV 的stap支持的虚拟内存模式添加可配置选项
  - [#956](https://github.com/riscv/sail-riscv/pull/956) : 为Sail-RISCV 添加smcsrind/sscsrind扩展
  - [#990](https://github.com/riscv/sail-riscv/pull/990) : 解决Sail-RISCV Issue 提出regidx 的优化问题
  - [#792](https://github.com/riscv/sail-riscv/pull/792) : 推进PR 并完成Issue中新需求
  - [重构CI](https://github.com/riscv/sail-riscv/pull/876)
  - [Linux](https://github.com/riscv/sail-riscv/pull/889#issuecomment-2906609771)
  - [openSBI](https://github.com/riscv/sail-riscv/pull/966)
  - 更新了为ACT添加缺失的RV32 Zdinx共117个测试用例[#642](https://github.com/riscv-non-isa/riscv-arch-test/pull/642)并成功合并
  - 更新了为ACT添加缺失的RV32 Zfinx的一些新测试用例[#642](https://github.com/riscv-non-isa/riscv-arch-test/pull/642)

    | 测试用例名 | 所属拓展 | 添加测试用例数 | 地址                                                         |
    | ---------- | -------- | -------------- | ------------------------------------------------------------ |
    | fmadd-b11  | zfinx    | 13             | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fmsub-b11  | zfinx    | 13             | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fnmadd-b11 | zfinx    | 13             | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fnmsub-b11 | zfinx    | 13             | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fmadd-b1   | zfh      | 18             | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fmsub-b1   | zfh      | 18             | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fnmadd-b1  | zfh      | 18             | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fnmsub-b1  | zfh      | 18             | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |

  - 提交了一个修复rv 32 Zdinx测试错误的bug的pr[#651](https://github.com/riscv-non-isa/riscv-arch-test/pull/651)
  - 为ACT添加缺失的rv64 Zdinx fmadd.d/fmsub.d共330个测试用例[#654](https://github.com/riscv-non-isa/riscv-arch-test/pull/654)

    | 测试指令名 | 所属拓展 | 测试用例数 | 地址                                                         |
    | ---------- | -------- | ---------- | ------------------------------------------------------------ |
    | fadd.d     | Zdinx    | 11         | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fclass.d   | Zdinx    | 1          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fdiv.d     | Zdinx    | 11         | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | feq.d      | Zdinx    | 2          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fle.d      | Zdinx    | 2          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | flt.d      | Zdinx    | 2          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fmadd.d    | Zdinx    | 62         | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fmax.d     | Zdinx    | 2          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fmin.d     | Zdinx    | 2          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fmsub.d    | Zdinx    | 62         | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fmul.d     | Zdinx    | 9          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fnmadd.d   | Zdinx    | 62         | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fnmsub.d   | Zdinx    | 62         | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fsgnj.d    | Zdinx    | 1          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fsgnjn.d   | Zdinx    | 1          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fsgnjx.d   | Zdinx    | 1          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fsqrt.d    | Zdinx    | 10         | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
    | fsub.d     | Zdinx    | 12         | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
- Toolchain
  - [升级到 gdb16.3](https://github.com/riscv-collab/riscv-gnu-toolchain/commit/56f96d1d4bb07de62dd6d54393899cb1fe078b20)
  - [升级到 qemu10](https://github.com/riscv-collab/riscv-gnu-toolchain/commit/23863c2ca74e6c050f0c97e7af61f5f1776aadd1)
  - [升级到 gcc15.1](https://github.com/riscv-collab/riscv-gnu-toolchain/commit/3eafd26d0b8c1898b45c3557f3e127b06b1e32e8)
  - [重新计算白名单](https://github.com/riscv-collab/riscv-gnu-toolchain/commit/84c30862e7a5d3d4914aaaea74117adf4abd7247)


- Issues
  - [ISSUE](https://github.com/rems-project/sail/issues/1323)Could not resolve quantifiers for newtype
  - 帮助 ACT 社区 Zalasr PR 作者调试问题 <https://lists.riscv.org/g/sig-arch-test/message/757> Help with creating ACT for Zalasr
  - [#849](https://github.com/riscv/sail-riscv/issues/849) : 解决Sail-RISCV Zicsr 未能适配可自由配置的情况
  - [#796](https://github.com/riscv/sail-riscv/issues/796) : 解决Sail-RISCV stap 在可能不支持对应的虚拟内存模式下仍无条件写入的缺陷
  
#### 3.2 SAIL技术分享
  
- [sail code gen](https://github.com/rez5427/plct/blob/main/Report/sailcodegen.pptx)

#### 3.3 SAIL会议

- tech-golden-model meeting [`05.05`, `05.12`, `05.19`](https://docs.google.com/document/d/11f9ihMT8vcmgijmvebMiHttwSbw9eY_MKkR9ea3CNFCg)
- 5.25 东亚双周会 [ppt](https://docs.google.com/presentation/d/1J-bFnPVufIPIQ3J8_Ez_K8x2ezQKF51vRKYAXyKEHS8/edit?slide=id.g327cde8f41c_0_68)
- 5.19 东亚双周会 [ppt](https://docs.google.com/presentation/d/13iFQVe8wpXD9Cvnz16ve9unU2n2Sq6yHHhZlMj9Rp68/edit?slide=id.g327cde8f41c_0_68)
  
### 4. 独立测试项目/应用软件生态观测

#### 4.1 中国科学院软件研究所公众科学日

- 提交RISC-V和ROS机器人操作系统2篇海报

- 准备展示和互动项目
  - RISC-V设备展示
  - RISC-V应用生态互动体验
  - RISC-V开发板操作系统刷写互动体验——RuyiSDK
  - RISC-V程序开发互动体验——RuyiSDK IDE
  - RISC-V嵌入控制
  - RISC-V生成式AI互动体验
  - RISC-V目标检测互动体验
  - RISC-V HPC互动体验
  - RISC-V教育展示
  - RISC-V发展史
  - RISC-V机器小车互动体验
  - RISC-V四旋翼无人机互动体验
  - 机器学习在RISC-V ROS2中的应用
- [ScienceDay](https://github.com/wychlw/plct/tree/main/doc/ScienceDay)
  - OpenWRT on BPI-F3：提供会场网络
  - 大模型
    - llama.cpp 运行 Deepseek，包含GGML Q4K VLEN128优化 或 以OpenBLAS为后端使用VLEN256优化（运行于Muse Book）
    - EIC7700 NPU 运行 Qwen2 0.5B
  - Box64 运行Turing Complete
  - RevyOS及Fedora桌面生态展示
  - RuyiIDE 及 RuyiSDK展示
  - OpenMPI on Lichee Cluster（本次带分子动力学模拟程序，Thanks to @ArielQueen 's help!）
  
- [代码仓库2](https://gitee.com/yan-mingzhu/demos)
  - 编写 risc-v 知识问答游戏，并结合了嵌入式灯光控制
  - 调试了 duo256 驱动摄像头，舵机，蜂鸣器，传感器 demo
  - 调试了 K230, duos baby llama
- RISC-V嵌入控制——GPIO灯光控制
  - 见 Arduino 部分
- RISC-V HPC互动体验——MPI+RISC-V开发板Cluster
  - 见 [LAMMPS](https://github.com/Arielfoever/Work-PLCT/blob/master/show/LAMMPS)
  - 原始演示视频 [movie.mp4](https://github.com/Arielfoever/Work-PLCT/blob/master/show/LAMMPS/movie.mp4)

-  k230演示
   - [K230 AI例程演示说明](https://github.com/DuoQilai/PLCT-Works/blob/main/Notes/XuanTie/K230AIDemoManualForDeployment.md)
- [在Duo S运行故事机baby llama2](https://github.com/DuoQilai/PLCT-Works/blob/main/Milk-V/DuoS/Report_DuoS__babyllama2.md)
  
#### 4.2 OpenGauss test

openGauss 7.0.0-RC1 test report on LicheePi 4A based on oERV 24.04 LTS

- OpenGauss on TH1520 (LicheePi 4a) performance test.
  - [Add openGauss 7.0.0-RC1 test report for TH1520.](https://github.com/QA-Team-lo/dbtest/commit/158d29a1fb323fa50e3bb0b0e0cd0afa242e9568)

#### 4.3 ROS1/2 测试和Demo原型开发


- [演示视频](https://github.com/lalafua/sim_llm/blob/main/assets/demo_iscas.webm)

- [文档](https://github.com/lalafua/plct-working/blob/main/other/%E5%BC%80%E6%94%BE%E6%97%A5/sim_llm.pdf)

- [源代码](https://github.com/lalafua/slides/blob/main/slides/sim_llm.md)

- 使用 MavRos 开发树莓派和 APM 飞控的小车
  - [过程记录](https://github.com/lalafua/recording/tree/main)
  
#### 4.4 英麒 RISC-V Lab

- [活动方案](https://github.com/DuoQilai/PLCT-Works/blob/main/Notes/Project_Introduction.md)
- 
- [新闻稿](https://mp.weixin.qq.com/s?__biz=Mzg5ODg0OTY0Ng==&mid=2247485471&idx=1&sn=344ad985afa3117f8a616b63772ecd25&chksm=c165048991b6d5abe70d6adcebcec03fe60fc2fe49010e3d4fb91ca4b29dd0b46263a4601af1&mpshare=1&scene=1&srcid=0509PKdXQRmTNgQWeTcnHqXq&sharer_shareinfo=b0322e3f2b2de1cb881d2536001cf87c&sharer_shareinfo_first=cca2016d429daa0744089643b6e4ff92#rd)
  
- 部署荔枝派和香橙派
 
### 5. RISC-V教育和短视频

#### 5.1 短视频课程设计

- 项目迭代计划

https://github.com/DuoQilai/PLCT-Works/tree/main/RISC-V_short_video/Plan_Document

- 项目迭代回溯

https://github.com/DuoQilai/PLCT-Works/tree/main/RISC-V_short_video/Review_Document
  
#### 5.2 短视频设计和实现

- [Milk-V Duo YOLO实战教程](https://www.bilibili.com/video/BV195JJzVESz)

- [在 Duo S 上使用 Pico-ePaper-2.13 显示屏](https://www.bilibili.com/video/BV1FZEkzJE8N)
  
- [Milk-V Duo新手入门环境配置](https://www.bilibili.com/video/BV12AE9zREWE)
 
#### 5.3 短视频剧本和文档、素材

- [使用Visuino给Milk-V Duo编程](https://github.com/jason-hue/plct/blob/main/%E6%B5%8B%E8%AF%95%E6%96%87%E6%A1%A3/%E4%BD%BF%E7%94%A8Visuino%E7%BB%99Milk-V%20Duo%E7%BC%96%E7%A8%8B.md)

- [Milk-V Duo新手常用命令汇总](https://github.com/jason-hue/plct/blob/main/%E6%B5%8B%E8%AF%95%E6%96%87%E6%A1%A3/Milk-V%20Duo%E6%96%B0%E6%89%8B%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4%E6%B1%87%E6%80%BB.md)

- [Milk-V Duo新手入门](https://github.com/jason-hue/plct/blob/main/%E6%B5%8B%E8%AF%95%E6%96%87%E6%A1%A3/Milk-V%20Duo%E6%96%B0%E6%89%8B%E5%85%A5%E9%97%A8.md)

- [Duo S 上使用 Pico-ePaper-2.13 显示屏](https://github.com/jason-hue/plct/blob/main/%E6%B5%8B%E8%AF%95%E6%96%87%E6%A1%A3/%E5%9C%A8%20Duo%20S%20%E4%B8%8A%E4%BD%BF%E7%94%A8%20Pico-ePaper-2.13%20%E6%98%BE%E7%A4%BA%E5%B1%8F.md)

- [导出onnx模型](https://github.com/LizzyLoong/Practice/blob/main/yolo/3.3%E5%AF%BC%E5%87%BAonnx%E6%A8%A1%E5%9E%8B/%E5%AF%BC%E5%87%BAonnx.md) 
       
- [视频脚本](https://github.com/LizzyLoong/Practice/blob/main/yolo/3.3%E5%AF%BC%E5%87%BAonnx%E6%A8%A1%E5%9E%8B/%E8%A7%86%E9%A2%91%E8%84%9A%E6%9C%AC.md)      

- [ubuntu安装docker](https://github.com/LizzyLoong/Practice/blob/main/yolo/4.1%E9%85%8D%E7%BD%AE%20TPU-MLIR%20%E5%B7%A5%E4%BD%9C%E7%8E%AF%E5%A2%83/Ubuntu%E5%AE%89%E8%A3%85docker.md)   

- [tpumlir实际逻辑](https://github.com/LizzyLoong/Practice/blob/main/yolo/4.1%E9%85%8D%E7%BD%AE%20TPU-MLIR%20%E5%B7%A5%E4%BD%9C%E7%8E%AF%E5%A2%83/%E5%AE%9E%E9%99%85%E9%80%BB%E8%BE%91.md)       

- [配置tpumlir工作环境](https://github.com/LizzyLoong/Practice/blob/main/yolo/4.1%E9%85%8D%E7%BD%AE%20TPU-MLIR%20%E5%B7%A5%E4%BD%9C%E7%8E%AF%E5%A2%83/%E9%85%8D%E7%BD%AE%20TPU-MLIR%20%E5%B7%A5%E4%BD%9C%E7%8E%AF%E5%A2%83.md)     

- [视频脚本](https://github.com/LizzyLoong/Practice/blob/main/yolo/4.1%E9%85%8D%E7%BD%AE%20TPU-MLIR%20%E5%B7%A5%E4%BD%9C%E7%8E%AF%E5%A2%83/%E8%A7%86%E9%A2%91%E8%84%9A%E6%9C%AC.md)   

- [合集脚本](https://github.com/LizzyLoong/Practice/blob/main/yolo/%E5%90%88%E9%9B%86%E8%84%9A%E6%9C%AC.md)   

- [合集文档](https://github.com/LizzyLoong/Practice/blob/main/yolo/%E5%90%88%E9%9B%86%E6%96%87%E6%A1%A3.md)  

#### 5.5 短视频技术分享

- 2025年 RISC-V 欧洲峰会海报讲解
- 宣传文章编写
 
### 6. 职工

#### 6.1 蔡玮霖

- ruyi v0.32.0 测试完成 pr [!68](https://gitee.com/yunxiangluo/ruyisdk-test/pulls/68)
- ruyi v0.33.0 测试完成 pr [!69](https://gitee.com/yunxiangluo/ruyisdk-test/pulls/69) [!70](https://gitee.com/yunxiangluo/ruyisdk-test/pulls/70) [!71](https://gitee.com/yunxiangluo/ruyisdk-test/pulls/71)
- ruyi 提交并修复 1 个 issue
    - [ruyi device provision 调用 fastboot 镜像刷写步骤异常 #297](https://github.com/ruyisdk/ruyi/issues/297)
- ruyisdk-website 提交 9 个 pr
    - [pages: add github releases download to total download #117](https://github.com/ruyisdk/ruyisdk-website/pull/117)
    - [pages: fetch ruyi download link with ruyi backend api #118](https://github.com/ruyisdk/ruyisdk-website/pull/118)
    - [pages: fix download page ReleaseProvider context #119](https://github.com/ruyisdk/ruyisdk-website/pull/119)
    - [pages: update i18n ruyi download page with ruyi backend api #121](https://github.com/ruyisdk/ruyisdk-website/pull/121)
    - [pages: use blured slide news background #123](https://github.com/ruyisdk/ruyisdk-website/pull/123)
    - [docs: fetch ruyi download link with ruyi backend api #125](https://github.com/ruyisdk/ruyisdk-website/pull/125)
    - [pages: remove meetup page #131](https://github.com/ruyisdk/ruyisdk-website/pull/131)
    - [pages: fix news show link #132](https://github.com/ruyisdk/ruyisdk-website/pull/132)
    - [pages: add open internship to footer #136](https://github.com/ruyisdk/ruyisdk-website/pull/136)
- ruyisdk-website 合作 2 个 pr
    - [docs: fetch ruyi download link in translations and update contents #126](https://github.com/ruyisdk/ruyisdk-website/pull/126)
    - [Updated homepage with new content #128](https://github.com/ruyisdk/ruyisdk-website/pull/128)
- ruyisdk-website 审核 3 个 pr
    - [beautify homepage & add demoboardpages & fix some statistic pages bugs #115](https://github.com/ruyisdk/ruyisdk-website/pull/115)
    - [docs: update English version #120](https://github.com/ruyisdk/ruyisdk-website/pull/120)
    - [docs: update English version #122](https://github.com/ruyisdk/ruyisdk-website/pull/122)
- ruyisdk-website 关闭 8 个 issue
    - [需要找到专人检查维护 俄语 页面，否则需要隐藏起来更新不及时的俄语页面 #24](https://github.com/ruyisdk/ruyisdk-website/issues/24)
    - [需要找到专人检查维护 日语 页面，否则需要隐藏起来更新不及时的俄语页面 #25](https://github.com/ruyisdk/ruyisdk-website/issues/25)
    - [移动端网页适配 #64](https://github.com/ruyisdk/ruyisdk-website/issues/64)
    - [[BUG] 部分设备点击数据统计按钮会无反应 #65](https://github.com/ruyisdk/ruyisdk-website/issues/65)
    - [[需求] 更新页面内容 #72](https://github.com/ruyisdk/ruyisdk-website/issues/72)
    - [[需求] 更新页面布局 #73](https://github.com/ruyisdk/ruyisdk-website/issues/73)
    - [[优化] 移动端 数据统计页面 #109](https://github.com/ruyisdk/ruyisdk-website/issues/109)
    - [Ruyi包管理器-安装部分 跨域访问导致报错 #130](https://github.com/ruyisdk/ruyisdk-website/issues/130)
- ruyisdk-website 新开 1 个 issue
    - [官网多语言支持情况 #134](https://github.com/ruyisdk/ruyisdk-website/issues/134)
- packages-index 提交 9 个 pr
    - [Manually fix revyos version 20250323 of sipeed-lpi4a #73](https://github.com/ruyisdk/packages-index/pull/73)
    - [Bump RevyOS image to version 20250420 for LicheePi 4A #74](https://github.com/ruyisdk/packages-index/pull/74)
    - [Swap buildroot-sdk-milkv-{duo,duo256m} and buildroot-sdk-milkv-{duo,duo256m}-python v1.0.7 image #75](https://github.com/ruyisdk/packages-index/pull/75)
    - [Manually fix RevyOS version 20250123 and 20250323 for Milkv Meles #76](https://github.com/ruyisdk/packages-index/pull/76)
    - [board-image/revyos-milkv-meles: fix old version and add new versions #76](https://github.com/ruyisdk/packages-index/pull/76)
    - [board-image/buildroot-sdk-milkv-duos-sd: add image version Duo-V1.1.1, Duo-V1.1.2, v1.1.4 and fix v1.1.3, v2.0.0 #77](https://github.com/ruyisdk/packages-index/pull/77)
    - [board-image/buildroot-sdk-milkv-duos-sd: add upstream\_version metadata for old versions #78](https://github.com/ruyisdk/packages-index/pull/78)
    - [board-image/buildroot-sdk-milkv-duo: add some old image version and f… #79](https://github.com/ruyisdk/packages-index/pull/79)
    - [board-image/buildroot-sdk-milkv-duo256: add some old image version and fix new image version #80](https://github.com/ruyisdk/packages-index/pull/80)
- wechat-articles 提交 1 个 pr
    - [Add update of ruyisdk.org #152](https://github.com/ruyisdk/wechat-articles/pull/152)
- docs 审核 1 个 pr
    - [Updates to installation.md and packages.md #83](https://github.com/ruyisdk/docs/pull/83)
- ruyi-packaging 审核 4 个 pr
    - [Add multithreading, current version check, Fix type mismatch in OpenEulerLpi4aChecker #13](https://github.com/ruyisdk/ruyi-packaging/pull/13)
    - [Update DB #14](https://github.com/ruyisdk/ruyi-packaging/pull/14)
    - [Implement gen\_report and update file structure #15](https://github.com/ruyisdk/ruyi-packaging/pull/15)
    - [Remove test flag #16](https://github.com/ruyisdk/ruyi-packaging/pull/16)
- 参加 RISC-V 欧洲峰会，提供现场照片，记录展品内容，张贴和介绍两张海报
- 微信文章供图 [原文](https://mp.weixin.qq.com/s/wx7IwcPNIkk_u_J5LT3j4A)
- 微信文章共图和文字修改 [原文](https://mp.weixin.qq.com/s/hUnChz2EH5qzvVxTRHw-HQ)
- 文章供图和文字 [欧洲峰会见闻](https://gitlab.inuyasha.love/weilinfox/plct-working/-/blob/master/Done/Month23/欧洲峰会见闻.docx)
- 文章供图和文字 [2025年RISC-V欧洲峰会游记](https://gitlab.inuyasha.love/weilinfox/plct-working/-/blob/master/Done/Month23/2025年RISC-V欧洲峰会游记.docx)
- 第 102 次东亚时区双周会，补充和参会介绍“RISC-V 德语社区的同步与八卦”部分
- RISC-V Infra 分享[欧洲峰会见闻](https://gitlab.inuyasha.love/weilinfox/plct-working/-/blob/master/Done/Month23/欧洲峰会见闻.pptx)
- 玄铁课程介绍录音 [Intro 内容](https://gitlab.inuyasha.love/weilinfox/plct-working/-/blob/master/Done/Month23/Intro.md)
- 协助吴干琼老师完成 5 月 23 日的 RuyiSDK Office Hours 演示准备
- 新实习生面试考核 [Marco 面试考核](https://gitlab.inuyasha.love/weilinfox/plct-working/-/blob/master/Done/Month23/Macro.md)
- 新实习生面试 [Marco 面试](https://gitlab.inuyasha.love/weilinfox/plct-working/-/blob/master/Done/Month23/Macro-update.md)

#### 6.2 郑景坤

##### 6.2.1 操作系统支持矩阵

- PR Review (对测试团队操作系统支持矩阵产出的review审核，以下内容同测试团队产出，此处为review)
  - [Star64/Ubuntu: fix typo](https://github.com/ruyisdk/support-matrix/pull/285)
  - [Duo/Alpine: Bump to 3.21.3](https://github.com/ruyisdk/support-matrix/pull/286)
  - [Megrez/RockOS: Bump to 20250423](https://github.com/ruyisdk/support-matrix/pull/287)
  - [Pioneer/openCloudOS: Bump to main repo version](https://github.com/ruyisdk/support-matrix/pull/289)
  - [LicheePi4A8+32G: Add Arch Linux](https://github.com/ruyisdk/support-matrix/pull/290)
  - [Add ArchLinux test reports for Mars.](https://github.com/ruyisdk/support-matrix/pull/291)
  - [Meles/RevyOS: Bump to 20250420](https://github.com/ruyisdk/support-matrix/pull/292)
  - [Add Pine64 Ox64](https://github.com/ruyisdk/support-matrix/pull/293)
  - [Update RV-STAR](https://github.com/ruyisdk/support-matrix/pull/294)
  - [Add new Board HengShanPi and it's RT-Thread test report.](https://github.com/ruyisdk/support-matrix/pull/295)
  - [Add Alpine test report for Mars and fix typos.](https://github.com/ruyisdk/support-matrix/pull/296)
  - [Update Ubuntu 24.04.02 test report for Nezha.](https://github.com/ruyisdk/support-matrix/pull/297)
  - [Update: ESP32C2, ESP32H2, ESP32C6 test reports](https://github.com/ruyisdk/support-matrix/pull/298)
  - [LicheeRV_Dock: update ubuntu to 25.04](https://github.com/ruyisdk/support-matrix/pull/299)
  - [Metadata: fix wrong sys metadata](https://github.com/ruyisdk/support-matrix/pull/300)
  - [LiP4A_8_32: Add NixOS and Slackware](https://github.com/ruyisdk/support-matrix/pull/301)
  - [MusePi Pro: Init board and add systems](https://github.com/ruyisdk/support-matrix/pull/303)
  - [Add new board OrangePi RV with OpenWRT and Ubuntu LTS test report and…](https://github.com/ruyisdk/support-matrix/pull/304)
  - [Metadata: Add cpu_arch, fill-in all vendor and board_variant](https://github.com/ruyisdk/support-matrix/pull/305)
  - [Mars: add Armbian and DietPi test report; Fix some typos.](https://github.com/ruyisdk/support-matrix/pull/306)
  - [Add Premier P550 & Megrez test report on Deepin](https://github.com/ruyisdk/support-matrix/pull/309)
  - [DuoS: dump Debian to 1.6.23](https://github.com/ruyisdk/support-matrix/pull/310)
  - [Duo 256M: update Debian 13.0 test report and fix some typos.](https://github.com/ruyisdk/support-matrix/pull/311)
  - New PRs
    - [megrez: RockOS: update to 20250423](https://github.com/ruyisdk/support-matrix/pull/288)（完成实际启动测试部分）
    - [Pioneer/OpenCloudOS: Add desktop](https://github.com/ruyisdk/support-matrix/pull/302)（完成实际启动测试部分）

##### 6.2.2 RuyiSDK 双周报/支持矩阵部分

- https://github.com/ruyisdk/wechat-articles/pull/149
- https://github.com/ruyisdk/wechat-articles/pull/156

##### 6.2.3 RevyOS 小队

- [东亚双周会](https://docs.google.com/presentation/d/13iFQVe8wpXD9Cvnz16ve9unU2n2Sq6yHHhZlMj9Rp68/edit?slide=id.g327cde8f41c_0_161#slide=id.g327cde8f41c_0_161) 宣发（新版本镜像）

#### 6.3 阎明铸

##### 6.3.1 sail/act
- \[PR\] <https://github.com/riscv/sail-riscv/pull/930> Fix build failure due to plat_enable_htif signature mismatch
- \[PR\] <https://github.com/riscv/sail-riscv/pull/970> Fix printf in first party test
- \[PR\] <https://github.com/rems-project/sail/pull/1312> Add --sail_config flag for sail compiler
- \[PR\] <https://github.com/rems-project/sail/pull/1313> Enhance AST printing for better debugging
- \[PR\] <https://github.com/rems-project/sail/pull/1314> Enhance fmt for Index
- \[ISSUE\] <https://github.com/rems-project/sail/issues/1323> Could not resolve quantifiers for newtype
- \[PR\] <https://github.com/rems-project/sail/pull/1325> Add test case for mapping
- 帮助 ACT 社区 Zalasr PR 作者调试问题 <https://lists.riscv.org/g/sig-arch-test/message/757> Help with creating ACT for Zalasr

##### 6.3.2 会议/技术分享

- tech-golden-model meeting [`05.05`, `05.12`, `05.19`](https://docs.google.com/document/d/11f9ihMT8vcmgijmvebMiHttwSbw9eY_MKkR9ea3CNFCg)
- 5.25 东亚双周会 [ppt](https://docs.google.com/presentation/d/1J-bFnPVufIPIQ3J8_Ez_K8x2ezQKF51vRKYAXyKEHS8/edit?slide=id.g327cde8f41c_0_68)
- 5.19 东亚双周会 [ppt](https://docs.google.com/presentation/d/13iFQVe8wpXD9Cvnz16ve9unU2n2Sq6yHHhZlMj9Rp68/edit?slide=id.g327cde8f41c_0_68)

##### 6.3.3 公众科学日

- 代码仓库：<https://gitee.com/yan-mingzhu/demos>
- 编写 risc-v 知识问答游戏，并结合了嵌入式灯光控制
- 调试了 duo256 驱动摄像头，舵机，蜂鸣器，传感器 demo
- 调试了 K230, duos baby llama

#### 6.4 张馥媛

##### 6.4.1 Milk-V Duo

- 发布Milk-V Duo YOLO实战完结合集课程
  - [【完结】【Milk-V Duo】YOLO实战教程_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV195JJzVESz/?spm_id_from=333.1387.homepage.video_card.click&vd_source=417238cd96b1b549d14bcb35a9da3cf0)

- 视频AI配音
  - [【Milk-V Duo S】在 Duo S 上使用 Pico-ePaper-2.13 显示屏_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1FZEkzJE8N/?spm_id_from=333.1387.homepage.video_card.click&vd_source=417238cd96b1b549d14bcb35a9da3cf0)
  - [【Milk-V Duo】新手入门环境配置_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV12AE9zREWE/?spm_id_from=333.1387.homepage.video_card.click&vd_source=417238cd96b1b549d14bcb35a9da3cf0)

- 项目迭代计划：

https://github.com/DuoQilai/PLCT-Works/tree/main/RISC-V_short_video/Plan_Document

- 项目迭代回溯：

https://github.com/DuoQilai/PLCT-Works/tree/main/RISC-V_short_video/Review_Document

##### 6.4.2 软件所开放日素材

-  k230演示
   - [K230 AI例程演示说明](https://github.com/DuoQilai/PLCT-Works/blob/main/Notes/XuanTie/K230AIDemoManualForDeployment.md)
- 在Duo S运行故事机baby llama2
  - [PLCT-Works/Milk-V/DuoS/Report_DuoS__babyllama2.md at main · DuoQilai/PLCT-Works · GitHub](https://github.com/DuoQilai/PLCT-Works/blob/main/Milk-V/DuoS/Report_DuoS__babyllama2.md)
- 
##### 6.4.3 RISC-V short video项目
建议和修改同学们提交的视频，发布视频和控制进度

- 项目迭代计划：

https://github.com/DuoQilai/PLCT-Works/tree/main/RISC-V_short_video/Plan_Document

- 项目迭代回溯：

https://github.com/DuoQilai/PLCT-Works/tree/main/RISC-V_short_video/Review_Document

##### 6.4.4 英麒 RISC-V Lab

- [后续活动方案](https://github.com/DuoQilai/PLCT-Works/blob/main/Notes/Project_Introduction.md)
- [新闻稿](https://mp.weixin.qq.com/s?__biz=Mzg5ODg0OTY0Ng==&mid=2247485471&idx=1&sn=344ad985afa3117f8a616b63772ecd25&chksm=c165048991b6d5abe70d6adcebcec03fe60fc2fe49010e3d4fb91ca4b29dd0b46263a4601af1&mpshare=1&scene=1&srcid=0509PKdXQRmTNgQWeTcnHqXq&sharer_shareinfo=b0322e3f2b2de1cb881d2536001cf87c&sharer_shareinfo_first=cca2016d429daa0744089643b6e4ff92#rd)
- 部署荔枝派和香橙派

#### 6.5 朱旭昌

- 更新了为ACT添加缺失的RV32 Zdinx共117个测试用例[#642](https://github.com/riscv-non-isa/riscv-arch-test/pull/642)并成功合并
- 更新了为ACT添加缺失的RV32 Zfinx的一些新测试用例[#642](https://github.com/riscv-non-isa/riscv-arch-test/pull/642)

| 测试用例名 | 所属拓展 | 添加测试用例数 | 地址                                                         |
| ---------- | -------- | -------------- | ------------------------------------------------------------ |
| fmadd-b11  | zfinx    | 13             | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fmsub-b11  | zfinx    | 13             | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fnmadd-b11 | zfinx    | 13             | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fnmsub-b11 | zfinx    | 13             | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fmadd-b1   | zfh      | 18             | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fmsub-b1   | zfh      | 18             | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fnmadd-b1  | zfh      | 18             | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fnmsub-b1  | zfh      | 18             | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |

- 提交了一个修复rv 32 Zdinx测试错误的bug的pr[#651](https://github.com/riscv-non-isa/riscv-arch-test/pull/651)
- 为ACT添加缺失的rv64 Zdinx fmadd.d/fmsub.d共330个测试用例[#654](https://github.com/riscv-non-isa/riscv-arch-test/pull/654)

| 测试指令名 | 所属拓展 | 测试用例数 | 地址                                                         |
| ---------- | -------- | ---------- | ------------------------------------------------------------ |
| fadd.d     | Zdinx    | 11         | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fclass.d   | Zdinx    | 1          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fdiv.d     | Zdinx    | 11         | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| feq.d      | Zdinx    | 2          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fle.d      | Zdinx    | 2          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| flt.d      | Zdinx    | 2          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fmadd.d    | Zdinx    | 62         | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fmax.d     | Zdinx    | 2          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fmin.d     | Zdinx    | 2          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fmsub.d    | Zdinx    | 62         | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fmul.d     | Zdinx    | 9          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fnmadd.d   | Zdinx    | 62         | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fnmsub.d   | Zdinx    | 62         | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fsgnj.d    | Zdinx    | 1          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fsgnjn.d   | Zdinx    | 1          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fsgnjx.d   | Zdinx    | 1          | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fsqrt.d    | Zdinx    | 10         | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |
| fsub.d     | Zdinx    | 12         | [github](https://github.com/riscv-non-isa/riscv-arch-test/tree/dev/riscv-test-suite/rv32i_m/Zfinx/src) |

## SG2042/SG2044 Upstream

SG2042 Upstream

- [[PATCH 0/4] Add Sophgo x8/x4 EVB Board support][sg2042-lk-1]: 支持 EVB 开发板，第 1 版
- [[PATCH v2 0/4] Add Sophgo EVB V1/V2 Board support][sg2042-lk-5]: 支持 EVB 开发板，第 2 版
- [[PATCH 0/2] riscv: dts: sophgo: add more sg2042 isa extension support][sg2042-lk-2]: 支持更多 isa 扩展，第 1 版
- [[PATCH v2 0/3] riscv: dts: sophgo: add more sg2042 isa extension support][sg2042-lk-6]: 支持更多 isa 扩展，第 2版
- [[PATCH 0/3] spi: sophgo: Add SPI NOR controller for SG2042][sg2042-lk-3]: SPI NOR 控制器补丁 第 1 版。
- [[PATCH v2 0/3] spi: sophgo: Add SPI NOR controller for SG2042][sg2042-lk-4]: SPI NOR 控制器补丁 第 2 版。

[sg2042-lk-1]:https://lore.kernel.org/linux-riscv/cover.1746811744.git.rabenda.cn@gmail.com
[sg2042-lk-2]:https://lore.kernel.org/linux-riscv/cover.1746828006.git.rabenda.cn@gmail.com/
[sg2042-lk-3]:https://lore.kernel.org/linux-riscv/20250523-sfg-spifmc-v1-0-4cf16cf3fd2a@gmail.com/
[sg2042-lk-4]:https://lore.kernel.org/linux-riscv/20250525-sfg-spifmc-v2-0-a3732b6f5ab4@gmail.com/
[sg2042-lk-5]:https://lore.kernel.org/linux-riscv/cover.1747231254.git.rabenda.cn@gmail.com/
[sg2042-lk-6]:https://lore.kernel.org/linux-riscv/cover.1747235487.git.rabenda.cn@gmail.com/

## Milk-V Duo Upstream

- [[PATCH v4 0/2] riscv: sophgo: add mailbox support for CV18XX series SoC][cv18xx-1k-1]: Mailbox 驱动，第 4 版。

[cv18xx-1k-1]: https://lore.kernel.org/linux-riscv/20250520-cv18xx-mbox-v4-0-fd4f1c676d6e@pigmoral.tech

## TPU-MLIR （甲辰计划 J123）

默认无更新。本项目 RISC-V 支持由实习生提供。

## LuaJIT

Found a bug with FFI, the patch is WIP.

- [Incorrect FFI pass-by-value struct call convention](https://github.com/ruyisdk/LuaJIT/issues/3)

Interpreter fixes and improvements.

- [Fix BC_TSETS_Z overwriting the mark of the write barrier](https://github.com/plctlab/LuaJIT/commit/ff5c7a772491a1de2216fd6d790a2eb01abbc72f)
- [Fix BC_UNM out-of-range check](https://github.com/plctlab/LuaJIT/commit/3a67a177f0b89374c4a0a88b8b05f6effcc1baef)
- [Optimize BC_CALLMT](https://github.com/plctlab/LuaJIT/commit/43742cb0a43d9e36542e0e13097b081d47ff5f41)
- [Optimize unary test-and-copy ops](https://github.com/plctlab/LuaJIT/commit/9c7339d95ba6ea980b12080d92473657fef70858)
- [Optimize BC_RETM and BC_RET](https://github.com/plctlab/LuaJIT/commit/3279bff973e789203cef6737dedc425ce257ab82)

## gem5

默认无更新。目前无员工或实习生投入，欢迎投递简历继续做 RISC-V 支持。

## Spike

默认无更新。目前无员工或实习生投入，欢迎投递简历继续做 RISC-V 支持。

## QEMU
- [PATCH v5] target/riscv/kvm: add satp mode for host cpu | https://lists.nongnu.org/archive/html/qemu-devel/2025-05/msg06720.html

## RustSBI 小队

全实习生小队，独立宣传渠道。

## FreeBSD
- 构建全球首个FreeBSD 14 riscv quarterly镜像 https://mirror.iscas.ac.cn/FreeBSD-pkgs/FreeBSD%3A14%3Ariscv64/quarterly/
- riscv: add Sifive p550/p650 identification | https://github.com/freebsd/freebsd-src/pull/1674

## Nixpkgs

默认无更新。目前无员工或实习生投入。

## Fedora

全实习生小队，独立宣传渠道。

## The Aya Theorem Prover

默认无更新。目前无员工或实习生投入。

## Arch Linux

全实习生小队，独立宣传渠道。

## Songsong Zhang

- CentOS Stream

  [Enable riscv64 arch for 'portable' OpenJDK](https://gitlab.com/redhat/centos-stream/rpms/java-21-openjdk/-/merge_requests/43)
  
  [Enable 'riscv64' arch for C10S](https://gitlab.com/redhat/centos-stream/rpms/java-21-openjdk/-/merge_requests/44)

- Sail

  [New Package: lem](https://bugzilla.redhat.com/show_bug.cgi?id=2291284)

## 参考链接

- [PLCT 实验室的开放职位（实习生）](https://github.com/plctlab/weloveinterns/blob/master/open-internships.md)
- [PLCT 开源进展 (PLCT Weekly)](https://github.com/plctlab/PLCT-Weekly)
- [PLCT 公开报告幻灯片（选集）](https://github.com/plctlab/PLCT-Open-Reports)
