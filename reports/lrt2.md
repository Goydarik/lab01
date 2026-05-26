## Laboratory work II(Tutorial+Homework)

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

(Вводные данные "-"
 Выходные данные "--"
 Вводные данные в cat ">")

```
- export GITHUB_USERNAME=Goydarik
- export GITHUB_EMAIL=rosgorzion@gmail.com
- export GITHUB_TOKEN=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
- alias edit=nano
- cd ${GITHUB_USERNAME}/workspace
- source scripts/activate
- mkdir ~/.config
- cat > ~/.config/hub <<EOF
-- github.com:
-- - user: ${GITHUB_USERNAME}
--   oauth_token: ${GITHUB_TOKEN}
--   protocol: https
-- EOF
- git config --global hub.protocol https
- mkdir projects/lab02 && cd projects/lab02
- git init
-- hint: Using 'master' as the name for the initial branch. This default branch name is subject to change. To configure the initial branch name to use in all other repositories, which will suppress this warning, call:
-- hint:
-- hint:    git config --global init.defaultBranch <name>
-- hint:
-- hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and 'development'. The just-created branch can be renamed via this command:
-- hint:
-- hint:    git branch -m <name>
-- Initialized empty Git repository in /home/rasul/Goydarik/workspace/projects/lab02/.git/
- git config --global user.name ${GITHUB_USERNAME}
- git config --global user.email ${GITHUB_EMAIL}
- git config -e --global
-- 
-- [hub]
-- protocol = https
-- 
-- [user]
-- name = Goydarik
-- email = rosgorzion@gmail.com
-- 
- git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
- git pull origin main
-- remote: Enumerating objects: 3, done.
-- remote: Counting objects: 100% (3/3), done.
-- remote: Compressing objects: 100% (2/2), done.
-- remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
-- Unpacking objects: 100% (3/3), 1.43 KiB | 1.43 MiB/s, done.
-- From https://github.com/Goydarik/lab02
--  * branch    main    -> FETCH_HEAD
--  * [new branch]   main    -> origin/main
- touch README.md
- git status
-- On branch master
-- Untracked files:
--   (use "git add <file>..." to include in what will be committed)
--     README.md
-- 
-- nothing added to commit but untracked files present (use "git add" to track)
- git add README.md
- git commit -m"added README.md"
- git commit -m"added README.md"
-- [master a696b70] added README.md
--  1 file changed, 0 insertions(+), 0 deletions(-)
--  create mode 100644 README.md
- git push origin master
-- Username for 'https://github.com': Goydarik
-- Password for 'https://Goydarik@github.com':
-- Enumerating objects: 4, done.
-- Counting objects: 100% (4/4), done.
-- Delta compression using up to 2 threads
-- Compressing objects: 100% (2/2), done.
-- Writing objects: 100% (3/3), 280 bytes | 280.00 KiB/s, done.
-- Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
-- remote:
-- remote: Create a pull request for 'master' on GitHub by visiting:
-- remote:    https://github.com/Goydarik/lab02/pull/new/master
-- remote:
-- To https://github.com/Goydarik/lab02.git
--  * [new branch]    master -> master
- nano .gitignore
-- *build*/
-- *install*/
-- *.swp
-- .idea/
- git pull origin main
-- remote: Enumerating objects: 6, done.
-- remote: Counting objects: 100% (6/6), done.
-- remote: Compressing objects: 100% (3/3), done.
-- remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
-- Unpacking objects: 100% (4/4), 1.81 KiB | 1.81 MiB/s, done.
-- From https://github.com/Goydarik/lab02
--  * branch    main    -> FETCH_HEAD
--    48d14ad..05fa0aa main    -> origin/main
-- Updating a696b70..05fa0aa
-- Fast-forward
-- .gitignore | 4 ++++
-- 1 file changed, 4 insertions(+)
-- create mode 100644 .gitignore
- git log
-- commit 05fa0aae54cbf53bcc4b618d873b4cc334c3f027 (HEAD -> master, origin/main)
-- Author: Goydarik <rosgorzion@gmail.com>
-- Date:    Wed Apr 8 17:10:57 2026 +0300
-- 
-- Create .gitignore
-- 
-- commit 4b8b40ce9f471dfd284998afb7c0a2a13e3491f2
-- Merge: 48d14ad a696b70
-- Author: Goydarik <rosgorzion@gmail.com>
-- Date:    Wed Apr 8 17:04:42 2026 +0300
-- 
-- Merge pull request #1 from Goydarik/master
-- 
-- added README.md
-- 
-- commit a696b706e02028bc364ad6f60719b3c43d0b1548 (origin/master)
-- Author: Goydarik <rosgorzion@gmail.com>
-- Date:    Wed Apr 8 09:41:44 2026 -0400
-- 
-- added README.md
-- 
-- commit 48d14ad75c36add4d5754625722d11c3d4557e30
-- Author: Goydarik <rosgorzion@gmail.com>
-- Date: Wed Apr 8 15:41:49 2026 +0300
-- 
-- Initial commit
- mkdir sources
- mkdir include
- mkdir examples
- cat > sources/print.cpp <<EOF
-- #include <print.hpp>
-- 
-- void print(const std::string& text, std::ostream& out)
-- {
--   out << text;
-- }
-- 
-- void print(const std::string& text, std::ofstream& out)
-- {
--   out << text;
-- }
-- EOF
- cat > include/print.hpp <<EOF
-- #include <fstream>
-- #include <iostream>
-- #include <string>
-- 
-- void print(const std::string& text, std::ofstream& out);
-- void print(const std::string& text, std::ostream& out = std::cout);
-- EOF
- cat > examples/example1.cpp <<EOF
-- #include <print.hpp>
-- 
-- int main(int argc, char** argv)
-- {
--   print("hello");
-- }
-- EOF
- cat > examples/example2.cpp <<EOF
-- #include <print.hpp>
-- 
-- #include <fstream>
-- 
-- int main(int argc, char** argv)
-- {
--   std::ofstream file("log.txt");
--   print(std::string("hello"), file);
-- }
-- EOF
- edit README.md
- git status
- git add .
- git commit -m"added sources"
- git add .
- git commit -m"added sources"
-- [master de89ad3] added sources
--  4 files changed, 32 insertions(+)
--  create mode 100644 examples/example1.cpp
--  create mode 100644 examples/example2.cpp
--  create mode 100644 include/print.hpp
--  create mode 100644 sources/print.cpp
- git push origin master
-- Username for 'https://github.com': Goydarik
-- Password for 'https://Goydarik@github.com':
-- Enumerating objects: 10, done.
-- Counting objects: 100% (10/10), done.
-- Delta compression using up to 2 threads
-- Compressing objects: 100% (7/7), done.
-- Writing objects: 100% (9/9), 966 bytes | 966.00 KiB/s, done.
-- Total 9 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
-- To https://github.com/Goydarik/lab02.git
-- a696b70...de89ad3    master -> master
- git push origin master
-- Username for 'https://github.com': Goydarik
-- Password for 'https://Goydarik@github.com':
-- Enumerating objects: 10, done.
-- Counting objects: 100% (10/10), done.
-- Delta compression using up to 2 threads
-- Compressing objects: 100% (7/7), done.
-- Writing objects: 100% (9/9), 966 bytes | 966.00 KiB/s, done.
-- Total 9 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
-- To https://github.com/Goydarik/lab02.git
-- a696b70..de89ad3    master -> master
```
__________________________________________________________________________________________
HOMEWORK
__________________________________________________________________________________________

1.
```
- nano hello_world.cpp

Пишем hello_world.cpp:
#include <iostream>

using namespace std;

int main() {
    cout << "Hello world" << endl;
    return 0;
}

- nano hello_world.cpp
-- $ git add hello_world.cpp
-- $ git commit -m "Add hello_world.cpp"
-- [master 6f91e32] Add hello_world.cpp
--  1 file changed, 6 insertions(+)
--  create mode 100644 hello_world.cpp
- nano hello_world.cpp

В hello_world.cpp пишем:
#include <iostream>
#include <string>

using namespace std;

int main() {
    string name;
    cout << "Enter your name: ";
    cin >> name;
    cout << "Hello world from " << name << endl;
    return 0;
}

- $ git commit -am "Modified hello_world.cpp to accept user name input"
-- [master 11a42cc] Modified hello_world.cpp to accept user name input
--  1 file changed, 5 insertions(+), 1 deletion(-)
- git push origin master
-- Username for 'https://github.com': Goydarik
-- Password for 'https://Goydarik@github.com':
-- Enumerating objects: 7, done.
-- Counting objects: 100% (7/7), done.
-- Delta compression using up to 2 threads
-- Compressing objects: 100% (6/6), done.
-- Writing objects: 100% (6/6), 727 bytes | 727.00 KiB/s, done.
-- Total 6 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
-- remote: Resolving deltas: 100% (2/2), completed with 1 local object.
-- To https://github.com/Goydarik/lab02.git
--     de89ad3..11a42cc   master -> master
- git log --oneline
-- 11a42cc (HEAD -> master, origin/master) Modified hello_world.cpp to accept user input
-- 6f91e32 Add hello_world.cpp
-- de89ad3 added sources
-- 05fa0aa (origin/main) Create .gitignore
-- 4b8b40c Merge pull request #1 from Goydarik/master
-- a696b70 added README.md
-- 48d14ad Initial commit
```

2.
1)
```
-git status
--Текущая ветка: master
нечего коммитить, нет изменений в рабочем каталоге
-git checkout -b patch1
--Переключились на новую ветку «patch1»
```
2)
```
-git branch
--master
* patch1
-git status
--Текущая ветка: patch1
Изменения, которые не в индексе для коммита:
  (используйте «git add <файл>...», чтобы добавить файл в индекс)
  (используйте «git restore <файл>...», чтобы отменить изменения в рабочем каталоге)
	изменено:      hello_world.cpp

индекс пуст (используйте «git add» и/или «git commit -a»)
-git diff
--diff --git a/hello_world.cpp b/hello_world.cpp
index d5e3ac1..c5da6d6 100644
--- a/hello_world.cpp
+++ b/hello_world.cpp
@@ -1,12 +1,12 @@
 #include <iostream>
 #include <string>
 
-using namespace std;
+
 
 int main(){
        string n;
-       cout << "Enter your name: "
-       cin >> n; 
-       cout << "hello world from " << n;
+       std::cout << "Enter your name: "
+       std::cin >> n; 
+       std::cout << "hello world from " << n;
 
 }
```
3)
```
-git add hello_world.cpp
-git commit -m "Fix code style: remove using namespace std"
--[patch1 bfbe7a1] Fix code style: remove using namespace std
 1 file changed, 4 insertions(+), 4 deletions(-)
-git push origin patch1
--Перечисление объектов: 5, готово.
Подсчет объектов: 100% (5/5), готово.
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (3/3), 390 байтов | 390.00 КиБ/с, готово.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote: 
remote: Create a pull request for 'patch1' on GitHub by visiting:
remote:      https://github.com/Goydarik/lab02/pull/new/patch1
remote: 
To https://github.com/Goydarik/lab02.git
 * [new branch]      patch1 -> patch1
```
4)
Проверка
5)
Создание
6)
```
-nano hello_world.cpp
```
(добавляем комменарии)
7)
```
-git add hello_world.cpp
-git commit -m "Add comments to hello_world.cpp"
--[patch1 791cb07] Add comments to hello_world.cpp
 1 file changed, 4 insertions(+), 4 deletions(-)
-git push origin patch1
--Перечисление объектов: 5, готово.
Подсчет объектов: 100% (5/5), готово.
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (3/3), 463 байта | 463.00 КиБ/с, готово.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/Goydarik/lab02.git
   bfbe7a1..791cb07  patch1 -> patch1
```
8)
```
-git checkout master
```
--Переключились на ветку «master»
9)
Удаляем ветку patch1
10)
```
-git pull origin master
--remote: Enumerating objects: 22, done.
remote: Counting objects: 100% (22/22), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 14 (delta 5), reused 0 (delta 0), pack-reused 0 (from 0)
Распаковка объектов: 100% (14/14), 7.02 КиБ | 423.00 КиБ/с, готово.
Из https://github.com/Goydarik/lab02
 * branch            master     -> FETCH_HEAD
   eaa73c1..d065802  master     -> origin/master
Обновление eaa73c1..d065802
Fast-forward
 .gitignore      | 4 ++++
 hello_world.cpp | 9 +++++----
 2 files changed, 9 insertions(+), 4 deletions(-)
 create mode 100644 .gitignore
```
11)
```
-git log --oneline
--d065802 (HEAD -> master, origin/master) Merge pull request #6 from Goydarik/patch1
07aa3a4 Merge branch 'revert-4-master' into patch1
1c642fd (origin/patch1, patch1) Add comments to hello_world.cpp
3982c92 Add comments to hello_world.cpp
22fa24d Revert "Master"
791cb07 Add comments to hello_world.cpp
0b4fa7e Merge pull request #4 from Goydarik/master
119c5a8 Merge pull request #3 from Goydarik/patch1
bfbe7a1 Fix code style: remove using namespace std
e291cb0 Merge pull request #2 from Goydarik/master
eaa73c1 REPROGRAM hello_world.cpp
a6c285b ADD hello_world.cpp
7b151ec added sources
6171f6c Create .gitignore
c95d6d2 Merge pull request #1 from Goydarik/master
ce8b8b8 added README.md
338d3c2 (origin/main) Initial commit
```
12)
```
-git branch -d patch1
--Ветка patch1 удалена (была 1c642fd).
```

3.
1)
```
-git checkout -b patch2
--Переключились на новую ветку «patch2»
-git branch
-- master
* patch2
```
2)
Установка
```
-sudo apt update
-sudo apt install clang-format
Работа
-clang-format -style=Mozilla -i hello_world.cpp
-git diff
--diff --git a/hello_world.cpp b/hello_world.cpp
index 35d9027..64e0dc8 100644
--- a/hello_world.cpp
+++ b/hello_world.cpp
@@ -3,11 +3,12 @@
 
 using namespace std;
 
-int main(){
-       string n;//Объявляем n
-       std::cout << "Enter your name: "//Запрашиваем имя
-       std::cin >> n; //Вводим n
-       std::cout << "hello world from " << n;//Выводим текст
-
-
+int
+main()
+{
+  string n;                        // Объявляем n
+  std::cout << "Enter your name: " // Запрашиваем имя
+      std::cin >>
+    n;                                   // Вводим n
+  std::cout << "hello world from " << n; // Выводим текст
```
}
3)
```
-git add hello_world.cpp
-git commit -m "Format hello_world.cpp with Mozilla style using clang format"
--[patch2 7640f50] Format hello_world.cpp with Mozilla style using clang format
 1 file changed, 8 insertions(+), 7 deletions(-)
-git push -u origin patch2
--Перечисление объектов: 5, готово.
Подсчет объектов: 100% (5/5), готово.
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (3/3), 510 байтов | 510.00 КиБ/с, готово.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote: 
remote: Create a pull request for 'patch2' on GitHub by visiting:
remote:      https://github.com/Goydarik/lab02/pull/new/patch2
remote: 
To https://github.com/Goydarik/lab02.git
 * [new branch]      patch2 -> patch2
branch 'patch2' set up to track 'origin/patch2'.
```
4)
```
-git checkout master
--Переключились на ветку «master»
-nano hello_world.cpp
-git add hello_world.cpp
-git commit -m "Fix comments: translate them into english"
--[master 6b2db32] Fix comments: translate them into english
 1 file changed, 4 insertions(+), 4 deletions(-)
-git push origin master
--Перечисление объектов: 5, готово.
Подсчет объектов: 100% (5/5), готово.
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (3/3), 377 байтов | 377.00 КиБ/с, готово.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/Goydarik/lab02.git
   d065802..6b2db32  master -> master
-git checkout patch2
--Переключились на ветку «patch2»
Эта ветка соответствует «origin/patch2».
-git fetch origin
```
5)
Убедимся в наличии конфликтов
6)
```
-git pull --rebase origin master
--Из https://github.com/Goydarik/lab02
 * branch            master     -> FETCH_HEAD
Автослияние hello_world.cpp
КОНФЛИКТ (содержимое): Конфликт слияния в hello_world.cpp
error: не удалось применить коммит 7640f50... Format hello_world.cpp with Mozilla style using clang format
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
hint: Disable this message with "git config advice.mergeConflict false"
Не удалось применить коммит 7640f50... Format hello_world.cpp with Mozilla style using clang format
-nano hello_world.cpp
```
(Удаляем версию с изменёнными комментариями)
7)
```
-git add hello_world.cpp
-git rebase --continue
--[отделённый HEAD cfa03ee] Format hello_world.cpp with Mozilla style using clang format
 1 file changed, 8 insertions(+), 9 deletions(-)
Успешно перемещён и обновлён refs/heads/patch2.
---format hello_world.cpp with Mozilla style using clang format

# Conflicts:
#       hello_world.cpp

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# интерактивное перемещение в процессе; над 6b2db32
# Last command done (1 command done):
#    pick 7640f50 Format hello_world.cpp with Mozilla style using clang format
# Команд больше не осталось.
# Вы сейчас перемещаете ветку «patch2» над «6b2db32».
#
# Изменения, которые будут включены в коммит:
#       изменено:      hello_world.cpp
#

-git push --force origin patch2
--Перечисление объектов: 5, готово.
Подсчет объектов: 100% (5/5), готово.
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (3/3), 502 байта | 502.00 КиБ/с, готово.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/Goydarik/lab02.git
 + 7640f50...cfa03ee patch2 -> patch2 (forced update)
```
8)
Убедимся, что конфликты пропали
9)
Замержим



