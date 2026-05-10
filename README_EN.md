# ResidenceBridge-Velocity

ResidenceBridge-Velocity is a bridge plugin that runs on the Velocity proxy side.

It does not produce gameplay events itself. Its main responsibility is to receive plugin messages sent from the Paper side and forward players to the target sub-server.

## Important Notes

This plugin cannot work by itself.

You must also install ResidenceBridge on the Paper side, otherwise no messages will be sent to Velocity and the transfer logic will not be triggered.

Paper-side project:

https://github.com/hahaTT0902/ResidenceBridge

## Features

- Lightweight: no standalone runtime configuration file, ready to use out of the box.
- Proxy-side forwarding: resolves the target server on the Velocity side and initiates the connection.
- CI ready: the repository includes GitHub Actions automated build workflows.

## Requirements

- Java 17
- Velocity 3.x
- ResidenceBridge installed on the Paper side
- Gradle Wrapper (already included in the repository)

## Quick Start

1. Build the plugin.
2. Put ResidenceBridge-Velocity into the plugins directory of Velocity.
3. Install ResidenceBridge on your Paper sub-server.
4. Start Velocity and Paper.
5. Confirm that the Velocity console shows ResidenceBridge-Velocity enabled.

## Build

### Release Build (Runnable)

Linux/macOS:

```bash
./gradlew clean build
```

Windows:

```powershell
.\gradlew.bat clean build
```

Default artifact:

```text
build/libs/ResidenceBridge-Velocity-1.0.0.jar
```

### Development Build (Not Runnable)

```bash
./gradlew taboolibBuildApi -PDeleteCode
```

`-PDeleteCode` removes logic code to reduce the artifact size. This output is only intended for development dependency scenarios.

## Deployment and Runtime

1. Velocity side:
   - Put the built jar from this repository into the Velocity root plugins folder.
2. Paper side:
   - Install ResidenceBridge: https://github.com/hahaTT0902/ResidenceBridge
3. Startup order:
   - Start Velocity first, then start each Paper sub-server.
4. Verification:
   - The Velocity log shows ResidenceBridge-Velocity enabled.
   - After triggering the Paper-side logic, players can be forwarded to the target server.

## Configuration

This version does not provide a separate configuration file. Behavior is fixed in code:

- Plugin message channel: `residencebridge:main`
- Message payload: target sub-server name (for example `lobby`)
- Target resolution: based on the server list already registered in Velocity

If the target server does not exist, a `Target server not found` warning will be logged.

If ResidenceBridge is not installed on the Paper side, this channel will not receive valid messages.

## Project Structure

```text
.github/workflows/      GitHub Actions CI
src/main/kotlin/        Plugin source code
gradle/wrapper/         Gradle Wrapper
build.gradle.kts        Build script
```

## Development and Collaboration

- Main branch: `main`
- CI: automatic builds on push and pull request
- Recommended check before submitting: `./gradlew clean build`

## Automated Release

The repository supports automated GitHub Releases and uploads the plugin jar when a tag is pushed.

Release steps:

1. Make sure the code on the `main` branch is ready and pushed.
2. Create and push a version tag (recommended format: `vX.Y.Z`).

```bash
git tag v1.0.1
git push origin v1.0.1
```

3. GitHub Actions will automatically:
   - run the build
   - create a Release
   - upload the jar produced in `build/libs`

See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## License

This project uses the MIT License. See [LICENSE](LICENSE) for details.
