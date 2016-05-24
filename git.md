# Git

#### Tests

- `ssh -T -p 443 git@ssh.github.com`
- `ssh -T git@github.com`

#### Edit local config

- `git config --local -e`

#### Fixing .gitignore

 - `git rm -r --cached .`
 - `git add -A`
 - `git commit -vm '.gitignore is now working'`

You can create a **alias** for that in your `.gitconfig`

	# Fix gitignore
	fix = "!fix() { git rm -r --cached . && git add -A && git commit -vm '.gitignore is now working'; }; fix"

#### Backing to specific commit

 - `git fetch remote-name && git merge 98fe123` - commit hash

or

 - `git reset --hard 98fe123` - be careful

#### Generating SSH Key

- `ssh-keygen -t rsa -C "account@host.com"` save in a file like id_rsa-github
- `ssh-add ~/.ssh/id_rsa-github`

#### Configuration

- `git config --global user.name "Thiago Lagden"`
- `git config --global user.email "lagden@lagden.in"`
- `git config --global github.user idvlpsw`
- `git config --global github.token e0e9e3498b7b2780b33eece4a46fb674`
- `git config --global --list`
- `git config --global color.ui "auto"`
- `git config --global core.autocrlf input` **(for mac/linux)**
- `git config --global core.autocrlf true` **(for windows)**
- `git config --global core.editor vim`
- `git config format.pretty oneline`
- `git config --global merge.log true`

#### User Name and E-Mail Address

###### Global identity

- `git config --global user.name "Thiago Lagden"`
- `git config --global user.email "lagden@lagden.in"`

###### Overriding settings for individual repos

- `git config user.name "Lucas Tadashi"`
- `git config user.email "tadashi@tadashi.in"`

#### New Repositories

- `git init`

#### Pushing Existing Repository to GitHub:

    cd existing_git_repo
    git remote add origin git@github.com:lagden/example.git
    git push origin master

#### Adding/Updating Files

    git add <filename>
    git commit -m "comment goes here" <filename>
    git commit -m "comment goes here" -a

#### Status Information

    git log ---pretty=oneline
    git status

#### Diff

    git diff
    git diff --cached
    git diff HEAD

#### Ignoring/Excluding Files

- `vi .git/info/exclude`
- `vi .gitignore`

#### Branching

    git branch
    git branch new
    git checkout -b alternate master
    git blame hello.html

#### To list branches

    git branch

- Add `-a` to list all branches, local and remote.
- Add `-r` to list all branches on the remote site.

#### To merge changes from another branch into current branch

    git checkout {source-branch}
    git pull origin {source-branch}
    git checkout {target-branch}
    git pull origin {target-branch}
    git merge {source-branch}

#### To delete a remote branch

- `git push origin :{branch-name}`

#### Tagging

- `git tag`
- `git tag -a {tagname} -m '{comment}'`
- `git tag {tagname}`
- `git tag -d {tagname}`
- `git show {tagname}`

#### Submodules

###### To add a submodule

- `git submodule add git://github.com/awesome/stuff.git stuff`
- `git submodule init stuff`
- `git submodule`

###### To update existing submodules

- `git submodule update`
- `git submodule update --recursive`

###### To remove a submodule

- `vi .gitmodules (remove line mentioning submodule)`
- `vi .git/config (remove line mentioning submodule)`
- `git rm --cached path/to/submodule`

## Alias

Put in your `.gitconfig`


		[alias]
			# View abbreviated SHA, description, and history graph of the latest 20 commits
			l = log --pretty=oneline -n 20 --graph --abbrev-commit

			# View the current working tree status using the short format
			s = status -s

			# Show the diff between the latest commit and the current state
			d = !"git diff-index --quiet HEAD -- || clear; git --no-pager diff --patch-with-stat"

			# `git di $number` shows the diff between the state `$number` revisions ago and the current state
			di = !"d() { git diff --patch-with-stat HEAD~$1; }; git diff-index --quiet HEAD -- || clear; d"

			# Pull in remote changes for the current repository and all its submodules
			p = !"git pull; git submodule foreach git pull origin master"

			# Clone a repository including all submodules
			c = clone --recursive

			# Switch to a branch, creating it if necessary
			go = "!f() { git checkout -b \"$1\" 2> /dev/null || git checkout \"$1\"; }; f"

			# Show verbose output about tags, branches or remotes
			tags = tag -l
			branches = branch -a
			remotes = remote -v

			# Amend the currently staged files to the latest commit
			amend = commit --amend --reuse-message=HEAD

			# Credit an author on the latest commit
			credit = "!f() { git commit --amend --author \"$1 <$2>\" -C HEAD; }; f"

			# Interactive rebase with the given number of latest commits
			reb = "!r() { git rebase -i HEAD~$1; }; r"

			# Remove the old tag with this name and tag the latest commit with it.
			retag = "!r() { git tag -d $1 && git push origin :refs/tags/$1 && git tag $1; }; r"

			# Find branches containing commit
			fb = "!f() { git branch -a --contains $1; }; f"

			# Find tags containing commit
			ft = "!f() { git describe --always --contains $1; }; f"

			# Find commits by source code
			fc = "!f() { git log --pretty=format:'%C(yellow)%h  %Cblue%ad  %Creset%s%Cgreen  [%cn] %Cred%d' --decorate --date=short -S$1; }; f"

			# Find commits by commit message
			fm = "!f() { git log --pretty=format:'%C(yellow)%h  %Cblue%ad  %Creset%s%Cgreen  [%cn] %Cred%d' --decorate --date=short --grep=$1; }; f"

			# Remove branches that have already been merged with master
			# a.k.a. ‘delete merged’
			dm = "!git branch --merged | grep -v '\\*' | xargs -n 1 git branch -d"

			# Lagden Stuff
			st = status
			ci = commit
			co = checkout
			br = branch
			lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit

			# Commit all with custom msg
			cam = "!cam() { git add -A && git commit -vm \"$1\"; }; cam"

			# Fix gitignore
			fix = "!fix() { git rm -r --cached . && git add -A && git commit -vm '.gitignore is now working'; }; fix"

			# Force update tag (release)
			force = "!force() { git tag $1 --force && git push origin $1 --force; }; force"

