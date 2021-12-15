
# 重装ubuntu

先使用pe安装win10，然后再参考之前的教程安装ubuntu。安装完成后需要进行的步骤如下。

## 安装必要软件(For me)

[谷歌浏览器](https://www.google.cn/intl/zh-CN/chrome/)

vpn  这个因人而异

[vscode](https://go.microsoft.com/fwlink/?LinkID=760868)

[Typora](https://typora.io/)

录制屏幕 sudo apt-get install simplescreenrecorder

播放视频 sudo apt-get installmplayer

### vscode相关

相关字体： 在https://github.com/tonsky/FiraCode下载字体

```json
{
    "editor.fontFamily": "Fira Code",//后边的引号中写上要设置的字体类型，个人比较喜欢Fira Code
    "editor.fontLigatures": true,//这个控制是否启用字体连字，true启用，false不启用，这里选择启用
    "editor.fontSize": 18,//设置字体大小，这个不多说都明白
    "editor.fontWeight": "normal"
}
```

vscode插件：C/C++， run code， git graph 可视化git， git 强化功能 GitLens，括号高亮插件 Bracket Pair Colorizer ，TODO 高亮 todo highlighter，缩进深度提示 Indenticator，图标美化 VSCode Great Icons， 

一款vscode颜色主题 ：安装命令`ext install dracula-theme.theme-dracula`，安装后在首选项中配置即可。

### NodeJs 

`nvm install`默认是从 http://nodejs.org/dist/ 下载安装包的，但这是国外服务器，通常速度会非常缓慢。

幸好，nvm提供了一种方式可以指定下载源，我们通过设置环境变量`NVM_NODEJS_ORG_MIRROR`，把下载源指向到[淘宝的镜像](https://npm.taobao.org/mirrors/node)，安装速度就能大大提高。

代码如下：

```bash
NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node nvm install 6.3
```

可以把环境变量加到 `~/.profile` 或者 `~/.bashrc` 里面

```bash
NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node
source ~/.nvm/nvm.sh 
```

另外，npm的加速也是一样的原理. [淘宝的cnmp镜像](https://developer.aliyun.com/mirror/NPM?from=tnpm)

## 更换国内镜像源

[更换清华镜像源](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)

## ZSH 配置

### 安装 zsh

```shell
sudo apt-get install zsh
```

### 修改 shell

- 查看系统安装了哪些 shell

  ```shell
  cat /etc/shells
  ```

- 查看正在使用的 shell

  ```shell
  echo $SHELL
  ```

- 修改默认 shell（重启系统后生效）

  ```shell
  # username 可缺省，表示当前用户
  chsh -s /bin/zsh username
  ```

### 安装 git

```shell
sudo apt-get install git
```

### 安装 oh-my-zsh

oh-my-zsh官网： https://ohmyz.sh/

如果下载install.sh有问题可以直接使用这个install.sh。

### 安装 zsh-syntax-highlighting 语法高亮插件

```shell
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

git clone git@github.com:zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

修改 .zshrc，在 plugins 里添加 `zsh-syntax-highlighting`

```shell
sudo gedit ~/.zshrc
```

修改后如：`plugins=(git zsh-syntax-highlighting)`

### 安装 zsh-autosuggestions 语法历史记录插件

```shell
git clone git://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

修改 .zshrc，在 plugins 里添加 `zsh-autosuggestions`

```shell
sudo gedit ~/.zshrc
```

修改后如：`plugins=(git zsh-syntax-highlighting zsh-autosuggestions)`



##### 修改颜色

```shell
sudo vim /usr/share/zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
```


### 修改主题

```shell
sudo vim ~/.zshrc
```

修改主题为 `ZSH_THEME="ys"`

或者 https://github.com/sindresorhus/purepure

```shell
# pure theme config
fpath+=$HOME/.zsh/pure
autoload -U promptinit; promptinit
prompt pure
export PURE_PROMPT_SYMBOL="➜ "
zstyle :prompt:pure:git:stash show yes
zmodload zsh/nearcolor
zstyle :prompt:pure:path color "#C2ABE3"
zstyle :prompt:pure:prompt:success color "#C3B54B"
```

### 修复在tmux下背景白色问题

```shell
echo  "export TERM=xterm-256color" >> ~/.zshrc
```


### 参考

https://segmentfault.com/a/1190000013612471