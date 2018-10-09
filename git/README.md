# Frontend Masters Notes
[Frontend Masters](https://frontendmasters.com/courses/git-in-depth)

See [resources](https://github.com/nnja/advanced-git)

##
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