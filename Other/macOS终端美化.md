# macOS美化及设置

> macOS美化及设置教程

### iTerm

* 安装：[下载地址](https://iterm2.com/downloads/stable/latest)

  ```bash
  $ brew cask install iterm
  ```

### oh-my-zsh

* 安装

  ```python
  # via curl
  sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
  
  # via wget
  sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
  ```

* oh-my-zsh主题及插件插件

  * zsh-autosuggestion

    ```bash
    # 安装
    git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
    
    # 添加到./zshrc中
    plugins=(zsh-autosuggestions)
    
    source ~/.zshrc
    ```

  * zsh-syntax-highlighting

    ```bash
    # 安装
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
    
    # 添加到./zshrc中
    plugins=(zsh-syntax-highlighting)
    
    source ~/.zshrc
    ```

  * autojump

    ```bash
    # 安装
    brew install autojump
    
    #在.zshrc中添加
    plugins=(autojump)
    
    [[ -s $(brew --prefix)/etc/profile.d/autojump.sh ]] && . $(brew --prefix)/etc/profile.d/autojump.sh
    
    source ~/.zshrc
    ```

* brew安装，更换及替换Homebrew默认源

  * 安装

    ```bash
    $ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    ```

  * 安装brew cask

    ```bash
    $ brew install cask
    ```

  * 替换默认源

    ```bash
    $ cd "$(brew --repo)"
    $ git remote set-url origin https://mirrors.ustc.edu.cn/brew.git
    
    $ cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
    $ git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
    
    $ brew update
    ```

  * 替换Homebrew-bottles二进制预编译包

    ```bash
    $ echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
    $ source ~/.bash_profile
    ```

  * 替换brew cask源

    ```bash
    cd "$(brew --repo)"/Library/Taps/homebrew/homebrew-cask
    git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git
    ```

  * 重置为默认源

    ```bash
    # 重置brew.git:
    $ cd "$(brew --repo)"
    $ git remote set-url origin https://github.com/Homebrew/brew.git
    
    # 重置homebrew-core.git:
    $ cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
    $ git remote set-url origin https://github.com/Homebrew/homebrew-core.git
    
    # Homebrew-bottles二进制只需注释或删除.bash_profile中的代码即可
    
    # 重置brew cask源
    $ cd "$(brew --repo)"/Library/Taps/homebrew/homebrew-cask
    $ git remote set-url origin https://github.com/Homebrew/homebrew-cask
    ```


### App允许任何来源下载安装

  ```bash
  $ sudo spctl --master-disable
  ```
### Dock设置

  * 设置启动台每行显示数量

    ```bash
    $ defaults write com.apple.dock springboard-columns -int 8 # 每行8个
    $ defaults write com.apple.dock ResetLaunchPad -bool TRUE;killall Dock # 重启dock
    ```

* 显示隐藏文件

  ```bash
  defaults write com.apple.finder AppleShowAllFiles -bool true ; killall Finder
  ```

* 隐藏隐藏文件

  ```bash
  defaults write com.apple.finder AppleShowAllFiles -bool false ; killall Finder
  ```

### 修改终端欢迎画面

1. `cd /etc`
2. `sudo pico motd`
3. [神奇的网站]
4. control + x，然后输入y保存

### 开启终端显示信息

  * 效果如下所示

  ![img](https://ws3.sinaimg.cn/large/006tKfTcly1ftoi367zyvj30qm0aaacz.jpg)


  * 相关链接

    * GitHub地址：https://github.com/athlonreg/archey-osx
    * 官网地址：https://athlonreg.github.io/archey-osx/

  * 安装

    ```bash
    $ cd && git clone https://github.com/athlonreg/archey-osx #若无法下载可直接到github下载zip文件
    $ sudo mv archey-osx/ /usr/local/ 
    $ sudo ln -s /usr/local/archey-osx/bin/archey /usr/local/bin/archey #中文版
    $ sudo ln -s /usr/local/archey-osx/bin/archey-en /usr/local/bin/archey-en #英文版
    ```
    设置终端自启动

    ```
    $ echo archey >> ./.bashrc #中文版
    $ echo archey-en >> ./.bashrc #英文版
    $ echo "[[ -s ~/.bashrc ]] && source ~/.bashrc" >> ./.bash_profile 
    $ source ./.bashrc && source ./.bash_profile 
    ```

  * oh-my-zsh用户

    ```bash
    $ echo archey >> ./.zshrc #中文版
    $ echo archey-en >> ./.zshrc #英文版
    $ source ./.zshrc 
    ```

  * 更新

    ```bash
    cd /usr/local/archey-osx/ && git pull && cd
    ```

  * 修改

    因为我的电脑显示显卡信息太长了，因此替换为用户名，只需修改archey文件中的User即可。

    ```bash
    User=$(echo $(whoami) | sed "s/-/ /g")
    ```

### 取消自动大写字词的首字母

	设置-键盘-文本-取消自动大写字词的首字母






