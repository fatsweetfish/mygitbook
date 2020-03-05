## github免密提交代码

* **准备好pub key**

```
rm -rf ~/.ssh/*
ssh-keygen -t rsa -C "fatsweetfish@aliyun.com"

```

把id_rsa.pub内容贴到github ssh key上

```
账号头像->setting->SSH and GPG keys->New SSH key->添加title名字和公玥->Add SSH key
```

验证成功与否

```
ssh -T git@github.com
```

出现

```
Hi fatsweetfish! You've successfully authenticated, but GitHub does not provide shell access.
```

表示成功

* **ssh 免密提交**

```
git remote -v
origin	https://github.com/fatsweetfish/mygitbook (fetch)
origin	https://github.com/fatsweetfish/mygitbook (push)

```

我们clone用https，现在要更改它为ssh方式

```
git remote set-url origin git@github.com:fatsweetfish/mygitbook.git
git remote -v
origin	git@github.com:fatsweetfish/mygitbook.git (fetch)
origin	git@github.com:fatsweetfish/mygitbook.git (push)

```

`git@github.com:fatsweetfish/mygitbook.git`这个url是在github上复制的

Clone or download-> Uss SSH->复制url

执行git push后不用输密码了