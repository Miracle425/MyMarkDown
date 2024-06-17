# 修复pip

Fatal error in launcher: Unable to create process using '"d:\VSCode\VSCodeProject\Code\Python\Jupyter\.venv\Scripts\python.exe"  "D:\VSCode\VSCodeProject\notebook\jupyter\.venv\Scripts\pip.exe" list': ???????????

```shell
pip uninstall pip
python -m ensurepip --default-pip
```
