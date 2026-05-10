# ResidenceBridge-Velocity

ResidenceBridge-Velocity 是一个运行在 Velocity 代理端的桥接插件, 用于接收 `residencebridge:main` 插件消息并将玩家转发到指定子服。

## 特性

- 轻量化: 无独立运行时配置文件, 开箱即用。
- 代理侧转发: 在 Velocity 侧解析目标服并发起连接。
- CI 就绪: 仓库自带 GitHub Actions 自动构建流程。

## 环境要求

- Java 17
- Velocity 3.x
- Gradle Wrapper (仓库已内置)

## 快速开始

1. 构建插件。
2. 将产物放入 Velocity 的 `plugins` 目录。
3. 启动 Velocity 并确认插件日志。

## 构建

### 发行版本 (可运行)

Linux/macOS:

```bash
./gradlew clean build
```

Windows:

```powershell
.\gradlew.bat clean build
```

默认产物:

```text
build/libs/ResidenceBridge-Velocity-1.0.0.jar
```

### 开发版本 (不可运行)

```bash
./gradlew taboolibBuildApi -PDeleteCode
```

`-PDeleteCode` 用于移除逻辑代码以缩小体积, 该产物仅用于开发依赖场景。

## 部署与运行

1. 将发行版 jar 复制到 Velocity 根目录的 `plugins` 文件夹。
2. 启动 Velocity。
3. 在控制台确认日志 `ResidenceBridge-Velocity enabled.`。

## 设置说明

当前版本不提供独立配置文件, 行为由代码固定定义:

- 插件消息频道: `residencebridge:main`
- 消息载荷: 目标子服名 (例如 `lobby`)
- 目标服解析: 基于 Velocity 已注册服务器列表

若目标服不存在, 会记录 `Target server not found` 警告。

## 项目结构

```text
.github/workflows/      GitHub Actions CI
src/main/kotlin/        插件源码
gradle/wrapper/         Gradle Wrapper
build.gradle.kts        构建脚本
```

## 开发与协作

- 主分支: `main`
- CI: Push/PR 自动构建
- 提交前建议执行: `./gradlew clean build`

详情可见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 许可证

本项目使用 MIT License, 详见 [LICENSE](LICENSE)。
