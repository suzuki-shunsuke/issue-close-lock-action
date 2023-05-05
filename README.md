# issue-close-lock-action

Close and lock GitHub Issues automatically to keep Issues maintainable

[action.yaml](action.yaml)

## Requirements

- GitHub CLI
- GitHub Access Token
  - The permission `issues: write` is required to update issues (close, lock, post comment)

## How to use

```yaml
- uses: suzuki-shunsuke/issue-close-lock-action@main
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
