# GitHub Action to turn off PR comments if user is in GitHub team for the test summary GitHub action

Turn off PR comments if a user is in a specified GitHub team.  

## What?

This action extends the [GitHub Action](https://github.com/marketplace/actions/publish-test-results): [EnricoMi/publish-unit-test-result-action](https://github.com/EnricoMi/publish-unit-test-result-action) to allow you to suppress comments on PRs for users who join a GitHub Team.

## Why?

It seems that the behaviour to comment PRs when tests fail was quite controversial in my department!  Some devs found it really useful, others found it really annoying.

Therefore rather than having to turn off for everyone and some miss out on the value, or turned on for everyone and annoy people this action solves that.

## How to use

1. Set up a new GitHub Team for users to join who want to switch off the comments for their PR
2. Add this action

  ```yaml
    - name: Turn off PR comments for users in 'Suppress PR test summary comments'
      uses: eloisetaylor5693/turn-off-pr-comments-for-test-summary-github-action@v2.0.1
      id: suppress-pr-comments-for-some-users
      with:
        default_comment_mode: 'failures'
        github_organisation: 'my-org'
        github_team_for_switching_off_comments: 'Suppress PR test summary comments'
        github_token: ${{ secrets.github_token }}
  ```

3. Use the `test_summary_comment_mode` output when using [EnricoMi/publish-unit-test-result-action](https://github.com/EnricoMi/publish-unit-test-result-action)

  ```yaml
   - name: Publish test results
      uses: EnricoMi/publish-unit-test-result-action@v2
      if: always()
      with:
        files: *.xml
        comment_mode: ${{ steps.suppress-pr-comments-for-some-users.outputs.test_summary_comment_mode }}
        check_name: "Tests"
  ```

## Input Options

|Option|Default Value|Description|
|:-----|:-----:|:----------|
|`default_comment_mode`|"failures"|The comment mode to use when a commit author isn't in any GitHub Teams for suppressing comments on the PR.|
|`github_token`|`${{github.token}}`|An alternative GitHub token, other than the default provided by GitHub Actions runner.|
|`github_team_for_switching_off_comments`|"Suppress PR test summary comments"|GitHub Team users can join to suppress comments on their PR.|
|`github_organisation`|`${{ github.repository_owner }}`|GitHub Organisation the team is part of.|

## Output

`test_summary_comment_mode`: is either the default you gave for the input `default_comment_mode` or `off`


## Contributing

See <https://github.com/eloisetaylor5693/turn-off-pr-comments-for-test-summary-github-action/blob/main/CONTRIBUTING.md>
