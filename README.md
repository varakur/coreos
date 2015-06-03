****************** ****************** ******************

Authors : Prasad Varakur     (gangavara.varakur@huawei.com)
          Raghavan Santhanam (raghavan.santhanam@huawei.com)
Date    : June 1st 2015
Company : Huawei Technologies Co. Ltd, Santa Clara, CA

****************** ****************** ******************

Overview:
=========
This is a hand built CoreOS (www.github.com/coreos) ARM64 QEMU image, which 
includes CoreOS kernel, customizations/configurations and bunch of manually
ported CoreOS packages. Purpose is to provide a usable working CoreOS ARM64
image for early adopters, developers and testers, until official images are
released by CoreOS (porting work is in-progress).

A docker image is available in DockerHub at:
   https://registry.hub.docker.com/u/varakur/arm64-coreos/

Following CoreOS packages are ported and included in this image:
('TESTED' indicates successful validation/testing of the basic functionality)

1) systemd  (TESTED)
2) etcd     (TESTED)
3) fleet    (TESTED)
4) docker   (TESTED)
5) rkt
6) grub2    (TESTED)
7) core-admin
8) coreos-cloudinit
9) coreos-cloudinit-validator
10) coretest
11) etcd-ca
12) etcdctl
13) etcd-starter
14) flannel
16) ignition
17) mayday
18) nova-agent-watcher
19) nsproxy
20) sdnotify-proxy
21) subgun
22) updateservicectl


Other general development tools & packages included are:
1) Go language
2) curl
3) sshd
4) nano (text editor)
5) squash FS
6) gpg
7) iptables

 
Building C/C++ packages:
========================
* External aarch64-gnu-toolchain obtained from ubuntu repo and the arm64
  libraries obtained from buildroot(buildroot.org) have been used to
  successfully build various C/C++ packages of CoreOS like systemd, etc.

* In some cases, when required arm64 binaries are not available, the sources
  of the respective components (like iptables, golang etc.,) have been
  fetched from their developmental repositories and binaries cross-compiled.

  To avoid further dependencies of these independently built arm64 binaries
  inside the rfs, they have been built as static executables.


Building Go packages:
=====================
The Go-based packages are built using the latest arm64 support available
in the yet to be officially released Go v1.5 but available in its code 
base that can be bootstraped following the steps outlined here:
   http://dave.cheney.net/2015/03/03/cross-compilation-just-got-a-whole-lot-better-in-go-1-5

Procedure followed to include miscellaneous packages :
Packages such as init involving shells scripts, have been manually
included in the rfs as closer as possible to the original CoreOS/AMD64
environment. There are yet more miscellaneous packages that need
to be built and verified.


Credits:
========
* The arm64/docker binary is provided by HuangQiang (h.huangqiang@huawei.com)
