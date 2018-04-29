
- 修改`.gitconfig`文件,路径：` C:\Users\你的用户名\.gitconfig`。
![](https://i.imgur.com/lh6LW3b.png) 

- 可以通过记事本打开，我这里习惯用`sublime`。`[user]`不变。添加`[gui]`、`[core]`。
![](https://i.imgur.com/3JeDNnh.png)

- 生成`ssh key`，输入： `ssh-keygen -t rsa -C "你的邮箱"`
![](https://i.imgur.com/DFASdfU.png)

- 复制ssh key，在`C:/Users/Administrator/.ssh/id_rsa.pub`文件找到直接复制。
![](https://i.imgur.com/wIZZ2un.png)

- 也可以输入：` clip < ~/.ssh/id_rsa.pub `会自动复制`ssh key`，可以直接粘贴。

- 打开`GitHub`，进入`setting`找到`ssh key`并新建。将内容复制过来。
![](https://i.imgur.com/Y01RydB.png)

- 输入完成后会有一个`key`在`SSH`中。
![](https://i.imgur.com/0PYhpwy.png)

- 在`git`中输入：`ssh -T git@github.com`，`yes`，`回车`。出现如图所示，就证明连接成功了。
![](https://i.imgur.com/fldwseN.png)

在`git`中输入：`git clone XX`，`XX`是你复制的自己仓库的地址。我的地址是`https://github.com/xuchaoyu2000/Bblog.git`。
![](https://i.imgur.com/UHHWnYJ.png)

---

