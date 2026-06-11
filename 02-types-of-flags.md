# Types of Flags

Feature flags fall into four working categories that differ mainly by lifespan and who controls them: release, ops, experiment, and permission flags. Release flags are short-lived and exist to manage the rollout of in-progress work. Ops flags are operational switches controlled by engineers and on-call staff. Experiment flags drive measurement and are tied to an analysis window. Permission flags are long-lived and gate behavior by who the user is. Classifying a flag at creation time tells you how long it should live and when it should be removed, which is the single most useful habit for keeping flag count under control.

## Release flags

Release flags exist to control the rollout of new or in-progress functionality and should be the most common type. They are deliberately short-lived: once a feature is fully rolled out and stable, the flag has done its job and should be deleted. Typical lifespan is days to a few weeks, and they are usually toggled by the engineers shipping the work. Because they are temporary, they accumulate the fastest and cause the most debt when teams forget to remove them.

## Ops flags

Ops flags are operational switches that let engineers change system behavior in production without a deploy, often during incidents. Common examples include kill switches for an expensive or risky feature, circuit breakers around a flaky dependency, and toggles that shed load by disabling nonessential work. These flags tend to be longer-lived than release flags because they are part of your operational toolkit. They are typically owned by the platform or on-call team and should be clearly labeled so nobody deletes them thinking they are stale release flags.

## Experiment flags

Experiment flags split traffic between variants to measure the effect of a change on a metric, the engine behind A/B and multivariate tests. Each user is assigned deterministically to a variant so their experience stays consistent for the duration of the test. The flag lives exactly as long as the experiment needs to reach statistical significance, then it is removed and the winning variant is made permanent. Discipline matters here because abandoned experiments leave branched code paths that quietly rot.

## Permission flags

Permission flags gate behavior based on who the user is, such as plan tier, role, or beta enrollment. Unlike release flags, these are intentionally long-lived because they encode a durable product rule like entitlements or premium access. They are often managed by product or business stakeholders rather than purely by engineering. Because they persist, they should be documented as product configuration, not treated as temporary toggles awaiting cleanup.
