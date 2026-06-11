# What Feature Flags Are

A feature flag is a runtime conditional that controls whether a piece of behavior is active, evaluated against context without requiring a new deployment. It is the mechanism that decouples deploying code from releasing functionality, letting a team merge and ship code that stays dormant until a flag is flipped on. In practice a flag is a named value, usually boolean but sometimes multivariate, looked up at the point in code where the decision matters. The lookup returns a value based on the current rules and the context passed in, such as the user, the environment, or a request attribute. This small indirection is what turns a binary deploy into a controllable, reversible release.

## Decoupling deploy from release

The central benefit of flags is that shipping code and turning on a feature become two separate actions. Without flags, the only way to release is to deploy, which couples risk to your build and rollback pipeline. With flags you can merge to main continuously, deploy whenever, and keep new code behind a flag set to off, a practice often called dark launching. When you are ready, you flip the flag and the feature goes live for the targeted audience in seconds. If it misbehaves, you flip it back rather than scrambling to revert and redeploy.

## The evaluation model

A flag is resolved by evaluating its rules against a context object at the moment the code asks for it. The context typically carries identifiers and attributes like user ID, account tier, region, device, or environment name. Rules are checked in order: explicit targeting first, then segment or percentage rules, then a default fallback value. Good implementations make evaluation fast and local by caching rule sets in memory and updating them through a stream or short poll. Evaluation should also be deterministic, so the same user consistently gets the same result during a gradual rollout.

## Why teams adopt them

Teams adopt flags to reduce the blast radius of change and to release on business time rather than deploy time. Flags enable trunk-based development by letting unfinished work live safely in main behind an off switch. They make gradual rollouts, instant rollback, and A/B testing possible from a single mechanism. They also unlock operational control, like shedding load by disabling an expensive feature during an incident. The cost is added conditional complexity, which is why disciplined cleanup matters as much as adoption.
