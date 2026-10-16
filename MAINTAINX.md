# MaintainX fork of policy-bot

This fork exists to run [palantir/policy-bot#1363](https://github.com/palantir/policy-bot/pull/1363)
(`policy_from_default_branch`) before it is released upstream. It unblocks GitHub's native
stacked pull requests in MaintainX/maintainx ([BF-8653](https://linear.app/maintainx/issue/BF-8653)).

- `maintainx/v1.41.2`: upstream `v1.41.2` plus the two #1363 commits, cherry-picked, and a
  test-only import fix (`go-github/v89`, the version v1.41.2 vendors).
- Tags `v1.41.2-mx.N` publish `policy-bot/policy-bot:1.41.2-mx.N` to the tooling ECR
  (`154574718005.dkr.ecr.ca-central-1.amazonaws.com`) through
  `.github/workflows/maintainx-release.yml`, built with upstream's own toolchain (`godelw`).
  The ECR repo and push role live in atmos-infra (`stacks/catalog/apps-tooling/policy-bot.yaml`);
  only release tags can use the `Tooling` environment the role trusts.
- Deployed by [MaintainX/mx-policy-bot](https://github.com/MaintainX/mx-policy-bot).

Drop this fork once an upstream release includes #1363: point mx-policy-bot back at
`palantirtechnologies/policy-bot` and keep `policy_from_default_branch: true`.
