# Goal

Small dummy project to make some tests on the Enhanced Git Flow branching model introduced [here](https://www.toptal.com/gitflow/enhanced-git-flow-explained).

# Set up the project
* Create an initial commit with `README` and `.gitignore`
* Create an empty `develop` branch

# Release scenario: default path

## Implement addition and subtraction features
* Create a `feature/add` branch
* Create a `feature/sub` branch
* Implement the addition feature
* Squash merge the `feature/add` branch back to `develop`
* Delete the `feature/add` branch
* Implement the subtraction feature with an error
* Squash merge the `feature/sub` branch back to `develop`
* Delete the `feature/sub` branch

In terms of Git commands, that would be:
```shell
git checkout -b feature/add
git branch feature/sub
# Implement the addition in an editor
git commit -am "Implemented addition"
git checkout develop
git merge --squash feature/add
git commit -am "Implemented addition"
git branch -d feature/add
git checkout feature/sub
# Implement the subtraction in an editor
git commit -am "Implemented subtraction"
git checkout develop
git merge --squash feature/sub
git commit -am "Implemented subtraction"
git branch -d feature/sub
git push
```

## Release the two features
* Tag the tip of the `master` branch, push the tag
* Delete the local `master` branch
* Create a new `master` branch from the `develop` branch, push (force) the branch
* Fix the subtraction feature directly on the `master` branch
* Push the fixes [Release is considered done]
* Squash merge the `master` branch back to `develop`

Again, using Git commands:
```shell
git checkout master
git tag -a v2020-12.1 -m "v2020-12.1"
git push --tags
git checkout develop
git branch -D master
git checkout -b master
git push --force
# Fix subtraction in an editor
git commit -am "Fixed subtraction"
git push # Release done
git checkout develop
git merge --squash master
git commit -am "Fixes from release"
git push
```

# Release scenario: alternative path

## Implement addition and subtraction features
* That part is actually the same

## Release the two features
* Tag the tip of the `master` branch, push the tag
* Reset hard the `master` branch to `develop`
* Fix the subtraction feature directly on the `master` branch
* Push the fixes [Release is considered done]
* Squash merge the `master` branch back to `develop`

```shell
git checkout master
git tag -a v2020-12.1 -m "v2020-12.1"
git push --tags
git reset --hard develop
git push --force
# Fix subtraction in an editor
git commit -am "Fixed subtraction"
git push # Release done
git checkout develop
git merge --squash master
git commit -am "Fixes from release"
git push
```
