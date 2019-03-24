## iterm美化

[屏蔽](https://blog.csdn.net/z3512498/article/details/51245853)

[iterm2配置](https://www.cnblogs.com/xishuai/p/mac-iterm2.html)

[iterm2美化](https://www.jianshu.com/p/7de00c73a2bb)

将用户名变短
sudo hostname shaw

ys主题，agnoster主题

bullet-train



## iterm设置别名
1.`vim .bashrc   .bash_profile   .zshrc`

2.

```
## project path
alias meili="cd ~/Desktop/meili"
alias learn="cd ~/Desktop/learning"
alias note="cd ~/Desktop/learning/note"
alias ml="cd ~/Desktop/meili"
alias blog="/Users/shawzhou/Desktop/learning/blog"
alias docs="/Users/shawzhou/Desktop/meili/docs"


# git command
alias gm="git commit -am"
alias gp="git push"
alias gn="git commit -n -am"

# task
#alias mysql='/usr/local/mysql/bin/mysql'
alias mysqluse="mysql -u root -p"
alias code='/Applications/Visual\ Studio\ Code.app/Contents/Resources/app/bin/code'
```


3. 设置git commit 进入vim编辑模式
`git config --global  core.editor vim`


