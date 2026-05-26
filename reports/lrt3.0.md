## Laboratory work III(Tutorial)

Данная лабораторная работа посвещена изучению систем автоматизации сборки проекта на примере **CMake**

(Вводные данные "-"
 Выходные данные "--"
 Вводные данные в cat ">")

```
-export GITHUB_USERNAME=Goydarik
-cd ${GITHUB_USERNAME}/workspace
-pushd .
--~/Goydarik/workspace ~/Goydarik/workspace
-source scripts/activate
-git clone https://github.com/${GITHUB_USERNAME}/lab02.git projects/lab03
-cd projects/lab03
-git remote remove origin
-git remote add origin https://github.com/${GITHUB_USERNAME}/lab03.git
-g++ -std=c++11 -I./include -c sources/print.cpp
-ls print.o
--print.o
-nm print.o | grep print
--0000000000000000 T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSo
0000000000000026 T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E
-ar rvs print.a print.o
--ar: создаётся print.a
a - print.o
-file print.a
--print.a: current ar archive
-g++ -std=c++11 -I./include -c examples/example1.cpp
-ls example1.o
--example.o
-g++ example1.o print.a -o example1
-./example1 && echo
--hello
-g++ -std=c++11 -I./include -c examples/example2.cpp
-nm example2.o
--0000000000000000 V DW.ref.__gxx_personality_v0
                 U __gxx_personality_v0
0000000000000000 T main
                 U _Unwind_Resume
                 U _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEEC1EPKcSt13_Ios_Openmode
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEED1Ev
0000000000000000 W _ZNSt15__new_allocatorIcED1Ev
0000000000000000 W _ZNSt15__new_allocatorIcED2Ev
0000000000000000 n _ZNSt15__new_allocatorIcED5Ev
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEC1EPKcRKS3_
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEED1Ev
                 U _ZSt21ios_base_library_initv
0000000000000000 r _ZStL19piecewise_construct
-g++ example2.o print.a -o example2
-./example2
-cat log.txt && echo
--hello
-rm -rf example1.o example2.o print.o
-rm -rf print.a
-rm -rf example1 example2
-rm -rf log.txt
-cat > CMakeLists.txt <<EOF
>cmake_minimum_required(VERSION 3.4)
>project(print)
>EOF
-cat >> CMakeLists.txt <<EOF
>set(CMAKE_CXX_STANDARD 11)
>set(CMAKE_CXX_STANDARD_REQUIRED ON)
>EOF
-cat >> CMakeLists.txt <<EOF
>add_library(print STATIC \${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
>EOF
-cat >> CMakeLists.txt <<EOF
>include_directories(\${CMAKE_CURRENT_SOURCE_DIR}/include)
>EOF
-cmake -H. -B_build
--CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.


-- Configuring done (0.1s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rasul/Goydarik/workspace/projects/lab03/_build
-cmake --build _build
--[100%] Built target print
-cat >> CMakeLists.txt <<EOF
>add_executable(example1 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example1.cpp)
>add_executable(example2 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example2.cpp)
>EOF
-cat >> CMakeLists.txt <<EOF
>target_link_libraries(example1 print)
>target_link_libraries(example2 print)
>EOF
-cmake --build _build
--CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rasul/Goydarik/workspace/projects/lab03/_build
[ 33%] Built target print
[ 66%] Built target example1
[100%] Built target example2
-cmake --build _build --target print
--[100%] Built target print
-cmake --build _build --target example1
--[ 50%] Built target print
[100%] Built target example1
-cmake --build _build --target example2
--[ 50%] Built target print
[100%] Built target example2
-ls -la _build/libprint.a
-- -rw-rw-r-- 1 rasul rasul 2110 апр 29 14:33 _build/libprint.a
-_build/example1 && echo
--hello
-_build/example2
-cat log.txt && echo
--hello
-rm -rf log.txt
-git clone https://github.com/tp-labs/lab03 tmp
--Клонирование в «tmp»...
remote: Enumerating objects: 91, done.
remote: Counting objects: 100% (30/30), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 91 (delta 23), reused 21 (delta 21), pack-reused 61 (from 1)
Получение объектов: 100% (91/91), 1.02 МиБ | 1.47 МиБ/с, готово.
Определение изменений: 100% (41/41), готово.
-mv -f tmp/CMakeLists.txt .
-rm -rf tmp
-cat CMakeLists.txt
--cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

option(BUILD_EXAMPLES "Build examples" OFF)

project(print)

add_library(print STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)

target_include_directories(print PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
)

if(BUILD_EXAMPLES)
  file(GLOB EXAMPLE_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/examples/*.cpp")
  foreach(EXAMPLE_SOURCE ${EXAMPLE_SOURCES})
    get_filename_component(EXAMPLE_NAME ${EXAMPLE_SOURCE} NAME_WE)
    add_executable(${EXAMPLE_NAME} ${EXAMPLE_SOURCE})
    target_link_libraries(${EXAMPLE_NAME} print)
    install(TARGETS ${EXAMPLE_NAME}
      RUNTIME DESTINATION bin
    )
  endforeach(EXAMPLE_SOURCE ${EXAMPLE_SOURCES})
endif()

install(TARGETS print
    EXPORT print-config
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)

install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/ DESTINATION include)
install(EXPORT print-config DESTINATION cmake)
-cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
--CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rasul/Goydarik/workspace/projects/lab03/_build
-cmake --build _build --target install
--[100%] Built target print
Install the project...
-- Install configuration: ""
-- Up-to-date: /home/rasul/Goydarik/workspace/projects/lab03/_install/lib/libprint.a
-- Up-to-date: /home/rasul/Goydarik/workspace/projects/lab03/_install/include
-- Up-to-date: /home/rasul/Goydarik/workspace/projects/lab03/_install/include/print.hpp
-- Up-to-date: /home/rasul/Goydarik/workspace/projects/lab03/_install/cmake/print-config.cmake
-- Up-to-date: /home/rasul/Goydarik/workspace/projects/lab03/_install/cmake/print-config-noconfig.cmake
-tree _install
--install
├── cmake
│   ├── print-config.cmake
│   └── print-config-noconfig.cmake
├── include
│   └── print.hpp
└── lib
    └── libprint.a

4 directories, 4 files
-git add CMakeLists.txt
-git commit -m"added CMakeLists.txt"
-git push origin master
-popd
--~/Goydarik/workspace
-export LAB_NUMBER=03
-export LAB_NUMBER=03
-git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
-mkdir reports/lab${LAB_NUMBER}
-cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
-cd reports/lab${LAB_NUMBER}
-edit REPORT.md
-gist REPORT.md
--https://gist.github.com/Goydarik/9d98d17b0987b886833dc9299be07752
```