### python写leetcode中 遇到的基本问题

1.

problem:`mapping.reverse()` 的返回值是 None，而不是字符串，因此无法使用 `+=` 运算符。

solution:使用 `mapping[::-1]` 来反转字符串。

2.range打错次数 ： 1 

3. 'str' object cannot be interpreted as an integer 这个错误信息表明你正在尝试在一个期待整数（integer）的地方使用字符串（string）

3. truncation 截断

3. `zfill` 方法只能用于字符串对象 (`str`)，而不能直接用于整数 (`int`) 类型。前导零通过 zfill 填充

   ```python
   str_num = "42"
   filled_str = str_num.zfill(5)
   print(filled_str)  # 输出 "00042"
   ```

3. `1 << i` 是一个位运算表达式，表示将数字 `1` 向左移动 `i` 位。

3. 在Python中，字符串切片操作 s[i:i+k] 是安全的，即使切片的**结束索引**超出了字符串的实际长度，也不会引发越界错误。Python会自动处理这种情况，返回从起始索引 i 开始到字符串末尾的所有字符。

   **开始索引超出字符串长度时**：如果开始索引 `i` 大于等于字符串的长度，Python 会返回一个空字符串，而不会引发错误。

3. 因为 set 是可变的类型，不能作为字典（dict）的键，而 frozenset 是不可变的集合类型，可以作为字典的键。

3. 修改字符串的某一个字符： 字符串拼接 join函数

   

   ### 解释：

### 使用jupyter notebook遇到问题

**切换盘符命令** 直接输入 d:

问题：Bad file descriptor (C:\ci\zeromq_1602704446950\work\src\epoll.cpp:100) 

解决办法：**卸载重新安装`pyzmq`**

用管理员身份打开 anaconda powershell prompt

pip uninstall pyzmq

pip install pyzmq

问题：ModuleNotFoundError: No module named 'ipympl'

解决办法：

用管理员身份打开anaconda

执行conda install -c conda-forge ipympl

重启jupyter notebook即可正常使用%matplotlib widget 进行3D交互式绘图模式