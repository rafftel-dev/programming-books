# Git Learning

## Create an empty Git repository or reinitialize an existing one

```shell
git init
```

## Add file contents to the index

```shell
git add <file/folder/.>
```

## Remove files from the working tree and the index

```shell
git rm --cached <file>
```

## Show the working tree status

```shell
git commit -m "your massage"
```

## git commit with add

```shell
git commit -am "massage"
```

## Show commit logs

```shell
git log
```

## Show commit logs the last 3 files or more

```shell
git log -<number>
```

## Show commit logs with specific

```shell
git log -- <name_file.txt>
```

## Set and read git configuration variables

```shell
git config
```

## Manual git

```shell
git help
```

## push more web Hosting internet Github or Gitlab

```shell
git push --set-upstream git@gitlab.com:kevinaltaf/wiki-arch.git master
```

# Fetch & Pull

## Put last update from repository

```shell
git fetch
```

## Pull and override last update from repository

```shell
git pull
```

# Branch

## alias graph="git log --all --decorate --oneline --graph"

```shell
graph
```

## Сreate Git Branch

```shell
git branch <branch_name>
```

## Switch new Branch

```shell
git checkout <branch_name>
```

## can find missing files via git log - <file>

```shell
git checkout <hash of 5 digit example your hash 6040E>
```

## Create a Git branch and checkout in one command

```shell
git branch -b <branch_name>
```

## Delete Branch when your Branch useless

```shell
git branch -d <branch_name>
```

## error: The branch '<name_branch>' is not fully merged

```shell
git branch -D <branch_name>
```

## Merge a new Branch

```shell
git checkout master && git merge <brance_name>
```
