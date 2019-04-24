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


## vim

* :w - 保存文件，不退出 vim
* :w file -将修改另外保存到 file 中，不退出 vim
* :w! -强制保存，不退出 vim
* :wq -保存文件，退出 vim
* :wq! -强制保存文件，退出 vim
* :q -不保存文件，退出 vim
* :q! -不保存文件，强制退出 vim
* :e! -放弃所有修改，从上次保存文件开始再编辑

