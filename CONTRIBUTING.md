# Contributing

As the owner of the repository, I generally commit directly to main if not likely to break anything.

For others, please create a PR.  I will review and release.

## Publishing changes

- Work out the next SemVer version
- Commit a change to the readme to update the version [here](https://github.com/eloisetaylor5693/turn-off-pr-comments-for-test-summary-github-action/blob/main/README.md?plain=1#L19)
- Create a new tag with version number eg v2.0.0.  `git push --follow-tags`
- Go to releases: <https://github.com/eloisetaylor5693/turn-off-pr-comments-for-test-summary-github-action/releases>
- "Draft a new release"
  - Select tag from dropdown with the new version number
  - Click "Generate release notes"
  - Check the release info in release description is meaningful to people consuming this GitHub Action.  If not extend and reword.
  - Once happy, "Publish release"
