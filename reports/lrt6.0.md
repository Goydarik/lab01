## Laboratory work VI(Tutorial + Homework)

Данная лабораторная работа посвящена изучению средств пакетирования на примере CPack

(Вводные данные "-"
 Выходные данные "--"
 Вводные данные в cat ">")

```
-export GITHUB_USERNAME=Goydarik
-export GITHUB_EMAIL=rosgorzion@gmail.com
-alias edit=nano
-alias gsed=sed # for *-nix system
-cd ${GITHUB_USERNAME}/workspace
-pushd .
--~/Goydarik/workspace ~/Goydarik/workspace
-source scripts/activate
```
```
-git clone https://github.com/${GITHUB_USERNAME}/lab05 projects/lab06
--Клонирование в «projects/lab06»...
remote: Enumerating objects: 101, done.
remote: Counting objects: 100% (101/101), done.
remote: Compressing objects: 100% (51/51), done.
remote: Total 101 (delta 31), reused 101 (delta 31), pack-reused 0 (from 0)
Получение объектов: 100% (101/101), 19.78 КиБ | 2.47 МиБ/с, готово.
Определение изменений: 100% (31/31), готово.
```
```
-cd projects/lab06
-git remote remove origin
-git remote add origin https://github.com/${GITHUB_USERNAME}/lab06
```
```
-gsed -i '/project(print)/a\
set(PRINT_VERSION_STRING "v\${PRINT_VERSION}")
' CMakeLists.txt
- gsed -i '/project(print)/a\
set(PRINT_VERSION\
  \${PRINT_VERSION_MAJOR}.\${PRINT_VERSION_MINOR}.\${PRINT_VERSION_PATCH}.\${PRINT_VERSION_TWEAK})
' CMakeLists.txt
- gsed -i '/project(print)/a\
set(PRINT_VERSION_TWEAK 0)
' CMakeLists.txt
- gsed -i '/project(print)/a\
set(PRINT_VERSION_PATCH 0)
' CMakeLists.txt
- gsed -i '/project(print)/a\
set(PRINT_VERSION_MINOR 1)
' CMakeLists.txt
- gsed -i '/project(print)/a\
set(PRINT_VERSION_MAJOR 0)
' CMakeLists.txt
```
```
- git diff
--diff --git a/CMakeLists.txt b/CMakeLists.txt
index 02df29e..31fe12b 100644
--- a/CMakeLists.txt
+++ b/CMakeLists.txt
@@ -7,6 +7,16 @@ option(BUILD_EXAMPLES "Build examples" OFF)
 option(BUILD_TESTS "Build tests" OFF)
 
 project(print)
+set(PRINT_VERSION_MAJOR 0)
+set(PRINT_VERSION_MINOR 1)
+set(PRINT_VERSION_PATCH 0)
+set(PRINT_VERSION_TWEAK 0)
+set(PRINT_VERSION
+  ${PRINT_VERSION_MAJOR}.${PRINT_VERSION_MINOR}.${PRINT_VERSION_PATCH}.${PRINT_VERSION_TWEAK})
+set(PRINT_VERSION_STRING "v${PRINT_VERSION}")
+set(PRINT_VERSION
+  ${PRINT_VERSION_MAJOR}.${PRINT_VERSION_MINOR}.${PRINT_VERSION_PATCH}.${PRINT_VERSION_TWEAK})
+set(PRINT_VERSION_STRING "v${PRINT_VERSION}")
 
 add_library(print STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
```
```
- touch DESCRIPTION && edit DESCRIPTION
- touch ChangeLog.md
- export DATE="`LANG=en_US date +'%a %b %d %Y'`"
```
```
- cat > ChangeLog.md <<EOF
>* ${DATE} ${GITHUB_USERNAME} <${GITHUB_EMAIL}> 0.1.0.0
>- Initial RPM release
>EOF
```
```
-cat > CPackConfig.cmake <<EOF
>include(InstallRequiredSystemLibraries)
>EOF
```
```
-nano CPackConfig.cmake
-set(CPACK_PACKAGE_CONTACT ${GITHUB_EMAIL})
set(CPACK_PACKAGE_VERSION_MAJOR \${PRINT_VERSION_MAJOR})
set(CPACK_PACKAGE_VERSION_MINOR \${PRINT_VERSION_MINOR})
set(CPACK_PACKAGE_VERSION_PATCH \${PRINT_VERSION_PATCH})
set(CPACK_PACKAGE_VERSION_TWEAK \${PRINT_VERSION_TWEAK})
set(CPACK_PACKAGE_VERSION \${PRINT_VERSION})
```
```
-cat >> CPackConfig.cmake <<EOF

>set(CPACK_RESOURCE_FILE_LICENSE \${CMAKE_CURRENT_SOURCE_DIR}/LICENSE)
>set(CPACK_RESOURCE_FILE_README \${CMAKE_CURRENT_SOURCE_DIR}/README.md)
>EOF
```
```
-cat >> CPackConfig.cmake <<EOF

>set(CPACK_RPM_PACKAGE_NAME "print-devel")
>set(CPACK_RPM_PACKAGE_LICENSE "MIT")
>set(CPACK_RPM_PACKAGE_GROUP "print")
>set(CPACK_RPM_CHANGELOG_FILE \${CMAKE_CURRENT_SOURCE_DIR}/ChangeLog.md)
>set(CPACK_RPM_PACKAGE_RELEASE 1)
>EOF
```
```

-cat >> CPackConfig.cmake <<EOF

>set(CPACK_DEBIAN_PACKAGE_NAME "libprint-dev")
>set(CPACK_DEBIAN_PACKAGE_PREDEPENDS "cmake >= 3.0")
>set(CPACK_DEBIAN_PACKAGE_RELEASE 1)
>EOF
```
```

-cat >> CPackConfig.cmake <<EOF

>include(CPack)
>EOF
```
```
-cat >> CMakeLists.txt <<EOF

>include(CPackConfig.cmake)
>EOF
```
```
-gsed -i 's/lab05/lab06/g' README.md
```
```
-git add .
-git commit -m"added cpack config"
--[main 3a167d1] added cpack config
 5 files changed, 35 insertions(+), 2 deletions(-)
 create mode 100644 CPackConfig.cmake
 create mode 100644 ChangeLog.md
 create mode 100644 DESCRIPTION
-git tag v0.1.0.0
-git push origin main --tags
--Перечисление объектов: 107, готово.
Подсчет объектов: 100% (107/107), готово.
Сжатие объектов: 100% (57/57), готово.
Запись объектов: 100% (107/107), 20.70 КиБ | 5.17 МиБ/с, готово.
Total 107 (delta 34), reused 98 (delta 31), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (34/34), done.
To https://github.com/Goydarik/lab06
 * [new branch]      main -> main
 * [new tag]         v0.1.0.0 -> v0.1.0.0
-git push origin main
--Перечисление объектов: 5, готово.
Подсчет объектов: 100% (5/5), готово.
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (3/3), 307 байтов | 307.00 КиБ/с, готово.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/Goydarik/lab06
   bf7ed2c..79805cd  main -> main
```
(наблюдаем синхронизацию с Github Actions)
```
-cmake -H. -B_build
--CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.
```


-- The C compiler identification is GNU 14.2.0
-- The CXX compiler identification is GNU 14.2.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done (0.6s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rasul/Goydarik/workspace/projects/lab06/_build
-cmake --build _build
--[ 50%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[100%] Linking CXX static library libprint.a
[100%] Built target print
-cd _build
-cpack -G "TGZ"
--CPack: Create package using TGZ
CPack: Install projects
CPack: - Run preinstall target for: print
CPack: - Install project: print []
CPack: Create package
CPack: - package: /home/rasul/Goydarik/workspace/projects/lab06/_build/print--Linux.tar.gz generated.
-cd ..
-cmake -H. -B_build -DCPACK_GENERATOR="TGZ"
--CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rasul/Goydarik/workspace/projects/lab06/_build
-cmake --build _build --target package
--[100%] Built target print
Run CPack packaging tool...
CPack: Create package using TGZ
CPack: Install projects
CPack: - Run preinstall target for: print
CPack: - Install project: print []
CPack: Create package
CPack: - package: /home/rasul/Goydarik/workspace/projects/lab06/_build/print--Linux.tar.gz generated.
-mkdir artifacts
-mv _build/*.tar.gz artifacts
-tree artifacts
--artifacts
└── print--Linux.tar.gz

1 directory, 1 file
```
____________________________________________________________________
HOMEWORK
____________________________________________________________________

```
-nano .github/workflows/build-and-package.yml
-name: Build and Package
on:
  push:
    tags:
      - 'v*'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Configure and Build
        run: |
          cmake -H. -B_build -DCPACK_GENERATOR="TGZ;DEB;RPM"
          cmake --build _build --target package
      - name: Create Release
        uses: softprops/action-gh-release@v1
        with:
          files: _build/*.deb, _build/*.rpm, _build/*.tar.gz
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
