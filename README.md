# Practice Git - Beginner to Intermediate Tutorial

This repo is a hands-on tutorial for learning Git from beginner to intermediate level. Go through these steps chronologically to build your Git skills progressively. Each section builds on the previous one, so don't skip ahead!

**Looking for Git security?** Check out the companion tutorial: [practice-git-security](https://github.com/nathaniellarson/practice-git-security) to learn how to scan for secrets, remove them from history, and prevent security leaks.

Any step that has "(no action)" at the end indicates that no action is required before moving to the next step of the tutorial.

## Prerequisites
- Git installed on your system (`git --version` to check)
- A terminal/command line interface
- A text editor (vim, nano, VS Code, etc.)
- Basic familiarity with command line navigation

**Note**: If you're completely new to Git, you'll learn `git init`, `git add`, and `git commit` in the first few steps!

---

## Part 1: Git Basics & Your First Branch

### Section A: Understanding Branches

Branches in Git let you work on different versions of your project at the same time. Think of `main` as your stable production code, and `dev` as where you develop new features. This is a fundamental workflow used by developers worldwide!

1. If you haven't already, fork or clone this repo. Navigate to the repo root: `cd /path/to/practice-git`
2. Make sure you're on the main branch: `git checkout main`
3. Check your current status: `git status`. This shows you which branch you're on and if you have any changes. (no action)
4. Create a new file to work with: `echo "# My Git Practice Project" > project.md`
5. Stage the file (this prepares it to be committed): `git add project.md`
6. Commit it (this saves a snapshot of your work): `git commit -m "initialize project file"`
7. Now let's create a `dev` branch where we'll do our development work: `git checkout -b dev`
8. Verify you're on the new branch: `git branch`. You should see an asterisk (*) next to `dev`. The asterisk shows which branch you're currently on. (no action)
9. Add content to your file: `echo "\n## Description\nThis project helps me learn Git!" >> project.md`
10. Check what changed: `git diff project.md`. The green text shows what you added. This is useful before committing to review your changes! (no action)
11. Stage and commit your changes: `git add project.md` then `git commit -m "Add project description"`
12. Switch back to main: `git checkout main`
13. Look at your project file: `cat project.md`. Notice the description isn't there! That's because it only exists on your `dev` branch. Each branch has its own version of the files. (no action)
14. Merge your dev branch into main: `git merge dev`
15. Check the file again: `cat project.md`. Now you should see the description! The merge brought the changes from `dev` into `main`. (no action)
16. View your commit history: `git log --oneline --graph --all`. You'll see your branch and merge history visualized. (no action)

### Section B: Handling Merge Conflicts

Merge conflicts happen when two branches change the same part of a file differently. Git doesn't know which version to keep, so it asks you to decide. Don't worry - this is normal and easy to fix!

17. Let's create a merge conflict on purpose so you know how to handle it. First, make sure you're on dev: `git checkout dev`
18. Create a new file with some content: `echo "Version from dev branch" > feature.txt`
19. Commit it: `git add feature.txt` then `git commit -m "Add feature from dev"`
20. Switch to main: `git checkout main`
21. Now create the same file but with different content: `echo "Version from main branch" > feature.txt`
22. Commit it: `git add feature.txt` then `git commit -m "Add feature from main"`
23. Try to merge dev into main: `git merge dev`. You should get a merge conflict error! This is expected. (no action)
24. Check the status: `git status`. It will show you which file has conflicts and what to do next. (no action)
25. Open the conflicted file: `cat feature.txt`. You'll see conflict markers like `<<<<<<<`, `=======`, and `>>>>>>>`. Everything between `<<<<<<< HEAD` and `=======` is from your current branch (main). Everything between `=======` and `>>>>>>> dev` is from the dev branch. (no action)
26. Resolve the conflict by editing the file. You can choose one version, combine them, or write something new: `echo "Combined version: main and dev working together" > feature.txt`
27. Stage the resolved file: `git add feature.txt`
28. Complete the merge: `git commit -m "Resolve merge conflict between main and dev"`
29. View your history: `git log --oneline --graph --all`. You'll see the merge commit connecting both branches. (no action)
30. Congratulations! You just resolved your first merge conflict. This is a key skill for working with teams. (no action)

---

## Part 2: Fixing Mistakes

Sometimes you commit too early or make a typo in your commit message. Git lets you fix these mistakes! 

**⚠️ WARNING**: Only fix commits that you haven't pushed yet! Once you share commits with others, don't change them.

### Section A: Amending Commits (Fixing Your Last Commit)

"Amending" means modifying your most recent commit. This is useful when you forget to add a file or want to fix a typo in your commit message.

31. Switch to dev to practice: `git checkout dev`
32. Create a file: `echo "Function 1" > functions.txt`
33. Commit it: `git add functions.txt` then `git commit -m "Add function 1"`
34. Oops! You forgot to add another function. Add it now: `echo "Function 2" >> functions.txt`
35. Instead of creating a new commit, amend (modify) the previous one: `git add functions.txt` then `git commit --amend --no-edit`
36. Check your log: `git log --oneline -1`. You'll see only one commit with both functions. The `--amend` flag modified the last commit instead of creating a new one! (no action)
37. Let's say you also want to fix the commit message: `git commit --amend -m "Add functions 1 and 2"`
38. Verify the change: `git log --oneline -1`. The message should be updated. (no action)

### Section B: Interactive Rebase (Combining Multiple Commits)

Sometimes you make several small commits while working, but you want to combine them into one clean commit before merging to main. This is called "squashing" commits.

39. Make sure you're still on dev: `git checkout dev` (no action)
40. Create commit 1: `echo "Line 1" > rebase-demo.txt` then `git add rebase-demo.txt` then `git commit -m "Add line 1"`
41. Create commit 2: `echo "Line 2" >> rebase-demo.txt` then `git add rebase-demo.txt` then `git commit -m "Add line 2"`
42. Create commit 3: `echo "Line 3" >> rebase-demo.txt` then `git add rebase-demo.txt` then `git commit -m "Add line 3"`
43. Create commit 4: `echo "Line 4" >> rebase-demo.txt` then `git add rebase-demo.txt` then `git commit -m "Add line 4"`
44. View your last 4 commits: `git log --oneline -4`. You should see all four commits. (no action)
45. Now let's squash (combine) them into one commit. Run: `git rebase -i HEAD~4`
46. An editor will open showing your commits. The first line should say `pick` followed by the commit hash and message. (no action)
47. Change the word `pick` to `squash` (or just `s`) for commits 2, 3, and 4. Leave the first one as `pick`. This tells Git to combine commits 2-4 into commit 1. Save and close the editor (in vim: press `Esc`, type `:wq`, press Enter).
48. Another editor will open for you to edit the combined commit message. You can keep all messages or write a new one like "Add lines 1-4". Save and close.
49. Check your log: `git log --oneline -1`. All four commits are now squashed into one! This makes your history much cleaner. (no action)

---

## Part 3: Stashing - Saving Work in Progress

Imagine you're working on something but suddenly need to switch branches to fix a bug. You don't want to commit half-finished work, but you also don't want to lose it. That's where "stashing" comes in - it's like putting your work in a temporary drawer.

50. Switch to dev: `git checkout dev`
51. Start working on something new: `echo "Work in progress" > wip.txt`
52. Stage it: `git add wip.txt`
53. Suddenly you need to switch to main to fix a bug, but you're not ready to commit. Stash (temporarily save) your changes: `git stash save "WIP: new feature"`
54. Check your status: `git status`. Your working directory is clean! The changes are safely stored. (no action)
55. View your stashes: `git stash list`. You should see your stash with the message you provided. Think of this as a list of temporary drawers. (no action)
56. Let's create another stash. Make a change: `echo "Another WIP" > another-wip.txt` then `git add another-wip.txt`
57. Stash it: `git stash save "WIP: another feature"`
58. List your stashes again: `git stash list`. You should see two stashes, numbered 0 and 1. The most recent is always 0. (no action)
59. Apply the most recent stash: `git stash apply`. The file `another-wip.txt` should reappear.
60. The stash still exists in the list. Check: `git stash list`. `apply` brings back the changes but keeps the stash. (no action)
61. Let's clean up. Remove the file: `rm another-wip.txt` then `git reset HEAD another-wip.txt`
62. Apply and remove a stash in one command: `git stash pop`. This applies `stash@{0}` and removes it from the list in one step.
63. Verify: `git stash list`. You should see one fewer stash. (no action)
64. Clear all remaining stashes: `git stash clear`
65. Verify they're gone: `git stash list`. Should be empty. (no action)

---

## Part 4: Cherry-Picking Commits

"Cherry-picking" means taking one specific commit from one branch and applying it to another. It's like saying "I want just that one change, not everything else."

66. Switch to dev: `git checkout dev`
67. Create a utility file: `echo "function add(a, b) { return a + b; }" > utils.js`
68. Commit it: `git add utils.js` then `git commit -m "Add addition utility"`
69. Add another function: `echo "function subtract(a, b) { return a - b; }" >> utils.js`
70. Commit it: `git add utils.js` then `git commit -m "Add subtraction utility"`
71. Add a third function: `echo "function multiply(a, b) { return a * b; }" >> utils.js`
72. Commit it: `git add utils.js` then `git commit -m "Add multiplication utility"`
73. View your commits: `git log --oneline -3`. Note the commit hash (the short code at the start) for "Add addition utility". (no action)
74. Switch to main: `git checkout main`
75. Let's say you only want the addition function on main, not the others. Cherry-pick that specific commit: `git cherry-pick <commit-hash>` (replace `<commit-hash>` with the actual hash from step 73)
76. Check the file: `cat utils.js`. You should see only the addition function! Cherry-pick copied just that one commit. (no action)
77. View the log: `git log --oneline -1`. You'll see the cherry-picked commit. (no action)

---

## Part 5: Undoing Changes

Everyone makes mistakes! Git has several ways to undo changes. Let's learn the main ones.

### Section A: Git Reset (Undoing Commits)

Reset moves your branch back to an earlier commit. There are three types: soft (keep changes staged), mixed (keep changes unstaged), and hard (delete changes completely).

**⚠️ WARNING**: `git reset --hard` permanently deletes uncommitted changes. Be very careful!

78. Switch to dev: `git checkout dev`
79. Create some commits to experiment with: `echo "Commit 1" > reset-demo.txt` then `git add reset-demo.txt` then `git commit -m "Reset demo commit 1"`
80. Add more: `echo "Commit 2" >> reset-demo.txt` then `git add reset-demo.txt` then `git commit -m "Reset demo commit 2"`
81. Add more: `echo "Commit 3" >> reset-demo.txt` then `git add reset-demo.txt` then `git commit -m "Reset demo commit 3"`
82. View your history: `git log --oneline -3`. You should see all three commits. (no action)
83. Let's undo the last commit but keep the changes staged: `git reset --soft HEAD~1` (HEAD~1 means "one commit before HEAD")
84. Check status: `git status`. The changes from commit 3 are still staged! Soft reset only moved the branch pointer back. (no action)
85. Check the file: `cat reset-demo.txt`. All three "commits" are still in the file. (no action)
86. Commit again: `git commit -m "Reset demo commit 3 (re-committed)"`
87. Now let's undo with mixed reset (default): `git reset HEAD~1`
88. Check status: `git status`. The changes are in your working directory but not staged. Mixed reset unstages the changes. (no action)
89. Stage and commit again: `git add reset-demo.txt` then `git commit -m "Reset demo commit 3 (re-committed again)"`
90. Finally, let's do a hard reset that discards everything: `git reset --hard HEAD~1`
91. Check the file: `cat reset-demo.txt`. "Commit 3" is gone! Hard reset deleted the changes completely. (no action)
92. Check status: `git status`. Clean working directory. (no action)

### Section B: Git Revert (Undoing by Creating a New Commit)

Revert is different from reset. Instead of erasing history, it creates a new commit that undoes a previous commit. This is safer when working with others!

93. Create a "bad" commit: `echo "This is a mistake" > mistake.txt` then `git add mistake.txt` then `git commit -m "Add mistake (oops)"`
94. Instead of using reset (which erases history), use revert: `git revert HEAD`
95. An editor will open with a default commit message. Save and close it (in vim: press `Esc`, type `:wq`, press Enter).
96. Check your log: `git log --oneline -2`. You'll see both the original commit AND the revert commit. The history is preserved! (no action)
97. Check your files: `ls`. The `mistake.txt` file is gone, but the history shows what happened. (no action)
98. This is much safer for shared branches because it doesn't rewrite history - it just adds a new commit that undoes the old one! (no action)

### Section C: Git Reflog - Your Safety Net

Reflog is like Git's "undo history." It records every time HEAD moves, so you can recover from almost any mistake!

99. Let's say you accidentally did a hard reset and want to recover. First, let's see our reflog: `git reflog`
100. The reflog shows every movement of HEAD, even "deleted" commits. Each entry has a hash you can return to. (no action)
101. Find a commit hash from before your reset operations (look for "Reset demo commit 3" entries). (no action)
102. You can recover any commit using: `git reset --hard <commit-hash>` (replace with the hash you want to recover to)
103. The reflog is your safety net! It keeps commits for about 90 days even after they're "deleted". If you mess up, reflog can save you! (no action)

---

## Part 6: Exploring Git History

Git has powerful tools to explore your project's history. Let's learn the most useful ones!

### Section A: Git Log - Viewing Commit History

104. Let's explore powerful log commands. First, the visual log: `git log --oneline --graph --decorate --all`
105. This shows your entire commit history as a graph. Very useful for understanding branch relationships! (no action)
106. Filter by date: `git log --since="1 week ago"` (adjust the time period as needed)
107. Search commit messages: `git log --grep="demo"` (this finds all commits with "demo" in the message)
108. See what changed in each commit: `git log -p -2` (shows the last 2 commits with their diffs)
109. See statistics: `git log --stat -3` (shows files changed in the last 3 commits)
110. Custom format: `git log --pretty=format:"%h - %an, %ar : %s" -5` (shows hash, author, relative date, and subject)

### Section B: Git Diff - Comparing Changes

Diff shows you exactly what changed between different versions of your files.

111. Make a change without staging: `echo "Unstaged change" >> project.md`
112. See the diff: `git diff project.md`. This shows changes between working directory and staging area. (no action)
113. Stage the change: `git add project.md`
114. Now try the same diff: `git diff project.md`. Nothing shows because the change is staged! (no action)
115. To see staged changes: `git diff --staged project.md`. There's your change! (no action)
116. Undo the staging: `git reset HEAD project.md`
117. Compare two commits: `git log --oneline -5` (note two commit hashes)
118. Run: `git diff <older-hash> <newer-hash>` (replace with actual hashes)
119. Compare branches: `git diff main..dev`. This shows all differences between main and dev!

### Section C: Git Blame & Show - Finding Who Changed What

120. See who changed each line of a file: `git blame project.md`
121. This shows the commit hash, author, date, and line number for each line. Very useful for finding when a bug was introduced! (no action)
122. Show details of a specific commit: `git log --oneline -1` (note the hash)
123. Run: `git show <commit-hash>` (replace with actual hash)
124. This shows the commit message, author, date, and full diff. Perfect for understanding what a commit did! (no action)

---

## Part 7: Productivity Boosters

Let's make Git faster and easier to use with aliases and configurations!

### Section A: Git Aliases - Creating Shortcuts

Aliases are shortcuts for long commands. Instead of typing `git checkout`, you can type `git co`!

125. Create shortcuts for common commands. Start with checkout: `git config --global alias.co checkout`
126. Now you can use: `git co main` instead of `git checkout main`. Try it!
127. Add more aliases: `git config --global alias.br branch`
128. Add status: `git config --global alias.st status`
129. Add commit: `git config --global alias.ci commit`
130. Add a visual log alias: `git config --global alias.lg "log --oneline --graph --decorate --all"`
131. Try it: `git lg`. Much easier to type! (no action)
132. Add an unstage alias: `git config --global alias.unstage "reset HEAD --"`
133. Add a last commit alias: `git config --global alias.last "log -1 HEAD"`
134. View all your aliases: `git config --global --get-regexp alias`

### Section B: Useful Configurations

135. Set your default branch name: `git config --global init.defaultBranch main`
136. Enable color output (makes Git easier to read): `git config --global color.ui auto`
137. Set your default editor (choose one): `git config --global core.editor "vim"` or `git config --global core.editor "nano"`
138. View all your configurations: `git config --list`
139. View just your global configurations: `git config --global --list`

---

## Part 8: Real-World Workflows

Now let's practice how professional developers use Git every day!

### Section A: The Main-Dev Workflow

In real projects, you keep `main` stable and do all development in `dev` or feature branches.

140. Start from main: `git co main` (using your alias!)
141. Make sure you're up to date: `git pull origin main` (this will fail if you don't have a remote, which is fine for this tutorial)
142. Switch to dev to start new work: `git co dev`
143. Do your work: `echo "# Real World Feature\n\nThis is how I'd work on a real project." > real-world.md`
144. Commit your work: `git add real-world.md` then `git ci -m "Add real world example"` (using your alias!)
145. In a real scenario, you'd push this: `git push origin dev` (skip if no remote)
146. Then you'd create a pull request from dev to main on GitHub/GitLab/Bitbucket for code review. (no action)
147. After approval and testing, you'd merge dev into main (usually via the web interface). (no action)

### Section B: Keeping Dev Updated with Main

Sometimes main gets updated (like when a hotfix is merged) while you're working in dev. You need to bring those changes into dev.

148. Let's simulate main moving forward. Switch to main: `git co main`
149. Make a change: `echo "Hotfix applied to main" > hotfix.txt`
150. Commit it: `git add hotfix.txt` then `git ci -m "Apply hotfix to main"`
151. Switch back to dev: `git co dev`
152. Your dev branch is now behind main. You have two options: merge or rebase. (no action)
153. Option 1 - Merge: `git merge main` (creates a merge commit, keeps all history)
154. Check your log: `git lg`. You'll see the merge commit connecting main and dev. (no action)
155. Option 2 - Rebase: First, undo the merge: `git reset --hard HEAD~1`
156. Now rebase: `git rebase main` (replays your dev commits on top of main)
157. Check your log: `git lg`. Your dev commits are now on top of main's commits, no merge commit! Cleaner history. (no action)
158. Rebase creates a cleaner history, but never rebase commits you've already pushed to a shared branch! (no action)

---

## Part 9: Cleaning Up

Let's clean up all the practice branches and files we created!

159. View all branches: `git br -a`
160. Switch to main: `git co main`
161. You can keep dev, but let's delete any other branches we created. Try: `git branch -d feature/add-description` (this might fail if the branch doesn't exist, which is fine)
162. View branches again: `git br`. You should see just main and dev. (no action)

### Cleaning Untracked Files

163. Create some temporary files: `echo "temp" > temp1.txt` and `echo "temp" > temp2.txt`
164. Create a directory: `mkdir temp-dir` then `echo "temp" > temp-dir/temp3.txt`
165. Check status: `git st`. You'll see untracked files. (no action)
166. See what would be cleaned (dry run): `git clean -n`. This shows what would be deleted without actually deleting.
167. Clean untracked files: `git clean -f`
168. The files are gone but not the directory. To remove directories too: `git clean -fd`
169. Check status: `git st`. Clean! (no action)

---

## Part 10: Best Practices & Tips

Now that you've learned the commands, here are the habits that make you a great Git user:

170. **Commit Often**: Make small, focused commits. It's easier to understand and revert if needed. (no action)
171. **Write Good Commit Messages**: Use imperative mood ("Add feature" not "Added feature"). First line should be 50 characters or less. (no action)
172. **Use Main and Dev Branches**: Keep main stable for production. Do all development in dev. Merge to main only when tested. (no action)
173. **Pull Before Push**: Always `git pull` before `git push` to avoid conflicts. (no action)
174. **Review Before Committing**: Use `git diff --staged` to review what you're about to commit. (no action)
175. **Don't Commit Secrets**: Use `.gitignore` for sensitive files. Never commit passwords, API keys, or credentials! For a complete guide on Git security, see the [practice-git-security](https://github.com/nathaniellarson/practice-git-security) tutorial. (no action)
176. **Use `.gitignore`**: Create a `.gitignore` file to exclude build artifacts, dependencies, and OS files. GitHub maintains helpful [.gitignore templates](https://github.com/github/gitignore) for different languages. (no action)
177. **Communicate with Your Team**: Before force-pushing or rebasing shared branches, talk to your team! (no action)

---

## Quick Reference Card

Here are the most useful commands you've learned:

**Branching**
- `git branch <name>` - Create a branch
- `git checkout <name>` - Switch to a branch
- `git checkout -b <name>` - Create and switch to a branch
- `git branch -d <name>` - Delete a merged branch
- `git branch -D <name>` - Force delete a branch

**Merging & Rebasing**
- `git merge <branch>` - Merge a branch into current branch
- `git rebase <branch>` - Rebase current branch onto another branch
- `git cherry-pick <hash>` - Apply a specific commit to current branch

**Undoing**
- `git reset --soft HEAD~1` - Undo last commit, keep changes staged
- `git reset HEAD~1` - Undo last commit, keep changes unstaged
- `git reset --hard HEAD~1` - Undo last commit, discard changes
- `git revert <hash>` - Create a new commit that undoes a previous commit
- `git reflog` - View all HEAD movements (safety net!)

**Stashing**
- `git stash save "message"` - Save work in progress
- `git stash list` - View all stashes
- `git stash apply` - Apply most recent stash
- `git stash pop` - Apply and remove most recent stash
- `git stash clear` - Remove all stashes

**History & Inspection**
- `git log --oneline --graph --all` - Visual commit history
- `git log --grep="text"` - Search commit messages
- `git diff` - Show unstaged changes
- `git diff --staged` - Show staged changes
- `git blame <file>` - See who changed each line
- `git show <hash>` - Show commit details

**Productivity**
- `git commit --amend` - Modify the last commit
- `git rebase -i HEAD~n` - Interactive rebase last n commits
- `git config --global alias.<name> <command>` - Create an alias

---

## Troubleshooting Common Issues

**Detached HEAD State**
If you see "detached HEAD", you checked out a specific commit instead of a branch.
- To keep your changes: `git checkout -b new-branch-name`
- To discard and return: `git checkout main`

**Accidentally Committed to Main Instead of Dev**
- Move the commit to dev: `git branch dev` (if dev doesn't exist) or `git checkout dev` then `git cherry-pick main` then `git checkout main` then `git reset --hard HEAD~1`

**Merge Conflict During Rebase**
- Resolve conflicts in the files, then: `git add <file>` then `git rebase --continue`
- Or abort: `git rebase --abort`

**Pushed Wrong Commit**
- If no one else has pulled: `git revert <hash>` then `git push`
- Never use `git push --force` on shared branches!

---

## Next Steps

Congratulations! You've completed the beginner to intermediate Git tutorial. Here's what to explore next:

1. **Set up a remote repository** on GitHub, GitLab, or Bitbucket and practice pushing/pulling
2. **Learn Git security** - Scan for secrets, remove them from history, and use pre-commit hooks with the [practice-git-security](https://github.com/nathaniellarson/practice-git-security) tutorial!
3. **Explore Git workflows** (Gitflow, GitHub Flow, trunk-based development)
4. **Collaborate with others** - the best way to learn is by working on real projects with a team
5. **Practice, practice, practice** - Git becomes second nature with repetition!

## Additional Resources

- [Official Git Documentation](https://git-scm.com/doc)
- [Pro Git Book](https://git-scm.com/book/en/v2) - Free and comprehensive
- [Interactive Git Branching Tutorial](https://learngitbranching.js.org/)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)

---

## Contributing

Found an error or want to improve this tutorial? Feel free to submit a pull request!

## Related Projects

Check out the companion tutorial on Git security: [practice-git-security](https://github.com/nathaniellarson/practice-git-security)

## License

This tutorial is provided as-is for educational purposes.
