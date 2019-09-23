# release process

## overview

the following describes the manual process for release a new version of the solution and is based off of the [gitflow guide](https://nvie.com/posts/a-successful-git-branching-model/)

## process

### determine new solution version

- checkout `develop` branch and update to latest changes ( i.e. `git pull` )
- run `yarn lerna changed -l` to view the proposed package versions.
- identify the greatest package change and use this to dictate what the next solution version should be ( i.e. if a package has a major version bump, the solution will then as well)

### create and configure release branch

- create a new release branch using the new solution version e.g. `git checkout -b release/1.1.0 develop`
- bump the various package versions and update respective CHANGELOG.md's with `yarn bump`
- make any further changes you deem necessary prior to release.
- commit changes `git commit -am 'bumped version to 1.1.0'`

### release version

- `git checkout master` and update
- `git merge --no-ff release/1.1.0`
- `git tag -a 1.1.0`
- publish the release to the production branch `git push --follow-tags`

### update the `develop` branch

release related changes must also be propagated to the develop branch.

- `git checkout develop`
- `git merge --no-ff release/1.1.0`

### cleanup

- delete locatl branch `git branch -D release/1.1.0`
- delete remote branch `git push origin --delete release/1.1.0`
