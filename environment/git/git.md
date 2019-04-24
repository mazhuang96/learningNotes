# git

## git config

配置信息存储在`~/.gitconfig`

```sh
# 查看帮助信息
git help config
# 查看配置的信息
git config --list  
# 修改全局名字
git config --global user.name "myname"
# 修改全局邮箱
git config --global user.email "123456789@qq.com"
# 删除全局设置
git config --global --unset <entry-name>  
```

## SSH KEY

```sh
# 生成密钥
ssh-keygen -t rsa -C '123456789@qq.com'
# 测试是否成功
ssh -T git@github.com
```