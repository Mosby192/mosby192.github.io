#git对应多个远端

##生成 ssh key

系统默认得ssh key存放在`~/.ssh/`目录下；
```
ssh-keygen -t rsa -f ~/.ssh/key -C "youemail@email.com"
```
其中：
- `-t`指定加密类型（此处为rsa,默认为rsa）;
- `-f`指定路径及文件名（key为ssh key名称，可以不指定，可以不指定，在提示后命令行输入）;
- `-C`注释(一般填写邮箱账号，用于注释账号或者用途);

按照提示输入密码（也可以不输，直接回车），之后得到两个密钥文件（key私钥，key.pub公钥）；

如果不修改路径及文件名，可以直接使用如下命令：
```
ssh-keygen -t rsa -C "youemail@email.com"
```
得到两个密钥文件（id_rsa和id_rsa.pub）;

##配置config

在`~/.ssh/`新建一个`config`文件;
内容为：
```
Host github.com
    HostName github.com
    User xxx@qq.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/ssh1
Host xiao.com
    HostName github.com
    User xxx@qq.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/ssh2
```
其中：
```
Host #用来匹配将要连接服务器得地址，可是使用任意字段或者通配符，实际使用的地址为HostName中的地址
    HostName #真正连接服务器的地址
    User #自定义用户名
    Port #自定义端口号
    PreferredAuthentications #指定优先使用哪种验证方式（publickey公钥）
    IdentityFile ~/.ssh/ssh2 #密钥的路径
```

##上传公钥

将公钥（.pub）内容复制到github或者gitlab等平台上；

##连接测试

在命令行中输入：
```
ssh -T git@host //host是在config中自定义的
```
根据提示判断配置是否正确；

##拉取代码

在命令行中输入：
```
git clone git@host:account/project.git
```
其中：
- `host`对应于之前config文件中的Host配置；
- `account`为用户名（例如github的账号）；
- `project`为仓库的名称；

##关联本地仓库和远端仓库

```
git remote add origin git@host:account/project.git
```
在 ./.git/config文件中可以修改配置

##*ssh-agent

ssh-agent就是一个密钥管理器(临时存储,重启后清空)，用户只需要输入一次密码（如果设置了密码）;

- 使用`eval "$(ssh-agent -s)"`启用ssh-agent，或者输入`ssh-agent bash`进入ssh-agent操作环境；
```
eval "$(ssh-agent -s)" //等效于
eval `ssh-agent -s`
```
- 获取ssh-agent中代理的ssh-key私钥`ssh-add -l`;
- 查看私钥对应的公钥`ssh-agent -L`;
- 添加私钥`ssh-add ~/.ssh/id_rsa`;
- 移除指定私钥`ssh-add -d /path/key_name`;
- 移除代理的所有私钥`ssh-add -D`;