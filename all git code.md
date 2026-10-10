# Git & GitHub Commands — Practical Cheat Sheet

Beginner-friendly notes in Roman Urdu. Daily-use commands are listed first.

## 1. Daily Use Commands ⭐

| Command | Kaam |
|---|---|
| `git status` | Files ka status check karo |
| `git add .` | Tamam changes staging mein add karo |
| `git add filename` | Specific file staging mein add karo |
| `git commit -m "message"` | Changes ka snapshot save karo |
| `git push` | Commits GitHub par upload karo |
| `git pull` | Remote changes lao aur integrate karo |
| `git fetch` | Remote updates lao, integrate kiye baghair |
| `git log --oneline` | Commit history short mein dekho |
| `git diff` | Unstaged changes dekho |
| `git diff --staged` | Staged changes dekho |

### Daily workflow

```bash
git status
git add .
git commit -m "update project"
git push
```

**Yaad rakho:** Add → Commit → Push

Agar remote changes pehle lana zaroori ho, to apne changes ko safely save karne ke baad `git pull` karo.

## 2. Git Setup

```bash
git --version
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
git config --global --list
git config user.name
git config user.email
```

- `git --version` — Git installed hai ya nahi, check karo.
- `user.name` — Commit par dikhne wala naam.
- `user.email` — Commit ke saath record hone wali email.
- `--global` — Setting tamam repositories ke liye.
- Without `--global` — Setting current repository ke liye.

Note: Git name/email set karna GitHub mein login karne se alag hai.

## 3. Repository Commands

```bash
git init
git clone https://github.com/username/repo.git
git status
git rev-parse --show-toplevel
```

- `git init` — Current folder mein Git repository banao.
- `git clone URL` — GitHub repository download karo.
- `git status` — Current changes check karo.
- `git rev-parse --show-toplevel` — Repository ka root folder dekho.

## 4. GitHub Remote Commands

```bash
git remote -v
git remote add origin https://github.com/username/repo.git
git remote set-url origin https://github.com/username/repo.git
git push -u origin main
git push origin main
git pull origin main
git fetch origin
```

- `git remote -v` — Connected remote URL dekho.
- `git remote add origin URL` — Remote repository connect karo.
- `git remote set-url origin URL` — Remote URL change karo.
- `git push -u origin main` — Push karo aur upstream set karo.
- `git push origin main` — Main branch push karo.
- `git pull origin main` — Main branch ke changes integrate karo.
- `git fetch origin` — Remote updates download karo.

`origin` remote ka naam hai aur `main` branch ka naam hai. Tumhare project mein branch ka naam different bhi ho sakta hai.

## 5. Branch Commands

```bash
git branch
git branch -a
git switch main
git switch -c feature-login
git branch -d feature-login
git push -u origin feature-login
git push origin --delete feature-login
```

- `git branch` — Local branches dekho.
- `git branch -a` — Local aur remote-tracking branches dekho.
- `git switch main` — Main branch par jao.
- `git switch -c feature-login` — Nayi branch banao aur switch karo.
- `git branch -d feature-login` — Merged local branch delete karo.
- `git push -u origin feature-login` — Feature branch push karo.
- `git push origin --delete feature-login` — Remote branch delete karo.

## 6. Commit History

```bash
git log
git log --oneline
git log --oneline --all
git show
git show COMMIT_ID
git blame filename
```

- `git log` — Complete commit history.
- `git log --oneline` — Short commit history.
- `git log --oneline --all` — Available branches ki history.
- `git show` — Latest commit ki details.
- `git show COMMIT_ID` — Specific commit ki details.
- `git blame filename` — Har line kis commit se aayi, dekho.

## 7. Undo and Restore

```bash
git restore filename
git restore .
git restore --staged filename
git reset --soft HEAD~1
git revert COMMIT_ID
git commit --amend -m "new message"
```

- `git restore filename` — File ke unstaged changes discard karo.
- `git restore .` — Tamam files ke unstaged changes discard karo.
- `git restore --staged filename` — File ko staging se hatao.
- `git reset --soft HEAD~1` — Aakhri commit hatao, changes staged rakho.
- `git revert COMMIT_ID` — Commit ko reverse karne wala naya commit banao.
- `git commit --amend` — Latest commit update karo.

**Warning:** Restore aur reset commands se kaam lose ho sakta hai. Shared history mein `git revert` aksar safer choice hoti hai.

## 8. Stash Commands

```bash
git stash
git stash push -m "work in progress"
git stash list
git stash pop
git stash apply
git stash drop
```

- `git stash` — Incomplete changes temporarily side par rakho.
- `git stash push -m` — Message ke saath stash save karo.
- `git stash list` — Saved stashes dekho.
- `git stash pop` — Stash apply karo aur successful hone par remove karo.
- `git stash apply` — Stash apply karo, list mein rehne do.
- `git stash drop` — Stash delete karo.

## 9. Merge and Rebase

```bash
git merge main
git rebase main
git rebase --continue
git rebase --abort
git cherry-pick COMMIT_ID
```

- `git merge main` — Main ke changes current branch mein combine karo.
- `git rebase main` — Current branch ke commits ko main ke commits ke baad replay karo.
- `git rebase --continue` — Conflict resolve karne ke baad continue karo.
- `git rebase --abort` — Rebase cancel karo.
- `git cherry-pick COMMIT_ID` — Specific commit current branch par apply karo.

Merge conflict aaye to conflicting files edit karo, phir `git add` aur zaroorat ke mutabiq `git merge --continue` ya `git rebase --continue` use karo.

## 10. File Tracking and .gitignore

```bash
git add .
git add filename
git rm filename
git rm --cached filename
git check-ignore -v filename
```

- `git add .` — Current directory se changes stage karo.
- `git add filename` — Specific file stage karo.
- `git rm filename` — File delete aur deletion stage karo.
- `git rm --cached filename` — Tracking remove karo, local file rakho.
- `git check-ignore -v filename` — Ignore rule check karo.

Example `.gitignore`:

```gitignore
node_modules/
.env
*.log
```

Secrets, passwords aur API keys GitHub par push na karo.

## 11. Tags and Releases

```bash
git tag
git tag -a v1.0 -m "First release"
git show v1.0
git push origin v1.0
git push origin --tags
git tag -d v1.0
```

- `git tag` — Tags dekho.
- `git tag -a` — Version tag banao.
- `git show v1.0` — Tag details dekho.
- `git push origin v1.0` — Specific tag push karo.
- `git push origin --tags` — Tags push karo.
- `git tag -d v1.0` — Local tag delete karo.

## 12. Useful Advanced Commands

```bash
git diff --name-only
git diff main..feature-login
git reflog
git grep "text"
git clean -n
git clean -f
git shortlog -sn
```

- `git diff --name-only` — Changed filenames dekho.
- `git diff main..feature-login` — Branch differences dekho.
- `git reflog` — Local HEAD/branch movement history dekho.
- `git grep "text"` — Tracked files mein text search karo.
- `git clean -n` — Untracked files delete karne se pehle preview.
- `git clean -f` — Untracked files delete karo.
- `git shortlog -sn` — Author-wise commits ki tadaad dekho.

**Caution:** `git clean -f` untracked files permanently delete kar sakta hai.

## 13. Git Interview Quick Revision

| Term | Short Explanation |
|---|---|
| Git | Version Control System |
| GitHub | Online platform for hosting Git repositories |
| Repository | Project aur uski Git history |
| Working directory | Jahan files edit karte ho |
| Staging area | Commit ke liye selected changes |
| Commit | History mein saved snapshot |
| Branch | Separate development line |
| Merge | Branches ke changes combine karna |
| Rebase | Commits ko doosri base par replay karna |
| Clone | Remote repository ki local copy |
| Fork | GitHub par apne account mein repository ki copy |
| Pull request | Changes review aur merge karne ki request |
| .gitignore | Untracked files ko ignore karne ke rules |
| Conflict | Jab Git changes automatically combine na kar sake |

## 14. Recommended Daily Practice

1. `git status` se shuru karo.
2. Files edit karo.
3. `git diff` se changes check karo.
4. `git add .` se changes stage karo.
5. `git diff --staged` se staged changes check karo.
6. `git commit -m "meaningful message"` se commit banao.
7. `git push` se GitHub par upload karo.

**Best practice:** Meaningful commit messages likho, push se pehle status check karo, aur shared branches par destructive commands se bacho.
