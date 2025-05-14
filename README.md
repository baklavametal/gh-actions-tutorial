# gh-actions-tutorial

[color]

    ui = auto

[merge]

    ff = false

    tool = vimdiff

    conflictstyle = diff3

[core]

    autocrlf = input

    editor = $EDITOR

    pager = less -R -M

    excludesfile = /Users/bengtbrodersen/.gitignore_global

    ignorecase = false

[pull]

    rebase = merges

[rebase]

    autoStash = true

[tag]

    sort = version:refname

[credential]

    helper = osxkeychain

[diff]

    tool = vimdiff

[mergetool]

    prompt = false

[alias]

    alias = "!git config --name-only --get-regexp ^alias\\. | sed s/^alias\\.// | sort | while read alias; do \n  printf \"[1;34m${alias}[m \" && git config --get alias.${alias}\ndone"

    amend = commit --amend --no-edit

    squash = "!f() { \n  git reset --soft \"$1\" -- && shift && git commit --amend \"$@\"\n}; f"

    fixup = "!f() { \n  TARGET=$(git rev-parse \"$1\")\n  git commit --fixup=$TARGET ${@:2} \\\n  && EDITOR=true git rebase -i --autostash --autosquash $TARGET^\n}; f"

    retract = reset HEAD^

    thrust = push --force-with-lease

    ignore = "!f() {\n  if [ $# -eq 0 ]; then\n    ${EDITOR:-vi} .gitignore\n  else\n    for IGNORE_PATH in \"$@\"\n    do\n      if !(grep -s \"^${IGNORE_PATH}$\" .gitignore >/dev/null); then\n        echo \"$IGNORE_PATH\" >> .gitignore\n      fi\n    done\n  fi\n  \n  if [ -e .gitignore ]; then\n    git add .gitignore\n  fi\n}; f"

    ignore-change = update-index --skip-worktree

    hash = "!f() { \n  git rev-parse ${1:-HEAD}\n}; f"

    bootstrap = !git init && git commit -m root --allow-empty

    situation = status --short --branch

    whoami = "!f() { \n  printf \"[1;34mname[0m  \" && git config user.name\n  printf \"[1;34memail[0m \" && git config user.email\n}; f"

    workspace = "!f() { \n  WORKSPACE=$PWD; \n  CMD=\"$@\"; \n  for repo in */; do \n    ( cd $repo 2>/dev/null && git status >/dev/null 2>&1 && printf \"\\e[34m${PWD#$WORKSPACE/}:\\e[39m\\n\" && eval git $CMD && echo)\n    true\n  done\n}; f"

    take = "!f() { git clone \"$@\"; for arg; do if [[ \"$arg\" != -* ]]; then dir=\"$arg\"; fi; done; cd \"$(basename \"$dir\" .git)\"; }; f"

    graph = log --graph --color=always \n  --date=format:'%a %Y-%m-%d %H:%M' \n  --pretty=tformat:'%C(dim blue)%h%C(reset) %C(dim cyan)%ad%C(reset) %C(dim green)%ar%C(reset) %C(dim white)%an%C(reset)%n  %C(default bold)%s%C(reset)%C(auto)%d%C(reset)%n'\n  -m

[includeIf "gitdir:/Users/bengtbrodersen/Workspace/"]

    path = /Users/bengtbrodersen/Workspace/.gitconfig

[includeIf "gitdir:/Users/bengtbrodersen/Workspace-qoomon/"]

    path = /Users/bengtbrodersen/Workspace-qoomon/.gitconfig

[difftool "sourcetree"]

    cmd = opendiff \"$LOCAL\" \"$REMOTE\"

    path =

[mergetool "sourcetree"]

    cmd = /Applications/Sourcetree.app/Contents/Resources/opendiff-w.sh \"$LOCAL\" \"$REMOTE\" -ancestor \"$BASE\" -merge \"$MERGED\"

    trustExitCode = true

[maintenance]

    repo = /Users/bengtbrodersen/Workspace-qoomon/github-dashboard

[push]

    autoSetupRemote = true

    followTags = true

[user]

    name = Bengt Brodersen

git config user.email

includeIf
