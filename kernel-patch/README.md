# Kernel Patch Usage Guide

During cloud compilation using GitHub Actions, you can use the `kernel_patch` parameter to specify the directory of the kernel patches in your repository. The common kernel patches that can be used for each series of kernels adopt a fixed directory name (`common-kernel-patches`). Only the patches specific to a particular series, for example, [linux-5.15.y](https://github.com/unifreq/linux-5.15.y), use the directory name `identical to the kernel source library`. Other custom named directories (such as the `deprecated-patches` directory for storing obsolete patches) will be skipped during kernel compilation and will not be used.

```shell
~/kernel
    └── <your-kernel-patches>
        ├── common-kernel-patches  # Fixed directory name: Stores kernel patches common to all versions
        ├── linux-5.15.y           # Same as the kernel source library: stores dedicated patches
        ├── linux-6.1.y
        ├── linux-5.10.y-rk35xx
        └── more kernel directory...
```

The usage in the kernel compilation script can refer to the settings in [compile-beta-general-kernel.yml](../.github/workflows/compile-beta-general-kernel.yml):

```yaml
- name: Compile the kernel
  uses: ophub/amlogic-s9xxx-armbian@main
  with:
    build_target: kernel
    kernel_version: 5.15.1_6.1.1
    kernel_auto: true
    kernel_config: kernel-config/beta
    kernel_patch: kernel-patch/beta
    auto_patch: true
```

When compiling the kernel, it will first enumerate all the patches with `.patch` suffix under `common-kernel-patches` and apply them, then enumerate and apply the dedicated patches for the current compiled kernel (such as: linux-6.1.y). For more instructions, please refer to the detailed introduction in [Kernel Compilation Method](https://github.com/ophub/amlogic-s9xxx-armbian/tree/main/compile-kernel) and [Kernel Patch Addition Method](https://github.com/ophub/amlogic-s9xxx-armbian/tree/main/documents/README.md#9-compiling-armbian-kernel).

# 内核补丁使用说明

在 GitHub Actions 云编译时，可以使用 `kernel_patch` 参数指定内核补丁在你仓库中的目录。其中每个系列的内核都能使用的通用内核补丁，采用固定目录名称（`common-kernel-patches`），仅适用于指定系列，例如 [linux-5.15.y](https://github.com/unifreq/linux-5.15.y) 的内核补丁，使用 `与内核源码库同名` 的目录名称。使用其他自定义命名的目录（例如存放已弃用补丁的目录`deprecated-patches`）在内核编译时将跳过，不会被使用。

```shell
~/kernel
    └── <your-kernel-patches>
        ├── common-kernel-patches  # 固定目录名：存放各版本都通用的内核补丁
        ├── linux-5.15.y           # 与内核源码库同名：存放专用补丁
        ├── linux-6.1.y
        ├── linux-5.10.y-rk35xx
        └── more kernel directory...
```

在内核编译脚本中使用方法可以参考 [compile-beta-general-kernel.yml](../.github/workflows/compile-beta-general-kernel.yml) 的设置：

```yaml
- name: Compile the kernel
  uses: ophub/amlogic-s9xxx-armbian@main
  with:
    build_target: kernel
    kernel_version: 5.15.1_6.1.1
    kernel_auto: true
    kernel_config: kernel-config/beta
    kernel_patch: kernel-patch/beta
    auto_patch: true
```

在编译内核时，会先遍列 `common-kernel-patches` 下后缀是 `.patch` 的全部补丁并应用，然后再遍列当前编译内核（如：linux-6.1.y）的专用补丁并应用。更多说明请参考 [内核编译方法](https://github.com/ophub/amlogic-s9xxx-armbian/tree/main/compile-kernel) 和 [内核补丁添加方法](https://github.com/ophub/amlogic-s9xxx-armbian/tree/main/documents/README.cn.md#9-编译-armbian-内核) 中的详细介绍。
