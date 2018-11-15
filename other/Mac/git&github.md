# git 
安装完成后在终端输入git查看是否安装成功。
# github
- 在终端中输入:  
- git config --global user.name "black"
- git config --global user.email "black20@foxmail.com"
- ssh-keygen -t rsa -C "black20@foxmail.com"
- 一路回车，然后输入mac密码并确认。
- cat .ssh/id_rsa.pub
- 复制ssh在github中设置ssh key里添加。
- ssh -T git@github.com 后输入yes并输入密码后验证是否添加成功。
- 克隆到本地:   
- cd /Users/localadmin/Desktop  (每个人的本地路径都不太一样)
- git clone git@github.com:xuchaoyu2000/myMind.git
- 修改内容后:
- cd /Users/localadmin/Desktop/myMind
- git add .
- git commit -m "change"
- git push
