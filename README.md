# .github

本仓库用于存放 wmy2981 账号下的默认社区健康文件（default community health files）。

## FUNDING.yml

`.github/FUNDING.yml` 为用户级默认收款配置，账号下所有**未自带** `FUNDING.yml` 的仓库都会继承它，收款链接：

- 爱发电：https://afdian.com/a/wmy2981

路径按官方文档要求放在 `.github` 文件夹内；文档同时给出的优先级为 `.github` 文件夹 → 仓库根目录 → `docs` 文件夹，实测根目录与 `.github` 文件夹两种位置都能被识别。

## 重要：Sponsor 按钮需要两层配置

GitHub 的 Sponsor 按钮由两个独立开关共同决定，缺任意一个，仓库页面上都不会出现按钮：

1. **捐款链接**：账号级 `.github/FUNDING.yml`（即本仓库），或由仓库自身的 `.github/FUNDING.yml` 覆盖。
2. **仓库开关**：该仓库的 `Settings → General → Features → Sponsorships`，对应 GraphQL 字段 `hasSponsorshipsEnabled`。

新建仓库时第 2 个开关默认关闭，需要手动打开，或执行一次 GraphQL：

```graphql
mutation {
  updateRepository(input: {repositoryId: "<repo node id>", hasSponsorshipsEnabled: true}) {
    repository { nameWithOwner hasSponsorshipsEnabled }
  }
}
```

因此本仓库的默认文件只解决了第 1 层；每个新增仓库仍需自行开启第 2 层。
fork 仓库不会被改动，其按钮状态取决于 fork 自身的 `hasSponsorshipsEnabled`。

参考文档：[Displaying a sponsor button in your repository](https://docs.github.com/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/displaying-a-sponsor-button-in-your-repository)
