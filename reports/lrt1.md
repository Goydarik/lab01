## Laboratory work I(Homework)

Данная лабораторная работа посвещена изучению утилит для разработки проектов

(Вводные данные "-"
 Выходные данные "--"
 Вводные данные в cat ">")

```
- find . -maxdepth 1 -type f | wc -l
-- 12
- find . -type f | wc -l
-- 61191

- find . -type f -name "*.h" -o -name "*.hpp" | wc -l
-- 15208
- find . -type f -name "*.cpp" | wc -l
-- 13774
- find . -type f ! -name "*.h" -a ! -name "*.hpp" -a ! -name "*.cpp" | wc -l
-- 32209

- find / -name "any.hpp" 2>/dev/null | xargs realpath
-- /home/rasul/boost_1_69_0/boost/hana/any.hpp
-- /home/rasul/boost_1_69_0/boost/hana/fwd/any.hpp
-- /home/rasul/boost_1_69_0/boost/xpressive/detail/utility/any.hpp
-- /home/rasul/boost_1_69_0/boost/fusion/algorithm/query/detail/any.hpp
-- /home/rasul/boost_1_69_0/boost/fussion/algorithm/query/any.hpp
-- /home/rasul/boost_1_69_0/boost/fusion/include/any.hpp
-- /home/rasul/boost_1_69_0/boost/spirit/home/support/algorithm/any.hpp
-- /home/rasul/boost_1_69_0/boost/proto/detail/any.hpp
-- /home/rasul/boost_1_69_0/boost/type_erasure/any.hpp

- grep -rl "boost::asio" .

- ./bootstrap.sh --prefix=/usr/local --with-libraries=all
-- Building Boost.Build engine with toolset gcc... tools/build/src/engine/bin.linuxx86_64/b2
-- Unicode/ICU support for Boost.Regex?... not found.
-- Generating Boost.Build configuration in project-config.jam...
-- 
-- Bootstraping is done. To build, run:
-- 
-- ./b2
-- 
-- To adjust configuration, edit 'project-config.jam'.
-- Further information:
-- 
-- - Command line help:
--   ./b2 --help
-- 
-- - Getting started guide:
--   http://www.boost.org/more/getting_started/unix-variants.html
-- 
-- - Boost.Build documentation:
--   http://www.boost.org/build/doc/html/index.html

-- 888
-- 
-- BOOSTITERATORCONVERTIBLE(Derived2,Derived1)
-- 
-- 889
-- 
-- usr/include/c++/14/bits/stl vector.h:1673:21:
-- required from'void std::vector<Tp,Alloc>::M range initialize(InputIterator,InputIterator,std::input iterator tag)[with InputIterator = boost::iterators::transform iterator<boost::algorithm::detail::copy_iterator_rangeF<std::cxxll::basic_string<char>,gnu cxx::normal_iterator<char*,std::cxxll::basic_string<char>>>,boost::algorithm::split_iterator<gnucxx::normal_iterator<char*>,std::cxxll::basic_string<char>>>,boost::iterators::use_default,boost::iterators::use_default>; =std::cxx11::basic_string<char>;Alloc=std::allocator<std::cxx11::basic string<char> >]'
-- 1673
-- for（；first！=last;++first）
-- usr/include/c++/14/bits/stl vector.h:711:23:
-- required from'std::vector<Tp,Alloc>::vector(InputIterator,InputIterator,const allocator_type&)[with InputIterator = boost::iterators::transform iterator<boost::algorithm::detail::copyiterator_rangeF<std::cxxll::basic_string<char>,gnucxx::normal_iterator<char*,std::cxxll::basic_string<char>>>,boost::algorithm::split_iterator<gnucxx::normal_iterator<char*>,std::cxxll::basic_string<char>>>,boost

- nano test.cpp
- g++ test.cpp -o test
- cat test.cpp
-- #include <boost/version.hpp>
-- #include <iostream>
-- 
-- int main() {
--     std::cout << "Boost version: " << BOOST_VERSION << std::endl;
--     std::cout << "Boost lib version: " << BOOST_LIB_VERSION << std::endl;
--     return 0;
-- }

- ./test
-- Boost version: 106900
-- Boost lib version: 1_69

- mkdir -p ~/boost-libs
- cd boost_1_69_0
- sudo mv /usr/local/lib/libboost_*.a ~/boost-libs
-- [sudo] наполь для raspul:
- cd boost-libs
-- bash: cd: boost-libs: Нет такого файла или каталога
- cd
- ls
-- libboost_atomic.a    libboost_random.a
-- libboost_chrono.a    libboost_regex.a
-- libboost_container.a  libboost_serialization.a
-- libboost_context.a   libboost_stacktrace_addr2line.a
-- libboost_contract.a   libboost_stacktrace_backtrace.a
-- libboost_date_time.a libboost_stacktrace_basic.a
-- libboost_exception.a libboost_stacktrace_noop.a
-- libboost_fiber.a    libboost_system.a
-- libboost_filesystem.a libboost_test_exec_monitor.a
-- libboost_graph.a    libboost_timer.a
-- libboost_istreams.a  libboost_unit_test_framework.a
-- libboost_locate.a   libboost_wave.a
-- libboost_prg_exec_monitor.a libboost_wserialization.a
-- libboost_program_options.a

- find ~/boost-libs -type f -exec ls -lh {} \; | awk
'{print $5 "|" $9}'
-- 319K    /home/rasul/boost-libs/libboost_contract.a
-- 206K    /home/rasul/boost-libs/libboost_prg_exec_monitor.a
-- 229K    /home/rasul/boost-libs/libboost_chrono.a
-- 2,4K    /home/rasul/boost-libs/libboost_atomic.a
-- 19K    /home/rasul/boost-libs/libboost_stacktrace_backtrace.a
-- 824K    /home/rasul/boost-libs/libboost_graph.a
-- 773K    /home/rasul/boost-libs/libboost_wserialization.a
-- 2,2M    /home/rasul/boost-libs/libboost_unit_test_framework.a
-- 400K    /home/rasul/boost-libs/libboost_filesystem.a
-- 229K    /home/rasul/boost-libs/libboost_fiber.a
-- 2,7M    /home/rasul/boost-libs/libboost_regex.a
-- 4,5M    /home/rasul/boost-libs/libboost_wave.a
-- 2,0M    /home/rasul/boost-libs/libboost_locale.a
-- 20K    /home/rasul/boost-libs/libboost_context.a
-- 35K    /home/rasul/boost-libs/libboost_stacktrace_addr2line.a
-- 1,3K    /home/rasul/boost-libs/libboost_system.a

- find ~/boost-libs -type f -exec ls -lh {} \; | awk '{print $5 "|" $9}' | sort -hr | head -10
-- 4,5M    /home/rasul/boost-libs/libboost_wave.a
-- 2,7M    /home/rasul/boost-libs/libboost_regex.a
-- 2,2M    /home/rasul/boost-libs/libboost_unit_test_framework.a
-- 2,2M    /home/rasul/boost-libs/libboost_test_exec_monitor.a
-- 2,0M    /home/rasul/boost-libs/libboost_locate.a
-- 1,5M    /home/rasul/boost-libs/libboost_program_options.a
-- 1,2M    /home/rasul/boost-libs/libboost_serialization.a
-- 824K    /home/rasul/boost-libs/libboost_graph.a
-- 773K    /home/rasul/boost-libs/libboost_wserialization.a
-- 400K    /home/rasul/boost-libs/libboost_filesystem.a
```
