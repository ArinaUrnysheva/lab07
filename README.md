
```sh

> export GITHUB_USERNAME=ArinaUrnysheva

> cd ${GITHUB_USERNAME}/workspace

> pushd .

> source scripts/activate

> git clone git@github.com:ArinaUrnysheva/lab02.git projects/lab03
Клонирование в «projects/lab03»...
remote: Enumerating objects: 25, done.
remote: Counting objects: 100% (25/25), done.
remote: Compressing objects: 100% (17/17), done.
Получение объектов: 100% (25/25), готово.
Определение изменений: 100% (3/3), готово.
remote: Total 25 (delta 3), reused 21 (delta 2), pack-reused 0

> cd projects/lab03

> git remote remove origin

> git remote add origin git@github.com:ArinaUrnysheva/lab03.git

> g++ -std=c++11 -I./include -c sources/print.cpp

> ls print.o
print.o

> nm print.o | grep print
00000000000000aa t _GLOBAL__sub_I__Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSo
0000000000000000 T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSo
000000000000002a T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E

> ar rvs print.a print.o
ar: создаётся print.a
a - print.o

> file print.a
print.a: current ar archive

> g++ -std=c++11 -I./include -c examples/example1.cpp

> ls example1.o
example1.o

>  g++ example1.o print.a -o example1

> ./example1 && echo
hello

> g++ -std=c++11 -I./include -c examples/example2.cpp

> nm example2.o
                 U __cxa_atexit
                 U __dso_handle
0000000000000000 V DW.ref.__gxx_personality_v0
                 U _GLOBAL_OFFSET_TABLE_
000000000000017e t _GLOBAL__sub_I_main
                 U __gxx_personality_v0
0000000000000000 T main
                 U __stack_chk_fail
                 U _Unwind_Resume
0000000000000128 t _Z41__static_initialization_and_destruction_0ii
                 U _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E
                 U _ZNSaIcEC1Ev
                 U _ZNSaIcED1Ev
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEEC1EPKcSt13_Ios_Openmode
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEED1Ev
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEC1EPKcRKS3_
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEED1Ev
                 U _ZNSt8ios_base4InitC1Ev
                 U _ZNSt8ios_base4InitD1Ev
0000000000000000 r _ZStL19piecewise_construct
0000000000000000 b _ZStL8__ioinit

> g++ example2.o print.a -o example2

> ./example2

> cat log.txt && echo
hello

> rm -rf example1.o example2.o print.o

> rm -rf print.a

> rm -rf example1 example2

> rm -rf log.txt

> cat > CMakeLists.txt <<EOF
cmake_minimum_required(VERSION 3.4)
project(print)
EOF

> cat >> CMakeLists.txt <<EOF
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
EOF

> cat >> CMakeLists.txt <<EOF
add_library(print STATIC \${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
EOF

> cat >> CMakeLists.txt <<EOF
include_directories(\${CMAKE_CURRENT_SOURCE_DIR}/include)
EOF

> cmake -H. -B_build
-- The C compiler identification is GNU 11.4.0
-- The CXX compiler identification is GNU 11.4.0
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
-- Configuring done
-- Generating done
-- Build files have been written to: /home/arina/ArinaUrnysheva/workspace/projects/lab03/_build

> cmake --build _build
[ 50%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[100%] Linking CXX static library libprint.a
[100%] Built target print

> cat >> CMakeLists.txt <<EOF

add_executable(example1 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example1.cpp)
add_executable(example2 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example2.cpp)
EOF

> cat >> CMakeLists.txt <<EOF

target_link_libraries(example1 print)
target_link_libraries(example2 print)
EOF

> cmake --build _build
-- Configuring done
-- Generating done
-- Build files have been written to: /home/arina/ArinaUrnysheva/workspace/projects/lab03/_build
Consolidate compiler generated dependencies of target print
[ 33%] Built target print
[ 50%] Building CXX object CMakeFiles/example1.dir/examples/example1.cpp.o
[ 66%] Linking CXX executable example1
[ 66%] Built target example1
[ 83%] Building CXX object CMakeFiles/example2.dir/examples/example2.cpp.o
[100%] Linking CXX executable example2
[100%] Built target example2

> cmake --build _build --target print
[100%] Built target print

> cmake --build _build --target example1
[ 50%] Built target print
Consolidate compiler generated dependencies of target example1
[100%] Built target example1

> cmake --build _build --target example2
[ 50%] Built target print
Consolidate compiler generated dependencies of target example2
[100%] Built target example2

> ls -la _build/libprint.a
-rw-rw-r-- 1 arina arina 3126 апр 29 23:29 _build/libprint.a

> _build/example1 && echo
hello

> _build/example2

> cat log.txt && echo
hello

> rm -rf log.txt

> git clone https://github.com/tp-labs/lab03 tmp
Клонирование в «tmp»...
remote: Enumerating objects: 91, done.
remote: Counting objects: 100% (30/30), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 91 (delta 23), reused 21 (delta 21), pack-reused 61
Получение объектов: 100% (91/91), 1.02 МиБ | 402.00 КиБ/с, готово.
Определение изменений: 100% (41/41), готово.

> mv -f tmp/CMakeLists.txt .

> rm -rf tmp

> cat CMakeLists.txt
cmake_minimum_required(VERSION 3.4)

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

> cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
-- Configuring done
-- Generating done
-- Build files have been written to: /home/arina/ArinaUrnysheva/workspace/projects/lab03/_build

> cmake --build _build --target install
Consolidate compiler generated dependencies of target print
[100%] Built target print
Install the project...
-- Install configuration: ""
-- Installing: /home/arina/ArinaUrnysheva/workspace/projects/lab03/_install/lib/libprint.a
-- Installing: /home/arina/ArinaUrnysheva/workspace/projects/lab03/_install/include
-- Installing: /home/arina/ArinaUrnysheva/workspace/projects/lab03/_install/include/print.hpp
-- Installing: /home/arina/ArinaUrnysheva/workspace/projects/lab03/_install/cmake/print-config.cmake
-- Installing: /home/arina/ArinaUrnysheva/workspace/projects/lab03/_install/cmake/print-config-noconfig.cmake

> tree _install
_install
├── cmake
│   ├── print-config.cmake
│   └── print-config-noconfig.cmake
├── include
│   └── print.hpp
└── lib
    └── libprint.a

3 directories, 4 files

> git add CMakeLists.txt

> git commit -m"added CMakeLists.txt"
[main 3867402] added CMakeLists.txt
 1 file changed, 36 insertions(+)
 create mode 100644 CMakeLists.txt


```














