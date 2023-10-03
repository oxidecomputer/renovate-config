# renovate-config

Oxide's self-hosted Renovate runner and shared configuration

## Running Renovate against a new repository

## Default configuration

Any presets that you want to enable across all repos with Renovate enabled in Oxide's GitHub organization can be added to `default.json`. Avoid putting any rules directly in default, instead using separate preset files for a cleaner configuration.

## Running post upgrade scripts

## More info

To learn more about how to include these shared config files in your own Renovate setup see Renovate's [preset hosting](https://docs.Renovatebot.com/config-presets/#preset-hosting) documentation.
