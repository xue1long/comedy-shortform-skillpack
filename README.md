# Comedy Shortform Skill Pack

一组可独立调用的 Codex Skills，用于创作或诊断可拍喜剧短剧。默认以 60 秒为规划参考；用户可指定其他时长，初稿会记录估算时长，并可继续精简或补充。

## Skills

- **`comedy-shortform-writer`**：从一句创意或已有剧本写短剧初稿，估算时长并给出后续修改方向；主入口自足，不依赖辅助 Skill 自动加载。
- **`comedy-engine`**：提炼可重复、可变化的喜剧规则。
- **`structure-sketch`**：设计 Sketch 的建立、变化与兑现。
- **`structure-duo`**：设计双主角目标、攻防与权力变化；可与 Sketch 叠加。
- **`script-diagnosis`**：诊断已有剧本，并在明确授权时做一次定向改写。

## 适用范围与输出

主入口支持完整创作与改稿。未指定时长时以 60 秒为规划参考；用户明确要求其他时长时按该目标继续。初稿时长偏离目标时，标注估算并指出后续精简或补充方向。只有用户明确要求成片时长或硬上限时，才按该要求修订并验收。

验收量表检查时间码和时长估算是否自洽、偏离目标时是否给出可执行的精简或补充方向。试读用于验证估算并指导修改；初稿偏离目标本身不判失败。量表见 `evaluations/rubric.md`。

完成创作或改稿时，主入口依次输出：

1. 创意或原稿摘要与保留项／假设。
2. 喜剧形式与人物配置。
3. 时间码 Beat Sheet。
4. 短剧本。
5. 诊断和本轮修订点。

时长调整可以分两轮完成。第一轮先写完整初稿，标出时长估算和建议精简／补充的位置；你决定调整方向后，再要求压到成片上限或补足到目标长度。精简会先合并重复节拍、压缩冗长对白，同时保留核心笑点的建立、升级和兑现；不会只重标时间码。

例如：先说“以 60 秒为目标写完整初稿，保留所有有效笑点，给出估算和建议剪辑点”；看完后再说“按你建议的方案，把这份稿子精简到不超过 60 秒，保留核心机制和结尾兑现”。如果你一开始就要求成片版或硬上限，主入口会直接按该限制整理成稿。

如果关键事实冲突、核心要求冲突，或需要改动用户要求保留的原稿核心项，先提问并暂停完整剧本。只有明确的成片时长或制作限制仍未满足时，才标注「待修改稿」并说明原因。

## 安装

在仓库根目录运行 PowerShell。Codex 从仓库的 `.agents/skills` 发现项目 Skill，也从 `$HOME/.agents/skills` 发现用户 Skill。本包测试应在隔离测试目录的 `.agents/skills` 下准备技能；通过 Task 8 测试环境验收后，用户侧安装目标为 `$HOME/.agents/skills`。遇到任何同名 Skill 时停止，不覆盖已有目录。

```powershell
$sourceRoot = Join-Path (Get-Location) 'skills'
$targetRoot = Join-Path $env:USERPROFILE '.agents\skills'
$names = @('comedy-shortform-writer','comedy-engine','structure-sketch','structure-duo','script-diagnosis')
foreach ($name in $names) {
    if (-not (Test-Path -LiteralPath (Join-Path $sourceRoot "$name\SKILL.md"))) { throw "Missing source Skill: $name" }
}
New-Item -ItemType Directory -Path $targetRoot -Force | Out-Null
foreach ($name in $names) {
    if (Test-Path -LiteralPath (Join-Path $targetRoot $name)) { throw "Skill already exists: $name" }
}
foreach ($name in $names) {
    Copy-Item -LiteralPath (Join-Path $sourceRoot $name) -Destination (Join-Path $targetRoot $name) -Recurse
}
```

安装步骤只是 Task 8 通过后的用户侧交付步骤（Task 9）；在此之前不得复制到用户目录。CLI runtime 检查和 Codex 桌面版技能选择器检查是两种独立证据：`codex.exe exec` 可用于非 UI 的 CLI 检查，但不能替代桌面版选择器、触发行为、读者反馈或计时试读。比如，完整创作或改稿选 `comedy-shortform-writer`；只提炼喜剧机制选 `comedy-engine`；只诊断已有稿件选 `script-diagnosis`。

## 检查

在仓库根目录运行静态包检查：

```powershell
pwsh -NoProfile -File evaluations/check-package.ps1
```

也可以只检查一个 Skill：

```powershell
pwsh -NoProfile -File evaluations/check-package.ps1 -Only comedy-shortform-writer
```

静态检查验证文件、frontmatter、必要栏目，以及主入口的四个包内相对引用和对应目标文件；它不证明 Skill 在 Codex 中可发现、触发正确、剧本通过试读或短于 60 秒。场景、触发测试和人工评估量表见 `evaluations/`。
