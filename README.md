# pipa-edl-kit — 小米平板 6（pipa）免解锁降级 → 解锁 BL 资料包

本仓库整合 **小米平板 6（pipa / 23043RP34C）** 从 HyperOS 2.0 **免解锁降级至 MIUI 14 → 绑定解锁 BL** 所需的全套**资料、工具与执行手册**。

> **先读 [`RUNBOOK.md`](RUNBOOK.md)** —— 完整流程、验证点、救砖预案与风险清单。

## ⚠️ 免责声明

- 仅供**个人设备的玩机研究**使用；所有操作会**清空数据、存在变砖风险**，请自行评估并**提前完整备份**。
- 固件 / 工具的原始版权归各自权利人（小米、高通、酷安 @锐骁、萤火虫资源站等）；本仓库仅作**归档与索引**，不对任何文件提供担保。
- 严禁用于非法用途。

## 目录

| 文件 | 说明 | 校验 |
|---|---|---|
| `RUNBOOK.md` | **执行手册**（流程 / 验证点 / 救砖 / 风险 / 资源档案）| — |
| `SOURCE-README.md` | 原作者说明（含解压码 `HTTENG24HTT25` 与 lun5 操作要点）| ✅ |
| `小米平板6降级小包.7z` | 降级小包①（9008 刷写 / 防回滚处理组合）| ✅ |
| `小米平板6降级小包-2.7z` | 降级小包②（2024-07 更新版）| ✅ |
| `Xiaomi Pad 6 (pipa) ENG Firmware … .7z` | 工厂工程固件（1.71 GB → 解压 3.38 GB / 102 文件）| ✅ |
| `pipa_images_V14_part00/01/02.tgz` | **降级目标**：MIUI 14 官方线刷包（5.33 GB，拆 3 段，合并见下）| ✅ |
| `pipa_images_OS2_part00/01/02/03.tgz` | **救砖保险**：HyperOS 2.0 官方线刷包（6.43 GB，拆 4 段，合并见下）| ✅ |
| `MiFlash.7z` | 9008 免授权刷写工具（解压密码 `pipa`）| ✅ |
| `Qualcomm-HS-USB-QDLoader-9008-Driver.zip` | 高通 9008 驱动 | ✅ |
| `CHECKSUMS.sha256` | 全文件 SHA256 清单 | — |

大文件（`*.7z` / `*.tgz` / `*.zip`）使用 **Git LFS** 管理，克隆需安装 [git-lfs](https://git-lfs.com)。

## 校验

```bash
sha256sum -c CHECKSUMS.sha256   # 校验全部文件
```

两个官方 TGZ 另与官方 MD5 尾缀交叉核对（文件名内嵌）：`…dbc25f30be.tgz`、`…9a0b9b3fc8.tgz`。

### 官方固件分段合并

两个官方包超过 GitHub LFS 单文件上限（2 GiB），已切为 `_partNN.tgz` 分段（各段 SHA256 见 `CHECKSUMS.sha256`）。下载后按序合并并校验：

```bash
# MIUI 14 V14.0.4.0.TMZCNXM（3 段；合并后应为 5,329,505,711 B，MD5 dbc25f30be…）
cat pipa_images_V14_part*.tgz > pipa_images_V14.tgz

# HyperOS 2.0 OS2.0.20.0.UMZCNXM（4 段；合并后应为 6,430,379,139 B，MD5 9a0b9b3fc8…）
cat pipa_images_OS2_part*.tgz > pipa_images_OS2.tgz
```

（`_part*` 通配按字典序展开，顺序即拼接顺序；Windows 下用 `copy /b 各段 目标` 按 段00→段01→… 顺序拼接。）

## 资源来源（索引）

- **降级三件套**：萤火虫资源站（yhcres.top）/ 酷安 @锐骁 工厂包（原帖已删，详见 `RUNBOOK.md` §5）
- **官方固件**：XiaomiFirmwareUpdater 镜像直链（`xmfirmwareupdater.com`）
- **教程**：B 站 **BV1kyEKzHEJe**（pipa 专属全流程，2025-05）

## 免责与红线（执行前必读）

绑定 / 解锁存在**"卡 144"（满 168h 仍被拒）与概率拉黑**风险，不可控；请先阅读 `RUNBOOK.md` §6 风险与红线 与 §7 决策检查点，确认自身风险承受能力后再动手。