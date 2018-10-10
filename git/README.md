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