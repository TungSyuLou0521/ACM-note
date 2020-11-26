- 如果网站存在备份文件，在地址栏最末加上/index.php~或/index.php.bak，即可得到备份文件

- Robots.txt

- php一句话,用菜刀连接，使用webshell

- 命令执行漏洞（| || & && 称为 管道符）
windows 或 linux 下:
command1 && command2 先执行 command1，如果为真，再执行 command2
command1 | command2 只执行 command2
command1 & command2 先执行 command2 后执行 command1
command1 || command2 先执行 command1，如果为假，再执行 command2


- 127.0.0.1 && ls ../
cat 读入