## Laboratory work V(Tutorial)

Данная лабораторная работа посвящена изучению фреймворков для тестирования на примере GTest

(Вводные данные "-"
 Выходные данные "--"
 Вводные данные в cat ">")

```
-export GITHUB_USERNAME=Goydarik
-alias gsed=sed # for *-nix system
-cd ${GITHUB_USERNAME}/workspace
-pushd .
--~/Goydarik/workspace ~/Goydarik/workspace
```
```
-source scripts/activate
-git clone https://github.com/${GITHUB_USERNAME}/lab04 projects/lab05
--Клонирование в «projects/lab05»...
remote: Enumerating objects: 83, done.
remote: Counting objects: 100% (83/83), done.
remote: Compressing objects: 100% (49/49), done.
remote: Total 83 (delta 25), reused 79 (delta 21), pack-reused 0 (from 0)
Получение объектов: 100% (83/83), 17.83 КиБ | 3.57 МиБ/с, готово.
Определение изменений: 100% (25/25), готово.
```
```
-cd projects/lab05
-git remote remove origin
-git remote add origin https://github.com/${GITHUB_USERNAME}/lab05
-mkdir third-party
```
```
-git submodule add https://github.com/google/googletest third-party/gtest
--Клонирование в «/home/rasul/Goydarik/workspace/projects/lab05/third-party/gtest»...
remote: Enumerating objects: 28627, done.
remote: Counting objects: 100% (64/64), done.
remote: Compressing objects: 100% (48/48), done.
remote: Total 28627 (delta 32), reused 16 (delta 16), pack-reused 28563 (from 2)
Получение объектов: 100% (28627/28627), 13.78 МиБ | 973.00 КиБ/с, готово.
Определение изменений: 100% (21268/21268), готово.
-cd third-party/gtest && git checkout release-1.8.1 && cd ../..
--Примечание: переключение на «release-1.8.1».

Вы сейчас в состоянии «отсоединённого указателя HEAD». Можете осмотреться,
внести экспериментальные изменения и зафиксировать их, также можете
отменить любые коммиты, созданные в этом состоянии, не затрагивая другие
ветки, переключившись обратно на любую ветку.

Если хотите создать новую ветку для сохранения созданных коммитов, можете
сделать это (сейчас или позже), используя команду switch с параметром -c.
Например:

  git switch -c <новая-ветка>

Или отмените эту операцию с помощью:

  git switch -

Отключите этот совет, установив переменную конфигурации
advice.detachedHead в значение false

HEAD сейчас на 2fe3bd99 Merge pull request #1433 from dsacre/fix-clang-warnings
```
```
-git add third-party/gtest
-git commit -m"added gtest framework"
--[main 3f307a1] added gtest framework
 2 files changed, 4 insertions(+)
 create mode 100644 .gitmodules
 create mode 160000 third-party/gtest
```
```
-gsed -i '/option(BUILD_EXAMPLES "Build examples" OFF)/a\
option(BUILD_TESTS "Build tests" OFF)
' CMakeLists.txt
```
```
-cat >> CMakeLists.txt <<EOF
> if(BUILD_TESTS)
>   enable_testing()
>   add_subdirectory(third-party/gtest)
>   file(GLOB \${PROJECT_NAME}_TEST_SOURCES tests/*.cpp)
>   add_executable(check \${\${PROJECT_NAME}_TEST_SOURCES})
>   target_link_libraries(check \${PROJECT_NAME} gtest_main)
>   add_test(NAME check COMMAND check)
> endif()
> EOF
```
```
-mkdir tests
```
```
-cat > tests/test1.cpp <<EOF
> #include <print.hpp>
> #include <gtest/gtest.h>
> TEST(Print, InFileStream)
> {
>   std::string filepath = "file.txt";
>   std::string text = "hello";
>   std::ofstream out{filepath};
>   print(text, out);
>   out.close();
>   std::string result;
>   std::ifstream in{filepath};
>   in >> result;
>   EXPECT_EQ(result, text);
> }
> EOF
```
```
-nano .github/workflows/ci.yml
-name: CI

on:
  push:
    branches: [ main, master ]
  pull_request:
    branches: [ main, master ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout code
      uses: actions/checkout@v4
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
    
    - name: Install CMake
      run: sudo apt-get update && sudo apt-get install -y cmake
    
    - name: Configure
      run: cmake -H. -B build -DCMAKE_INSTALL_PREFIX=__install    
    - name: Build
      run: cmake --build build
    
    - name: Install
      run: cmake --build build --target install
```
```
-sed -i 's/lab04/lab05/g' README.md
-git add .
-git commit -m "added tests and GitHub Actions workflow"
--[main 94af720] added tests and GitHub Actions workflow
 4 files changed, 39 insertions(+), 12 deletions(-)
 create mode 100644 tests/test1.cpp
-git push origin main
```
(Наблюдаем синхронизацию с Github Actions)