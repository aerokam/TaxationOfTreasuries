# SETUP
git clone <url>              # copy repo to local
git checkout -b <branch>     # create and switch to new branch

# SOLO WORKFLOW (working directly on main)
git checkout main            # make sure you're on main
git pull                     # sync from GitHub
# ...edit files...
git add <file>               # stage file (or git add . for all)
git commit -m "message"      # snapshot staged changes
git pull                     # sync before push (catch conflicts)
git push                     # send to GitHub

# BRANCH WORKFLOW (for collaborative review)
git checkout main            # switch to main
git pull                     # sync from GitHub
git checkout -b <branch>     # create new branch for edits
# ...edit files...
git add <file>               # stage file (or git add . for all)
git commit -m "message"      # snapshot staged changes
git pull                     # sync before push (catch conflicts)
git push --set-upstream origin <branch>  # first push of new branch
git push                     # subsequent pushes

# MERGING
git checkout main            # switch to main
git merge <branch>           # merge branch into main
git push                     # push merged main to GitHub

# CLEANUP
git branch -d <branch>               # delete local branch
git push origin --delete <branch>    # delete remote branch

# STATUS / INSPECTION
git status                   # what's changed, what's staged
git branch                   # list branches (* = current)
git log --oneline            # compact commit history
