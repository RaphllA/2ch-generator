---
description: 同步2ch-generator到site-publish并部署
---

# 同步 2ch-generator 到 site-publish

当你修改了 `2ch-generator` 的内容（帖子、样式、脚本等），需要同步到 `site-publish/2ch/` 才能在线上生效。

## 步骤

// turbo-all

1. 同步文件（镜像复制，排除 .git 目录）：
```powershell
robocopy "F:\所长的谣言\2ch-generator" "F:\所长的谣言\site-publish\2ch" /MIR /XD .git /NJH /NJS
```
> 注意：robocopy 返回 exit code 1 表示文件已成功复制，不是错误。

2. 查看变更：
```powershell
git -C "F:\所长的谣言\site-publish" status --short -- 2ch/
```

3. 提交并推送（把 `<描述>` 替换为本次更新内容）：
```powershell
cd "F:\所长的谣言\site-publish" ; git add 2ch/ ; git commit -m "sync: 2ch <描述>" ; git push
```

4. 等待 GitHub Pages 部署完成（通常1-2分钟），然后刷新 https://tukuyomi.cc.cd/2ch/ 验证。
