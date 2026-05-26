##Laboratory work IV(Tutorial)

Данная лабораторная работа посвящена изучению систем непрерывной интеграции на примере сервиса Travis CI

(Вводные данные "-"
 Выходные данные "--"
 Вводные данные в cat ">")

```
-export GITHUB_USERNAME=Goydarik
-export GITHUB_TOKEN=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
-cd ${GITHUB_USERNAME}/workspace
-pushd .
--~/Goydarik/workspace ~/Goydarik/workspace
-source scripts/activate
-\curl -sSL https://get.rvm.io | bash -s -- --ignore-dotfiles
--Turning on ignore dotfiles mode.
Downloading https://github.com/rvm/rvm/archive/master.tar.gz
Installing RVM to /home/rasul/.rvm/
Installation of RVM in /home/rasul/.rvm/ is almost complete:

  * To start using RVM you need to run `source /home/rasul/.rvm/scripts/rvm`
    in all your open shell windows, in rare cases you need to reopen all shell windows.
Thanks for installing RVM 🙏
Please consider donating to our open collective to help us maintain RVM.

👉  Donate: https://opencollective.com/rvm/donate

-echo "source $HOME/.rvm/scripts/rvm" >> scripts/activate
-. scripts/activate
-rvm autolibs disable
-rvm install ruby-3.3.8
--ruby-3.3.8 - #removing src/ruby-3.3.8..
Searching for binary rubies, this might take some time.
No binary rubies available for: debian/13/x86_64/ruby-3.3.8.
Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.
Installing Ruby from source to: /home/rasul/.rvm/rubies/ruby-3.3.8, this may take a while depending on your cpu(s)...
ruby-3.3.8 - #downloading ruby-3.3.8, this may take a while depending on your connection...
ruby-3.3.8 - #extracting ruby-3.3.8 to /home/rasul/.rvm/src/ruby-3.3.8.....
ruby-3.3.8 - #autogen.sh.
ruby-3.3.8 - #configuring..................................................................
ruby-3.3.8 - #post-configuration..
ruby-3.3.8 - #compiling........................................................................................|
ruby-3.3.8 - #installing......................
ruby-3.3.8 - #making binaries executable...
Installed rubygems 3.5.22 is newer than 3.0.9 provided with installed ruby, skipping installation, use --force to force installation.
ruby-3.3.8 - #gemset created /home/rasul/.rvm/gems/ruby-3.3.8@global
ruby-3.3.8 - #importing gemset /home/rasul/.rvm/gemsets/global.gems............................................|
ruby-3.3.8 - #generating global wrappers........
ruby-3.3.8 - #gemset created /home/rasul/.rvm/gems/ruby-3.3.8
ruby-3.3.8 - #importing gemsetfile /home/rasul/.rvm/gemsets/default.gems evaluated to empty gem list
ruby-3.3.8 - #generating default wrappers........
ruby-3.3.8 - #adjusting #shebangs for (gem irb erb ri rdoc testrb rake).
Install of ruby-3.3.8 - #complete 
Ruby was built without documentation, to build it run: rvm docs generate-ri

-rvm use ruby-3.3.8 
--Using /home/rasul/.rvm/gems/ruby-3.3.8
-rvm use ruby-3.3.8 --default
--Using /home/rasul/.rvm/gems/ruby-3.3.8
-gem install travis
--Fetching net-http-pipeline-1.0.1.gem
Fetching connection_pool-3.0.2.gem
Fetching net-http-persistent-4.0.8.gem
Fetching multi_json-1.21.1.gem
Fetching typhoeus-1.6.0.gem
Fetching ethon-0.18.0.gem
Fetching faraday-net_http-3.0.2.gem
Fetching ffi-1.17.4-x86_64-linux-gnu.gem
Fetching faraday-2.7.12.gem
Fetching faraday-typhoeus-2.0.0.gem
Fetching faraday-retry-2.4.0.gem
Fetching public_suffix-7.0.5.gem
Fetching addressable-2.9.0.gem
Fetching concurrent-ruby-1.3.6.gem
Fetching tzinfo-2.0.6.gem
Fetching i18n-1.14.8.gem
Fetching activesupport-7.0.10.gem
Fetching travis-gh-0.21.0.gem
Fetching rack-3.2.6.gem
Fetching rack-test-2.1.0.gem
Fetching websocket-1.2.11.gem
Fetching pusher-client-0.6.2.gem
Fetching launchy-2.5.2.gem
Fetching json_pure-2.6.3.gem
Fetching travis-1.14.0.gem
Fetching highline-2.1.0.gem
Fetching faraday-rack-2.1.3.gem
Successfully installed net-http-pipeline-1.0.1
Successfully installed connection_pool-3.0.2
Successfully installed net-http-persistent-4.0.8
Successfully installed multi_json-1.21.1
Successfully installed ffi-1.17.4-x86_64-linux-gnu
Successfully installed ethon-0.18.0
Successfully installed typhoeus-1.6.0
Successfully installed faraday-net_http-3.0.2
Successfully installed faraday-2.7.12
Successfully installed faraday-typhoeus-2.0.0
Successfully installed faraday-retry-2.4.0
Successfully installed public_suffix-7.0.5
Successfully installed addressable-2.9.0
Successfully installed concurrent-ruby-1.3.6
Successfully installed tzinfo-2.0.6
Successfully installed i18n-1.14.8
Successfully installed activesupport-7.0.10
Successfully installed travis-gh-0.21.0
Successfully installed rack-3.2.6
Successfully installed rack-test-2.1.0
Successfully installed websocket-1.2.11
Successfully installed pusher-client-0.6.2
Successfully installed launchy-2.5.2
Successfully installed json_pure-2.6.3
Successfully installed highline-2.1.0
Successfully installed faraday-rack-2.1.3
Successfully installed travis-1.14.0
Parsing documentation for net-http-pipeline-1.0.1
Installing ri documentation for net-http-pipeline-1.0.1
Parsing documentation for connection_pool-3.0.2
Installing ri documentation for connection_pool-3.0.2
Parsing documentation for net-http-persistent-4.0.8
Installing ri documentation for net-http-persistent-4.0.8
Parsing documentation for multi_json-1.21.1
Installing ri documentation for multi_json-1.21.1
Parsing documentation for ffi-1.17.4-x86_64-linux-gnu
Installing ri documentation for ffi-1.17.4-x86_64-linux-gnu
Parsing documentation for ethon-0.18.0
Installing ri documentation for ethon-0.18.0
Parsing documentation for typhoeus-1.6.0
Installing ri documentation for typhoeus-1.6.0
Parsing documentation for faraday-net_http-3.0.2
Installing ri documentation for faraday-net_http-3.0.2
Parsing documentation for faraday-2.7.12
Installing ri documentation for faraday-2.7.12
Parsing documentation for faraday-typhoeus-2.0.0
Installing ri documentation for faraday-typhoeus-2.0.0
Parsing documentation for faraday-retry-2.4.0
Installing ri documentation for faraday-retry-2.4.0
Parsing documentation for public_suffix-7.0.5
Installing ri documentation for public_suffix-7.0.5
Parsing documentation for addressable-2.9.0
Installing ri documentation for addressable-2.9.0
Parsing documentation for concurrent-ruby-1.3.6
Installing ri documentation for concurrent-ruby-1.3.6
Parsing documentation for tzinfo-2.0.6
Installing ri documentation for tzinfo-2.0.6
Parsing documentation for i18n-1.14.8
Installing ri documentation for i18n-1.14.8
Parsing documentation for activesupport-7.0.10
Installing ri documentation for activesupport-7.0.10
Parsing documentation for travis-gh-0.21.0
Installing ri documentation for travis-gh-0.21.0
Parsing documentation for rack-3.2.6
Installing ri documentation for rack-3.2.6
Parsing documentation for rack-test-2.1.0
Installing ri documentation for rack-test-2.1.0
Parsing documentation for websocket-1.2.11
Installing ri documentation for websocket-1.2.11
Parsing documentation for pusher-client-0.6.2
Installing ri documentation for pusher-client-0.6.2
Parsing documentation for launchy-2.5.2
Installing ri documentation for launchy-2.5.2
Parsing documentation for json_pure-2.6.3
Installing ri documentation for json_pure-2.6.3
Parsing documentation for highline-2.1.0
Installing ri documentation for highline-2.1.0
Parsing documentation for faraday-rack-2.1.3
Installing ri documentation for faraday-rack-2.1.3
Parsing documentation for travis-1.14.0
Installing ri documentation for travis-1.14.0
Done installing documentation for net-http-pipeline, connection_pool, net-http-persistent, multi_json, ffi, ethon, typhoeus, faraday-net_http, faraday, faraday-typhoeus, faraday-retry, public_suffix, addressable, concurrent-ruby, tzinfo, i18n, activesupport, travis-gh, rack, rack-test, websocket, pusher-client, launchy, json_pure, highline, faraday-rack, travis after 7 seconds
27 gems installed
-git clone https://github.com/${GITHUB_USERNAME}/lab03 projects/lab04
-cat > .travis.yml <<EOF
>language: cpp
>EOF
-cat >> .travis.yml <<EOF
>script:
>- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
>- cmake --build _build
>- cmake --build _build --target install
>EOF
-cat >> .travis.yml <<EOF
>addons:
>  apt:
>    sources:
>      - george-edison55-precise-backports
>    packages:
>      - cmake
>      - cmake-data
>EOF
-travis login --github-token ${GITHUB_TOKEN}
--Shell completion not installed. Would you like to install it now? |y| 
Successfully logged in as Goydarik!
-travis lint
--Hooray, .travis.yml looks valid :)
-travis token
--Your access token is bXIG3sP1doq1CNis8kfB6Q
-ex -sc '1i|bXIG3sP1doq1CNis8kfB6Q' -cx README.md
-git add .travis.yml
-git add README.md
-git commit -m"added CI"
--[main 15c90e3] added CI
 2 files changed, 13 insertions(+)
 create mode 100644 .travis.yml
-git push origin main
--Перечисление объектов: 6, готово.
Подсчет объектов: 100% (6/6), готово.
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (4/4), 487 байтов | 487.00 КиБ/с, готово.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/Goydarik/lab04
   2196cf1..15c90e3  main -> main
-travis lint
--Hooray, .travis.yml looks valid :)
-travis accounts
--Goydarik (Goydarik): not subscribed, 1 repository
To set up a subscription, please visit app.travis-ci.com.
-travis sync
--synchronizing: . done
-travis repos

(из-за невозможности продолжить работу в Travis CI переходим на Github Actions)
-mkdir -p .github/workflows
-cat > .github/workflows/ci.yml << 'EOF'
> name: CI
> on:
>   push:
>     branches: [ main, master ]
>   pull_request:
>     branches: [ main, master ]
> jobs:
>   build:
>     runs-on: ubuntu-latest
>     steps:
>     - name: Checkout code
>       uses: actions/checkout@v4
>     - name: Install CMake
>       run: sudo apt-get update && sudo apt-get install -y cmake
>     - name: Configure
>       run: cmake -H. -B build -DCMAKE_INSTALL_PREFIX=__install
>     - name: Build
>       run: cmake --build build
>     - name: Install
>       run: cmake --build build --target install
> EOF
-cat > README.md << 'EOF'
> # lab04
> [![CI](https://github.com/Goydarik/lab04/actions/workflows/ci.yml/badge.svg)](https://github.com/Goydarik/lab04/actions/workflows/ci.yml)
> ## О проекте
> Проект для демонстрации непрерывной интеграции с Github Actions.
> EOF
-git add .github/workflows/ci.yml README.md
-git commit -m "Add Github Actions CI workflow"
--[main 2d87e6b] Add Github Actions CI workflow
 2 files changed, 25 insertions(+), 2 deletions(-)
 create mode 100644 .github/workflows/ci.yml
-git push origin main
--Перечисление объектов: 9, готово.
Подсчет объектов: 100% (9/9), готово.
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (5/5), 441 байт | 441.00 КиБ/с, готово.
Total 5 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/Goydarik/lab04
   db82a94..5233c95  main -> main
```
(наблюдаем синхронизацию с Githab Actions)


