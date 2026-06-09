## Лабораторная работа 09
## Тема:
Изучение процесса создания артефактов на примере GitHub Release
## Ход выполнения:
(строки со входными данными начинаются с $)
```
$ sudo apt install xclip
Installing:                     
  xclip

Summary:
  Upgrading: 0, Installing: 1, Removing: 0, Not Upgrading: 238
  Download size: 21.3 kB
  Space needed: 63.5 kB / 7,340 MB available

Get:1 http://deb.debian.org/debian trixie/main amd64 xclip amd64 0.13-4 [21.3 kB]
Fetched 21.3 kB in 0s (119 kB/s)  
Selecting previously unselected package xclip.
(Reading database ... 128341 files and directories currently installed.)
Preparing to unpack .../xclip_0.13-4_amd64.deb ...
Unpacking xclip (0.13-4) ...
Setting up xclip (0.13-4) ...
Processing triggers for man-db (2.13.1-1) ...
```
```
$ alias gsed=sed
$ alias pbcopy='xclip -selection clipboard'
$ alias pbpaste='xclip -selection clipboard -o'
```
```
$ git clone https://github.com/Goydarik/lab08 projects/lab09
Cloning into 'projects/lab09'...
remote: Enumerating objects: 209, done.
remote: Counting objects: 100% (209/209), done.
remote: Compressing objects: 100% (96/96), done.
remote: Total 209 (delta 77), reused 209 (delta 77), pack-reused 0 (from 0)
Receiving objects: 100% (209/209), 46.18 KiB | 788.00 KiB/s, done.
Resolving deltas: 100% (77/77), done.
```
```
$ cd projects/lab09
$ git remote remove origin
$ git remote add origin https://Goydarik/lab09
$ gsed -i 's/lab08/lab09/g' README.md
```
```
$ sudo apt install gpg
gpg is already the newest version (2.4.7-21+deb13u1+b3).
gpg set to manually installed.
Summary:
  Upgrading: 0, Installing: 0, Removing: 0, Not Upgrading: 238
```
```
$ gpg --full-generate-key
gpg (GnuPG) 2.4.7; Copyright (C) 2024 g10 Code GmbH
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

gpg: keybox '/home/rasul/.gnupg/pubring.kbx' created
Please select what kind of key you want:
   (1) RSA and RSA
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (9) ECC (sign and encrypt) *default*
  (10) ECC (sign only)
  (14) Existing key from card
Your selection? 1
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 4096
Requested keysize is 4096 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 0
Key does not expire at all
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: Goydarik
Email address: rosgorzion@gmail.com
Comment: comment
You selected this USER-ID:
    "Goydarik (comment) <rosgorzion@gmail.com>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: /home/rasul/.gnupg/trustdb.gpg: trustdb created
gpg: directory '/home/rasul/.gnupg/openpgp-revocs.d' created
gpg: revocation certificate stored as '/home/rasul/.gnupg/openpgp-revocs.d/8D2001A8DF6BA49474CB88C9507D84D8FDBBC988.rev'
public and secret key created and signed.

pub   rsa4096 2026-05-31 [SC]
      8D2001A8DF6BA49474CB88C9507D84D8FDBBC988
uid                      Goydarik (comment) <rosgorzion@gmail.com>
sub   rsa4096 2026-05-31 [E]
```
```
$ gpg --list-secret-keys --keyid-format LONG
gpg: checking the trustdb
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
/home/rasul/.gnupg/pubring.kbx
-----------------------------
sec   rsa4096/0E8FD092C884A6FD 2026-06-09 [SC]
      84163A9A69AC0B8A16CA384C0E8FD092C884A6FD
uid               [  ultimate ] Goydarik (comment) <rosgorzion@gmail.com>
ssb   rsa4096/56D0EDA3BB845803 2026-06-09 [E]
```
```
$ gpg -K Goydarik
sec   rsa4096 2026-06-09 [SC]
      84163A9A69AC0B8A16CA384C0E8FD092C884A6FD
uid         [  ultimate ] Goydarik (comment) <rosgorzion@gmail.com>
ssb   rsa4096 2026-06-09 [E]
```
```

$ GPG_KEY_ID=$(gpg --list-secret-keys --keyid-format LONG | grep sec | tail -1 | awk '{print $2}' | cut -d'/' -f2)
$ GPG_SEC_KEY_ID=$(gpg --list-secret-keys --keyid-format LONG | grep ssb | tail -1 | awk '{print $2}' | cut -d'/' -f2)
```
```
$ gpg --armor --export ${GPG_KEY_ID} | pbcopy
$ pbpaste
-----BEGIN PGP PUBLIC KEY BLOCK-----

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
dgebHvY=
=lhRq
-----END PGP PUBLIC KEY BLOCK-----

```
```
$ open https://github.com/settings/keys
```
в настройках github добавляем gpg ключ
```
$ git config user.signingkey ${GPG_SEC_KEY_ID}
$ git config gpg.program gpg
$ test -r ~/.bash_profile && echo 'export GPG_TTY=$(tty)' >> ~/.bash_profile
$ echo 'export GPG_TTY=$(tty)' >> ~/.profile
```
```
$ cmake -H. -B_build -DCPACK_GENERATOR="TGZ"
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
-- Configuring done (2.7s)
-- Generating done (0.0s)
-- Build files have been written to: /home/rasul/Goydarik/workspace/projects/lab09/_build
```
```
$ cmake --build _build --target package
[  5%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 11%] Linking CXX static library libprint.a
[ 11%] Built target print
[ 17%] Building CXX object _deps/googletest-build/googletest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
[ 23%] Linking CXX static library ../../../lib/libgtest.a
[ 23%] Built target gtest
[ 29%] Building CXX object _deps/googletest-build/googletest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
[ 35%] Linking CXX static library ../../../lib/libgtest_main.a
[ 35%] Built target gtest_main
[ 41%] Building CXX object CMakeFiles/check.dir/tests/test1.cpp.o
[ 47%] Building CXX object CMakeFiles/check.dir/tests/test_print.cpp.o
[ 52%] Linking CXX executable check
[ 52%] Built target check
[ 58%] Building CXX object CMakeFiles/demo.dir/demo/main.cpp.o
[ 64%] Linking CXX executable demo
[ 64%] Built target demo
[ 70%] Building CXX object _deps/googletest-build/googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
[ 76%] Linking CXX static library ../../../lib/libgmock.a
[ 76%] Built target gmock
[ 82%] Building CXX object _deps/googletest-build/googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
[ 88%] Linking CXX static library ../../../lib/libgmock_main.a
[ 88%] Built target gmock_main
[ 94%] Building CXX object tests/CMakeFiles/tests.dir/test_print.cpp.o
[100%] Linking CXX executable tests
[100%] Built target tests
Run CPack packaging tool...
CPack: Create package using TGZ
CPack: Install projects
CPack: - Run preinstall target for: print
CPack: - Install project: print []
CPack: Create package
CPack: - package: /home/rasul/projects/lab09/_build/print--Linux.tar.gz generated.
```
```

$ git tag -s v0.1.0.0 -m"Initial release v0.1.0.0"

$ git tag -v v0.1.0.0
object 4b0feaeb8a77eea7dd805fd7a6bf205f6788991b
type commit
tag v0.1.0.0
tagger Goydarik <rosgorzion@gmail.com> 1780256036 -0400

Initial release v0.1.0.0
gpg: Signature made Tue 09 June 16:14:35 MSK
gpg:                using RSA key 84163A9A69AC0B8A16CA384C0E8FD092C884A6FD
gpg: Good signature from "Goydarik (comment) <rosgorzion@gmail.com>" [ultimate]
```
```
$ git show v0.1.0.0
tag v0.1.0.0
Tagger: Goydarik <rosgorzion@gmail.com>
Date:   Tue June 09 15:33:56 2026 -0400

tag v0.1.0.0
Tagger: Goydarik <rosgorzion@gmail.com>
Date:   Tue Jun 9 16:14:35 2026 +0300

Initial release v0.1.0.0
-----BEGIN PGP SIGNATURE-----

iQIzBAABCgAdFiEEhBY6mmmsC4oWyjhMDo/QksiEpv0FAmooEbsACgkQDo/QksiE
pv3xtA//Ssm/ki4/PryqhwQg5gko6TfkUgLnhgMURt/PJ1L9sO27o5MjcHNpf0LZ
/1cj5biny4nCZkn1gPVU7RnrWHEAPeoW3rsvV4rWOmD0nB/47me1z/LFqUIrY79K
BZomFGpK8OHY4vv5EhpwuyHm/uO2BBcfd1V4g6qKbZ0jwt2bQMLdMay1i/iVYW9P
wvitjAQr+7ThJdL0re2nOaNqm4k0mxWPnsJtaHpySck2dl7Xe6ToKY9VB95TtpUu
Ys++F2R19EvoFEr52PMEhTbwL/r20wWDeIaIKeAjJjr0C6JInDxV8meUexIhWB5u
lgoVxZ0c+x7XcvTzBShlDfSbDQCiB8PQmjr+cwMHcomUCtuolnmkBjWznyrO141O
QRm678DnmOkiuAwTnoWj71YZwM+r93GbXdaHV2v6n+574Zwe2mt3xyNTmy5JXxsM
6y9Hzowsdg3YjyYmyh0mtavoq1NmAKVgT/Z5PRqQ0HpODIbjbsxuVgd4UG8N4gN8
hEbQaClmAaqbva8JGQFbMbgDYFh73q5jSqZ6VuTqA6+RjGHf7ZEes699OAMVV3jV
yxgiHNIBbnSpv1y3Uj18OxetsMdQUMda8Y1gye4CX6RJEavcZ+b6+V9/BzQ42djn
O3jubACacKNuaL0f6AQL4PJuGj5M1QwHMBVpsoSS37m9HmBx1XQ=
=MEac
-----END PGP SIGNATURE-----

```
```
$ git push origin main --tags
Enumerating objects: 210, done.
Counting objects: 100% (210/210), done.
Delta compression using up to 2 threads
Compressing objects: 100% (97/97), done.
Writing objects: 100% (210/210), 46.94 KiB | 23.47 MiB/s, done.
Total 210 (delta 77), reused 209 (delta 77), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (77/77), done.
To https://github.com/Goydarik/lab09
 * [new branch]      main -> main
 * [new tag]         v0.1.0.0 -> v0.1.0.0
```
```
$ gh release create v0.1.0.0 --title "libprint" --notes "my first release" _build/*.tar.gz
https://github.com/Goydarik/lab09/releases/tag/v0.1.0.0
```
```
$ gh release list
TITLE     TYPE    TAG NAME  PUBLISHED          
libprint  Latest  v0.1.0.0  about 8 minutes ago
```
```
$ gh release view v0.1.0.0
v0.1.0.0
Goydarik released this less than a minute ago

  my first release                                                                                           


Assets
print--Linux.tar.gz  724.85 KiB

View on GitHub: https://github.com/Goydarik/lab09/releases/tag/v0.1.0.0

```
```
$ gh release download v0.1.0.0 --pattern "*.tar.gz"
$ tar -zxf print--Linux.tar.gz
```
```
$ tar -tzf print--Linux.tar.gz
print--Linux/cmake/
print--Linux/cmake/print-config.cmake
print--Linux/cmake/print-config-noconfig.cmake
print--Linux/include/
print--Linux/include/gmock/
print--Linux/include/gmock/gmock-more-matchers.h
print--Linux/include/gmock/gmock-cardinalities.h
print--Linux/include/gmock/gmock-more-actions.h
print--Linux/include/gmock/gmock-matchers.h
print--Linux/include/gmock/gmock-function-mocker.h
print--Linux/include/gmock/gmock-actions.h
print--Linux/include/gmock/internal/
print--Linux/include/gmock/internal/custom/
print--Linux/include/gmock/internal/custom/gmock-matchers.h
print--Linux/include/gmock/internal/custom/gmock-port.h
print--Linux/include/gmock/internal/custom/README.md
print--Linux/include/gmock/internal/custom/gmock-generated-actions.h
print--Linux/include/gmock/internal/gmock-internal-utils.h
print--Linux/include/gmock/internal/gmock-port.h
print--Linux/include/gmock/internal/gmock-pp.h
print--Linux/include/gmock/gmock-nice-strict.h
print--Linux/include/gmock/gmock-spec-builders.h
print--Linux/include/gmock/gmock.h
print--Linux/include/gtest/
print--Linux/include/gtest/gtest-typed-test.h
print--Linux/include/gtest/gtest-param-test.h
print--Linux/include/gtest/gtest-message.h
print--Linux/include/gtest/gtest_prod.h
print--Linux/include/gtest/gtest-matchers.h
print--Linux/include/gtest/gtest-assertion-result.h
print--Linux/include/gtest/gtest-test-part.h
print--Linux/include/gtest/internal/
print--Linux/include/gtest/internal/gtest-filepath.h
print--Linux/include/gtest/internal/gtest-internal.h
print--Linux/include/gtest/internal/custom/
print--Linux/include/gtest/internal/custom/gtest.h
print--Linux/include/gtest/internal/custom/gtest-printers.h
print--Linux/include/gtest/internal/custom/README.md
print--Linux/include/gtest/internal/custom/gtest-port.h
print--Linux/include/gtest/internal/gtest-port-arch.h
print--Linux/include/gtest/internal/gtest-param-util.h
print--Linux/include/gtest/internal/gtest-death-test-internal.h
print--Linux/include/gtest/internal/gtest-string.h
print--Linux/include/gtest/internal/gtest-port.h
print--Linux/include/gtest/internal/gtest-type-util.h
print--Linux/include/gtest/gtest.h
print--Linux/include/gtest/gtest-printers.h
print--Linux/include/gtest/gtest-spi.h
print--Linux/include/gtest/gtest_pred_impl.h
print--Linux/include/gtest/gtest-death-test.h
print--Linux/include/print.hpp
print--Linux/bin/
print--Linux/bin/demo
print--Linux/lib/
print--Linux/lib/libprint.a
print--Linux/lib/libgtest_main.a
print--Linux/lib/pkgconfig/
print--Linux/lib/pkgconfig/gtest_main.pc
print--Linux/lib/pkgconfig/gmock_main.pc
print--Linux/lib/pkgconfig/gtest.pc
print--Linux/lib/pkgconfig/gmock.pc
print--Linux/lib/cmake/
print--Linux/lib/cmake/GTest/
print--Linux/lib/cmake/GTest/GTestConfigVersion.cmake
print--Linux/lib/cmake/GTest/GTestConfig.cmake
print--Linux/lib/cmake/GTest/GTestTargets-noconfig.cmake
print--Linux/lib/cmake/GTest/GTestTargets.cmake
print--Linux/lib/libgmock_main.a
print--Linux/lib/libgtest.a
print--Linux/lib/libgmock.a
```