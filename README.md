1. Создайте локальный Git-репозиторий.
2. Настройте имя пользователя и email для текущего репозитория.
3. Создайте структуру проекта с несколькими директориями.
4. Добавьте не менее трёх файлов в разные каталоги.
5. Настройте .gitignore, исключив один из подкаталогов от отслеживания.
6. Создайте две ветки от main: feature/api и feature/ui.
7. В каждой ветке внесите независимые изменения.
8. Сделайте как минимум по 2 коммита в каждой ветке с осмысленными сообщениями.
9. Выполните слияние ветки feature/api в main с использованием --no-ff.
10. Зафиксируйте изменения.
11. Убедитесь, что история коммитов отображает ветвление.
12. Выполните ребейз ветки feature/ui относительно main.
13. Разрешите возможные конфликты.
14. Зафиксируйте изменения.
15. Создайте тег v1.0.0 на коммите, в котором объединены все изменения.
16. Подпишите тег с сообщением.
17. Иммитируйте ошибочный коммит в любой из веток.
18. Отмените его с помощью git revert, а затем — другим способом с использованием git reset.
19. Смоделируйте ситуацию с временными изменениями.
20. Используйте git stash для сохранения незакоммиченных изменений.
21. Затем восстановите их и продолжите работу.
22. Настройте удалённый репозиторий.
23. Опубликуйте ветки, включая теги.

========================================================================

2. Настройте имя пользователя и email для текущего репозитория.
```
ym@Evgeniy:~/Lesta_hw2$ git config --list
user.email=mazurov1804@gmail.com
user.name=YMazurov
user.name=Yauheni
user.name=Yauheni
core.editor=nano
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
```

3-5. Создайте структуру проекта с несколькими директориями. Добавьте не менее трёх файлов в разные каталоги. Настройте .gitignore, исключив один из подкаталогов от отслеживания.
```
ym@Evgeniy:~/Lesta_hw2$ ll
total 24
drwxr-xr-x  6 ym ym 4096 May 20 18:54 ./
drwxr-x--- 18 ym ym 4096 May 20 18:53 ../
drwxr-xr-x  7 ym ym 4096 May 20 18:50 .git/
drwxr-xr-x  2 ym ym 4096 May 20 18:54 catalog_1/
drwxr-xr-x  2 ym ym 4096 May 20 18:54 catalog_2/
drwxr-xr-x  2 ym ym 4096 May 20 18:54 catalog_3/
```

```
ym@Evgeniy:~/Lesta_hw2$ cat .gitignore
catalog_3/
```

```
ym@Evgeniy:~/Lesta_hw2$ git commit -m "first commit"
[master (root-commit) 22f1153] first commit
 3 files changed, 3 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 catalog_1/file_1.txt
 create mode 100644 catalog_2/file_2.txt
```

6. Создайте две ветки от main: feature/api и feature/ui.
```
ym@Evgeniy:~/Lesta_hw2$ git checkout -b feature/api
Switched to a new branch 'feature/api'
ym@Evgeniy:~/Lesta_hw2$ git checkout -b feature/ui
Switched to a new branch 'feature/ui'
```

7. В каждой ветке внесите независимые изменения.

```
ym@Evgeniy:~/Lesta_hw2$ git checkout feature/ui
M       catalog_1/file_1.txt
Switched to branch 'feature/ui'
ym@Evgeniy:~/Lesta_hw2$ echo "add note file2" >> catalog_2/file_2.txt
ym@Evgeniy:~/Lesta_hw2$ cat catalog_2/file_2.txt
file2
add note file2
ym@Evgeniy:~/Lesta_hw2$ git branch
  feature/api
* feature/ui
  master
```

```
ym@Evgeniy:~/Lesta_hw2$ git checkout feature/api
Switched to branch 'feature/api'
ym@Evgeniy:~/Lesta_hw2$ echo "add note file1" >> catalog_1/file_1.txt
ym@Evgeniy:~/Lesta_hw2$ cat catalog_1/file_1.txt
file1
add note file1
ym@Evgeniy:~/Lesta_hw2$ git branch
* feature/api
  feature/ui
  master
```

8. Сделайте как минимум по 2 коммита в каждой ветке с осмысленными сообщениями.
```
ym@Evgeniy:~/Lesta_hw2$ git branch
  feature/api
* feature/ui
  master
ym@Evgeniy:~/Lesta_hw2$ git add .
ym@Evgeniy:~/Lesta_hw2$ git commit -m "add note "file2" to file 2.txt"
[feature/ui b72af6a] add note file2 to file 2.txt
 2 files changed, 2 insertions(+)
ym@Evgeniy:~/Lesta_hw2$ echo "add note file2.1" >> catalog_2/file_2.txt
ym@Evgeniy:~/Lesta_hw2$ git commit -m "add note "file2.1" to file 2.txt"
On branch feature/ui
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   catalog_2/file_2.txt

no changes added to commit (use "git add" and/or "git commit -a")
ym@Evgeniy:~/Lesta_hw2$ git add .
ym@Evgeniy:~/Lesta_hw2$ git commit -m "add note "file2.1" to file 2.txt"
[feature/ui ea46bbb] add note file2.1 to file 2.txt
 1 file changed, 1 insertion(+)
```

```
ym@Evgeniy:~/Lesta_hw2$ git branch
* feature/api
  feature/ui
  master
ym@Evgeniy:~/Lesta_hw2$ echo "v.1.0.1" >> catalog_1/file_1.txt
ym@Evgeniy:~/Lesta_hw2$ cat catalog_1/file_1.txt
file1
v.1.0.1
ym@Evgeniy:~/Lesta_hw2$ git add .
ym@Evgeniy:~/Lesta_hw2$ git commit -m "add note "v.1.0.1" to file1.txt"
[feature/api 73fe014] add note v.1.0.1 to file1.txt
 1 file changed, 1 insertion(+)
ym@Evgeniy:~/Lesta_hw2$ echo "v.1.0.2" >> catalog_1/file_1.txt
ym@Evgeniy:~/Lesta_hw2$ cat catalog_1/file_1.txt
file1
v.1.0.1
v.1.0.2
ym@Evgeniy:~/Lesta_hw2$ git commit -m "add note "v.1.0.2" to file1.txt"
On branch feature/api
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   catalog_1/file_1.txt

no changes added to commit (use "git add" and/or "git commit -a")
ym@Evgeniy:~/Lesta_hw2$ git add .
ym@Evgeniy:~/Lesta_hw2$ git commit -m "add note "v.1.0.2" to file1.txt"
[feature/api 58695d4] add note v.1.0.2 to file1.txt
 1 file changed, 1 insertion(+)
```

9-11. Выполните слияние ветки feature/api в main с использованием --no-ff. Зафиксируйте изменения. Убедитесь, что история коммитов отображает ветвление.

```
ym@Evgeniy:~/Lesta_hw2$ git branch
  feature/api
  feature/ui
* main
ym@Evgeniy:~/Lesta_hw2$ git merge feature/api --no-ff
Merge made by the 'ort' strategy.
 catalog_1/file_1.txt | 2 ++
 1 file changed, 2 insertions(+)
ym@Evgeniy:~/Lesta_hw2$ git log --graph --oneline
*   7af812e (HEAD -> main) Merge branch 'feature/api' с использованием --no-ff ( задание 9)
|\
| * 58695d4 (feature/api) add note v.1.0.2 to file1.txt
| * 73fe014 add note v.1.0.1 to file1.txt
|/
* 22f1153 first commit
ym@Evgeniy:~/Lesta_hw2$ cat catalog_1/file_1.txt
file1
v.1.0.1
v.1.0.2
```

12-14. Выполните ребейз ветки feature/ui относительно main.
```
ym@Evgeniy:~/Lesta_hw2$ git branch
  feature/api
* feature/ui
  main
ym@Evgeniy:~/Lesta_hw2$ git rebase main
Auto-merging catalog_1/file_1.txt
CONFLICT (content): Merge conflict in catalog_1/file_1.txt
error: could not apply b72af6a... add note file2 to file 2.txt
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply b72af6a... add note file2 to file 2.txt
ym@Evgeniy:~/Lesta_hw2$ cat catalog_1/file_1.txt 
file1
<<<<<<< HEAD
v.1.0.1
v.1.0.2
=======
add note file1
>>>>>>> b72af6a (add note file2 to file 2.txt)
ym@Evgeniy:~/Lesta_hw2$ cat catalog_1/file_1.txt 
file1
v.1.0.1
v.1.0.2
add note file1

ym@Evgeniy:~/Lesta_hw2$ git add .
ym@Evgeniy:~/Lesta_hw2$ git rebase --continue
[detached HEAD 85aa8a7] Ребейз ветки feature/ui относительно main ( задание 12)
 2 files changed, 3 insertions(+)
Successfully rebased and updated refs/heads/feature/ui.
```

15-16. Создайте тег v1.0.0 на коммите, в котором объединены все изменения. Подпишите тег с сообщением.
```
ym@Evgeniy:~/Lesta_hw2$ git tag -a v1.0.0 -m "v.1.0.0 после  Merge branch 'feature/api'"
ym@Evgeniy:~/Lesta_hw2$ git tag
v1.0.0
ym@Evgeniy:~/Lesta_hw2$ git show v1.0.0
tag v1.0.0
Tagger: Yauheni <mazurov1804@gmail.com>
Date:   Tue May 20 20:21:50 2025 +0300

v.1.0.0 после  Merge branch 'feature/api'

commit 7af812ed1ae7c6743f26d299b316f663afa86fab (HEAD -> main, tag: v1.0.0, tag: v.1.0.0)
Merge: 22f1153 58695d4
Author: Yauheni <mazurov1804@gmail.com>
Date:   Tue May 20 19:36:40 2025 +0300

    Merge branch 'feature/api' с использованием --no-ff ( задание 9)
```

17-18. Иммитируйте ошибочный коммит в любой из веток. Отмените его с помощью git revert, а затем — другим способом с использованием git reset.
```
ym@Evgeniy:~/Lesta_hw2$ echo "17-18" >>file_error.txt
ym@Evgeniy:~/Lesta_hw2$ git add .
ym@Evgeniy:~/Lesta_hw2$ git commit -m "tasks 17-18"
[main 86aac44] tasks 17-18
 1 file changed, 1 insertion(+)
 create mode 100644 file_error.txt
ym@Evgeniy:~/Lesta_hw2$ git revert 86aac44
[main 23f9ab2] Revert "tasks 17-18"
 1 file changed, 1 deletion(-)
 delete mode 100644 file_error.txt
ym@Evgeniy:~/Lesta_hw2$ git log --oneline
23f9ab2 (HEAD -> main) Revert "tasks 17-18"
86aac44 tasks 17-18
7af812e (tag: v1.0.0, tag: v.1.0.0) Merge branch 'feature/api' с использованием --no-ff ( задание 9)
58695d4 (feature/api) add note v.1.0.2 to file1.txt
73fe014 add note v.1.0.1 to file1.txt
22f1153 first commit 
``` 

```
ym@Evgeniy:~/Lesta_hw2$ git log --oneline
23f9ab2 (HEAD -> main) Revert "tasks 17-18"
86aac44 tasks 17-18
7af812e (tag: v1.0.0, tag: v.1.0.0) Merge branch 'feature/api' с использованием --no-ff ( задание 9)
58695d4 (feature/api) add note v.1.0.2 to file1.txt
73fe014 add note v.1.0.1 to file1.txt
22f1153 first commit
ym@Evgeniy:~/Lesta_hw2$ git reset --hard HEAD~1
HEAD is now at 86aac44 tasks 17-18
ym@Evgeniy:~/Lesta_hw2$ git reset --hard HEAD~1
HEAD is now at 7af812e Merge branch 'feature/api' с использованием --no-ff ( задание 9)
```

19-21. Смоделируйте ситуацию с временными изменениями. Используйте git stash для сохранения незакоммиченных изменений. Затем восстановите их и продолжите работу.

```
ym@Evgeniy:~/Lesta_hw2$ touch 19_20.txt
ym@Evgeniy:~/Lesta_hw2$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        19_20.txt

nothing added to commit but untracked files present (use "git add" to track)
ym@Evgeniy:~/Lesta_hw2$ git add .
ym@Evgeniy:~/Lesta_hw2$ git stash save "задание 19-20"
Saved working directory and index state On main: задание 19-20
```
```
ym@Evgeniy:~/Lesta_hw2$ git stash list
stash@{0}: On main: задание 19-20
```

```
ym@Evgeniy:~/Lesta_hw2$ git stash list
stash@{0}: On main: задание 19-20
ym@Evgeniy:~/Lesta_hw2$ git stash apply stash@{0} 
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   19_20.txt
```

22-23. Настройте удалённый репозиторий. Опубликуйте ветки, включая теги.
https://github.com/YMazurau/Lesta_02_git

```
ym@Evgeniy:~/Lesta_hw2$ git add .
ym@Evgeniy:~/Lesta_hw2$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   19_20.txt

ym@Evgeniy:~/Lesta_hw2$ git commit -m "push в удаленный репозиторий"
[main 1f5e608] push в удаленный репозиторий
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 19_20.txt
ym@Evgeniy:~/Lesta_hw2$ git remote add origin git@github.com:YMazurau/Lesta_02_git.git
ym@Evgeniy:~/Lesta_hw2$ git push -u origin main
Enumerating objects: 19, done.
Counting objects: 100% (19/19), done.
Delta compression using up to 20 threads
Compressing objects: 100% (9/9), done.
Writing objects: 100% (19/19), 1.59 KiB | 1.59 MiB/s, done.
Total 19 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), done.
To github.com:YMazurau/Lesta_02_git.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

```
ym@Evgeniy:~/Lesta_hw2$ git push origin --tags
Enumerating objects: 1, done.
Counting objects: 100% (1/1), done.
Writing objects: 100% (1/1), 200 bytes | 200.00 KiB/s, done.
Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:YMazurau/Lesta_02_git.git
 * [new tag]         v.1.0.0 -> v.1.0.0
 * [new tag]         v1.0.0 -> v1.0.0
```

```
ym@Evgeniy:~/Lesta_hw2$ git push --all origin
Enumerating objects: 15, done.
Counting objects: 100% (15/15), done.
Delta compression using up to 20 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (10/10), 820 bytes | 820.00 KiB/s, done.
Total 10 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), done.
To github.com:YMazurau/Lesta_02_git.git
 * [new branch]      feature/api -> feature/api
 * [new branch]      feature/ui -> feature/ui
``` 