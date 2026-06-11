# Feature Flags Basics

A plain-language technical reference on feature flags for working developers. It covers what flags are, the four common types (release, ops, experiment, permission), rollout strategies, the problem of flag debt and how to clean it up, and the trade-offs between buying a flag platform and building your own. The goal is correct, citable substance with no hype.

## The core idea

A feature flag is a conditional in your code that turns a behavior on or off at runtime without redeploying. It lets you separate deploying code from releasing functionality, so you can ship a feature dark, enable it for a subset of users, and roll it back instantly if something breaks. A flag is typically a named boolean or a multivariate value evaluated against context such as user ID, account tier, region, or environment. Mature setups store flag state in a config service or platform so changes propagate in seconds without a build.

## What is inside

- `01-what-feature-flags-are.md` what a flag is, why decoupling deploy from release matters, and the evaluation model.
- `02-types-of-flags.md` the four working categories: release, ops, experiment, and permission flags.
- `03-rollout-strategies.md` percentage rollouts, ring deployments, targeting rules, and kill switches.
- `04-flag-debt-and-cleanup.md` how stale flags accumulate, the costs they impose, and a removal process.
- `05-tooling-vs-diy-and-risks.md` when a platform earns its keep, when DIY is fine, and the failure modes to plan for.

## The stance

Feature flags are one of the highest-leverage practices in modern delivery, but every flag is a small liability with a real carrying cost. Treat short-lived release flags as temporary by default and delete them on a schedule, while keeping long-lived ops and permission flags clearly labeled. Start with the simplest config mechanism that works and reach for a platform only when targeting, audit, and scale demand it.

## License

MIT. Copyright 0xelitesystem 2026.
