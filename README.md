# In-game Visual GT Machine Builder (ivgtmb)

在游戏内可视化搭建 **GTCEu**（GregTech CE Unofficial）机器与多方块结构的一个 Minecraft 1.12.2 客户端模组。

按下 `Y` 键或输入 `/ivgtmb` 打开建造界面。

基于 [CleanroomMC TemplateDevEnv](https://github.com/CleanroomMC/TemplateDevEnv) 开发，使用 **RetroFuturaGradle 2.0.3 + Forge 14.23.5.2847** 构建。

## 特性

- 在游戏内以图形界面搭建 GTCEu 单方块机器与多方块结构
- 实时机器预览与渲染
- 多方块构造时，可将 `/gs hand` 中的 blockstate 复制到方块输入栏
- 支持简体中文（`zh_cn`）与英文（`en_us`）

## 已知限制

- 尚未支持蒸汽机器（steam machine）

## 依赖

构建需要两个本地 jar，**未随本仓库分发**，请自行下载后放入项目根目录的 `libs/` 文件夹：

| 依赖 | 版本 | 许可 | 获取方式 |
| --- | --- | --- | --- |
| GregTech CE Unofficial (GTCEu) | 2.8.10-beta | LGPL-3.0 | [GitHub Releases](https://github.com/GregTechCEu/GregTech/releases)（`gregtech-1.12.2-2.8.10-beta-dev.jar`） |
| ModularUI (MUI2) | 3.1.6 | 以上游仓库为准 | [GitHub Releases](https://github.com/CleanroomMC/ModularUI/releases)（`modularui-3.1.6.jar`） |

> 说明：本项目通过本地 `libs/` 目录（Gradle `flatDir`）解析依赖，而非远程 Maven 仓库（GTCEu 的 Maven 服务不可达）。请将上述 jar 放入 `libs/` 后再执行构建。

## 构建

需要 **Java 25**（运行 Gradle）与 **JDK 8**（编译目标，Azul Zulu 等）。

```
gradlew build
```

开发环境运行客户端：

```
gradlew runClient
```

### 构建产物

| 产物 | 用途 |
| --- | --- |
| `build/libs/ivgtmb-<version>.jar` | **发布/安装用**，已 reobfuscate 为 SRG 名称，可放入正式实例的 `mods/` |
| `build/libs/ivgtmb-<version>-dev.jar` | 开发命名空间（MCP）产物，仅供调试参考，**不要**放进正式实例 |

> 注意：RetroFuturaGradle 中 `jar` 任务只产出开发命名空间的 jar，必须经过 `reobfJar` 才能在正式环境中运行，否则一旦调用到原版/Forge 成员就会抛出 `NoSuchMethodError`（例如 `ClientCommandHandler.registerCommand`）。
> 本项目已让 `assemble`（`gradlew build`）自动依赖 `reobfJar`；也可单独执行 `gradlew reobfJar`。

> 提示：本机专属的 Gradle 设置（JDK 安装路径、JVM 参数等）不提交到仓库，请按需写入用户级文件 `<USER_HOME>/.gradle/gradle.properties`。

## 许可

本项目源码基于 **GNU Lesser General Public License v3.0（LGPL-3.0）** 发布，见 [LICENSE](LICENSE)。

Copyright (c) 2026 SiO-0

第三方依赖许可：
- **GTCEu**：LGPL-3.0，© 其各自作者，见上游 [GregTechCEu/GregTech](https://github.com/GregTechCEu/GregTech)
- **ModularUI**：以 [上游仓库](https://github.com/CleanroomMC/ModularUI) 的 LICENSE 为准

本项目基于 [CleanroomMC TemplateDevEnv](https://github.com/CleanroomMC/TemplateDevEnv)（MIT）创建。
