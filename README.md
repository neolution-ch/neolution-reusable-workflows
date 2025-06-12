# neolution-reusable-workflows

This repository contains reusable workflows for GitHub Actions that can be used across multiple repositories.

## release-it-yarn-npm

This workflow automates the release process for projects using yarn. It will publish the package to NPM and optionally to GitHub Packages, depending on the provided inputs. It assumes that `release-it` is installed as a dev dependency in your project and that you have `release-it` configured correctly.

It will get a token from the `release-bot` application. The main reason for that is that we can add a bypass rule to the `release-bot` application to allow the release bot to push into protected branches.

### Inputs

| Name                           | Required           | Default | Description                                                          |
| ------------------------------ | ------------------ | ------- | -------------------------------------------------------------------- |
| **version-type**               | :heavy_check_mark: | -       | Specifies the type of version increment (e.g., major, minor, patch). |
| **pre-release-channel**        | :heavy_check_mark: | -       | Defines the pre-release channel (e.g., alpha, beta).                 |
| **dry-run**                    | :heavy_check_mark: | -       | Runs the release process without making any changes.                 |
| **publish-to-github-packages** | :heavy_minus_sign: | false   | Enables publishing the package to GitHub Packages.                   |

### Secrets

| Name                            | Required           | Default | Description                                  |
| ------------------------------- | ------------------ | ------- | -------------------------------------------- |
| **github-token**                | :heavy_check_mark: | -       | Token for authenticating with GitHub.        |
| **npm-token**                   | :heavy_check_mark: | -       | Token for authenticating with NPM.           |
| **release-bot-app-id**          | :heavy_check_mark: | -       | Application ID for the release bot.          |
| **release-bot-app-private-key** | :heavy_check_mark: | -       | Private key for the release bot application. |

### Usage

```yaml
release-it:
  uses: neolution-ch/neolution-reusable-workflows/.github/workflows/release-it-yarn-npm.yml@v1
  with:
    dry-run: ${{ github.event.inputs.dry_run == 'true' }}
    version-type: ${{ github.event.inputs.version_type }}
    pre-release-channel: ${{ github.event.inputs.pre_release }}
  secrets:
    github-token: ${{ secrets.GITHUB_TOKEN }}
    npm-token: ${{ secrets.NPM_TOKEN }}
    release-bot-app-id: ${{ secrets.RELEASE_BOT_APP_ID }}
    release-bot-app-private-key: ${{ secrets.RELEASE_BOT_APP_PRIVATE_KEY }}
```
