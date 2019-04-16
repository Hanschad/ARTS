# 使用 win10 自带ssh生成公私钥

1. 打开PowerShell执行`ssh-keygen`命令生成公私钥

    `ssh-keygen -t rsa -b 4096 -C "username@domain.com"`

2. 检查ssh-agent服务是否开启，如果没有开启ssh-agent服务，则无法把专用密钥添加到ssh-agent的高速缓存中

    检查服务：`Get-Service ssh-agent`

    开启服务（管理员）：`Start-Service ssh-agent`

3. 把专用密钥添加到ssh-agent的高速缓存中

    `ssh-add ~/.ssh/id_rsa`

    `ssh-add.exe -L` 可以查看当前ssh-agent管理的密钥

4. 查看公钥添加到github中

    `type ~/.ssh/id_rsa.pub`

    打开github->setting->SSH and GPG keys 添加公钥

5. 测试连接是否成功

    `ssh -T git@github.com`

Powershell一些操作服务的命令：

Get-Service, 获取服务。

Start-Service，启动服务。

Stop-Service，停止服务。

Restart-Service，重启服务。

Suspend-Service，挂起/暂停服务。

Resume-Service，继续服务。

Set-Service，设置服务的属性。

New-Service，创建新服务。
