# macOS终端美化

> macOS终端美化教程

* iTerm

* oh-my-zsh

* oh-my-zsh主题及插件插件

* 开启终端显示信息

  * 效果如下所示

    ![img](https://ws3.sinaimg.cn/large/006tNc79ly1ftcvzcwemfj30qw0aqwhd.jpg)

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

  * 设置终端自启动

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

    



