# Concourse PR Check

Play with [github-pr-resource](https://github.com/telia-oss/github-pr-resource) to mark PRs as successfully tested by a Concourse pipeline.

# Idea

Every pull request to a GitHub repo is tested in a Concourse pipeline. For that, the `github-pr-resource` is set up. After running the pipeline job, it marks the PR as good or bad using GitHub's status API.

# Setup

1. [Create an access token](https://github.com/settings/tokens) with `repo:status` scope

   Copy the value and export it as environment variable `GITHUB_STATUS_TOKEN`.

1. (Optional) Make up a URL-safe secret string that can be used as webhook token, e.g. with

   ```shell
   $ openssl rand -base64 48 | uuencode -m - | sed -n 2p
   ```

   Export the value as environment variable `$GITHUB_WEBHOOK_TOKEN`.

1. (Optional) Configure a new webhook for the GitHub repository:

    ```shell
    $ echo https://ci.uhlig.it/teams/main/pipelines/Pull%20Requests/resources/pull-request/check/webhook?webhook_token=$GITHUB_WEBHOOK_TOKEN
    ```

1. Set the pipeline:

    ```shell
    $ fly \
        set-pipeline \
        --target uh \
        --pipeline="Pull Requests" \
        --config=pipeline.yml \
        --var github-status-token="$GITHUB_STATUS_TOKEN" \
        --var github-webhook-token="$GITHUB_WEBHOOK_TOKEN"
    ```
