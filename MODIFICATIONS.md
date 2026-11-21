# 修改说明（基于 QCYTSN/dsh-dafeiyu）

本目录是 [QCYTSN/dsh-dafeiyu](https://github.com/QCYTSN/dsh-dafeiyu) **v0.1.23** 的自用修改版。
在官方版本基础上做了以下定制，供个人使用。

## 改动清单

| 改动 | 涉及文件 | 说明 |
|---|---|---|
| 任务结束立即刷新余额 | `src/plugin.js` | 每个任务回合结束（`turn/end`）立即强制刷新一次余额，不再只等 60 秒轮询 |
| 气泡默认隐藏 | `cordis.patch.yml` | `bubbleMode: always → hidden`，平时不显示气泡 |
| 任务完成自动弹气泡 | `runtime/helper.py` | 任务完成（SUCCESS）时气泡自动显示 8 秒，然后自动收起 |
| 点击交互与切换分离 | `runtime/helper.py` | 点击桌宠本体只播互动动画（摸头/戳尾巴/戳身体）；点击气泡本身才收起 |
| 隐藏时的泡泡把手 | `runtime/helper.py` | 气泡隐藏时鱼头顶出现一个「吐出的泡泡」把手，点击它重新显示气泡（径向渐变 + 高光，模拟真实泡泡） |
| 重新打包 Windows Helper | `runtime/bin/win32-x64/dsh-dafeiyu-helper.exe` | 用 PyInstaller 重新打包了包含以上 Python 改动的 Helper |

## 运行时配置（非代码改动）

以下通过 `$DSH_HOME/dsh-dafeiyu/user-settings.json` 配置（不在本仓库内）：

```json
{
  "version": 1,
  "overrides": {
    "scale": { "value": 0.55, "host": 1 },
    "bubbleScale": { "value": 0.8, "host": 1 }
  }
}
```

- `scale: 0.55` — 角色大小（最小档）
- `bubbleScale: 0.8` — 气泡大小（最小档）

## 安装

```bash
# 从 tgz 安装
dsh plugin --profile <你的 profile> add dsh-dafeiyu-custom-0.1.23.tgz

# 或从本地目录安装
dsh plugin --profile <你的 profile> add ./dsh-dafeiyu-custom
```

官方桌面端请在应用内「插件 → 添加插件」填入 `.tgz` 完整路径。

## 重新打包 Helper（改动了 `runtime/helper.py` 之后才需要）

```powershell
# 需要 Python 3 且已安装 PySide6 与 PyInstaller
pip install "PySide6>=6.7,<7" pyinstaller
node scripts/build-helper.mjs
```

## 版权与授权

- **代码**：MIT，版权归 [QCYTSN/dsh-dafeiyu](https://github.com/QCYTSN/dsh-dafeiyu) 及其贡献者。
- **角色素材（动画/形象）**：**CC BY-NC-SA 4.0（禁止商用）**，出处：
  - 桌宠动画来自 [PC2005-cloud/dsh-pet](https://github.com/PC2005-cloud/dsh-pet)（MIT 代码，素材 CC BY-NC-SA 4.0）
  - 大肥鱼（鲸鱼娘）形象为社区二创，非 DeepSeek 官方形象；原型「溟月」出自 B 站 [@上善无形](https://space.bilibili.com/4456176)，DeepSeek 版（女仆鲸鱼娘）出自 B 站 [@ZipZipPipe](https://space.bilibili.com/4168597)
  - 详见 `ASSET_LICENSE.md` 与 `assets/dsh-pet-LICENSE.txt`

> 本项目仅供个人非商业使用。请勿将角色素材用于任何商业用途。
