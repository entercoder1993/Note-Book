# Problems of Python

### 1. PyCharm:AttributeError: module 'pip' has no attribute 'main'

* 解决步骤

  * 打开/Applications/PyCharm.app/Contents/helpers/packaging_tool.py

  * 修改do_install和do_uninstall

    ```python
    原来：
    def do_install(pkgs):
        try:
            import pip
        except ImportError:
            error_no_pip()
        return pip.main(['install'] + pkgs)
    
    
    def do_uninstall(pkgs):
        try:
            import pip
        except ImportError:
            error_no_pip()
        return pip.main(['uninstall', '-y'] + pkgs)
    
    修改后
    def do_install(pkgs):
        try:
            #import pip
            try:
                from pip._internal import main
            except Exception:
                from pip import main
        except ImportError:
            error_no_pip()
        return main(['install'] + pkgs)
    
    
    def do_uninstall(pkgs):
        try:
            #import pip
            try:
                from pip._internal import main
            except Exception:
                from pip import main
        except ImportError:
            error_no_pip()
        return main(['uninstall', '-y'] + pkgs)
    ```


### 2. 安装pyspider失败，提示PycURL how to specify the SSL backend manually.

* 卸载已存在pycurl

  ```bash
  $ pip3 uninstall pycurl
  ```

* 使用link-time ssl后端导出变量

  ```bash
  $ export PYCURL_SSL_LIBRARY=openssl
  ```

* 重新安装pycurl

  ```bash
  $ pip3 install pycurl
  ```

* 参考

  https://stackoverflow.com/questions/21096436/ssl-backend-error-when-using-openssl

### 3. 运行pyspider提示async=True, get_object=False, no_input=False

* 因为async和await从python3.7开始已经加入保留关键字中，参考[What's New Python3.7](https://docs.python.org/3.7/whatsnew/3.7.html)，所以async和await不能作为函数的参数名
* 需要降低python版本至3.6
* 