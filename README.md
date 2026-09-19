# simadmin-ywt

SimAdmin **发行仓库** — 提供设备一键安装脚本与 OTA 发布包。

SimAdmin 是 Qualcomm msm8916 平台的调制解调器管理平台（VoLTE / VoWiFi / 短信 / eSIM）。源码在私有仓库开发，本仓库仅发布：

- `install_latest.sh` — 一键安装 / 升级脚本（支持 Debian / Ubuntu / **OpenWrt**）
- `scripts/` — systemd / modem-recovery 服务文件
- Releases — 各架构 OTA 发布包（`simadmin-{aarch64,armv7,x86_64}.tar.gz`）

> **说明**：本项目**不区分版本变体** — 默认发布包即为**全功能版本**，包含 VoLTE、VoWiFi、短信等全部能力，安装时无需选择。

## 一键安装

Debian / Ubuntu（systemd）：

```sh
curl -fsSL https://raw.githubusercontent.com/WynnYAY/simadmin-ywt/main/install_latest.sh | sh
```

OpenWrt（自动探测 `/etc/openwrt_release`，使用 procd init 脚本，无需 systemd / NetworkManager）：

```sh
curl -fsSL https://raw.githubusercontent.com/WynnYAY/simadmin-ywt/main/install_latest.sh | sh
```

安装指定版本：

```sh
sh install_latest.sh -v1.1.39
```

## 常用环境变量

| 变量 | 默认 | 说明 |
| --- | --- | --- |
| `VERSION` | `latest` | 指定安装版本 |
| `INSTALL_DIR` | `/opt/simadmin` | 安装目录 |
| `GH_PROXY` | `https://gh-proxy.com/` | GitHub 下载加速镜像（自动多级回退） |
| `SIMADMIN_VERIFY_ASSET` | `auto` | 发布包 SHA-256 校验（`auto`/`1`/`0`） |
| `SIMADMIN_ASSET_SHA256` | — | 手动指定期望摘要 |
| `SIMADMIN_SKIP_HEALTHCHECK` | `0` | 跳过安装后 `/api/health` 健康检查 |

更多选项见 `sh install_latest.sh --help`。

## OTA 更新源

- 官方源：<https://github.com/3899/SimAdmin>
- 本仓库（个人源）：<https://github.com/WynnYAY/simadmin-ywt/releases/latest>

## License

GPL-3.0，与上游 [SimAdmin](https://github.com/3899/SimAdmin) 一致。
