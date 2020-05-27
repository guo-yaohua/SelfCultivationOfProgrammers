# Ubuntu 子系统安装使用

## 目录

- [Ubuntu 子系统安装使用](#ubuntu-子系统安装使用)
  - [目录](#目录)
  - [背景](#背景)
  - [安装](#安装)
  - [使用](#使用)
    - [zsh](#zsh)
    - [更换阿里源](#更换阿里源)
    - [去除ls时目录背景色](#去除ls时目录背景色)
    - [配置Java环境](#配置java环境)

## 背景

操作系统：windows10  
最近使用时间：2020.5.25

## 安装

第一步：  

设置 -> 更新和安全 -> 开发者选项 -> 勾选 **开发人员模式**。  
![p1](./img/p1.png)  

第二步：  

控制面板 -> 程序 -> 启动或关闭 Windows 功能 -> 勾选 **适用于 Linux 的 Windows 子系统**。 

![p2](./img/p2.png)  
![p3](./img/p3.png)  

第三步：  

打开 Microsoft Store，搜索 Ubuntu 下载即可。

## 使用

第一次打开 Ubuntu 会加载一会，加载完成后会提示设置一个用户名和密码，然后就可以正常使用。  

### zsh

安装 zsh：  
```
sudo apt-get install zsh
```  
安装后通过 `zsh --version` 可以查看 zsh 的版本。  

安装 oh-my-zsh 可以通过 curl 或者 wget 方式，或者直接 git clone（2020.5.25 发现前两种方式失效，所以直接选择 git）：  
- curl：  
  ```
  sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
  ```  

- wget:  
  ```
  sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
  ```

- git：
  ```
  git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh

  cp ~/.zshrc ~/.zshrc.orig
  cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
  ```
把默认的 Shell 改成 zsh：  
```
chsh -s /bin/zsh
```

添加插件：
- 自动语法高亮 zsh-syntax-highlighting
  ```
  git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
  ```

- 自动输入建议 zsh-autosuggestions
  ```
  git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
  ```

- 修改 zshrc 文件 `vim ~/.zshrc`，启用插件：
  ```
  plugins(git
  zsh-syntax-highlighting
  zsh-autosuggestions
  )
  ```
  最后执行 `source ~/.zshrc`。

### 更换阿里源

第一步备份：
```shell
sudo rm /etc/apt/sources.list /etc/apt/sources.list.bak
```

第二步更换：
```shell
sudo vim /etc/apt/sources.list
```
添加阿里源：
```
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal universe
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates universe
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security universe
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security multiverse
```

第三步更新：
```shell
sudo apt update && sudo apt upgrade
```

### 去除ls时目录背景色

在 `./zshrc` 配置文件中添加设置：
```
# for ls colors
LS_COLORS="rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=01;34:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.Z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.jpg=01;35:*.jpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.axv=01;35:*.anx=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.axa=00;36:*.oga=00;36:*.spx=00;36:*.xspf=00;36:"
export LS_COLORS
```

### 配置Java环境

第一步：  
下载  JDK（笔者选择的版本为  JDK8，想选择其他版本可自行更改），下载地址：  
http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html  

选择 64 位，Linux 压缩包。  
![Linux x64 Compressed Archive	](./img/p4.png)  

第二步：  
打开 Utuntu 命令行，创建 /usr/lib/jvm 文件夹，并将下载的压缩包移到此处，然后解压。  
```
sudo mkdir /usr/lib/jvm
sudo mv /mnt/c/User/你的电脑用户名/Downloads/jdk-8u241-linux-x64.tar.gz /usr/lib/jvm
sudo tar -zxvf jdk-8u241-linux-x64.tar.gz
```

第三步：  
配置环境变量。使用命令：`sudo vim ~/.zshrc`（如果没有安装 zsh，则使用 `sudo vim ~/.bashrc`）。  

在打开的文件底部添加四行命令：  
```
export JAVA_HOME=/usr/lib/jvm/jdk1.8.0_241（如 jdk 版本与笔者不同就自行更改）
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```


最后执行命令：`source ~/.bashrc`（如果没有安装 zsh，则使用 `source ~/.bashrc`）使配置生效。

第四步：  
检查环境变量是否配置成功：`java -version`。