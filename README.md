# renovate-config

This is [Shareable Config Presets](https://docs.renovatebot.com/config-presets/) for SpotOn. It contains wide-use [Renovatebot](https://github.com/renovatebot/renovate) configs, based on our toolset and mindset.

* [Usage](#usage)
* [Development notes](#development-notes)
* [Useful links](#useful-links)
  * [Renovate App and presets configuration](#renovate-app-and-presets-configuration)
  * [Repos configuration](#repos-configuration)
* [Troubleshooting](#troubleshooting)

## Usage

<!-- markdownlint-disable-next-line no-inline-html -->
<details><summary><u>If Renovate has already been activated for repo</u></summary>

1. Check for `renovate.json` in [possible locations](https://docs.renovatebot.com/getting-started/installing-onboarding/#configuration-location).
2. Change `renovate` config to:

    ```json5
    {
      "$schema": "https://docs.renovatebot.com/renovate-schema.json",
      "extends": [
        "local>SpotOnInc/renovate-config"
      ]
    }
    ```

Go to step 3. below.
<!-- markdownlint-disable-next-line no-inline-html -->
</details>

Otherwise:

0. If the repo is too much outdated - prefer to update manually as much as you can before merging Renovate init PR.
1. Activate [Renovatebot Github App](https://github.com/marketplace/renovate) for your repo or ask Github org administrators.
2. Renovate will create [init [PR](https://docs.renovatebot.com/getting-started/installing-onboarding/#repository-onboarding) for the new repo - open it and check that it has:

    ```json5
    {
      "$schema": "https://docs.renovatebot.com/renovate-schema.json",
      "extends": [
        "local>SpotOnInc/renovate-config"
      ]
    }
    ```

3. (Optional) We recommend moving the config to `.github/renovate.json5`.
4. Be sure that the `Dependency graph` and `Dependabot alerts` are enabled for the repo. [Details](https://docs.renovatebot.com/configuration-options/#vulnerabilityalerts).

5. Merge PR and relax.  
   Renovate will create PRs based on provided schedules.  By default - you will see Renovate PRs on Mondays.

## Development notes

To change the default config, please edit [`default.template.json5`](default.template.json5) and create PR.

`default.json` will be automatically [generated and added](.github/workflows/generate-renovate-config.yaml) after your PR will be merged.

That needs to describe what settings do and save `renovate-config/default.json` name magic which [is not present for `.json5`](https://github.com/renovatebot/renovate/issues/15370#issuecomment-1113137651).

---

In case when new `default.json` config does not apply more than 6 hours - create test repo and copy-paste the whole `default.json`, but rename it to `renovate.json`. Renovatebot will test the configuration and create issues if it found problems with the configuration. Or you can ask ChatGPT :)

## Useful links

* [How Renovate find/create/update PRs](https://docs.renovatebot.com/key-concepts/pull-requests/)  
  TL;DR: Renovatebot checks branch names and PR titles. If PR is not found to match the branch - Renovatebot will create a new PR.  
  To recreate closed PR - just rename closed PR.

### Renovate App and presets configuration

* [Managing config for many repositories](https://docs.renovatebot.com/key-concepts/presets/#managing-config-for-many-repositories)
* [Shareable Config Presets](https://docs.renovatebot.com/config-presets/#shareable-config-presets)
  * [Organization level presets](https://docs.renovatebot.com/config-presets/#organization-level-presets) -  `myorg/renovate-config/default.json` magic name
  * [GitHub-hosted Presets](https://docs.renovatebot.com/config-presets/#github-hosted-presets)
  * [Contributing to presets](https://docs.renovatebot.com/config-presets/#contributing-to-presets)
  * [Preset Versioning](https://docs.renovatebot.com/config-presets/#github)

* [Managers: Supported, configuration, disabling, etc.](https://docs.renovatebot.com/modules/manager/)

* [Renovate App on GitHub Secrets Encryption](https://docs.renovatebot.com/getting-started/private-packages/#mend-renovate-hosted-app-encryption)

* [Known limitations](https://docs.renovatebot.com/known-limitations/)  
  Ie: GitHub hosted app Mend checks each active repository roughly every three hours, if no activity has been seen before then (merged PRs, etc).

  * [No rebasing if you have made edits](https://docs.renovatebot.com/updating-rebasing/#no-rebasing-if-you-have-made-edits) (conflicting with pre-commit auto-fixes)

* [onboardingConfigFileName](https://docs.renovatebot.com/self-hosted-configuration/#onboardingconfigfilename) (self-hosted only).  
  Useful to change onboarding Renovate config file location.

* [Docker Registries authentication](https://docs.renovatebot.com/docker/#registry-authentication)


### Repos configuration

* [Configuration location](https://docs.renovatebot.com/getting-started/installing-onboarding/#configuration-location)

* [Overriding global configs](https://docs.renovatebot.com/key-concepts/automerge/#overriding-global-automerge)

* [Scheduling syntax](https://docs.renovatebot.com/key-concepts/scheduling/#scheduling-syntax)
  * [Schedule Presets](https://docs.renovatebot.com/presets-schedule/)

* [Changing the Semantic Commit type](https://docs.renovatebot.com/semantic-commits/#changing-the-semantic-commit-type)
* [How to edit branch names, commit messages, PR titles, and PR content](https://docs.renovatebot.com/configuration-templates/)
* [Docker Digest pinning and Updating](https://docs.renovatebot.com/docker/#digest-pinning)
* [Separate `patch` and `minor` releases of dependencies into separate PRs](https://docs.renovatebot.com/presets-default/#separatepatchreleases).  
  More details [here](https://docs.renovatebot.com/faq/#separate-patch-releases-from-minor-releases)
* [Group all packages starting with `abc` together in one PR](https://docs.renovatebot.com/faq/#group-all-packages-starting-with-abc-together-in-one-pr)
* [:pinVersions](https://docs.renovatebot.com/presets-default/#pinversions) - maintain a single version only and not SemVer ranges
* [:rebaseStalePrs](https://docs.renovatebot.com/presets-default/#rebasestaleprs) - Rebase existing PRs any time the base branch has been updated.
* [Update package/GHA references in Markdown files](https://github.com/renovatebot/.github/blob/d9b3c1914f4bf9dbecc6456610ca89530260572f/default.json#L121-L140)


## Troubleshooting

* [Troubleshooting docs](https://docs.renovatebot.com/troubleshooting/)
* [Renovate dashboard](https://app.renovatebot.com/dashboard)
