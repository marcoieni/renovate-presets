# rust-lang Renovate presets

Shared [Renovate](https://docs.renovatebot.com/) presets for repositories in the Rust Project, maintained
by the Infrastructure Team.

## Presets

- `base`: extends [`config:recommended`](https://docs.renovatebot.com/presets-config/#configrecommended),
  and enables vulnerability alert PRs.
- `actions`: enables GitHub Actions updates, pinning action digests to SemVer-compatible refs.
  All GitHub Actions updates are grouped into a single PR and scheduled weekly.
  *(extends `base`)*
- `lockfile`: enables weekly lock file updates (e.g. `cargo update`) and disables
  PRs for non-breaking updates for Rust, JavaScript, and TypeScript packages.
  This is because lock file updates already include non-breaking updates.
  Breaking updates (e.g. `1.2.3` to `2.0.0`) are updated into separate PRs.
  *(extends `base`)*
- `default`: *(extends `actions` and `lockfile`)*.
  This is the recommended preset for most repositories in the Rust Project.

## Use In A Repository

Use the `default` preset:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>rust-lang/renovate-presets"]
}
```

## Personalization

Both the `actions` and `lockfile` presets default to Renovate's
[`schedule:weekly`](https://docs.renovatebot.com/presets-schedule/#scheduleweekly)
preset, which resolves to Monday before 4 AM.

To override them in a repository:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>rust-lang/renovate-presets"],
  "lockFileMaintenance": {
    "extends": ["schedule:monthly"]
  },
  "packageRules": [
    {
      "matchManagers": ["github-actions"],
      "schedule": ["* * * * 0,6"]
    }
  ]
}
```

> [!NOTE]
> `schedule:monthly` means "on the first day of the month, before 4AM".
> See the [Schedule Presets](https://docs.renovatebot.com/presets-schedule/#schedulemonthly) documentation for more details.

## References

- [Shareable Config Presets](https://docs.renovatebot.com/config-presets/)
- [Schedule Presets](https://docs.renovatebot.com/presets-schedule/)
- [Configuration Options](https://docs.renovatebot.com/configuration-options/)
