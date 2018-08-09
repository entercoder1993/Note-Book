# Problems of Python

### PyCharm:AttributeError: module 'pip' has no attribute 'main'

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

    