# 快速上手

[连接](broken-reference)

[选择用户文件夹](broken-reference)

[代码与数据集](broken-reference)

[安全删除](broken-reference)

[端口服务页面](broken-reference)

[创建自己的账户和密码](broken-reference)

[创建定时任务](broken-reference)

[常用命令](broken-reference)

[使用代码版本管理使用代码版本管理](broken-reference)

[搭建GitLab代码仓](broken-reference)

\[TOC]

## 连接

打开windows平台中的cmd(命令提示符) 同时键入下面命令 并回车

> ping [10.68.131.253](mailto:yao@10.68.131.253)

必须接入了校园网,包括有线和无线,在路由器局域网内不能连通

出现上图中的样子就是可以连通服务器

在连通后输入下面命令 与服务器建立SSH连接

> ssh -p 22 [yao@10.68.131.253](mailto:yao@10.68.131.253)

在后面输入密码Yao557...

密码成功后与服务器连通

灰色框中的(base)是conda环境中的基本环境base环境, 所有python的代码都需要在一个虚拟环境中运行, 但是每个项目的环境依赖不同的话会造成冲突,所以使用conda进行环境管理, 也就是每个项目需要自己创建一个环境来运行代码

白色框中的 /mnt/sda1 是当前处在的目录, 这是一个挂载了4T的机械硬盘, 可以在将代码和数据集放置在这里,

红色框中的$是只当前是非root用户进行操作 有很多的读写操作会收到限制,不过只是运行代码不会有很多问题

连接通服务器后在cmd中很难进行操作,一般使用第三方软件操作,有Xshell,Xftp vscode,tabby

这里推荐使用tabby

所有软件都可以通过服务器下载

> scp [yao@10.68.131.253](mailto:yao@10.68.131.253):/mnt/sda1/software/tabby-1.0.189-setup-x64.exe /D:

重新打开一个命令提示符软件, 在cmd中输入上面的命令可以将tabby的安装包下载至本地目录的D盘符下 在/D:/path使用path可以自定义D盘下的指定目录

> 🚾服务器中的常用软件安装包

| Xshell-7.0.0113p.exe           | python-3.9.8.exe                    | EasyConnectInstaller.exe |
| ------------------------------ | ----------------------------------- | ------------------------ |
| Xftp-7.0.0119.exe              | python-3.8.9.exe                    |                          |
| VSCodeUserSetup-x64-1.57.0.exe | python-3.10.8-amd64.exe             |                          |
| tabby-1.0.189-setup-x64.exe    | Everything-1.4.1.1009.x64-Setup.exe |                          |

以tabby使用为例

点击设置后进入设置界面

在新设置中选择ssh连接

如下进行设置 名称自便, 主机是10.68.131.253 用户名是yao 身份验证方法选择密码

点击设置密码 Yao557... 回车后点击下方保存

看到刚才设置好的557 点击三角进行连接

选择接受并记住密钥

如下和在cmd中出现了一致的界面

### ftp

在tabby中也可以进行文件的传输 选择右上角的sftp

这里会直接进入到服务器的根目录这里是无法进行文件交换的 点击mnt

看到挂载的硬盘sda1 点击进入

绿色是数据集的目录 将数据集放置在该目录下

红色为个人文件夹 存放自己的文件和代码 software是刚才下载tabby等软件的目录

在tabby中上传文件夹比较麻烦 首先进入到software中

点击Xftp 会弹出下载至本地目录

等待上方的文件传输结束 速度过几秒后会很快

完成后打开本地文件进行安装

打开Xftp后 在弹出的对话框中 点击New

如下图进行设置

点击connect

红色框中的绿点为连接状态 蓝色框中为当前目录 在蓝色框中进行编辑 填入 /mnt/sda1 回车

进入到了前面的目录中 在这里右边是服务器的目录 左边是本地目录 可以直接通过鼠标拖拽将本地文件或文件夹发送至服务器

下方为当前传输速度和进度 可以右键下方的条目进行暂停 取消

同时在不需要root权限的目录中可以通过右键删除或者编辑服务器的文件

## 选择用户文件夹

登陆服务器器后 输入ls 列出当前目录下的文件和文件夹

通过 mkdir xxx-xxx-xxx 创建名称为 xxx-xxx-xxx的文件夹

再次使用ls可以看到新创建的文件夹

使用cd XXX-XXX-XXX可以进入到新文件夹中 (在输入X时可以使用TAB键自动补全该文件夹的名称

进入后 在命令提示符前当前目录也发生了变化 使用ls

由于是新创建的文件夹所以在该目录下没有任何文件

打开Xftp进入到 /mnt/sda1 中去可以看到新创建的文件夹 双击进入

在该目录下右键空白处可以创建新的文件夹 或者在左边将代码拖拽至右侧

如下将文件发送至该目录下 在shell中进入code目录 使用ls同样可以看到该文件

### 创建自己的pyhton虚拟环境

在base环境下创建自己的python虚拟环境

虚拟环境可以保证每个程序之间依赖隔离,避免造成依赖冲突 yourname 为环境名称 3.x为该环境python的版本号

注意使用 shift + ins 进行粘贴至shell中

> conda create -n yourname pyhton=3.x

使用conda env list 检查当前所有的虚拟环境

使用 conda activate yourname 可以进入该环境中

如下命令提示符前的虚拟环境变为了torch环境 也就是此时可以使用该环境中的依赖了

使用 conda deactivate可以关闭该环境 返回值base环境中

> 🚫注意一定要创建自己的虚拟环境并且推荐使用自己的用户名命名,因为其他用户清理自己的进程时,如果有其他人在用自己的环境会一起清理掉

如下图绿色为目前占用GPU的进程 蓝色为进程的PID用于清理 红色为环境的名称 可以很清楚的看到自己的环境中是否还有进程在占有显存

使用kill 清除进程 释放显存

> kill 102044 104550

## 代码与数据集

### 数据集的地址需要改为/mnt/sda1/dataset/xxx 对应的数据集位置

### 使用GPU前请先使用nvidia-smi命令查看GPU的使用情况

> 📌nvidia-smi

其中蓝色内为当前GPU的使用情况,红框中分别是GPU温度.GPU当前功率/额定功率 显存占用 **GPU** 实际运算能力的利用率 下方黄色为使用GPU的进程

之前将代码放在了目录下 现在需要激活对应的python环境来运行

### 运行代码详见(点击)

[jupyter](broken-reference)

### jupyter

#### jupyter后台运行(需要进行长时间的运行的代码)

使用如下命令来通过运行ipynb文件 该操作会将结果写入到html中

> jupyter nbconvert --to html --execute notebook.ipynb

此时ls 发现多出了一个html文件

在xftp中进入到对应目录 将html文件取回至本地目录

在浏览器中打开后可以看到输出

该方法建议在确定没有错误时可以使用 最好在本地debug后确定可以正常运行 同时在运行时(如下图),不能退出断开与服务器连接

使用下面语句将会在后台挂起该程序,此时可以进行断开操作 返回该进程的PID号码 用于kill 符号&的意思是挂起该任务

> 📌nohup jupyter nbconvert --to notebook --execute use-GPU.ipynb --output use-GPU.report &

上面的任务命令如下, 意思是将use-GPU.ipynb中代码全部执行 并将结果保存在use-GPU.report.ipynb中

\--to notebook 是将输出保存为ipynb文件格式 文件名为use-GPU.report.ipynb

可以将输出保存为html格式 使用--to html 注意该选择需要安装依赖nbconvert

> jupyter nbconvert --to html --execute use-GPU.ipynb --output use-GPU.report

主要如果不存在nohup.out文件 会自动创建该文件 并将终端输出到该文件中

但是如果已经存在nohup.out文件 会将新的任务的输出覆盖 如果需要将后续任务输出添加到该文件中则需要

> nohup jupyter nbconvert --to notebook --execute use-GPU.ipynb --output use-GPU.report &

上面是将任务jupyter nbconvert --to notebook --execute use-GPU.ipynb --output use-GPU.report的输出结果将追加到nohup.out文件中

看到nohup.out为该程序的输出(不是代码运行结果而是终端输出)

使用vim nohup.out可以检查输出

看到writing XXXX bytes to xxxx.html 则说明程序结束了

按住shift和冒号 屏幕下方出现 : 此时输入 q 然后回车退出该界面(vim使用方法)

但是有时候需要将输出追加到nohup.out中也就是

> nohup jupyter nbconvert --to notebook --execute draft.ipynb --output draft.report >> draft.out 2>&1 &

注意第一条命令是新建一个文件draft.out来记录任务输出结果

而第二个是将该任务第二次执行的结果追加到之前的日志中

在draft.out中可以看到两个任务的情况

如果会有很多的任务输出结果添加在文件draft.out 中但是shell并没有提供时间戳这里可以使用函数

```python
def showProcessEndTime():
    os.system(time.strftime("echo %Y-%m-%d %H:%M:%S", time.localtime()))
```

在代码文件的末尾执行该函数则可以将任务结束时间记录在日志中

这里我们将在日志文件中添加这个任务的结束时间方便分辨任务

当然也可以将不同任务分开使用不同的文件记录输出 也方便分开查询任务是否在后台完成

### 使用 screen 程序保存当前shell的对话记录以及进程

[screen](https://www.wolai.com/jvQsnm1sokiAKzLUyUuTdo)

### VSCode(推荐使用)

vscode帮助集成了ssh远程连接, 文件上传下载, 代码编辑及运行, 可以十分方便的在本地使用服务器来运行调试代码

使用Xftp在服务器获取VSCode安装包进行安装 如下 点击扩展图标

搜索chinese 自动出现搜索结果 点击简体中文安装 然后右下角会提示restart

同理 继续搜索扩展remote 点击下图所示插件进行安装

安装成功后重启vscode在左下角看到橙色图标点击

在上方弹出窗口后选择Connect to Host

选择Configure SSH Hosts

在弹出的列表中选择第一个(一般是)注意红色框中一般为自己计算机的用户名(因人而异)

点击后自动打开该文件 按照红色框中的内容进行填写Host为自定义名称 使用ctrl+s 进行保存

保存后会在侧边栏的远程资源管理器中可以看到557选项,点击在新窗口中连接

应当选择Linux

缺失图片

输入密码 Yao557...

如下即为连接成功

点击打开文件夹 将/home/yao/ 改为/mnt/sda1/

此时会自动显示该目录下的文件夹 选择自己的文件夹

点击确定

点击红色图标显示操作终端 绿色为该目录下的文件 再次点击红色隐藏终端

点击右侧ipynb文件可以直接打开

此时有了代码 还需要选择python环境 点击红色选择内核在弹出的窗口中选择其他内核

选择 Python环境

可以看到目前服务器miniconda中所有的的虚拟环境 选择需要的环境即可 这里和在终端使用

conda env list 结果一致

有了环境之后 可以直接运行代码

选择绿色执行所有代码 点击每个cell的红色执行该代码

同理对于需要后台运行的代码可以在vscode调试好 然后在vscode提供的终端中进后台运行

vscode中可以直接使用ctrlcv复制粘贴

[在vscode中默认记住密码（点击）](broken-reference)

### 在vscode中默认记住密码（点击）

在自己电脑打开cmd 输入

> ssh-keygen

一路yes或者回车即可

进入自己的电脑目录 XXX为自己的电脑用户名

> C:\Users\XXX\\.ssh

在该目录下找打文件 id\_rsa.pub

复制文件并重命名为自己的服务器用户名 如 XXX-XXX-XXX.pub

打开tabby 打开sftp 一路点击进入.ssh 文件夹中 并将刚才改名的文件上传至该处

在终端中进入到 /home/yao/.ssh 目录中 键入 ll 看到上传的文件

将 XXX-XXX-XXX.pub 改为实际文件 并使用下述的命令执行

如需输入密码 则为 Yao557...

> sudo cat XXX-XXX-XXX.pub >> authorized\_keys

此时关闭vscode再次登陆的话则不需要输入密码了

### 需要注意要将数据放在GPU上运行

在运行时可以在vscode终端 输入nvidia-smi查看当前GPU占用

### pytorch

对于pytorch框架提供下面函数来选择GPU

```python
def try_gpu(i=0):
    """Return gpu(i) if exists, otherwise return cpu()."""
    if torch.cuda.device_count() >= i + 1:
        return torch.device(f'cuda:{i}')
    return torch.device('cpu')
```

## 安全删除

使用回收站形式来管理服务器删除的文件 自定义操作代替了rm命令

```bash
TRASH_DIR="/mnt/sda1/.trash"  

for i in $*; do  
    STAMP=`date +%s`
    STAMP=`date -d @$STAMP '+%m-%d-%H-%M'`  
    fileName=`basename $i`  
    mv $i $TRASH_DIR/$fileName.$STAMP  
done
```

注册该操作在 \~/.bashrc 中进行设定

```bash
alias rm="sh /home/yao/tools/remove.sh"
```

使用crontab执行每个月的第一天清空回收站

```bash
0 0 1 * * rm -rf /mnt/sda1/.trash/*
```

需要找回删除文件进入到 /mnt/sda1/.trash 中查看

```bash
cd /mnt/sda1/.trash
```

## 注意：任何时候删除不要使用通配符 \*

## 端口服务页面

80 动手学深度学习电子网页

15732 jupyter 内核基于pytorch

[8096 Emby在线影音服务](broken-reference)

### 8096 Emby在线影音服务

该端口服务提供音视频在线流媒体播放以及下载

在浏览器键入下方地址进入

> [http://10.68.131.253:8096/](http://10.68.131.253:8096/)

每个用户应当设定属于自己的用户名和账户, 一是方便管理, 二是使用不同的账户登陆可以进行个人个性化定制与账户的观影记录

#### 账户注册方式

自己想好账户名和密码 微管理员进行注册即可

#### 重要:自己上传音视频

打开Xftp 进入目录 /mnt/sda1/resource 下 看到音视频文件夹

#### 音乐

直接将本地的音乐文件上传至该文件夹下或者自行建立文件夹

> ‼️必须使用英文字符命名音乐文件

#### 视频

上传即可

> ‼️必须使用英文字符命名视频文件 格式为 SXEX 即第几季第几级

音乐视频均已启用文件夹实时监控 上传完毕后服务会自动扫描更新

如未发现则在设置中自行扫描

### 建立新的端口服务需要在port-mapping.json中注册

### 开放端口需要联系管理员

```bash
vim /mnt/sda1/port-mapping.json
```

## 创建自己的账户和密码

> ‼️(此为高级操作) 如无必要 则无需进行

此操作可以为用户创建一个属于自己的ssh连接账户,用户保护自己隐私,可以达到的目的是禁止其他用户进入或执行或修改自己文件夹下的所有文件

1. 使用yao用户进行登陆 键入命令

> lastlog

拉到最后可以看到一般账户yao以及我们需要自己创建的私人账户,这里是管理员自己创建的账户root-wang

使用下面的命令创建一个名为XXX-XXX-XXX 所属组为yao 登陆时进入的文件夹(用户根目录)为/mnt/sda1/XXX-XXX-XXX下 的账户 -m的意思是如果不存在该目录则会创建该目录

这里只需要修改XXX-XXX-XXX为自己的账户名

> 🚾sudo useradd -s /bin/bash -d /mnt/sda1/XXX-XXX-XXX -g yao -m XXX-XXX-XXX

输入密码Yao557... 进行用户创建

此时提示用户文件夹已经存在 则不需要重新创建

再次输入 此时在最后可以看到新的用户

> lastlog

但是还没有为该账户设置密码是无法使用的 输入命令设置新的密码

> sudo passwd XXX-XXX-XXX

这里密码设置为123456

进入终端应用主机设置不变 用户名为设置的用户名 XXX-XXX-XXX 密码为123456

点击连接进入到该用户的命令终端中去

此时可以看到用户为XXX-XXX-XXX 而用户组还是yao

输入ls则可以看到该用户目录下的所有文件

使用cd .. 可以退出到上一级目录 还记得我们设置用户登陆的目录是/mnt/sda1/XXX-XXX-XXX

则退到父目录为/mnt/sda1 如下则是

此时在XXX-XXX-XXX的父级目录键入

> ls -ll

可以看到所有文件夹的权限 首先看黄色的内容 d是文件类型无需理会

linux将文件夹权限分为读取(r) 改写(w) 执行(x)

对于使用者也分了三类为文件所属用户(u-User) 所属组(g-Group) 除开所属用户和组之外的所有用户(o-Others)

所以文件夹XXX-XXX-XXX的权限是用户XXX-XXX-XXX拥有所有权限, 组yao的其他用户拥有读取和执行权限,组外其他用户拥有读取和执行的权限

> 😅d rwx r-x r-x

| linux表示 | 说明      | linux表示 | 说明    |
| ------- | ------- | ------- | ----- |
| r—      | 只读      | -w-     | 仅可写   |
| —x      | 只可执行    | rw-     | 可读可写  |
| -wx     | 可读可执行   | r-x     | 可读可执行 |
| rwx     | 可读可写可执行 | —-      | 无权限   |

则我们需要的是将权限改变为所属用户u拥有所有权限 而其他两个不有任何权限 则如下的权限

```bash
d rwx --- ---
```

### 以下步骤请联系管理员进行操作

则是执行如下的操作 chmod 是改变文件夹的权限 g-r 的意思是对于该文件夹组内其他用户取消读取该文件夹的权限

> chmod g-r XXX-XXX-XXX/

此时键入ll 则可以看到文件夹的权限变化

但是这只是改变了文件夹的权限 而注意该文件夹的所有者是yao 而我们要做的是将所有者改为XXX-XXX-XXX

下述命令是将文件夹XXX-XXX-XXX/的所有这改为XXX-XXX-XXX

> chonw XXX-XXX-XXX XXX-XXX-XXX/

再次键入ll注意到所有者变为了XXX-XXX-XXX

### 测试

使用用户yao进入系统 然后尝试进入文件夹XXX-XXX-XXX会提示权限不足

### 此时使用账户XXX-XXX-XXX登陆终端

发现无法使用conda命令而且在命令提示符前也没有登陆就有的默认conda环境

这是因为新创建的用户没有办法读取到安装conda的用户yao的环境

此时使用用户yao登陆

使用下面的命令将yao用户的环境配置复制到新用户的根目录下也就是 /mnt/sda1/XXX-XXX-XXX

注意将XXX-XXX-XXX 改为实际用户目录

> sudo cp \~/.bashrc /mnt/sda1/XXX-XXX-XXX/.bashrc

输入密码后此时无法进入XXX-XXX-XXX的用户目录下

由于文件.bashrc的所有者是root 其他用户也只是只读无法执行 所以联系管理员更改该文件的所有者为XXX-XXX-XXX

修改文件.bashrc所有者为 XXX-XXX-XXX 所有组为yao

> chown XXX-XXX-XXX:yao .bashrc

### 使用用户XXX-XXX-XXX登陆

虽然获得了配置文件但是还没有生效 此时键入ll等命令无效

> source .bashrc

使用上述命令立即生效 则读取到系统的conda环境并激活为base

但是当关闭终端再次登陆时会发生问题

新登陆的终端并没有默认激活conda环境这是因为没有设置.bash\_profile文件

在用户根目录下使用命令

> vim .bash\_profile

在vim中复制下面的代码

```bash
# .bash_profile
        
if [ -f ~/.bashrc ]; then
    . ~/.bashrc                                                                                                                    
fi 

```

最后使用 :wq 回车保存退出

关闭终端再次连接 问题解决

.bashrc文件是用户yao的配置所以生效后会发现登陆的初始目录发生了变化

这里来修改文件的配置 进入XXX-XXX-XXX目录中

> vim .bashrc

红色为用户yao的环境配置文件所以默认进入目录为 /mnt/sda1

修改其为自己的目录 然后保存退出

关闭后重新连接 使用命令

> pwd

查看当目录的路径 解决问题

🎉

## 创建定时任务

## 常用命令

## 使用代码版本管理使用代码版本管理

## 搭建GitLab代码仓
