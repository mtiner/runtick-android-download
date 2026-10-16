# RunTick Android 下载源

静态 Worker，托管 Android APK 供官网下载（无代码逻辑，纯 assets）。

- 仓库：`mtiner/runtick-android-download`
- Worker：`runtick-android-download`
- 域名：<https://download.runtick.cc>
- 固定最新版链接：<https://download.runtick.cc/runtick-latest.apk>

## 发版流程（由 runtick-android CI 自动完成）

1. `runtick-android` 打 `v*` 标签 → GitHub Actions 构建签名 APK 并创建 Release；
2. CI 通过 GitHub API 把 APK 以 `runtick-latest.apk`（固定最新版）与 `runtick-X.Y.Z.apk`（版本化，文件名不带 v 前缀）提交到本仓库 `public/`；
3. Cloudflare Workers Builds 监听本仓库 main 分支自动 `wrangler deploy`。

## 手动更新

```sh
cp <新 APK> public/runtick-latest.apk
cp <新 APK> public/runtick-X.Y.Z.apk
git add public && git commit -m "release: vX.Y.Z" && git push
```
