# 一些简单的 Rust Github Workflows

## Build and Release

```yaml
name: Example

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build-and-release:
    name: Build and Release
    uses: azazo1/rust-workflows/.github/workflows/build-and-release.yml@main
    with:
      # Git ref (分支、标签或 SHA) 用于 checkout 代码。
      # 默认值: ${{ github.ref }} (触发当前工作流的 Git 引用)
      ref: ${{ github.ref }}
      # 是否在成功构建后创建 GitHub 预发布。
      # 默认值: true (即会创建预发布)
      create_prerelease: true
      # 如果为 true，将只构建并上传 artifact，但不会创建 GitHub release。
      # 默认值: false (即会尝试创建 GitHub release)
      # artifact 的名称为: ${{ inputs.package_name }}-${{ 操作系统平台 }}
      dry_run: false
      # 见: Swatinem/rust-cache@v2 (prefix_key)
      cache_prefix_key: "v0-rust"
      # 构建包名 (要发布的可执行文件名)
      package_name: "example-package"
    secrets:
      GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}

```
