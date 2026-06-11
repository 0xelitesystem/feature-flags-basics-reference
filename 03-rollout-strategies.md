# Rollout Strategies

A rollout strategy is the rule set that decides which users see a feature and how exposure expands over time, ranging from a flat percentage to ring-based and attribute-targeted schemes. The point of any strategy is to limit blast radius: expose the change to a small, observable slice first, watch your metrics, then widen. Good strategies are deterministic so individual users get a stable experience, and they pair with a fast off switch so you can reverse course instantly. The right choice depends on how risky the change is and how much you can measure as it spreads. Below are the strategies most teams reach for.

## Percentage rollouts

A percentage rollout exposes the feature to a defined fraction of users and increases that fraction over time. The key requirement is deterministic bucketing: hash a stable identifier like user ID with the flag key so the same user stays in or out as the percentage grows. This stickiness prevents users from flickering between old and new behavior as you ramp. A common cadence is something like 1 percent, then 10, 25, 50, and 100, pausing at each step to confirm error rates and latency hold. Always bucket on a stable ID, never on a per-request random number.

## Ring deployments

Ring deployments expand exposure through concentric audiences ordered by risk tolerance. A typical sequence is internal staff first, then a small set of beta or canary users, then the broad population. Each ring acts as a checkpoint where you validate behavior before promoting to the next, wider ring. This approach is well suited to high-risk changes because the people most able to absorb and report problems see them first. Rings are often combined with percentage rollouts inside the final, largest ring.

## Targeting and segmentation

Targeting rules expose a feature based on user or request attributes rather than a blind percentage. Rules evaluate context such as region, account tier, device type, or membership in a named segment. This is how you do geographic staged launches, enable a feature only for paying customers, or hand specific accounts early access. Rules are evaluated in order, so put explicit allow and block lists before broad percentage rules. Targeting is also how experiment assignment and permission gating are expressed.

## Kill switches and rollback

A kill switch is a flag whose only job is to disable a feature instantly when something goes wrong. The defining property of flag-based rollout is that reversal is a config change, not a redeploy, so recovery takes seconds. Keep kill switches simple, well named, and tested, because you will reach for them under pressure during an incident. Pair every risky rollout with a clear default value so that if the flag system itself is unavailable, the code falls back to safe behavior.
