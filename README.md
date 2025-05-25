# 🚀 GitHub Actions 自动编译一加内核工作流教程

本教程适用于本仓库的所有工作流文件，可实现一加内核的云端自动编译、打包与发布。

---

## 1. 前提条件

- 你已 Fork 或拥有本仓库的写权限。
- 仓库下存在工作流文件文件。

---

## 2. 工作流功能简介

- 自动拉取 kernel 相关源码和补丁
- 自动应用 SUSFS、KPM、LZ4KD、风驰等功能补丁
- 自动配置内核参数
- 自动编译内核并打包 AnyKernel3
- 自动上传产物并发布 Release

---

## 3. 如何使用

### 3.1 手动触发编译

1. 进入你的 GitHub 仓库页面
2. 点击顶部菜单栏的 **Actions**
3. 在左侧找到 **一加13构建** 工作流，点击进入
4. 点击右侧的 **Run workflow** 按钮
5. 填写参数（可用默认值，也可自定义）：

   | 参数名              | 说明                         | 示例值                      |
   |---------------------|------------------------------|-----------------------------|
   | CPU                 | 分支名                       | sm8750                      |
   | FEIL                | 配置文件名                   | oneplus_13                  |
   | CPUD                | 处理器代号                   | sun                         |
   | ANDROID_VERSION     | 内核安卓版本                 | android15                   |
   | KERNEL_VERSION      | 内核版本                     | 6.6                         |
   | KERNEL_NAME         | 内核名称后缀                 | -By-kuan-jiangbeichen       |
   | KERNEL_TIME_MODE    | 编译时间模式（自动/自定义）  | 自动获取/自定义             |
   | KERNEL_TIME_CUSTOM  | 自定义编译时间               | 2024-12-17 23:36:49 UTC     |
   | FEATURES            | 启用功能（逗号分隔）         | kpm,lz4kd,fengchi           |

6. 点击绿色的 **Run workflow** 开始云端自动编译

---

### 3.2 编译流程说明

- **依赖安装**：自动安装所需依赖和 repo 工具
- **源码同步**：自动拉取 kernel 相关源码
- **功能解析**：根据 FEATURES 参数自动启用/禁用 KPM、LZ4KD、风驰等功能
- **补丁应用**：自动应用 SUSFS、LZ4KD 等补丁
- **内核配置**：自动写入 defconfig 配置
- **编译内核**：自动调用 bazel 编译
- **产物打包**：自动打包 AnyKernel3
- **自动发布**：编译完成后自动上传产物并发布 Release

---

### 3.3 查看和下载产物

- 编译完成后，Actions 页面会显示每一步的日志
- 产物会自动上传到 Release 页面，也可在 Actions 的 Artifacts 区域下载

---

## 4. 常见问题

- **inputs 超过 10 个**：已合并为 FEATURES 字符串输入，避免超限
- **Release 描述乱码或不完整**：已用多行 echo 拼接，兼容性好
- **补丁冲突/编译失败**：请根据日志检查补丁和 defconfig 配置

---

## 5. 高级用法

- 可自定义 `FEATURES` 参数，灵活组合功能（如只写 `kpm` 或 `kpm,lz4kd`）
- 可自定义 `KERNEL_NAME`、`KERNEL_TIME_CUSTOM` 等参数，满足个性化需求
- 如需添加新功能，只需在 `FEATURES` 解析和相关步骤中扩展即可

---

## 6. 参考

- [GitHub Actions 官方文档](https://docs.github.com/en/actions)
- [本项目 README 或 Wiki](../README.md)

---

如有其它问题，欢迎在 Issues 区留言或继续提问！
