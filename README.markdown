# Concourse PR Check

Play with [github-pr-resource](https://github.com/telia-oss/github-pr-resource) and [concourse-github-status](https://github.com/colstrom/concourse-github-status) to mark PRs as successfully tested by a Concourse pipeline.

# Idea

* Have a repo
* Create a PR
* Pipeline job
  - runs tests because `github-pr-resource` is set up
  - marks the PR as good or bad with the help of `concourse-github-status`

# Setup

1. Set the pipeline:

    ```shell
    $ fly \
        set-pipeline \
        --target your-target \
        --pipeline="Pullrequest Check" \
        --config=pipeline.yml \
        --non-interactive
    ```

