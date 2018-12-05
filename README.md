# Auto-squasher
Automagically Git Squash the last N Commits.

## Background
In most cases, the commits I want to squash are at the tip of a certain branch. This tool allows me to squash them easily with a single command. If you need to squash commits that are somewhere in the middle of your commit history, than you will need to run `git squash` manually. 

## Code

```bash
squash () {
    if [[ "$1" ]]; then
        git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit | head -$1
        read -q "REPLY?Squash the commits above? [y/N]"
        if [[ $REPLY =~ ^([yY][eE][sS]|[yY])$ ]]; then
            echo -en '\n'
            git reset --hard HEAD~$1
            git merge --squash HEAD@{1}
            git commit
        else
            echo "No squash occured"
        fi
    fi
}

```

## Setup

- Add contents of `./squash.function` to your bashrc/zshrc file.
- Source the file.

## Usage

- Call `squash` with the number of commits at the tip of your branch to squash. For example `$ squash 10`. 
- Auto-squasher will confirm the commits to be squashed before running.
- After confirming, a premade commit messsage will appear in your default editor. Update this with a commit message that summarizes the child commits.

## License

MIT. Copyright (c) 2018 Michael. See `./LICENSE` file for details
