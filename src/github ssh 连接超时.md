# Github ssh 连接超时

# 背景

因为考试和其他一系列原因，两个月没写代码，考试过后想着看看之前搁置的项目，结果在使用 ssh 拉取仓库代码时，一直连接超时。检查、切换代理后依然没有解决问题，恰好某群群友正在讨论相关的问题，最后发现只需要将 `git@github.com:<username>/<responsitory name>.git` 改为 `git@ssh.github.com:<username>/<responsitory name>.git` 即可成功拉取仓库。

但这样只能解决拉取时的超时问题，代码提交时依然会连接超时。又经过一番搜索后，得到了如下的解决方案。

## 解决方案

创建 `~/.ssh/config` 文件，该文件包含以下内容：

```bash
Host github.com
User git
Hostname ssh.github.com
PreferredAuthentications publickey
# 将 $id_rsa 替换为对应的密钥
IdentityFile ~/.ssh/$id_rsa
Port 443
```

之后即可正常进行 `git clone`、`git push` 操作。