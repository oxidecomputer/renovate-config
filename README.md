# renovate-config

Oxide's self-hosted Renovate runner and shared configuration

## Running Renovate against a new repository

Renovate is available as a Mend hosted service or a self-hosted GitHub action. The [Renovate docs](https://docs.renovatebot.com/getting-started/use-cases/) describe the process of enabling the Mend hosted variant. To enable the Oxide self-hosted version the repository will need to be added to the allow list in `runner/config.json`. Once the change is merged to main, our self-hosted version of Renovate will start running against the repository.

### Why use the self-hosted version?

If your repository requires the use of post upgrade scripts, then you will need to use the self-hosted version instead of the Mend hosted version. Our self-hosted version also declares an allow list of expected script locations that are allowed to be run: [global config](runner/global.json). To make this easier you can extend the `post-upgrade` configuration file from this repository in your `renovate.json` configuration file.

## Default configuration

Any presets that you want to enable across all repos with Renovate enabled in Oxide's GitHub organization can be added to `default.json`. Avoid putting any rules directly in default, instead using separate preset files for a cleaner configuration.

## Rust configuration

By default, the Rust configuration does not automatically create branches (instead requiring users
to manually approve dependencies in the dependency dashboard).

To enable automatic branch creation, in your repository's `renovate.json`, extend from
`local>oxidecomputer/renovate-config//rust/autocreate` _after_ extending from the global preset.
This will enable:

- Automatic branch creation for dependencies
- Lockfile updates every Monday morning Pacific time

## Running post upgrade scripts

To run post-upgrade scripts:

1. Check in an executable script at the location `tools/renovate-post-upgrade.sh` in your repository.
2. Ensure you're using self-hosted Renovate, and add your repository to the list in the [global config](runner/global.json).
3. In your repository's `renovate.json`, extend from `local>oxidecomputer/renovate-config:post-upgrade`.

## More info

To learn more about how to include these shared config files in your own Renovate setup see Renovate's [preset hosting](https://docs.Renovatebot.com/config-presets/#preset-hosting) documentation.

## Future plans

### Pinning GitHub Actions digests

We may make it a requirement very soon for GitHub Actions digests to be pinned to a hash. To enable
pinning, plus automerging updates to some allowlisted actions (to reduce developer burden), extend
from `local>oxidecomputer/renovate-config:actions/pin` in your `renovate.json`.

If you have access to Oxide RFDs, see [RFD 434](https://rfd.shared.oxide.computer/rfd/0434) for more.

### Automatic merges

We currently do not perform any automatic merges of dependency PRs, but in the near future we might
want to enable automerges for allowlisted crates on an opt-in basis. Instructions to do so will be
added here.
