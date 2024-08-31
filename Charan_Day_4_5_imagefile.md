# Docker file creation

```
FROM  from base Image
RUN  - run this cmd on top of above image
COPY - copy cmd  will copy the samba.zip  directly to docker host to Docker container
ADD - add wll extract samba.zip file and copy extracted  samba.zip  to container
via add cmd url file also Downloaded in container

WORKDIR -- like cd ( Switch  to working  directory )
LABLE - image related sone information
LABEL created=" Samba"
maintainer="who is maintaing (nextops)"
EXPOSE = export the  port inside container
ENTRYPOINT -- container to be run as executable ( Startup Command   ) this will not change at runtime , if i want change arguments  then we need to used CMD
CMD  
ENV =
USER =


```


- difference between copy and add
```
i want to copy samba.zip

cp samba.zip /u02
add samba.zip /u02


copy cmd  will copy the file directly to docker host to Docker container

add wll extract zip file and copy to container
via add cmd url file also Downloaded in container
```
- CMD
```
it will specify entrypoint for running up
CMD [ " /bin/bash"]
```


```
root@shivadocker:~# mkdir Dockerfile
root@shivadocker:~# cd Dockerfile/
root@shivadocker:~/Dockerfile# nano Dockerfile
root@shivadocker:~/Dockerfile# cat Dockerfile
FROM ubuntu:latest
RUN apt update -y
RUN apt install net-tools vim nano -y
CMD ["/bin/bash"]
root@shivadocker:~/Dockerfile# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS             PORTS                                   NAMES
a804d4a7fc8d   nginx     "/docker-entrypoint.…"   14 minutes ago   Up 14 minutes      80/tcp                                  samba_mem
35b25f9840ad   nginx     "/docker-entrypoint.…"   54 minutes ago   Up 35 minutes      0.0.0.0:8001->80/tcp, :::8001->80/tcp   samba2
ac5303fe56b2   ubuntu    "/bin/bash"              2 hours ago      Up About an hour                                           myubuntu
root@shivadocker:~/Dockerfile# docker images
REPOSITORY      TAG       IMAGE ID       CREATED             SIZE
samba_own       latest    d2fb207acc49   36 minutes ago      188MB
custome_image   latest    a9d4d4a8af46   About an hour ago   78.1MB
<none>          <none>    c99d864fa2cb   About an hour ago   78.1MB
nginx           latest    5ef79149e0ec   2 weeks ago         188MB
ubuntu          latest    edbfe74c41f8   4 weeks ago         78.1MB
busybox         latest    65ad0d468eb1   15 months ago       4.26MB
root@shivadocker:~/Dockerfile# docker build -t Update_image .
DEPRECATED: The legacy builder is deprecated and will be removed in a future release.
            Install the buildx component to build images with BuildKit:
            https://docs.docker.com/go/buildx/

invalid argument "Update_image" for "-t, --tag" flag: invalid reference format: repository name must be lowercase
See 'docker build --help'.
root@shivadocker:~/Dockerfile# docker build -t update_image .
DEPRECATED: The legacy builder is deprecated and will be removed in a future release.
            Install the buildx component to build images with BuildKit:
            https://docs.docker.com/go/buildx/

Sending build context to Docker daemon  2.048kB
Step 1/4 : FROM ubuntu:latest
 ---> edbfe74c41f8
Step 2/4 : RUN apt update -y
 ---> Running in ad49964e7084

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

Get:1 http://archive.ubuntu.com/ubuntu noble InRelease [256 kB]
Get:2 http://security.ubuntu.com/ubuntu noble-security InRelease [126 kB]
Get:3 http://archive.ubuntu.com/ubuntu noble-updates InRelease [126 kB]
Get:4 http://archive.ubuntu.com/ubuntu noble-backports InRelease [126 kB]
Get:5 http://archive.ubuntu.com/ubuntu noble/universe amd64 Packages [19.3 MB]
Get:6 http://security.ubuntu.com/ubuntu noble-security/restricted amd64 Packages [354 kB]
Get:7 http://security.ubuntu.com/ubuntu noble-security/multiverse amd64 Packages [12.7 kB]
Get:8 http://security.ubuntu.com/ubuntu noble-security/main amd64 Packages [404 kB]
Get:9 http://security.ubuntu.com/ubuntu noble-security/universe amd64 Packages [337 kB]
Get:10 http://archive.ubuntu.com/ubuntu noble/restricted amd64 Packages [117 kB]
Get:11 http://archive.ubuntu.com/ubuntu noble/multiverse amd64 Packages [331 kB]
Get:12 http://archive.ubuntu.com/ubuntu noble/main amd64 Packages [1808 kB]
Get:13 http://archive.ubuntu.com/ubuntu noble-updates/universe amd64 Packages [449 kB]
Get:14 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 Packages [594 kB]
Get:15 http://archive.ubuntu.com/ubuntu noble-updates/multiverse amd64 Packages [16.9 kB]
Get:16 http://archive.ubuntu.com/ubuntu noble-updates/restricted amd64 Packages [354 kB]
Get:17 http://archive.ubuntu.com/ubuntu noble-backports/universe amd64 Packages [11.5 kB]
Fetched 24.7 MB in 4s (6135 kB/s)
Reading package lists...
Building dependency tree...
Reading state information...
29 packages can be upgraded. Run 'apt list --upgradable' to see them.
Removing intermediate container ad49964e7084
 ---> d7bcf7c7e317
Step 3/4 : RUN apt install net-tools vim nano -y
 ---> Running in 7b957fb42d3e

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

Reading package lists...
Building dependency tree...
Reading state information...
The following additional packages will be installed:
  libexpat1 libgpm2 libpython3.12-minimal libpython3.12-stdlib
  libpython3.12t64 libreadline8t64 libsodium23 libsqlite3-0 media-types
  netbase readline-common tzdata vim-common vim-runtime xxd
Suggested packages:
  gpm hunspell readline-doc ctags vim-doc vim-scripts
The following NEW packages will be installed:
  libexpat1 libgpm2 libpython3.12-minimal libpython3.12-stdlib
  libpython3.12t64 libreadline8t64 libsodium23 libsqlite3-0 media-types nano
  net-tools netbase readline-common tzdata vim vim-common vim-runtime xxd
0 upgraded, 18 newly installed, 0 to remove and 29 not upgraded.
Need to get 16.8 MB of archives.
After this operation, 73.7 MB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu noble/main amd64 libexpat1 amd64 2.6.1-2build1 [87.0 kB]
Get:2 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 libpython3.12-minimal amd64 3.12.3-1ubuntu0.1 [832 kB]
Get:3 http://archive.ubuntu.com/ubuntu noble/main amd64 media-types all 10.1.0 [27.5 kB]
Get:4 http://archive.ubuntu.com/ubuntu noble/main amd64 netbase all 6.4 [13.1 kB]
Get:5 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 tzdata all 2024a-3ubuntu1.1 [273 kB]
Get:6 http://archive.ubuntu.com/ubuntu noble/main amd64 readline-common all 8.2-4build1 [56.5 kB]
Get:7 http://archive.ubuntu.com/ubuntu noble/main amd64 libreadline8t64 amd64 8.2-4build1 [153 kB]
Get:8 http://archive.ubuntu.com/ubuntu noble/main amd64 libsqlite3-0 amd64 3.45.1-1ubuntu2 [701 kB]
Get:9 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 libpython3.12-stdlib amd64 3.12.3-1ubuntu0.1 [2069 kB]
Get:10 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 vim-common all 2:9.1.0016-1ubuntu7.1 [385 kB]
Get:11 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 xxd amd64 2:9.1.0016-1ubuntu7.1 [62.9 kB]
Get:12 http://archive.ubuntu.com/ubuntu noble/main amd64 libgpm2 amd64 1.20.7-11 [14.1 kB]
Get:13 http://archive.ubuntu.com/ubuntu noble/main amd64 nano amd64 7.2-2build1 [281 kB]
Get:14 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 libpython3.12t64 amd64 3.12.3-1ubuntu0.1 [2339 kB]
Get:15 http://archive.ubuntu.com/ubuntu noble/main amd64 libsodium23 amd64 1.0.18-1build3 [161 kB]
Get:16 http://archive.ubuntu.com/ubuntu noble/main amd64 net-tools amd64 2.10-0.1ubuntu4 [204 kB]
Get:17 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 vim-runtime all 2:9.1.0016-1ubuntu7.1 [7279 kB]
Get:18 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 vim amd64 2:9.1.0016-1ubuntu7.1 [1881 kB]
debconf: delaying package configuration, since apt-utils is not installed
Fetched 16.8 MB in 2s (7403 kB/s)
Selecting previously unselected package libexpat1:amd64.
(Reading database ... 4376 files and directories currently installed.)
Preparing to unpack .../00-libexpat1_2.6.1-2build1_amd64.deb ...
Unpacking libexpat1:amd64 (2.6.1-2build1) ...
Selecting previously unselected package libpython3.12-minimal:amd64.
Preparing to unpack .../01-libpython3.12-minimal_3.12.3-1ubuntu0.1_amd64.deb ...
Unpacking libpython3.12-minimal:amd64 (3.12.3-1ubuntu0.1) ...
Selecting previously unselected package media-types.
Preparing to unpack .../02-media-types_10.1.0_all.deb ...
Unpacking media-types (10.1.0) ...
Selecting previously unselected package netbase.
Preparing to unpack .../03-netbase_6.4_all.deb ...
Unpacking netbase (6.4) ...
Selecting previously unselected package tzdata.
Preparing to unpack .../04-tzdata_2024a-3ubuntu1.1_all.deb ...
Unpacking tzdata (2024a-3ubuntu1.1) ...
Selecting previously unselected package readline-common.
Preparing to unpack .../05-readline-common_8.2-4build1_all.deb ...
Unpacking readline-common (8.2-4build1) ...
Selecting previously unselected package libreadline8t64:amd64.
Preparing to unpack .../06-libreadline8t64_8.2-4build1_amd64.deb ...
Adding 'diversion of /lib/x86_64-linux-gnu/libhistory.so.8 to /lib/x86_64-linux-gnu/libhistory.so.8.usr-is-merged by libreadline8t64'
Adding 'diversion of /lib/x86_64-linux-gnu/libhistory.so.8.2 to /lib/x86_64-linux-gnu/libhistory.so.8.2.usr-is-merged by libreadline8t64'
Adding 'diversion of /lib/x86_64-linux-gnu/libreadline.so.8 to /lib/x86_64-linux-gnu/libreadline.so.8.usr-is-merged by libreadline8t64'
Adding 'diversion of /lib/x86_64-linux-gnu/libreadline.so.8.2 to /lib/x86_64-linux-gnu/libreadline.so.8.2.usr-is-merged by libreadline8t64'
Unpacking libreadline8t64:amd64 (8.2-4build1) ...
Selecting previously unselected package libsqlite3-0:amd64.
Preparing to unpack .../07-libsqlite3-0_3.45.1-1ubuntu2_amd64.deb ...
Unpacking libsqlite3-0:amd64 (3.45.1-1ubuntu2) ...
Selecting previously unselected package libpython3.12-stdlib:amd64.
Preparing to unpack .../08-libpython3.12-stdlib_3.12.3-1ubuntu0.1_amd64.deb ...
Unpacking libpython3.12-stdlib:amd64 (3.12.3-1ubuntu0.1) ...
Selecting previously unselected package vim-common.
Preparing to unpack .../09-vim-common_2%3a9.1.0016-1ubuntu7.1_all.deb ...
Unpacking vim-common (2:9.1.0016-1ubuntu7.1) ...
Selecting previously unselected package xxd.
Preparing to unpack .../10-xxd_2%3a9.1.0016-1ubuntu7.1_amd64.deb ...
Unpacking xxd (2:9.1.0016-1ubuntu7.1) ...
Selecting previously unselected package libgpm2:amd64.
Preparing to unpack .../11-libgpm2_1.20.7-11_amd64.deb ...
Unpacking libgpm2:amd64 (1.20.7-11) ...
Selecting previously unselected package nano.
Preparing to unpack .../12-nano_7.2-2build1_amd64.deb ...
Unpacking nano (7.2-2build1) ...
Selecting previously unselected package libpython3.12t64:amd64.
Preparing to unpack .../13-libpython3.12t64_3.12.3-1ubuntu0.1_amd64.deb ...
Unpacking libpython3.12t64:amd64 (3.12.3-1ubuntu0.1) ...
Selecting previously unselected package libsodium23:amd64.
Preparing to unpack .../14-libsodium23_1.0.18-1build3_amd64.deb ...
Unpacking libsodium23:amd64 (1.0.18-1build3) ...
Selecting previously unselected package net-tools.
Preparing to unpack .../15-net-tools_2.10-0.1ubuntu4_amd64.deb ...
Unpacking net-tools (2.10-0.1ubuntu4) ...
Selecting previously unselected package vim-runtime.
Preparing to unpack .../16-vim-runtime_2%3a9.1.0016-1ubuntu7.1_all.deb ...
Adding 'diversion of /usr/share/vim/vim91/doc/help.txt to /usr/share/vim/vim91/doc/help.txt.vim-tiny by vim-runtime'
Adding 'diversion of /usr/share/vim/vim91/doc/tags to /usr/share/vim/vim91/doc/tags.vim-tiny by vim-runtime'
Unpacking vim-runtime (2:9.1.0016-1ubuntu7.1) ...
Selecting previously unselected package vim.
Preparing to unpack .../17-vim_2%3a9.1.0016-1ubuntu7.1_amd64.deb ...
Unpacking vim (2:9.1.0016-1ubuntu7.1) ...
Setting up libexpat1:amd64 (2.6.1-2build1) ...
Setting up media-types (10.1.0) ...
Setting up net-tools (2.10-0.1ubuntu4) ...
Setting up libsodium23:amd64 (1.0.18-1build3) ...
Setting up libgpm2:amd64 (1.20.7-11) ...
Setting up libsqlite3-0:amd64 (3.45.1-1ubuntu2) ...
Setting up libpython3.12-minimal:amd64 (3.12.3-1ubuntu0.1) ...
Setting up xxd (2:9.1.0016-1ubuntu7.1) ...
Setting up tzdata (2024a-3ubuntu1.1) ...
debconf: unable to initialize frontend: Dialog
debconf: (TERM is not set, so the dialog frontend is not usable.)
debconf: falling back to frontend: Readline
debconf: unable to initialize frontend: Readline
debconf: (Can't locate Term/ReadLine.pm in @INC (you may need to install the Term::ReadLine module) (@INC entries checked: /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.38.2 /usr/local/share/perl/5.38.2 /usr/lib/x86_64-linux-gnu/perl5/5.38 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl-base /usr/lib/x86_64-linux-gnu/perl/5.38 /usr/share/perl/5.38 /usr/local/lib/site_perl) at /usr/share/perl5/Debconf/FrontEnd/Readline.pm line 8.)
debconf: falling back to frontend: Teletype
Configuring tzdata
------------------

Please select the geographic area in which you live. Subsequent configuration
questions will narrow this down by presenting a list of cities, representing
the time zones in which they are located.

  1. Africa   3. Antarctica  5. Asia      7. Australia  9. Indian    11. Etc
  2. America  4. Arctic      6. Atlantic  8. Europe     10. Pacific
Geographic area:
Use of uninitialized value $_[1] in join or string at /usr/share/perl5/Debconf/DbDriver/Stack.pm line 112.

Current default time zone: '/UTC'
Local time is now:      Sat Aug 31 06:18:36 UTC 2024.
Universal Time is now:  Sat Aug 31 06:18:36 UTC 2024.
Run 'dpkg-reconfigure tzdata' if you wish to change it.

Use of uninitialized value $val in substitution (s///) at /usr/share/perl5/Debconf/Format/822.pm line 84, <GEN6> line 4.
Use of uninitialized value $val in concatenation (.) or string at /usr/share/perl5/Debconf/Format/822.pm line 85, <GEN6> line 4.
Setting up vim-common (2:9.1.0016-1ubuntu7.1) ...
Setting up nano (7.2-2build1) ...
update-alternatives: using /bin/nano to provide /usr/bin/editor (editor) in auto mode
update-alternatives: warning: skip creation of /usr/share/man/man1/editor.1.gz because associated file /usr/share/man/man1/nano.1.gz (of link group editor) doesn't exist
update-alternatives: using /bin/nano to provide /usr/bin/pico (pico) in auto mode
update-alternatives: warning: skip creation of /usr/share/man/man1/pico.1.gz because associated file /usr/share/man/man1/nano.1.gz (of link group pico) doesn't exist
Setting up netbase (6.4) ...
Setting up vim-runtime (2:9.1.0016-1ubuntu7.1) ...
Setting up readline-common (8.2-4build1) ...
Setting up libreadline8t64:amd64 (8.2-4build1) ...
Setting up libpython3.12-stdlib:amd64 (3.12.3-1ubuntu0.1) ...
Setting up libpython3.12t64:amd64 (3.12.3-1ubuntu0.1) ...
Setting up vim (2:9.1.0016-1ubuntu7.1) ...
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/ex (ex) in auto mode
update-alternatives: warning: skip creation of /usr/share/man/man1/ex.1.gz because associated file /usr/share/man/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/da/man1/ex.1.gz because associated file /usr/share/man/da/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/de/man1/ex.1.gz because associated file /usr/share/man/de/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/fr/man1/ex.1.gz because associated file /usr/share/man/fr/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/it/man1/ex.1.gz because associated file /usr/share/man/it/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/ja/man1/ex.1.gz because associated file /usr/share/man/ja/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/pl/man1/ex.1.gz because associated file /usr/share/man/pl/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/ru/man1/ex.1.gz because associated file /usr/share/man/ru/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/tr/man1/ex.1.gz because associated file /usr/share/man/tr/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/rview (rview) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/rvim (rvim) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vi (vi) in auto mode
update-alternatives: warning: skip creation of /usr/share/man/man1/vi.1.gz because associated file /usr/share/man/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/da/man1/vi.1.gz because associated file /usr/share/man/da/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/de/man1/vi.1.gz because associated file /usr/share/man/de/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/fr/man1/vi.1.gz because associated file /usr/share/man/fr/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/it/man1/vi.1.gz because associated file /usr/share/man/it/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/ja/man1/vi.1.gz because associated file /usr/share/man/ja/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/pl/man1/vi.1.gz because associated file /usr/share/man/pl/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/ru/man1/vi.1.gz because associated file /usr/share/man/ru/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/tr/man1/vi.1.gz because associated file /usr/share/man/tr/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/view (view) in auto mode
update-alternatives: warning: skip creation of /usr/share/man/man1/view.1.gz because associated file /usr/share/man/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/da/man1/view.1.gz because associated file /usr/share/man/da/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/de/man1/view.1.gz because associated file /usr/share/man/de/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/fr/man1/view.1.gz because associated file /usr/share/man/fr/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/it/man1/view.1.gz because associated file /usr/share/man/it/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/ja/man1/view.1.gz because associated file /usr/share/man/ja/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/pl/man1/view.1.gz because associated file /usr/share/man/pl/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/ru/man1/view.1.gz because associated file /usr/share/man/ru/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/tr/man1/view.1.gz because associated file /usr/share/man/tr/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vim (vim) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vimdiff (vimdiff) in auto mode
Processing triggers for libc-bin (2.39-0ubuntu8.2) ...
Removing intermediate container 7b957fb42d3e
 ---> e2d07f7294da
Step 4/4 : CMD ["/bin/bash"]
 ---> Running in 16a92883b3bb
Removing intermediate container 16a92883b3bb
 ---> 04961b94f0ae
Successfully built 04961b94f0ae
Successfully tagged update_image:latest
root@shivadocker:~/Dockerfile#
```
- docker build with custome docker file

```
root@shivadocker:~/Dockerfile# cp -rp Dockerfile Dockerfile1
root@shivadocker:~/Dockerfile# docker build -t custome_me -f Dockerfile1 .
DEPRECATED: The legacy builder is deprecated and will be removed in a future release.
            Install the buildx component to build images with BuildKit:
            https://docs.docker.com/go/buildx/

Sending build context to Docker daemon  3.072kB
Step 1/4 : FROM ubuntu:latest
 ---> edbfe74c41f8
Step 2/4 : RUN apt update -y
 ---> Using cache
 ---> d7bcf7c7e317
Step 3/4 : RUN apt install net-tools vim nano -y
 ---> Using cache
 ---> e2d07f7294da
Step 4/4 : CMD ["/bin/bash"]
 ---> Using cache
 ---> 04961b94f0ae
Successfully built 04961b94f0ae
Successfully tagged custome_me:latest
root@shivadocker:~/Dockerfile#

```
