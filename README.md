# simbo/vale-action

A GitHub action to run Vale for spellchecking.

It does pretty much the same like the [official Vale action](https://github.com/errata-ai/vale-action),
but as this one is not using Docker, it's much faster.

## Usage

Use `simbo/vale-action@v1` in your GitHub action workflow.

### Example

```yml
jobs:
  notify:
    runs-on: ubuntu-latest
    steps:
      - name: 🛎 Checkout
        uses: actions/checkout@v3

      - name: 🧑‍🏫 Spellcheck
        env:
          GITHUB_TOKEN: ${{ github.token }}
        uses: simbo/vale-action@v1
```

## Inputs

| Input           | Required | Default                 | Description                                                                                                                                                        |
| --------------- | -------- | ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `version`       | no       | (latest)                | Vale release version to use.                                                                                                                                       |
| `flags`         | no       | `''`                    | Space-delimited list of flags for the Vale CLI. To see a full list of available flags, run `vale -h`.                                                              |
| `files`         | no       | `'.'`                   | Space-delimited list of file or directory arguments; equivalent to calling `vale input1 input2`.                                                                   |
| `reviewdog`     | no       | `'false'`               | Whether to use Vale with Reviewdog.                                                                                                                                |
| `github_token`  | no       | `'${{ github.token }}'` | The GitHub repo access token to be used for Reviewdog.                                                                                                             |
| `reporter`      | no       | `'github-pr-review'`    | Set the [reporter](https://github.com/reviewdog/reviewdog#reporters) type for Reviewdog.                                                                           |
| `fail_on_error` | no       | `'false'`               | By default, Reviewdog will return exit code 0 even if it finds errors. If `fail_on_error` is enabled, Reviewdog exits with 1 when at least one error was reported. |
| `filter_mode`   | no       | `'added'`               | Set the [filter mode](https://github.com/reviewdog/reviewdog#filter-mode) for Reviewdog.                                                                           |

## Outputs

This action has no outputs. 🤷‍♂️

## Development

### Creating a new Version

Use `./release.sh <major|minor|patch>` which will create a git tag for the
respective version.

A release workflow will pick up the tag when pushed to GitHub, create a release
and move major, minor and latest tags accordingly.

To publish the release into the GitHub marketplace open
[releases](https://github.com/simbo/vale-action/releases) and
update the release for marketplace publishing.

## License

[MIT &copy; Simon Lepel](http://simbo.mit-license.org/)
