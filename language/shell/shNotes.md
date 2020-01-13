# Shell Notes

## [Linux Shell 1>/dev/null 2>&1 含义](https://blog.csdn.net/ithomer/article/details/9288353)

shell中可能经常能看到：`echo log > /dev/null 2>&1`

命令的结果可以通过 %> 的形式来定义输出

- **/dev/null** ：代表空设备文件
- **\>** ：代表重定向到哪里，例如：echo "123" > /home/123.txt
- **1**  ：表示stdout标准输出，系统默认值是1，所以">/dev/null"等同于"1>/dev/null"
- **2**  ：表示stderr标准错误
- **&**  ：表示等同于的意思，2>&1，表示2的输出重定向等同于1

`1 > /dev/null 2>&1` 语句含义：

- 1 > /dev/null ： 首先表示标准输出重定向到空设备文件，也就是不输出任何信息到终端，说白了就是不显示任何信息。
- 2>&1 ：接着，标准错误输出重定向（等同于）标准输出，因为之前标准输出已经重定向到了空设备文件，所以标准错误输出也重定向到空设备文件。

## 整数比较

```text
-eq 等于,如:if [ "$a" -eq "$b" ]
-ne 不等于,如:if [ "$a" -ne "$b" ]
-gt 大于,如:if [ "$a" -gt "$b" ]
-ge 大于等于,如:if [ "$a" -ge "$b" ]
-lt 小于,如:if [ "$a" -lt "$b" ]
-le 小于等于,如:if [ "$a" -le "$b" ]
<   小于(需要双括号),如:(("$a" < "$b"))
<=  小于等于(需要双括号),如:(("$a" <= "$b"))
>   大于(需要双括号),如:(("$a" > "$b"))
>=  大于等于(需要双括号),如:(("$a" >= "$b"))
```

## shell中`$0,$?,$!`等的特殊用法

- `$$`  
Shell本身的PID（ProcessID）  
- `$!`  
Shell最后运行的后台Process的PID  
- `$?`  
最后运行的命令的结束代码（返回值）  
- `$-`  
使用Set命令设定的Flag一览  
- `$*`  
所有参数列表。如`"$*"`用「"」括起来的情况、以`"$1 $2 … $n"`的形式输出所有参数。  
- `$@`  
所有参数列表。如`"$@"`用「"」括起来的情况、以`"$1" "$2" … "$n"` 的形式输出所有参数。  
- `$#`  
添加到Shell的参数个数  
- `$0`  
Shell本身的文件名  
- `$1～$n`  
添加到 Shell 的各参数值。`$1`是第1参数、`$2`是第2参数…。

## 十位权限表示

常见的权限表示形式有：

```text
-rw------- (600)  只有拥有者有读写权限。  
-rw-r--r-- (644)  只有拥有者有读写权限；而属组用户和其他用户只有读权限。  
-rwx------ (700)  只有拥有者有读、写、执行权限。  
-rwxr-xr-x (755)  拥有者有读、写、执行权限；而属组用户和其他用户只有读、执行权限。  
-rwx--x--x (711)  拥有者有读、写、执行权限；而属组用户和其他用户只有执行权限。  
-rw-rw-rw- (666)  所有用户都有文件读、写权限。  
-rwxrwxrwx (777)  所有用户都有读、写、执行权限。
```

## sed 用法

- 参数
  - `-i` 直接修改文件
- 条件
  - `a\` 下一行追加
  - `i\` 上一行追加

```sh
# 在第4行后插入test
sed -i '4a\test' a.txt
# 在第5行前插入test
sed -i '5i\test' a.txt
# 在bbbb行后添加xiaowu
sed -i '/bbbb/a\xiaowu' file
# 在文件末尾添加一行
sed -i '$a\text' flie
```

## sleep

```sh
sleep 1  # 睡眠1秒
sleep 1s # 睡眠1秒
sleep 1m # 睡眠1分
sleep 1h # 睡眠1小时
```

## 执行sh ./xxx.sh出现：“Syntax error: “(” unexpected”的解决方法

代码对于标准bash而言没有错，因为Ubuntu/Debian为了加快开机速度，用dash代替了传统的bash，是dash在捣鬼，解决方法就是取消dash。

```sh
sudo dpkg-reconfigure dash
```

## expect

[ssh 自动交互脚本](http://xstarcd.github.io/wiki/shell/expect.html)
