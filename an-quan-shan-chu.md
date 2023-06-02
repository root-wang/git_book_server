# 安全删除

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

