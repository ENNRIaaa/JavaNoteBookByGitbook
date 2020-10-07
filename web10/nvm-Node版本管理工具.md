# nvm Node版本管理工具

官方地址：[https://github.com/nvm-sh/nvm](https://github.com/nvm-sh/nvm)



### 安装

在终端输入命令：

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```

安装好后，在`.bash_profile`中添加环境变量：

```
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

环境变量添加完成后，`source ~/.bash_profile`使配置文件生效。



### 查看nvm版本：

```bash
nvm -version
```



### 常用命令:

下载、编译安装最新版本的node：

```bash
nvm install node # "node" is an alias for the latest version
```



安装指定版本node：

```bash
nvm install 6.14.4 # or 10.10.0, 8.9.1, etc
```



查看远程所有版本：(会罗列出node的所有版本，通过上面命令就可以安装指定版本)

```bash
nvm ls-remote
```



选择使用本地的版本：（如果本地安装多个版本，可以在不同版本间切换）

```bash
nvm use node
```



**[更多命令参见官方文档](https://github.com/nvm-sh/nvm)**

