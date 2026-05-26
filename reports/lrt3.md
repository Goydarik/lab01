## Laboratory work III(Homework)

Данная лабораторная работа посвещена изучению систем автоматизации сборки проекта на примере **CMake**

(Вводные данные "-"
 Выходные данные "--"
 Вводные данные в cat ">")

1.
```
-git clone https://github.com/tp-labs/lab03.git
--Клонирование в «lab03»...
remote: Enumerating objects: 91, done.
remote: Counting objects: 100% (30/30), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 91 (delta 23), reused 21 (delta 21), pack-reused 61 (from 1)
Получение объектов: 100% (91/91), 1.02 МиБ | 110.00 КиБ/с, готово.
Определение изменений: 100% (41/41), готово.
-cd lab03
(Перемещаем папку lab03 из reports в projects)
-nano CMakeLists.txt (в папке formatter_lib)
-cmake_minimum_required(VERSION 3.4)
project(formatter)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(formatter STATIC formatter.cpp)
include_directories(\${CMAKE_CURRENT_SOURCE_DIR})
-mkdir build && cd build
-cmake ..
--CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.


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
-- Configuring done (0.3s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rasul/Goydarik/workspace/projects/lab03/lab03/formatter_lib/build
-cmake --build .
--[ 50%] Building CXX object CMakeFiles/formatter.dir/formatter.cpp.o
[100%] Linking CXX static library libformatter.a
[100%] Built target formatter
```

2.(Переходим в formatter_ex_lib)
```
-nano CMakeLists.txt
-cmake_minimum_required(VERSION 3.4)
project(formatter_ex)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Путь к библиотеке formatter
set(FORMATTER_LIB_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib)

# Добавляем поддиректорию с formatter
add_subdirectory(${FORMATTER_LIB_PATH} ${CMAKE_BINARY_DIR}/formatter_lib)

# Создаем библиотеку formatter_ex
add_library(formatter_ex STATIC 
    ${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex.cpp
)

# Добавляем пути для поиска заголовочных файлов
target_include_directories(formatter_ex PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${FORMATTER_LIB_PATH}
)

# Линкуем с библиотекой formatter
target_link_libraries(formatter_ex formatter)
-mkdir build && cd build
-cmake ..
--CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.


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
CMake Deprecation Warning at /home/rasul/Goydarik/workspace/projects/lab03/lab03/formatter_lib/CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.


-- Configuring done (0.3s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rasul/Goydarik/workspace/projects/lab03/lab03/formatter_ex_lib/build
-cmake --build .
--[ 25%] Building CXX object formatter_lib/CMakeFiles/formatter.dir/formatter.cpp.o
[ 50%] Linking CXX static library libformatter.a
[ 50%] Built target formatter
[ 75%] Building CXX object CMakeFiles/formatter_ex.dir/formatter_ex.cpp.o
[100%] Linking CXX static library libformatter_ex.a
[100%] Built target formatter_ex
```

3.
1)
```
(Создаём папку hello_world и переходим в неё)
-nano CMakeLists.txt
-cmake_minimum_required(VERSION 3.4)
project(hello_world)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(FORMATTER_EX_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib)
set(FORMATTER_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib)

add_executable(hello_world hello_world.cpp)

target_include_directories(hello_world
    PRIVATE
        /home/rasul/Goydarik/workspace/projects/lab03/lab03/formatter_ex_lib
)

target_link_libraries(hello_world
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib/build/libformatter_ex.a
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib/build/libformatter.a
)
-nano hello_world.cpp
-#include "formatter_ex.h"
#include <iostream>

int main() {
    formatter(std::cout, "Hello, World!") << std::endl;
    return 0;
}
-mkdir build 
-cd build
cmake ..
--CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.


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
-- Configuring done (0.3s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rasul/Goydarik/workspace/projects/lab03/lab03/hello_world/build
- cmake --build .
--[ 50%] Building CXX object CMakeFiles/hello_world.dir/hello_world.cpp.o
[100%] Linking CXX executable hello_world
[100%] Built target hello_world
-chmod +x hello_world.cpp
(проверка работы)
-./hello_world
---------------------------
Hello, World!
-------------------------
```

2)
(перходим в папку solver_lib)
```
-nano CMakeLists.txt
-cmake_minimum_required(VERSION 3.4)
project(solver_lib)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(solver_lib STATIC ${CMAKE_CURRENT_SOURCE_DIR}/solver.cpp)

target_include_directories(solver_lib PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

# Принудительно включаем cmath перед компиляцией
target_compile_options(solver_lib PRIVATE -include cmath)
-mkdir build
-cd build
-cmake ..CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.


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
-- Configuring done (0.3s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rasul/Goydarik/workspace/projects/lab03/lab03/solver_lib/build
-cmake --build .
--[ 50%] Building CXX object CMakeFiles/solver_lib.dir/solver.cpp.o
[100%] Linking CXX static library libsolver_lib.a
[100%] Built target solver_lib
(Переходим в папку solver_application)
-nano CMakeLists.txt
-cmake_minimum_required(VERSION 3.4)
project(solver_application)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(solver_application equation.cpp)

target_include_directories(solver_application PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib
    ${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib
)

target_link_libraries(solver_application
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib/build/libformatter_ex.a
    ${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib/build/libsolver_lib.a
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib/build/libformatter.a
)
-mkdir build
-cd build
-cmake ..
--CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.


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
-- Configuring done (0.3s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rasul/Goydarik/workspace/projects/lab03/lab03/solver_application/build
-cmake --build .
--[ 50%] Building CXX object CMakeFiles/solver_application.dir/equation.cpp.o
[100%] Linking CXX executable solver_application
[100%] Built target solver_application
(проверка работы)
-./solver_application
- 1 
- -3
- 2
---------------------------
x1 = 1.000000
-------------------------
-------------------------
x2 = 2.000000
-------------------------
```

