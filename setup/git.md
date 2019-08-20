# git 常用操作

## 複製/下載專案

```bash
git clone [repo_url]
# ex:
# git clone https://github.com/agileworks-tw/RN_Todo_Sample.git
```

## 提交版本

```bash
# 加入所有變更的檔案到 stage
git add .
# 提交版本，只會提交 stage 內的檔案
git commit -m "commit message"
```

## 檢視提交的歷史記錄

以新到舊的順序列出版本控制的歷史紀錄

```bash
git log
```

output example:

```text
# output
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    changed the version number

commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sat Mar 15 16:40:33 2008 -0700

    removed unnecessary test code

commit a11bef06a3f659402fe7563abf99ad00de2209e6
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sat Mar 15 10:31:28 2008 -0700

    first commit
```

## 清除變更（回復到上一次提交的版本紀錄）

```bash
git add .
git reset --hard HEAD
```

## 切換分支/提交版本

切換分支前，如果有未提交的變更，必須先提交，或是先清除變更

```bash
git checkout [branch_name]
# ex:
# git checkout feature/add-todo-list
```
