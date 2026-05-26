## Laboratory work I(Tutorial)

Данная лабораторная работа посвещена изучению утилит для разработки проектов

(Вводные данные "-"
 Выходные данные "--"
 Вводные данные в cat ">")

```
-export GITHUB_USERNAME=Goydarik
-export GIST_TOKEN=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
-alias edit=nano
-mkdir -p ${GITHUB_USERNAME}/workspace
-cd ${GITHUB_USERNAME}/workspace
-pwd
--/home/rasul/Goydarik/workspace
-cd ..
-/home/rasul/Goydarik
-mkdir -p workspace/tasks/
-mkdir -p workspace/projects/
-mkdir -p workspace/reports/
-cd workspace
-wget https://nodejs.org/dist/v6.11.5/node-v6.11.5-linux-x64.tar.xz
----2026-05-12 16:54:39--  https://nodejs.org/dist/v6.11.5/node-v6.11.5-linux-x64.tar.xz
Распознаётся nodejs.org (nodejs.org)… 104.16.212.131, 104.16.213.131, 2606:4700::6810:d483, ...
Подключение к nodejs.org (nodejs.org)|104.16.212.131|:443... соединение установлено.
HTTP-запрос отправлен. Ожидание ответа… 200 OK
Длина: 9356460 (8,9M) [application/x-xz]
Сохранение в: «node-v6.11.5-linux-x64.tar.xz»

node-v6.11.5-linux- 100%[===================>]   8,92M  2,54MB/s    за 3,7s    

2026-05-12 16:54:44 (2,44 MB/s) - «node-v6.11.5-linux-x64.tar.xz» сохранён [9356460/9356460]
-tar -xf node-v6.11.5-linux-x64.tar.xz
-rm -rf node-v6.11.5-linux-x64.tar.xz
-mv node-v6.11.5-linux-x64 node
-ls node/bin
--node  npm
-echo ${PATH}
--/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games
-export PATH=${PATH}:`pwd`/node/bin
-echo ${PATH}
--/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:/home/rasul/Goydarik/workspace/node/bin
-mkdir scripts
-cat > scripts/activate<<EOF
>export PATH=\${PATH}:`pwd`/node/bin
>EOF
-source scripts/activate
-gem install gist
--Fetching gist-6.0.0.gem
Defaulting to user installation because default installation directory (/var/lib/gems/3.3.0) is not writable.
WARNING:  You don't have /home/rasul/.local/share/gem/ruby/3.3.0/bin in your PATH,
	  gem executables (gist) will not run.
Successfully installed gist-6.0.0
Parsing documentation for gist-6.0.0
Installing ri documentation for gist-6.0.0
Done installing documentation for gist after 0 seconds
1 gem installed
-(umask 0077 && echo ${GIST_TOKEN} > ~/.gist)
-export LAB_NUMBER=01
-git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
--Клонирование в «tasks/lab01»...
remote: Enumerating objects: 74, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 74 (delta 0), reused 1 (delta 0), pack-reused 71 (from 1)
Получение объектов: 100% (74/74), 945.07 КиБ | 1.05 МиБ/с, готово.
Определение изменений: 100% (20/20), готово.
-mkdir reports/lab${LAB_NUMBER}
-cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
-cd reports/lab${LAB_NUMBER}
-edit REPORT.md
-gist REPORT.md
--https://gist.github.com/Goydarik/a89eba2edfa80f2b5e9ea01e92f3736a
```












