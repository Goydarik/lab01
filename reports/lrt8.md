# Лабораторная работа 08

## Тема
Изучение систем автоматизации развертывания и управления приложениями на примере Docker.

## Ход выполнения
(строки со входными данными начинаются с $)

```bash
$ cd Goydarik/workspace
$ pushd .
$ source scripts/activate
$ git clone https://github.com/Goydarik/lab07 lab08
$ cd lab08
$ git submodule update --init
$ git remote remove origin
$ git remote add origin https://github.com/Goydarik/lab08
$ nano Dockerfile
```

в Dockerfile пишем:
```bash
FROM ubuntu:22.04
RUN apt update
RUN apt install -yy gcc g++ cmake
COPY . print/
WORKDIR print

RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
RUN cmake --build _build
RUN cmake --build _build --target install
ENV LOG_PATH /home/logs/log.txt
VOLUME /home/logs
WORKDIR _install/bin
ENTRYPOINT ./demo
```
```bash
$ sudo apt update
Hit:1 http://deb.debian.org/debian trixie InRelease
Get:2 http://security.debian.org/debian-security trixie-security InRelease [43.4 kB]
Get:3 http://deb.debian.org/debian trixie-updates InRelease [47.3 kB]
Get:4 http://security.debian.org/debian-security trixie-security/main Sources [167 kB]
Get:5 http://security.debian.org/debian-security trixie-security/main amd64 Packages [175 kB]
Fetched 433 kB in 0s (887 kB/s)
251 packages can be upgraded. Run 'apt list --upgradable' to see them.

$ sudo apt install -y ca-certificates curl gnupg lsb-release
ca-certificates is already the newest version (20250419).
lsb-release is already the newest version (12.1-1).
lsb-release set to manually installed.
Upgrading:
  curl     gnupg-l10n   gpg-agent       gpgsm               libcurl4t64
  dirmngr  gnupg-utils  gpg-wks-client  gpgv
  gnupg    gpg          gpgconf         libcurl3t64-gnutls

Summary:
  Upgrading: 13, Installing: 0, Removing: 0, Not Upgrading: 238
  Download size: 4,450 kB
  Space needed: 3,072 B / 10.0 GB available

Get:1 http://deb.debian.org/debian trixie/main amd64 curl amd64 8.14.1-2+deb13u3 [270 kB]
Get:2 http://deb.debian.org/debian trixie/main amd64 libcurl4t64 amd64 8.14.1-2+deb13u3 [391 kB]
Get:3 http://deb.debian.org/debian trixie/main amd64 gpgsm amd64 2.4.7-21+deb13u1+b3 [276 kB]
Get:4 http://deb.debian.org/debian trixie/main amd64 gnupg-utils amd64 2.4.7-21+deb13u1+b3 [195 kB]
Get:5 http://deb.debian.org/debian trixie/main amd64 gpg-wks-client amd64 2.4.7-21+deb13u1+b3 [109 kB]
Get:6 http://deb.debian.org/debian trixie/main amd64 gpg amd64 2.4.7-21+deb13u1+b3 [635 kB]
Get:7 http://deb.debian.org/debian trixie/main amd64 dirmngr amd64 2.4.7-21+deb13u1+b3 [384 kB]
Get:8 http://deb.debian.org/debian trixie/main amd64 gnupg all 2.4.7-21+deb13u1 [417 kB]
Get:9 http://deb.debian.org/debian trixie/main amd64 gpgconf amd64 2.4.7-21+deb13u1+b3 [129 kB]
Get:10 http://deb.debian.org/debian trixie/main amd64 gpg-agent amd64 2.4.7-21+deb13u1+b3 [271 kB]
Get:11 http://deb.debian.org/debian trixie/main amd64 gnupg-l10n all 2.4.7-21+deb13u1 [749 kB]
Get:12 http://deb.debian.org/debian trixie/main amd64 gpgv amd64 2.4.7-21+deb13u1+b3 [241 kB]
Get:13 http://deb.debian.org/debian trixie/main amd64 libcurl3t64-gnutls amd64 8.14.1-2+deb13u3 [384 kB]
Fetched 4,450 kB in 1s (3,052 kB/s)          
apt-listchanges: Reading changelogs...
(Reading database ... 127887 files and directories currently installed.)
Preparing to unpack .../00-curl_8.14.1-2+deb13u3_amd64.deb ...
Unpacking curl (8.14.1-2+deb13u3) over (8.14.1-2+deb13u2) ...
Preparing to unpack .../01-libcurl4t64_8.14.1-2+deb13u3_amd64.deb ...
Unpacking libcurl4t64:amd64 (8.14.1-2+deb13u3) over (8.14.1-2+deb13u2) ...
Preparing to unpack .../02-gpgsm_2.4.7-21+deb13u1+b3_amd64.deb ...
Unpacking gpgsm (2.4.7-21+deb13u1+b3) over (2.4.7-21+b3) ...
Preparing to unpack .../03-gnupg-utils_2.4.7-21+deb13u1+b3_amd64.deb ...
Unpacking gnupg-utils (2.4.7-21+deb13u1+b3) over (2.4.7-21+b3) ...
Preparing to unpack .../04-gpg-wks-client_2.4.7-21+deb13u1+b3_amd64.deb ...
Unpacking gpg-wks-client (2.4.7-21+deb13u1+b3) over (2.4.7-21+b3) ...
Preparing to unpack .../05-gpg_2.4.7-21+deb13u1+b3_amd64.deb ...
Unpacking gpg (2.4.7-21+deb13u1+b3) over (2.4.7-21+b3) ...
Preparing to unpack .../06-dirmngr_2.4.7-21+deb13u1+b3_amd64.deb ...
Unpacking dirmngr (2.4.7-21+deb13u1+b3) over (2.4.7-21+b3) ...
Preparing to unpack .../07-gnupg_2.4.7-21+deb13u1_all.deb ...
Unpacking gnupg (2.4.7-21+deb13u1) over (2.4.7-21) ...
Preparing to unpack .../08-gpgconf_2.4.7-21+deb13u1+b3_amd64.deb ...
Unpacking gpgconf (2.4.7-21+deb13u1+b3) over (2.4.7-21+b3) ...
Preparing to unpack .../09-gpg-agent_2.4.7-21+deb13u1+b3_amd64.deb ...
Unpacking gpg-agent (2.4.7-21+deb13u1+b3) over (2.4.7-21+b3) ...
Preparing to unpack .../10-gnupg-l10n_2.4.7-21+deb13u1_all.deb ...
Unpacking gnupg-l10n (2.4.7-21+deb13u1) over (2.4.7-21) ...
Preparing to unpack .../11-gpgv_2.4.7-21+deb13u1+b3_amd64.deb ...
Unpacking gpgv (2.4.7-21+deb13u1+b3) over (2.4.7-21+b3) ...
Preparing to unpack .../12-libcurl3t64-gnutls_8.14.1-2+deb13u3_amd64.deb ...
Unpacking libcurl3t64-gnutls:amd64 (8.14.1-2+deb13u3) over (8.14.1-2+deb13u2) ...
Setting up libcurl4t64:amd64 (8.14.1-2+deb13u3) ...
Setting up libcurl3t64-gnutls:amd64 (8.14.1-2+deb13u3) ...
Setting up gnupg-l10n (2.4.7-21+deb13u1) ...
Setting up gpgv (2.4.7-21+deb13u1+b3) ...
Setting up gpgconf (2.4.7-21+deb13u1+b3) ...
Setting up curl (8.14.1-2+deb13u3) ...
Setting up gpg (2.4.7-21+deb13u1+b3) ...
Setting up gnupg-utils (2.4.7-21+deb13u1+b3) ...
Setting up gpg-agent (2.4.7-21+deb13u1+b3) ...
Setting up gpgsm (2.4.7-21+deb13u1+b3) ...
Setting up dirmngr (2.4.7-21+deb13u1+b3) ...
Setting up gnupg (2.4.7-21+deb13u1) ...
Setting up gpg-wks-client (2.4.7-21+deb13u1+b3) ...
Processing triggers for man-db (2.13.1-1) ...
Processing triggers for libc-bin (2.41-12+deb13u2) ...

$ sudo mkdir -p /etc/apt/keyrings
$ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
$ sudo apt update
Hit:1 http://security.debian.org/debian-security trixie-security InRelease
Hit:2 http://deb.debian.org/debian trixie InRelease         
Hit:3 http://deb.debian.org/debian trixie-updates InRelease 
Get:4 https://download.docker.com/linux/debian trixie InRelease [32.5 kB]
Get:5 https://download.docker.com/linux/debian trixie/stable amd64 Packages [37.0 kB]
Fetched 69.4 kB in 0s (161 kB/s)
238 packages can be upgraded. Run 'apt list --upgradable' to see them.

$ sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
Installing:                     
  containerd.io         docker-ce      docker-compose-plugin
  docker-buildx-plugin  docker-ce-cli

Installing dependencies:
  docker-ce-rootless-extras  iptables  libip4tc2  libip6tc2  pigz

Suggested packages:
  cgroupfs-mount  | cgroup-lite  docker-model-plugin  firewalld

Summary:
  Upgrading: 0, Installing: 10, Removing: 0, Not Upgrading: 238
  Download size: 99.5 MB
  Space needed: 381 MB / 10.0 GB available

Get:1 http://deb.debian.org/debian trixie/main amd64 libip4tc2 amd64 1.8.11-2 [20.0 kB]
Get:2 http://deb.debian.org/debian trixie/main amd64 libip6tc2 amd64 1.8.11-2 [20.3 kB]
Get:3 https://download.docker.com/linux/debian trixie/stable amd64 containerd.io amd64 2.2.4-1~debian.13~trixie [23.6 MB]
Get:4 http://deb.debian.org/debian trixie/main amd64 iptables amd64 1.8.11-2 [361 kB]
Get:5 http://deb.debian.org/debian trixie/main amd64 pigz amd64 2.8-1 [62.7 kB]
Get:6 https://download.docker.com/linux/debian trixie/stable amd64 docker-ce-cli amd64 5:29.5.2-1~debian.13~trixie [17.0 MB]
Get:7 https://download.docker.com/linux/debian trixie/stable amd64 docker-ce amd64 5:29.5.2-1~debian.13~trixie [22.9 MB]
Get:8 https://download.docker.com/linux/debian trixie/stable amd64 docker-buildx-plugin amd64 0.34.1-1~debian.13~trixie [17.2 MB]
Get:9 https://download.docker.com/linux/debian trixie/stable amd64 docker-ce-rootless-extras amd64 5:29.5.2-1~debian.13~trixie [10.2 MB]
Get:10 https://download.docker.com/linux/debian trixie/stable amd64 docker-compose-plugin amd64 5.1.4-1~debian.13~trixie [8,127 kB]
Fetched 99.5 MB in 16s (6,040 kB/s)                                            
Selecting previously unselected package containerd.io.
(Reading database ... 127887 files and directories currently installed.)
Preparing to unpack .../0-containerd.io_2.2.4-1~debian.13~trixie_amd64.deb ...
Unpacking containerd.io (2.2.4-1~debian.13~trixie) ...
Selecting previously unselected package docker-ce-cli.
Preparing to unpack .../1-docker-ce-cli_5%3a29.5.2-1~debian.13~trixie_amd64.deb ...
Unpacking docker-ce-cli (5:29.5.2-1~debian.13~trixie) ...
Selecting previously unselected package libip4tc2:amd64.
Preparing to unpack .../2-libip4tc2_1.8.11-2_amd64.deb ...
Unpacking libip4tc2:amd64 (1.8.11-2) ...
Selecting previously unselected package libip6tc2:amd64.
Preparing to unpack .../3-libip6tc2_1.8.11-2_amd64.deb ...
Unpacking libip6tc2:amd64 (1.8.11-2) ...
Selecting previously unselected package iptables.
Preparing to unpack .../4-iptables_1.8.11-2_amd64.deb ...
Unpacking iptables (1.8.11-2) ...
Selecting previously unselected package docker-ce.
Preparing to unpack .../5-docker-ce_5%3a29.5.2-1~debian.13~trixie_amd64.deb ...
Unpacking docker-ce (5:29.5.2-1~debian.13~trixie) ...
Selecting previously unselected package pigz.
Preparing to unpack .../6-pigz_2.8-1_amd64.deb ...
Unpacking pigz (2.8-1) ...
Selecting previously unselected package docker-buildx-plugin.
Preparing to unpack .../7-docker-buildx-plugin_0.34.1-1~debian.13~trixie_amd64.deb ...
Unpacking docker-buildx-plugin (0.34.1-1~debian.13~trixie) ...
Selecting previously unselected package docker-ce-rootless-extras.
Preparing to unpack .../8-docker-ce-rootless-extras_5%3a29.5.2-1~debian.13~trixie_amd64.deb ...
Unpacking docker-ce-rootless-extras (5:29.5.2-1~debian.13~trixie) ...
Selecting previously unselected package docker-compose-plugin.
Preparing to unpack .../9-docker-compose-plugin_5.1.4-1~debian.13~trixie_amd64.deb ...
Unpacking docker-compose-plugin (5.1.4-1~debian.13~trixie) ...
Setting up libip4tc2:amd64 (1.8.11-2) ...
Setting up libip6tc2:amd64 (1.8.11-2) ...
Setting up docker-buildx-plugin (0.34.1-1~debian.13~trixie) ...
Setting up containerd.io (2.2.4-1~debian.13~trixie) ...
Created symlink '/etc/systemd/system/multi-user.target.wants/containerd.service' → '/usr/lib/systemd/system/containerd.service'.
Setting up docker-compose-plugin (5.1.4-1~debian.13~trixie) ...
Setting up docker-ce-cli (5:29.5.2-1~debian.13~trixie) ...
Setting up pigz (2.8-1) ...
Setting up docker-ce-rootless-extras (5:29.5.2-1~debian.13~trixie) ...
Setting up iptables (1.8.11-2) ...
update-alternatives: using /usr/sbin/iptables-legacy to provide /usr/sbin/iptables (iptables) in auto mode
update-alternatives: using /usr/sbin/ip6tables-legacy to provide /usr/sbin/ip6tables (ip6tables) in auto mode
update-alternatives: using /usr/sbin/iptables-nft to provide /usr/sbin/iptables (iptables) in auto mode
update-alternatives: using /usr/sbin/ip6tables-nft to provide /usr/sbin/ip6tables (ip6tables) in auto mode
update-alternatives: using /usr/sbin/arptables-nft to provide /usr/sbin/arptables (arptables) in auto mode
update-alternatives: using /usr/sbin/ebtables-nft to provide /usr/sbin/ebtables (ebtables) in auto mode
Setting up docker-ce (5:29.5.2-1~debian.13~trixie) ...
Created symlink '/etc/systemd/system/multi-user.target.wants/docker.service' → '/usr/lib/systemd/system/docker.service'.
Created symlink '/etc/systemd/system/sockets.target.wants/docker.socket' → '/usr/lib/systemd/system/docker.socket'.
Processing triggers for man-db (2.13.1-1) ...
Processing triggers for libc-bin (2.41-12+deb13u2) ...

$ sudo usermod -aG docker $USER
$ docker build -t logger .
[+] Building 79.3s (14/14) FINISHED                              docker:default
 => [internal] load build definition from Dockerfile                       0.0s
 => => transferring dockerfile: 373B                                       0.0s
 => [internal] load metadata for docker.io/library/ubuntu:22.04            0.6s
 => [internal] load .dockerignore                                          0.0s
 => => transferring context: 2B                                            0.0s
 => [1/9] FROM docker.io/library/ubuntu:22.04@sha256:4f838adc7181d9039ac7  0.1s
 => => resolve docker.io/library/ubuntu:22.04@sha256:4f838adc7181d9039ac7  0.1s
 => [internal] load build context                                          0.0s
 => => transferring context: 5.90kB                                        0.0s
 => CACHED [2/9] RUN apt update                                            0.0s
 => [3/9] RUN apt install -yy gcc g++ cmake                               35.1s
 => [4/9] COPY . print/                                                    0.2s 
 => [5/9] WORKDIR print                                                    0.1s 
 => [6/9] RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install  8.2s 
 => [7/9] RUN cmake --build _build                                        15.6s 
 => [8/9] RUN cmake --build _build --target install                        1.6s 
 => [9/9] WORKDIR _install/bin                                             0.2s 
 => exporting to image                                                    17.2s 
 => => exporting layers                                                   12.1s 
 => => exporting manifest sha256:14560215ba683660dd2fa1f8c6ded93c001f3ef4  0.0s 
 => => exporting config sha256:0f04ce80bc28c07f5c46e28768f4154bfb424f2446  0.0s 
 => => exporting attestation manifest sha256:bdc0f057e33561cef76202a03f8b  0.1s 
 => => exporting manifest list sha256:d2d54ab534a8360bb251d2fcb005760b3f3  0.0s
 => => naming to docker.io/library/logger:latest                           0.0s
 => => unpacking to docker.io/library/logger:latest                        4.8s

 3 warnings found (use docker --debug to expand):
 - WorkdirRelativePath: Relative workdir "print" can have unexpected results if the base image changes (line 5)
 - LegacyKeyValueFormat: "ENV key=value" should be used instead of legacy "ENV key value" format (line 10)
 - JSONArgsRecommended: JSON arguments recommended for ENTRYPOINT to prevent unintended behavior related to OS signals (line 13)

$ docker images
IMAGE                ID             DISK USAGE   CONTENT SIZE   EXTRA
hello-world:latest   0e760fdfbc48       25.9kB         9.49kB        
logger:latest        d2d54ab534a8        690MB          200MB        

$ mkdir logs
$ docker run -it -v "$(pwd)/logs:/home/logs" logger
text1
text2
text3
<C-D>

$ docker inspect logger
[
    {
        "Id": "sha256:d2d54ab534a8360bb251d2fcb005760b3f313c1f2933828291f8a3c8ca169868",
        "RepoTags": [
            "logger:latest"
        ],
        "RepoDigests": [
            "logger@sha256:d2d54ab534a8360bb251d2fcb005760b3f313c1f2933828291f8a3c8ca169868"
        ],
        "Comment": "buildkit.dockerfile.v0",
        "Created": "2026-05-31T05:53:18.92022536-04:00",
        "Config": {
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "LOG_PATH=/home/logs/log.txt"
            ],
            "Entrypoint": [
                "/bin/sh",
                "-c",
                "./demo"
            ],
            "Volumes": {
                "/home/logs": {}
            },
            "WorkingDir": "/print/_install/bin",
            "Labels": {
                "org.opencontainers.image.version": "22.04"
            }
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 200316271,
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:8bba68e7621928237aa6d6e2c680cb9572c942ee23c2adabd22016bb67cb938d",
                "sha256:5d96cd15f7bbfe79e7b77a7634605808fd11b4ea9c7c81e592f1789f20117eb2",
                "sha256:fe973104bc26c35e2aa6eccdb9b67e45c73d6908787d6a0bd97140e30bb9bcc0",
                "sha256:14af9da199c1303619a421ebf1442d1e4ec814ac37e490699149a1422b29cc76",
                "sha256:5f70bf18a086007016e948b04aed3b82103a36bea41755b6cddfaf10ace3c6ef",
                "sha256:2dafb04d1adac7244071ab54b2f270ae09d227c98ac93628483acab1095af0cd",
                "sha256:33e36afa3948a4f26dbc383f44c30dd514f54cefef5080dfdb1190dd0b6d3394",
                "sha256:6a5d1c8c2ea059b4200697757e875e3e0ffaa2b600f5a872f136be87e2109cd6",
                "sha256:5f70bf18a086007016e948b04aed3b82103a36bea41755b6cddfaf10ace3c6ef"
            ]
        },
        "Metadata": {
            "LastTagTime": "2026-05-31T09:53:31.307699149Z"
        },
        "Descriptor": {
            "mediaType": "application/vnd.oci.image.index.v1+json",
            "digest": "sha256:d2d54ab534a8360bb251d2fcb005760b3f313c1f2933828291f8a3c8ca169868",
            "size": 856
        },
        "Identity": {
            "Build": [
                {
                    "Ref": "7xkeq4o1a8yvs0j9en7h2j949",
                    "CreatedAt": "2026-05-31T05:53:36.122874726-04:00"
                }
            ]
        }
    }
]

$ cat logs/log.txt
text1
text2
text3

$ nano .github/workflows/docker.yml
```

в docker.yml пишем:
```bash
name: Docker Build

on:
  push:
    branches: [ master, main ]
  pull_request:
    branches: [ master, main ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout code
      uses: actions/checkout@v4
      
    - name: Build Docker image
      run: |
        docker build -t logger .
        
    - name: Run container
      run: |
        mkdir -p logs
        echo -e "test1\ntest2\ntest3" | docker run -i -v "$(pwd)/logs:/home/logs/" logger
        
    - name: Verify logs
      run: |
        cat logs/log.txt
        grep -q "test1" logs/log.txt && echo "Log test passed"
```
```bash
$ git add .
$ git commit -m "added Dockerfile and docker.yml"
[main 9766705] added Dockerfile and docker.yml
 3 files changed, 46 insertions(+)
 create mode 100644 .github/workflows/docker.yml
 create mode 100644 Dockerfile
 create mode 100644 logs/log.txt

$ git push origin main
Username for 'https://github.com': EgorMezin
Password for 'https://Goydarik@github.com': 
Enumerating objects: 204, done.
Counting objects: 100% (204/204), done.
Delta compression using up to 2 threads
Compressing objects: 100% (94/94), done.
Writing objects: 100% (204/204), 40.79 KiB | 40.79 MiB/s, done.
Total 204 (delta 75), reused 195 (delta 74), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (75/75), done.
To https://github.com/Goydarik/lab08
 * [new branch]      main -> main
```