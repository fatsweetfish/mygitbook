## tiny skills

#### 1.github提交代码免密

```
cd ~
touch .git-credentials
```

写入

`https:account:pwd@github.com`

修改git 配置

```
git config --global credential.helper store
```

将会在.gitconfig末层生成(在~.）生成

```
.....
.....
[credential]
        helper = store

```

