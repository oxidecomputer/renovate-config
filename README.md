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
to manually check for dependencies). To enable automatic branch creation, in your repository's
`renovate.json`, extend from `local>oxidecomputer/renovate-config:rust/autocreate` _after_ extending
from the global preset.

## Running post upgrade scripts

To run post-upgrade scripts:

1. Check in an executable script at the location `tools/renovate-post-upgrade.sh` in your repository.
2. Ensure you're using self-hosted Renovate, and add your repository to the list in the [global config](runner/global.json).
2. In your repository's `renovate.json`, extend from `local>oxidecomputer/renovate-config:post-upgrade`.

## More info

To learn more about how to include these shared config files in your own Renovate setup see Renovate's [preset hosting](https://docs.Renovatebot.com/config-presets/#preset-hosting) documentation.
