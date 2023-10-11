
1. 安装vscode 插件 gitlens 成功后会有GitLens的图标
2. 点击图标, 点击Commits 这里会展开当前分支的所有历史提交记录
3. 右键选择一个你想要回退到的记录,在菜单上选择 Reset Current Branch to Commit...
4. 再在后面弹的菜单中选择Reset, 这样就会回退到当前这个记录被改成上一个记录还未提交的状态
5. 这个时候再去正常的Source Control那里把所有没提交的改动全部revert掉
6. 这个时候线上会同步显示的最新改动过来, 不要更新同步, 不然白改了
7. 直接用命令 git push origin xxx --force 把这个分支再提交为最新的状态

当然这个是比较保险的做法.
