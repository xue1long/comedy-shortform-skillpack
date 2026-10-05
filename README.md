# Comedy Shortform Skill Pack

用于创作和诊断可拍喜剧短剧的 Codex Skills。未指定时长时，主入口以 60 秒为规划参考；用户可以指定其他目标时长。初稿会标注估算时长，并给出具体的精简或补充方向。

需要调用示例、输入模板和完整改稿流程，请看 [使用说明](USAGE.md)。

## 当前发布内容

`publish` 分支的 `.agents/skills/` 是安装来源，目前包含 **62 个 Skill**：

- **5 个项目入口**：完整写作、喜剧机制、Sketch 结构、双主角结构和剧本诊断。
- **9 个书籍 Pack 路由**：`comic-toolbox`、`art-of-character`、`hidden-tools-comedy`、`comedy-writers-companion`、`comedy-bible`、`writing-dialogue`、`screenplay`、`comedy-movie`、`sitcom`。
- **48 个细分 Skill**：由路由 Skill 按任务选择，可单独调用。

常用入口：

| Skill | 用途 |
| --- | --- |
| [`comedy-shortform-writer`](.agents/skills/comedy-shortform-writer/SKILL.md) | 从创意或已有剧本写短剧初稿、估算时长并给出修改方向。 |
| [`comedy-engine`](.agents/skills/comedy-engine/SKILL.md) | 提炼可重复、可变化的喜剧规则。 |
| [`structure-sketch`](.agents/skills/structure-sketch/SKILL.md) | 设计 Sketch 的建立、变化与兑现。 |
| [`structure-duo`](.agents/skills/structure-duo/SKILL.md) | 设计双主角目标、攻防与权力变化；可与 Sketch 叠加。 |
| [`script-diagnosis`](.agents/skills/script-diagnosis/SKILL.md) | 诊断已有剧本；只有明确要求改稿时才定向重写。 |

主入口按其工作流阶段表加载相应路由和细分 Skill。仓库的 [`skills/SKILL.md`](skills/SKILL.md) 是主入口的单文件镜像；安装整套 Skill 时请使用 `.agents/skills/`，以保留它引用的其他 Skill。

## 写作与时长

主入口支持完整创作与改稿。初稿偏离目标时长时，会如实标注估算和可改段落；偏离目标本身不代表初稿失败。只有用户明确要求成片时长或硬上限时，才按该要求修订并复核。

完成创作或改稿时，主入口依次输出：

1. 创意或原稿摘要与保留项／假设。
2. 喜剧形式与人物配置。
3. 连续时间码 Beat Sheet。
4. 包含动作和对白的短剧本。
5. 诊断和本轮修订点。

例如，先说“以 60 秒为目标写完整初稿，保留所有有效笑点，给出估算和建议剪辑点”；看完后再说“把这份稿子精简到不超过 60 秒，保留核心机制和结尾兑现”。如果一开始就要求成片版或硬上限，主入口会直接按该限制整理成稿。

如果关键事实或核心要求冲突，或者必须改动用户指定的原稿保留项，主入口会先询问取舍。

## 安装

在 PowerShell 中运行以下命令。Codex 可从仓库内的 `.agents/skills/` 发现项目 Skill；命令会将整套 Skill 复制到当前用户的 `$HOME/.agents/skills/`。安装前会检查源文件和同名目标目录，遇到冲突即停止，不覆盖已有 Skill。

```powershell
git clone https://github.com/xue1long/comedy-shortform-skillpack.git
cd comedy-shortform-skillpack

$sourceRoot = Join-Path (Get-Location) '.agents\skills'
$targetRoot = Join-Path $env:USERPROFILE '.agents\skills'
$skillDirs = @(Get-ChildItem -LiteralPath $sourceRoot -Directory)
if ($skillDirs.Count -eq 0) { throw 'No skills found in .agents/skills' }

foreach ($dir in $skillDirs) {
    if (-not (Test-Path -LiteralPath (Join-Path $dir.FullName 'SKILL.md'))) {
        throw "Missing SKILL.md: $($dir.Name)"
    }
    if (Test-Path -LiteralPath (Join-Path $targetRoot $dir.Name)) {
        throw "Skill already exists: $($dir.Name)"
    }
}

New-Item -ItemType Directory -Path $targetRoot -Force | Out-Null
foreach ($dir in $skillDirs) {
    Copy-Item -LiteralPath $dir.FullName -Destination (Join-Path $targetRoot $dir.Name) -Recurse
}
"Installed $($skillDirs.Count) skills"
```

安装后开启新的 Codex 对话，让客户端重新扫描 Skill。完整创作或改稿选 `comedy-shortform-writer`；只提炼喜剧机制选 `comedy-engine`；只诊断已有稿件选 `script-diagnosis`。

## 检查

可在仓库根目录核对实际发布的 Skill 目录及其入口文件：

```powershell
$skillDirs = @(Get-ChildItem '.agents\skills' -Directory)
$missing = @($skillDirs | Where-Object { -not (Test-Path -LiteralPath (Join-Path $_.FullName 'SKILL.md')) })
if ($missing.Count -gt 0) { throw "Missing SKILL.md: $($missing.Name -join ', ')" }
"Found $($skillDirs.Count) skills"
```

当前 `publish` 分支没有 `evaluations/check-package.ps1`、`evaluations/rubric.md` 或 `evaluations/` 测试目录，因此不提供自动验收命令。目录检查只证明文件存在；Codex 中能否发现和触发 Skill、剧本是否可拍，以及成片时长，仍需分别在客户端试用、朗读和试拍验证。
