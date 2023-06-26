## 使用此令牌

如需使用此 API 令牌：

- 请将你的用户名设为 `__token__`
- 将你的密码设置为令牌值，包括`pypi-`前缀

举个例子，如果你使用[Twine](https://pypi.org/project/twine/)来将你的程序上传至PyPI，像这样来设置你的`$HOME/.pypirc`文件：
```
[pypi]
  username = __token__
  password = pypi-AgEIcHlwaS5vcmcCJDQ4MjAzMDZiLTRlZjQtNDQ1YS1iYmM1LTQ5ZDcyNTU0ZTg2MwACKlszLCI5OWM3ZGI3Yi1mZDgxLTQ5NjQtYTA3OS1mZDYzNzBhYTEwZDgiXQAABiBdGjZK70cCrEZFkyehHC7HzMCuJBvw-2cyZdXdA4lPoA
```