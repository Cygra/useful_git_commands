[用 reflog 恢复数据](https://git-scm.com/book/zh/v1/Git-%E5%86%85%E9%83%A8%E5%8E%9F%E7%90%86-%E7%BB%B4%E6%8A%A4%E5%8F%8A%E6%95%B0%E6%8D%AE%E6%81%A2%E5%A4%8D)

`git log -g`

`git branch recover-branch ab1afef`

---

- [How to change the commit author for one specific commit?](https://stackoverflow.com/questions/3042437/how-to-change-the-commit-author-for-one-specific-commit)

> `A-B-C-D-E-F` with `F` as HEAD

1. `git rebase -i B`（`git rebase -i --root`）
2. `pick` -> `edit`
3. `git commit --amend --author="Author Name <email@address.com>"`
4. `git rebase --continue`
5. -> 3 -> 4
6. `gpf`

---

`git add -p`

> 添加每个变化前，都会要求确认
> 对于同一个文件的多处变化，可以实现分次提交

---

To push a single tag:
`git push origin <tag_name>`

push all tags (not recommended)
`git push --tags`

---

To rename a branch both locally and remotely
https://stackoverflow.com/a/16220970

```
git branch -m old_branch new_branch

git push origin :old_branch

git push --set-upstream origin new_branch
```

---

If you want to revert the file to its state in master:

`git checkout origin/master [filename]`

---

文件历史

`git log --follow -p [filename]`

---

diff file between branches

`git diff master release/3.9.11 -- [filename]`

---

`git rm --cached FILE_NAME`

---

选出在一个分支中而不在另一个分支中的提交

查看 experiment 分支中还有哪些提交尚未被合并入 master 分支
`git log master..experiment`

如果你想看 master 或者 experiment 中包含的但不是两者共有的提交，你可以执行

`git log master...experiment`

这种情形下，log 命令的一个常用参数是 `--left-right`，它会显示每个提交到底处于哪一侧的分支。 这会让输出数据更加清晰。

`git log --left-right master...experiment`

---

如果我们想找到 `ScanExtraInfos` 是什么时候引入的，我们可以使用 `-S` 选项来显示新增和删除该字符串的提交。

`git log -SScanExtraInfos --oneline`

---

[Undo a fast-forward merge](https://stackoverflow.com/questions/14308580/undo-a-fast-forward-merge)

`git reset --hard @{1}`

---

To search the commit log (across all branches) for the given text:

`git log --all --grep='Build 0051'`

[How to search a Git repository by commit message?](https://stackoverflow.com/questions/7124914/how-to-search-a-git-repository-by-commit-message)

---

[4 Advanced Git Commands That Will Save Your Time](https://dev.to/codicacom/4-advanced-git-commands-alp)
This Git command gives you an opportunity to pull in the commits of another engineer and rebase your changes on top.

```
git pull --rebase --autostash
# alias `gupa`
```

---

[Advanced Git Commands You Will Actually Use
](https://stosb.com/blog/advanced-git-commands-you-will-actually-use/)

---

**Removing Parts of a Commit**

It's also very common to accidentally commit a file or a line that you didn't intend to. Especially when using git commit -a. This too can be easily fixed.

```
## Commit c42bc3a535 (can be anywhere in history)
$ git revert -n c42bc3a535
$ git reset # Remove everything from staging

## Add back the wanted changes
$ git add NEWS # All of this file
$ git add -p # Some parts of the rest

## Merge the commit into the original commit
## Either amend if it is the HEAD
$ git commit --amend
$ git checkout -f # Remove the rest of the changes
## Or fixup if anywhere else
$ git commit -m "Temp"
$ git checkout -f # Remove the rest of the changes
$ git rebase -i c42bc3a535^ # Mind the ^ (caret)
```

---
