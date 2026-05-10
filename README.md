# ResidenceBridge-Velocity

Velocity 代理端插件, 用于接收插件消息并将玩家转发到指定子服。

## 环境要求

- Java 17
- Velocity 3.x
- Gradle Wrapper (仓库已自带)

## 构建发行版本

发行版本用于正常使用, 不含 TabooLib 本体。

```
./gradlew build
```

Windows:

```
.\gradlew.bat clean build
```

构建产物:

```
build/libs/ResidenceBridge-Velocity-1.0.0.jar
```

## 构建开发版本

开发版本包含 TabooLib 本体, 用于开发者使用, 但不可运行。

```
./gradlew taboolibBuildApi -PDeleteCode
```

> 参数 -PDeleteCode 表示移除所有逻辑代码以减少体积。

## 运行方式

1. 将发行版 jar 放入 Velocity 根目录的 plugins 文件夹。
2. 启动 Velocity。
3. 日志中出现 ResidenceBridge-Velocity enabled 即表示加载成功。

## 设置说明

- 本插件当前没有独立配置文件。
- 监听的插件消息频道为 residencebridge:main。
- 消息体应为目标子服名, 例如 lobby。
- Velocity 必须已配置该子服, 否则会提示 Target server not found。

## GitHub 发布建议

1. 使用 main 作为主分支。
2. 通过 GitHub Actions 自动执行 CI 构建。
3. 仅上传源码和构建脚本, 不提交 build 目录。