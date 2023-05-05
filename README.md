# issue-close-lock-action

Close and lock GitHub Issues automatically to keep Issues maintainable

![image](https://user-images.githubusercontent.com/13323303/236376582-547f36e9-316c-4ee4-b79d-3dc972550611.png)

[action.yaml](action.yaml)

## Requirements

- GitHub CLI
- GitHub Access Token
  - The permission `issues: write` is required to update issues (close, lock, post comment)

## Inputs

Required

- `issue_number`: The issue number

Optional

- `github_token` (default: `${{github.token}}`): GitHub Access Token to update the issue
- `is_close` (default: `true`): If true, the issue is closed
- `is_lock` (default: `true`): If true, the issue is locked
- `message` (default: comment isn't posted): If the message is set, the message is posted to the issue as a comment

## Outputs

Nothing.

## How to use

1. Close and lock an issue. No comment is posted.

```yaml
- uses: suzuki-shunsuke/issue-close-lock-action@main
  with:
    issue_number: ${{github.event.issue.number}}
```

2. Close an issue and post a comment using the personal access token. The issue isn't locked

```yaml
- uses: suzuki-shunsuke/issue-close-lock-action@main
  with:
    issue_number: ${{github.event.issue.number}}
    github_token: ${{secrets.PERSONAL_ACCESS_TOKEN}}
    is_lock: "false"
    message: |
      # Please create a GitHub Discussion instead of this issue
  
      Only maintainers can create new Issues. If needed, a maintainer will create an Issue after your Discussion been triaged and confirmed.
  
      This Issue will now be closed and locked. This way we keep Issues actionable, and free of duplicates or wrong bug reports.
  
      Thanks
```

## Example

[GitHub Actions Workflow](https://github.com/aquaproj/aqua/blob/6d48f7c0462ce4654865f2284e2e488761dad559/.github/workflows/close-issue.yaml)

```yaml
name: Close issue
on:
  issues:
    types: [opened]
jobs:
  close-issue:
    runs-on: ubuntu-latest
    if: github.triggering_actor != 'suzuki-shunsuke'
    permissions:
      issues: write
    steps:
      - uses: suzuki-shunsuke/issue-close-lock-action@231aefd9a92cddfd2eb51e60965e9468f3d592bd # v0.1.0
        with:
          issue_number: ${{github.event.issue.number}}
          message: |
            # Please create a GitHub Discussion instead of this issue
      
            Only maintainers can create new Issues. If needed, a maintainer will create an Issue after your Discussion been triaged and confirmed.
            This Issue will now be closed and locked. This way we keep Issues actionable, and free of duplicates or wrong bug reports.
      
            Thanks
```

## LICENSE

[MIT](LICENSE)
