# Concourse PR Check

Play with [github-pr-resource](https://github.com/telia-oss/github-pr-resource) and [concourse-github-status](https://github.com/colstrom/concourse-github-status) to mark PRs as successfully tested by a Concourse pipeline.

# Idea

* Have a repo
* Create a PR
* Pipeline job
  - runs tests because `github-pr-resource` is set up
  - marks the PR as good or bad with the help of `concourse-github-status`

# Setup

1. [Create an access token](https://github.com/settings/tokens) with `repo:status` scope

   Copy the value and export it as environment variable `GITHUB_STATUS_TOKEN`.

1. Set the pipeline:

    ```shell
    $ fly \
        set-pipeline \
        --target uh \
        --pipeline="Pull Requests" \
        --config=pipeline.yml \
        --var github-status-token="$GITHUB_STATUS_TOKEN"
    ```
