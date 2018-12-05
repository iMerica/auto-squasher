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