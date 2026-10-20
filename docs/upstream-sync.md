# 自动同步上游

`.github/workflows/sync-upstream.yml` 每天新加坡时间 09:17 将
`xkinput/KeyTao` 的 `master` 合并到本仓库的默认分支。
也可以在 Actions → Sync upstream → Run workflow 手动运行。

将工作流提交并推送到默认分支后，在 GitHub Actions 页面启用工作流
（fork 的定时工作流可能需要手动启用）。使用内置 `GITHUB_TOKEN`，无需添加 Secret。
仓库规则需要允许 Actions 写入默认分支；若分支保护要求 PR，则直接推送会失败。

同步使用普通 Git 合并，保留本仓库的提交，不会强制覆盖历史。
出现冲突时工作流失败且不推送，请在本地合并上游、解决冲突后推送，再重试。
没有更新时不会创建提交。并发推送导致远端更新时，本次推送会安全失败，可重新运行。

若上游修改了 `.github/workflows/`，内置令牌可能因缺少工作流写入权限而无法推送；
此时请在本地完成同步并推送。同步不会自动同步标签或发布 Release。
