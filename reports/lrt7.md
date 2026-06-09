## Лабораторная работа 07
Тема: изучение систем управления пакетами на примере gtest

Ход выполнения:
```
$ alias gsed=sed
$ cd Goydarik/workspace
$ pushd .
~/Goydarik/workspace ~/Goydarik/workspace
$ source scripts/activate
```
```
$ git clone https://github.com/Goydarik/lab06 projects/lab07
Cloning into 'projects/lab07'...
remote: Enumerating objects: 166, done.
remote: Counting objects: 100% (166/166), done.
remote: Compressing objects: 100% (94/94), done.
remote: Total 166 (delta 62), reused 149 (delta 45), pack-reused 0 (from 0)
Receiving objects: 100% (166/166), 29.00 KiB | 1.45 MiB/s, done.
Resolving deltas: 100% (62/62), done.
```
```
$ cd projects/lab07
$ git remote remove origin
$ git remote add origin https://github.com/Goydarik/lab07
$ nano CMakeLists.txt

Содержимое CMakeLists.txt:
cmake_minimum_required(VERSION 3.4)

include(FetchContent)

FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/refs/tags/v1.14.0.tar.gz
)

FetchContent_MakeAvailable(googletest)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

option(BUILD_EXAMPLES "Build examples" OFF)
option(BUILD_TESTS "Build tests" ON)

project(print VERSION 1.0.0)
set(PRINT_VERSION_MAJOR 0)
set(PRINT_VERSION_MINOR 1)
set(PRINT_VERSION_PATCH 0)
set(PRINT_VERSION_TWEAK 0)
set(PRINT_VERSION
  ${PRINT_VERSION_MAJOR}.${PRINT_VERSION_MINOR}.${PRINT_VERSION_PATCH}.${PRINT_VERSION_TWEAK})
set(PRINT_VERSION_STRING "v${PRINT_VERSION}")

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

if(BUILD_TESTS)
  enable_testing()
  add_subdirectory(tests)
  
  file(GLOB TEST_SOURCES tests/*.cpp)
  add_executable(check ${TEST_SOURCES})
  target_link_libraries(check ${PROJECT_NAME} gtest_main)
  add_test(NAME check COMMAND check)
endif()
include(CPackConfig.cmake)
```
```

$ git rm -rf third-party/gtest
$ mkdir tests
$ cd tests
```
```
$ nano test_print.cpp

Содержимое test_print.cpp:
#include <gtest/gtest.h>
#include <print.hpp>

TEST(PrintTest, OutputCheck) {
    std::stringstream out;
    print("hello", out);
    EXPECT_EQ(out.str(), "hello");
}
```
```

$ nano CMakeLists.txt

Содержимое CMakeLists.txt:
add_executable(tests test_print.cpp)
target_link_libraries(tests PRIVATE print gtest_main)
add_test(NAME tests COMMAND tests)
```
```
$ cd ..
$ cmake -H. -B_builds -DBUILD_TESTS=ON
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.

CMake Warning (dev) at /usr/share/cmake-3.31/Modules/FetchContent.cmake:1373 (message):
  The DOWNLOAD_EXTRACT_TIMESTAMP option was not given and policy CMP0135 is
  not set.  The policy's OLD behavior will be used.  When using a URL
  download, the timestamps of extracted files should preferably be that of
  the time of extraction, otherwise code that depends on the extracted
  contents might not be rebuilt if the URL changes.  The OLD behavior
  preserves the timestamps from the archive instead, but
this is usually not
  what you want.  Update your project to the NEW behavior or specify the
DOWNLOAD_EXTRACT_TIMESTAMP option with a value of true to avoid this
  robustness issue.
Call Stack (most recent call first):
  CMakeLists.txt:5 (FetchContent_Declare)
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Configuring done (0.3s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rasul/Goydarik/workspace/projects/lab07/_builds
```
```
$ cmake --build _builds
[  7%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 14%] Linking CXX static library libprint.a
[ 14%] Built target print
[ 21%] Building CXX object _deps/googletest-build/googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
[ 28%] Linking CXX static library ../../../lib/libgtest.a
[ 28%] Built target gtest
[ 35%] Building CXX object _deps/googletest-build/googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
[ 42%] Linking CXX static library ../../../lib/libgtest_main.a
[ 42%] Built target gtest_main
[ 50%] Building CXX object CMakeFiles/check.dir/tests/test_print.cpp.o
[ 57%] Linking CXX executable check
[ 57%] Built target check
[ 64%] Building CXX object _deps/googletest-build/googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
[ 71%] Linking CXX static library ../../../lib/libgmock.a
[ 71%] Built target gmock
[ 78%] Building CXX object _deps/googletest-build/googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
[ 85%] Linking CXX static library ../../../lib/libgmock_main.a
[ 85%] Built target gmock_main
[ 92%] Building CXX object tests/CMakeFiles/tests.dir/test_print.cpp.o
[100%] Linking CXX executable tests
[100%] Built target tests
$ cmake --build _builds --target test
Running tests...
Test project /home/rasul/Goydarik/workspace/projects/lab07/_builds
    Start 1: check
1/2 Test #1: check ............................   Passed    0.00 sec
    Start 2: tests
2/2 Test #2: tests ............................   Passed    0.00 sec

100% tests passed, 0 tests failed out of 2

Total Test time (real) =   0.01 sec
```
```
$ mkdir demo
$ nano demo/main.cpp

Содержимое main.cpp:
#include <print.hpp>
#include <fstream>
#include <iostream>
#include <cstdlib>

int main(int argc, char* argv[]) {
    const char* log_path = std::getenv("LOG_PATH");
    if (log_path == nullptr) {
        std::cerr << "undefined environment variable: LOG_PATH" << std::endl;
        return 1;
    }
    std::string text;
    while (std::cin >> text) {
        std::ofstream out{log_path, std::ios_base::app};
        print(text, out);
        out << std::endl;
    }
}
```
```
$ nano CMakeLists.txt
```
дописываем в конец файла:
```
add_executable(demo ${CMAKE_CURRENT_SOURCE_DIR}/demo/main.cpp)
target_link_libraries(demo print)
install(TARGETS demo RUNTIME DESTINATION bin)
```
```
$ mkdir tools
$ git submodule add https://github.com/ruslo/polly_tools/polly
$ tools/polly/bin/polly.py --test
$ tools/polly/bin/polly.py --install
```
выдает ошибку:
```
== WARNING ==

Looks like cmake arguments changed. You have two options to fix it:
  * Remove build directory completely by adding '--clear' (works 100%)
  * Run configure again by adding '--reconfig' (you must understand how CMake cache variables works/updated)

- "cmake" "-H." "-B/home/rasul/Goydarik/workspace/projects/lab07/_builds/default" "-DCMAKE_TOOLCHAIN_FILE=/home/rasul/Goydarik/workspace/projects/lab07/tools/polly/default.cmake"
+ "cmake" "-H." "-B/home/rasul/Goydarik/workspace/projects/lab07/_builds/default" "-DCMAKE_TOOLCHAIN_FILE=/home/rasul/Goydarik/workspace/projects/lab07/tools/polly/default.cmake" "-DCMAKE_INSTALL_PREFIX=/home/rasul/Goydarik/workspace/projects/lab07/_install/default"
?                                                                                                                                                                                 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
```
исправляем, добавляя флаг --clear:
```
$ tools/polly/bin/polly.py --install --clear
Python version: 3.13
Build
dir:

/home/rasul/Goydarik/workspace/projects/lab07/_builds/default
Remove directory: /home/rasul/Goydarik/workspace/projects/lab07/_builds/default
Execute command: [
  `which`
  `cmake`
]

[/home/rasul/Goydarik/workspace/projects/lab07]> "which" "cmake"

/usr/bin/cmake
Execute command: [
  `cmake`
  `--version`
]

[/home/rasul/Goydarik/workspace/projects/lab07]> "cmake" "--version"

cmake version 3.31.6

CMake suite maintained and supported by Kitware (kitware.com/cmake).
Execute command: [
  `cmake`
  `-H.`
  `-B/home/rasul/Goydarik/workspace/projects/lab07/_builds/default`
  `-DCMAKE_TOOLCHAIN_FILE=/home/rasul/Goydarik/workspace/projects/lab07/tools/polly/default.cmake`
  `-DCMAKE_INSTALL_PREFIX=/home/rasul/Goydarik/workspace/projects/lab07/_install/default`
]

[/home/rasul/Goydarik/workspace/projects/lab07]> "cmake" "-H." "-B/home/rasul/Goydarik/workspace/projects/lab07/_builds/default" "-DCMAKE_TOOLCHAIN_FILE=/home/rasul/Goydarik/workspace/projects/lab07/tools/polly/default.cmake" "-DCMAKE_INSTALL_PREFIX=/home/rasul/Goydarik/workspace/projects/lab07/_install/default"

CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.

CMake Warning (dev) at /usr/share/cmake-3.31/Modules/FetchContent.cmake:1373 (message):
  The DOWNLOAD_EXTRACT_TIMESTAMP option was not given and policy CMP0135 is
  not set.  The policy's OLD behavior will be used.  When using a URL
  download, the timestamps of extracted files should preferably be that of
  the time of extraction, otherwise code that depends on the extracted
  contents might not be rebuilt if the URL changes.  The OLD behavior
  preserves the timestamps from the archive instead, but this is usually not
  what you want.  Update your project to the NEW behavior or specify the
  DOWNLOAD_EXTRACT_TIMESTAMP option with a value of true to avoid this
  robustness issue.
Call Stack (most recent call first):
  CMakeLists.txt:5 (FetchContent_Declare)
This warning is for project developers.  Use -Wno-dev to suppress it.

-- [polly] Used toolchain: Default
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
-- Found Python3: /usr/bin/python3 (found version "3.13.5") found components: Interpreter
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- [polly] Used toolchain: Default
-- Configuring done (2.3s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rasul/Goydarik/workspace/projects/lab07/_builds/default
Execute command: [
  `cmake`
  `--build`
  `/home/rasul/Goydarik/workspace/projects/lab07/_builds/default`
  `--target`
  `install`
  `--`
]

[/home/rasul/Goydarik/workspace/projects/lab07]> "cmake" "--build" "/home/rasul/Goydarik/workspace/projects/lab07/_builds/default" "--target" "install" "--"

[  6%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 12%] Linking CXX static library libprint.a
[ 12%] Built target print
[ 18%] Building CXX object _deps/googletest-build/googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
[ 25%] Linking CXX static library ../../../lib/libgtest.a
[ 25%] Built target gtest
[ 31%] Building CXX object _deps/googletest-build/googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
[ 37%] Linking CXX static
Building Solutions on Open Source Technologies
Building Solutions on Open Source Technologies
www.kitware.com
library ../../../lib/libgtest_main.a
[ 37%] Built target gtest_main
[ 43%] Building CXX object
CMakeFiles/check.dir/tests/test_print.cpp.o
[ 50%] Linking CXX executable check
[ 50%] Built target check
[ 56%] Building CXX object CMakeFiles/demo.dir/demo/main.cpp.o
[ 62%] Linking CXX executable demo
[ 62%] Built target demo
[ 68%] Building CXX object _deps/googletest-build/googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
[ 75%] Linking CXX static library ../../../lib/libgmock.a
[ 75%] Built target gmock
[ 81%] Building CXX object _deps/googletest-build/googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
[ 87%] Linking CXX static library ../../../lib/libgmock_main.a
[ 87%] Built target gmock_main
[ 93%] Building CXX object tests/CMakeFiles/tests.dir/test_print.cpp.o
[100%] Linking CXX executable tests
[100%] Built target tests
Install the project...
-- Install configuration: ""
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/lib/libprint.a
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/print.hpp
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/cmake/print-config.cmake
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/cmake/print-config-noconfig.cmake
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/bin/demo
-- Up-to-date: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/gmock.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/internal
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/internal/gmock-pp.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/internal/gmock-internal-utils.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/internal/custom
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/internal/custom/README.md
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/internal/custom/gmock-generated-actions.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/internal/custom/gmock-matchers.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/internal/custom/gmock-port.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/internal/gmock-port.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/gmock-actions.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/gmock-function-mocker.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/gmock-matchers.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/gmock-more-matchers.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/gmock-spec-builders.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/gmock-cardinalities.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/gmock-more-actions.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gmock/gmock-nice-strict.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/lib/libgmock.a
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/lib/libgmock_main.a
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/lib/pkgconfig/gmock.pc
-- Installing:
AI Tools Directory - dealsbe.com
AI Tools Directory - dealsbe.com
dealsbe.com
/home/rasul/Goydarik/workspace/projects/lab07/_install/default/lib/pkgconfig/gmock_main.pc
-- Installing:
/home/rasul/Goydarik/workspace/projects/lab07/_install/default/lib/cmake/GTest/GTestTargets.cmake
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/lib/cmake/GTest/GTestTargets-noconfig.cmake
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/lib/cmake/GTest/GTestConfigVersion.cmake
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/lib/cmake/GTest/GTestConfig.cmake
-- Up-to-date: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/gtest-death-test.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/gtest-matchers.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/gtest_prod.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/gtest-param-test.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/internal
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/internal/gtest-port-arch.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/internal/gtest-port.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/internal/gtest-internal.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/internal/custom
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/internal/custom/README.md
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/internal/custom/gtest-port.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/internal/custom/gtest-printers.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/internal/custom/gtest.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/internal/gtest-type-util.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/internal/gtest-param-util.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/internal/gtest-filepath.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/internal/gtest-death-test-internal.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/internal/gtest-string.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/gtest-printers.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/gtest-spi.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/gtest-message.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/gtest-typed-test.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/gtest-assertion-result.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/gtest_pred_impl.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/gtest-test-part.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/include/gtest/gtest.h
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/lib/libgtest.a
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/lib/libgtest_main.a
-- Installing: /home/rasul/Goydarik/workspace/projects/lab07/_install/default/lib/pkgconfig/gtest.pc
-- Installing:
AI Tools Directory - dealsbe.com
AI Tools Directory - dealsbe.com
dealsbe.com
/home/rasul/Goydarik/workspace/projects/lab07/_install/default/lib/pkgconfig/gtest_main.pc
-
Log saved: /home/rasul/Goydarik/workspace/projects/lab07/_logs/polly/default/log.txt
-
Generate: 0:00:03.298311s
Build: 0:00:08.953552s
-
Total: 0:00:12.252133s
-
SUCCESS
```
```
$ tools/polly/bin/polly.py --toolchain clang-cxx14
Python version: 3.13
Build dir: /home/rasul/Goydarik/workspace/projects/lab07/_builds/clang-cxx14
Execute command: [
  `which`
  `cmake`
]

[/home/rasul/Goydarik/workspace/projects/lab07]> "which" "cmake"

/usr/bin/cmake
Execute command: [
  `cmake`
  `--version`
]

[/home/rasul/Goydarik/workspace/projects/lab07]> "cmake" "--version"

cmake version 3.31.6

CMake suite maintained and supported by Kitware (kitware.com/cmake).
Execute command: [
  `cmake`
  `-H.`
  `-B/home/rasul/Goydarik/workspace/projects/lab07/_builds/clang-cxx14`
  `-GUnix Makefiles`
  `-DCMAKE_TOOLCHAIN_FILE=/home/rasul/Goydarik/workspace/projects/lab07/tools/polly/clang-cxx14.cmake`
]

[/home/rasul/Goydarik/workspace/projects/lab07]> "cmake" "-H." "-B/home/rasul/Goydarik/workspace/projects/lab07/_builds/clang-cxx14" "-GUnix Makefiles" "-DCMAKE_TOOLCHAIN_FILE=/home/rasul/Goydarik/workspace/projects/lab07/tools/polly/clang-cxx14.cmake"

CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.

CMake Warning (dev) at /usr/share/cmake-3.31/Modules/FetchContent.cmake:1373 (message):
  The DOWNLOAD_EXTRACT_TIMESTAMP option was not given and policy CMP0135 is
  not set.  The policy's OLD behavior will be used.  When using a URL
  download, the timestamps of extracted files should preferably be that of
  the time of extraction, otherwise code that depends on the extracted
  contents might not be rebuilt if the URL changes.  The OLD behavior
  preserves the timestamps from the archive instead, but this is usually not
  what you want.  Update your project to the NEW behavior or specify the
  DOWNLOAD_EXTRACT_TIMESTAMP option with a value of true to avoid this
  robustness issue.
Call Stack (most recent call first):
  CMakeLists.txt:5 (FetchContent_Declare)
This warning is for project developers.  Use -Wno-dev to suppress it.

-- [polly] Used toolchain: clang / c++14 support
-- Configuring incomplete, errors occurred!

clang not found

CMake Error at tools/polly/utilities/polly_fatal_error.cmake:10 (message):
Call Stack (most recent call first):
  tools/polly/compiler/clang.cmake:23 (polly_fatal_error)
  tools/polly/clang-cxx14.cmake:20 (include)
  /usr/share/cmake-3.31/Modules/CMakeDetermineSystem.cmake:146 (include)
  _builds/clang-cxx14/_deps/googletest-src/CMakeLists.txt:6 (project)

CMake Error: CMake was unable to find a build program corresponding to "Unix Makefiles".  CMAKE_MAKE_PROGRAM is not set.  You probably need to select a different build tool.
Command exit with status "1": [/home/rasul/Goydarik/workspace/projects/lab07]> "cmake" "-H." "-B/home/rasul/Goydarik/workspace/projects/lab07/_builds/clang-cxx14" "-GUnix Makefiles" "-DCMAKE_TOOLCHAIN_FILE=/home/rasul/Goydarik/workspace/projects/lab07/tools/polly/clang-cxx14.cmake"

Log: /home/rasul/Goydarik/workspace/projects/lab07/_logs/polly/clang-cxx14/log.txt
*** FAILED ***
```
пробуем установить clang:
```
$ sudo apt update
Get:1 http://security.debian.org/debian-security trixie-security InRelease [43.4 kB]
Hit:2 http://deb.debian.org/debian trixie InRelease  
Get:3 http://deb.debian.org/debian trixie-updates InRelease [47.3 kB]
Get:4 http://security.debian.org/debian-security trixie-security/main Sources [167 kB]
Get:5 http://security.debian.org/debian-security trixie-security/main amd64 Packages [176 kB]
Get:6 http://security.debian.org/debian-security trixie-security/main Translation-en [111
Index of /debian
ftp.debian.org
kB]
Fetched 545 kB in 23s (24.1 kB/s)                               
251 packages can be upgraded. Run 'apt list --upgradable' to see them.
$ sudo apt install clang-14 clang++-14
Error: Unable to locate package clang-14
Error: Unable to locate package clang++-14
```
Из-за невозможности установить clang выполняем эту команду через gcc:
```
$ gcc --version
gcc (Debian 14.2.0-19) 14.2.0
Copyright (C) 2024 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
$ tools/polly/bin/polly.py --toolchain gcc
Python version: 3.13
Build dir: /home/rasul/Goydarik/workspace/projects/lab07/_builds/gcc
Execute command: [
  `which`
  `cmake`
]

[/home/rasul/Goydarik/workspace/projects/lab07]> "which" "cmake"

/usr/bin/cmake
Execute command: [
  `cmake`
  `--version`
]

[/home/rasul/Goydarik/workspace/projects/lab07]> "cmake" "--version"

cmake version 3.31.6

CMake suite maintained and supported by Kitware (kitware.com/cmake).
Execute command: [
  `cmake`
  `-H.`
  `-B/home/rasul/Goydarik/workspace/projects/lab07/_builds/gcc`
  `-GUnix Makefiles`
  `-DCMAKE_TOOLCHAIN_FILE=/home/rasul/Goydarik/workspace/projects/lab07/tools/polly/gcc.cmake`
]

[/home/rasul/Goydarik/workspace/projects/lab07]> "cmake" "-H." "-B/home/rasul/Goydarik/workspace/projects/lab07/_builds/gcc" "-GUnix Makefiles" "-DCMAKE_TOOLCHAIN_FILE=/home/rasul/Goydarik/workspace/projects/lab07/tools/polly/gcc.cmake"

CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.

CMake Warning (dev) at /usr/share/cmake-3.31/Modules/FetchContent.cmake:1373 (message):
  The DOWNLOAD_EXTRACT_TIMESTAMP option was not given and policy CMP0135 is
  not set.  The policy's OLD behavior will be used.  When using a URL
  download, the timestamps of extracted files should preferably be that of
  the time of extraction, otherwise code that depends on the extracted
  contents might not be rebuilt if the URL changes.  The OLD behavior
  preserves the timestamps from the archive instead, but this is usually not
  what you want.  Update your project to the NEW behavior or specify the
  DOWNLOAD_EXTRACT_TIMESTAMP option with a value of true to avoid this
  robustness issue.
Call Stack (most recent call first):
  CMakeLists.txt:5 (FetchContent_Declare)
This warning is for project developers.  Use -Wno-dev to suppress it.

-- [polly] Used toolchain: gcc / c++11 support
-- The C compiler identification is GNU 14.2.0
-- The CXX compiler identification is GNU 14.2.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/gcc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/g++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Found Python3: /usr/bin/python3 (found version "3.13.5") found components: Interpreter
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- [polly] Used toolchain: gcc / c++11 support
-- Configuring done (2.1s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rasul/Goydarik/workspace/projects/lab07/_builds/gcc
Execute command: [
  `cmake`
  `--build`
  `/home/rasul/Goydarik/workspace/projects/lab07/_builds/gcc`
  `--`
]

[/home/rasul/Goydarik/workspace/projects/lab07]> "cmake" "--build" "/home/rasul/Goydarik/workspace/projects/lab07/_builds/gcc" "--"

[  6%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 12%]
Building Solutions on Open Source Technologies
Building Solutions on Open Source Technologies
www.kitware.com
Linking CXX static library libprint.a
[ 12%] Built target print
[ 18%] Building CXX object _deps/googletest-build/googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
[ 25%] Linking CXX static library ../../../lib/libgtest.a
[ 25%] Built target gtest
[ 31%] Building CXX object _deps/googletest-build/googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
[ 37%] Linking CXX static library ../../../lib/libgtest_main.a
[ 37%] Built target gtest_main
[ 43%] Building CXX object CMakeFiles/check.dir/tests/test_print.cpp.o
[ 50%] Linking CXX executable check
[ 50%] Built target check
[ 56%] Building CXX object CMakeFiles/demo.dir/demo/main.cpp.o
[ 62%] Linking CXX executable demo
[ 62%] Built target demo
[ 68%] Building CXX object _deps/googletest-build/googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
[ 75%] Linking CXX static library ../../../lib/libgmock.a
[ 75%] Built target gmock
[ 81%] Building CXX object _deps/googletest-build/googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
[ 87%] Linking CXX static library ../../../lib/libgmock_main.a
[ 87%] Built target gmock_main
[ 93%] Building CXX object tests/CMakeFiles/tests.dir/test_print.cpp.o
[100%] Linking CXX executable tests
[100%] Built target tests
-
Log saved: /home/rasul/Goydarik/workspace/projects/lab07/_logs/polly/gcc/log.txt
-
Generate: 0:00:03.135800s
Build: 0:00:07.942628s
-
Total: 0:00:11.079022s
-
SUCCESS
```