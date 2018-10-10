# Frontend Masters Notes
From the [Frontend Masters] course(https://frontendmasters.com/courses/git-in-depth)

See [resources](https://github.com/nnja/advanced-git)

## Git cat

```console
git cat-file -t 980a0
# prints the type

git cat-file -p 980a0
# prints the content

❯ git cat-file -t adf0e1
commit
❯ git cat-file -p adf0e1
tree 581caa0fe56cf01dc028cc0b089d364993e046b6
author Nina <nina@nnja.io> 1506214053 -0700
committer Nina <nina@nnja.io> 1506214053 -0700
Initial commit
```

## Refs under the hood

```console
❯ tree .git
.git
├── HEAD
└── refs
├── heads
│ └── master
└── tags

# refs/heads is where branches live

❯ git log --oneline
adf0e13 (HEAD -> master) Initial commit
❯ cat .git/refs/heads/master
adf0e13658d9b4424efe03c3ac3281facf288c13

# /refs/heads/master contains which commit the branch points to

❯ cat .git/HEAD
ref: refs/heads/master
# HEAD is usually a pointer to the current branch
```

## The staging area

```console
❯ git ls-files -s
100644 b8b2583b242add97d513d8d8b85a46b9b5fb29cb 0 index.txt
100644 ed52afd72f64b1f8575e81bb4cb02ef1215739f6 0 posts/
welcome.txt

# The plumbing command ls-files -s will show you what’s in the staging area.
```

### Moving files in and out of the staging area

```console
# add a file to the next commit
git add <file>

# delete a file in the next commit
git rm <file>

# rename a file in the next commit
git mv <file>
```

### Add commits in hunks interactively

```console
git add -p

.
.
.
diff displayed
.
.
.
Stage this hunk [y,n,q,a,d,/,j,J,g,e,?]? ?
y - stage this hunk
n - do not stage this hunk
q - quit; do not stage this hunk or any of the remaining ones
a - stage this hunk and all later hunks in the file
d - do not stage this hunk or any of the later hunks in the file
g - select a hunk to go to
/ - search for a hunk matching the given regex
j - leave this hunk undecided, see next undecided hunk
J - leave this hunk undecided, see next hunk
k - leave this hunk undecided, see previous undecided hunk
K - leave this hunk undecided, see previous hunk
s - split the current hunk into smaller hunks
e - manually edit the current hunk
? - print help
```

## Stashing

Save un-committed work.

The stash is safe from destructive operations.

### Basic use

stash changes
`git stash`

list changes
`git stash list`

show the contents
`git stash show stash@{0}`

apply the last stash
`git stash apply`

apply a specific stash
` git stash apply stash@{0}`

### Keeping files

Keep untracked files
`git stash --include-untracked`

Keep all files (even ignored ones!)
`git stash --all`

### Operations

Name stashes for easy reference
`git stash save "WIP: making progress on foo"`

Start a new branch from a stash
`git stash branch <optional stash name>`

Grab a single file from a stash
`git checkout <stash name> -- <filename>`

### Cleaning the stash

Remove the last stash and applying changes:
`git stash pop`
tip: doesn’t remove if there’s a merge conflict

Remove the last stash
`git stash drop`

Remove the nth stash
`git stash drop stash@{n}`

Remove all stashes
`git stash clear`

### Extra

Keep untracked files
`git stash --include-untracked`

Name stashes for easy reference
`git stash save "WIP: making progress on foo"`

## References

### Lightweight tags

```console
$ git checkout master
Switched to branch 'master'

$ git tag my-first-commit
```

### Annotated tags

```console
$ git tag -a v1.0 -m "Version 1.0 of my blog"

$ git tag
my-first-commit
v1.0

$ git show v1.0
tag v1.0
Tagger: Nina Zakharenko <nina@nnja.io>
Date: Sun Sep 24 17:01:21 2017 -0700

Version 1.0 of my blog
```

### Working with tags

List all the tags in a repo
`git tag`

List all tags, and what commit they’re pointing to
`git show-ref --tags`

List all the tags pointing at a commit
`git tag --points-at <commit>`

Looking at the tag, or tagged contents:
`git show <tag-name>`

### Tags and branches

#### Branch
➤ The current branch pointer moves with every commit to the repository

#### Tag
➤ The commit that a tag points doesn’t change.
➤ It’s a snapshot!

### Head-less / detached head

```console
$ git checkout cd0b57
Note: checking out 'cd0b57'.

You are in 'detached HEAD' state. You can look around, make experimental changes and commit them, and you can discard any commits you make in this state without impacting any branches by performing another checkout.

$ git add posts/second-post.txt

$ git commit -m "My second post"
[detached HEAD 1f6ee83] My second post
1 file changed, 1 insertion(+)
create mode 100644 posts/secondpost.txt

$ git checkout master
Warning: you are leaving 1 commit behind, not connected to any of your branches:
1f6ee83 My second post
```

## Merging

Merge commits are just commits

### Fast forward

Fast-forward happens when there are no commits on the bas branch that occurred after the feature branch was created.

```console
$ git checkout master

$ git merge feature
Updating 2733233..9703930
Fast-forward
index.txt | 2 +-
1 file changed, 1 insertion(+), 1 deletion(-)
```

#### --no-ff (no fast forward mode)

To retain history of a merge commit even if there are no changes to the base branch:

```console
$ git checkout master

$ git merge new_feature --no-ff
```

### Merge conflicts

Attempt to merge, but files have diverged
Git stops until the conflicts are resolved

```console
$ git merge feature
Auto-merging feature
CONFLICT (add/add): Merge conflict in feature
```

#### Git ReReRe (REuse REcorded REsolution)

Git saves how you resolve a conflict
Next time it finds the conflict it resuses the same resolution

Turn it on:
`git config rerere.enabled true`
use `--global` flag to use in all projects

```console
$ git config rerere.enabled true

$ git checkout master
$ git merge feature
Auto-merging feature
CONFLICT (add/add): Merge conflict in file
Recorded preimage for 'file'
Automatic merge failed; fix conflicts and then commit the result.
### Fix the merge conflict in file.
$ git add file
$ git commit -m "Resolve conflict"
Recorded resolution for 'feature'.
[master 0fe266d] Resolve conflict
```

If merge is rolled back for changes, next time it is merge same conflict resolution can be used:

```console
$ git merge feature
Auto-merging feature
CONFLICT (add/add): Merge conflict in feature
Resolved 'feature' using previous resolution.
Automatic merge failed; fix conflicts and then commit the result.

$ git add file

$ git diff --staged
diff --git a/file b/file
index 587be6b..a354eda 100644
--- a/file
+++ b/file
@@ -1 +1 @@
-The old change
+This is how I resolved my conflict.
\ No newline at end of file
```

## History and diffs

### Git log

`git log`

`git log --one-line`

`git log --since="yesterday"`

`git log --since="2 weeks ago"`

`git log --grep=mail --author=nina --since=2.weeks`

## Fixing mistakes

See the [exercise](https://github.com/nnja/advanced-git/blob/master/exercises/Exercise6-FixingMistakes.md)

`git checkout --file`
Can be very dangerous. Commit changes before checking out a file.

### Git clean
Deletes untracked files

!Warning this operation cannot be undone!

You can do a dry run:

`git clean --dry-run`

### Git reset

Another command that performs different action depending on arguments

By default, git performs a `git reset -mixed`

Git checkout will move the head, but branch will stay where it was. Whereas reset will move the head and will move the branch reference, so your branch will be modified.

For commits:
Move the HEAD pointer, optionally modifies files

For file paths:
Does not move the HEAD pointer, modifies files

### Git reset cheatsheet

1. Move HEAD and current branch
2. Reset the staging area
3. Reset the working area

`--soft` = (1)

`--mixed` =(1) & (2) (default)

`--hard` = (1) & (2) & (3)

### Undo a git reset with orig_head

In case of an accidental `git reset -`

Git keeps the previous value of `HEAD` in variable called
`ORIG_HEAD`

To go back to the way things were:

`git reset ORIG_HEAD`

### Git revert - the "safe" reset

Git revert creates a new commit that introduces the opposite
changes from the specified commit.

The original commit stays in the repository.

Tip:

Use revert if you’re undoing a commit that has already been
shared.

Revert does not change history.

## Git rebase, amend

### Amend

Can be useful if, for example you make a commit adding a file, but forget to add the file:

```console
$ cat index.txt

welcome.txt Welcome to my blog

python.txt Why python is my favorite language

$ git commit -m "Add a blog post about Python"
[tech_posts 4080a79] Add a blog post about Python
1 file changed, 0 insertions(+), 0 deletions(-)
create mode 100644 A

$ git add posts/python.txt

$ git commit --amend
[tech_posts de53317] Add a blog post about Python
Date: Wed Sep 27 22:12:31 2017 -0700
2 files changed, 1 insertion(+)
create mode 100644 A
create mode 100644 posts/python.txt
```

