# 手机 App 打包测试项目（线上网页地址 → 安卓 APK）

将线上网页地址打包成**安卓安装包（APK）**，无需上架应用商店、无需本地安装 Android 环境。

## 技术方案

- **Capacitor**（Ionic 官方开源框架）：把网页包成原生 App 壳
- **GitHub Actions**：在云端免费编译出 APK

## 使用步骤

### 1. 建 GitHub 私有仓库并推送本目录

```bash
# 在 GitHub 新建一个私有仓库（例如 mobile-packager）
cd mobile-packager
git init
git add .
git commit -m "初始化打包项目"
git branch -M main
git remote add origin <你的GitHub私有仓库地址>
git push -u origin main
```

### 2. 触发云端打包

1. 打开 GitHub 仓库 → 点 **Actions** 标签
2. 左侧选 **Build Android APK** 工作流
3. 点 **Run workflow**，填入：
   - **App 显示名称**：如 `我的备忘录`
   - **Android 包名**：如 `com.example.webapp`（需全局唯一）
   - **网页地址**：要打包的线上网址
4. 点 **Run workflow**，等约 5~10 分钟

### 3. 下载 APK

构建完成后，工作流页面会生成一个 **Artifact**（构建产物），点开即可下载 `app-debug.apk`，传到安卓手机安装即可使用。

## 说明

- 本项目的 `capacitor.config.json` 指向一个测试网址（`我的备忘录`），首次运行可直接用它验证链路是否跑通
- APK 为 **Debug 版**，不需要签名、可直接安装
- 网页内容由远程 URL 加载，**App 打开后需要能访问该网址**（即你的服务器/COS 保持在线）