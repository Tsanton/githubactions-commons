# **Semantic Versioning** #

A composite action that consumes a [Gitversion.yaml file](https://gitversion.net/docs/reference/configuration) to output a semantic version for your build.

## **How it works** ##

In short this is an action that requires you to check out all previous commit info so it can loop through the commit messages and calculate the current semantic version of your release.

## **Requirement** ##

As the action is recursive in nature it required you to check out all the previous commit metadata along with the repository. This is achived by setting ```fetch-depth``` to zero:

```yaml
- name: checkout
  uses: actions/checkout@v3
  with:
    fetch-depth: 0
```

## **Invocation** ##

```yaml
name: semver

on: [workflow_dispatch]


jobs:
  semver:
    runs-on: ubuntu-latest
    steps:
      - name: checkout
        uses: actions/checkout@v3
        with:
          fetch-depth: 0

      - name: semver
        id: semver
        uses: Fremtind/pda-githubactions-commons/actions/semver@main
        with:
          semantic_versioning_file_path: ./
          semantic_versioning_file_name: semver.yml

      - name: echo version
        shell: bash
        env:
          MAJOR: ${{ steps.semver.outputs.major }}
          MINOR: ${{ steps.semver.outputs.minor }}
          PATCH: ${{ steps.semver.outputs.patch }}
          MAJOR_MINOR_PATCH: ${{ steps.semver.outputs.major_minor_patch }}
          SEMVER: ${{ steps.semver.outputs.semver }}
        run: |
          echo $MAJOR
          echo $MINOR
          echo $PATCH
          echo $MAJOR_MINOR_PATCH
          echo $SEMVER
```

## **Default config** ##

Though you can configure this action however you like by tweeking your semver.yaml file, we've chosen to provide the following default example. \

```yaml
# semver.yaml
mode: Mainline
branches:
  main:
    increment: None
major-version-bump-message: '^(?i)(breaking|major).*'
minor-version-bump-message: '^(?i)(feat|minor).*'
patch-version-bump-message: '^(?i)(fix|patch).*'
tag-prefix: '[vV]'
commit-message-incrementing: Enabled
commit-date-format: yyyy-MM-dd
```

The behaviour of the config below is such that only commits directly to main, or pulls (squashed), with commit messages starting with the following keywords will increment your semantic version:
- ```breaking```: major increment
- ```major```: major increment
- ```feat```: major increment
- ```minor```: minor increment
- ```fix```: patch increment
- ```patch```: patch increment

The reason that we've chosen manual incrementation is due to the complex nature of rolling back version. \
In ```mode:Mainline``` the ```ignore``` map is not a part of the configuration. This means that with ```increment: Inherit``` every single commit into master will increment patch with one.
You can provide a ```no-bump-message: "'^(?i)(chore|doc).*'"``` to ignore certain bumps, but all in all it's a bit too much magic around incrementation that is hard to roll back if errors occur.

**Alter the commit message of the most resent commit?**

```sh
git commit --amend -m "New commit message."
```

**Changing an Older or Multiple Commits?**
If you need to change the message of an older or multiple commits, you can use an interactive ```git rebase``` to change one or more older commits.

The rebase command rewrites the commit history, and it is strongly discouraged to rebase commits that are already pushed to the remote Git repository.

```sh
# N is the number of commits to perform a rebase on.
git rebase -i HEAD~N, 
```

[More rebase guidance](https://linuxize.com/post/change-git-commit-message/#changing-an-older-or-multiple-commits)


## **Other modes** ##

You can configure your semver pretty much however you like. The two other modes to look into are ```ContinuousDelivery``` and ```ContinuousDeployment```. \
Another reason for us not documenting one of these as the default is the requirement that they refuse to increment the **patch** without a release having been tagged with the semver version. \
This would for many be an optimal solution, but not for multi project team doing multiple builds from a single repository.

- [mode: ContinuousDelivery](https://gitversion.net/docs/reference/modes/continuous-delivery)
- [mode: ContinuousDeployment](https://gitversion.net/docs/reference/modes/continuous-deployment)

