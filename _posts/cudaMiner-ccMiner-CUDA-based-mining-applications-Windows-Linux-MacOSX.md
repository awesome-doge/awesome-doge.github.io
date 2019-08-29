---
title: 'cudaMiner & ccMiner CUDA based mining applications [Windows/Linux/MacOSX]'
date: 2014-08-29 20:17:25
tags: [blogger, miner]
categories: Blogger
---

Here's my new pet project. I started this during the easter holidays in 2013 and this uses CUDA to squeeze up to 200%  more performance out of nVidia cards - as compared to OpenCL mining applications. Grin ccMiner is a collaborative project by me and a co author also named Christian (call us the C&C Hash Factory, if you will). ccMiner is less polished, but often features new coins+algorithms close to launch date (usually with a clear mining advantage for nVidia).

<!-- more --> 

More information can be found on our dedicated nVidia mining forum http://www.cudaminers.net/

cudaMiner Algorithms:

scrypt
scrypt-jane
scrypt-N
keccak
blake (github version only)

Installation requirements:

a recent nVidia driver supporting at least CUDA 5.5
Visual Studio 2010 SP1 redistributable (redist). Install when MSVCR100.DLL is not found.
  http://www.microsoft.com/de-de/download/details.aspx?id=8328  (x86)
  http://www.microsoft.com/de-de/download/details.aspx?id=13523  (x64)

cudaMiner latest full release:

cudaminer-2014-02-28.zip [32+64bit version] (7.0 MB) speed-up for YAC (compute 3.0 or later), keccak (compute 3.5 or later)
SHA256 sum: 214df7efa386fa4895bf529e72f26463e5469432e6d8d239ee6653809bf072e5
MAC-OS X compiled binaries are found here: http://www.johnchapman.net/cudaminer/  (a third party site maintained by John Chapman)

ccMiner Algorithms:
HeavyCoin
MjollnirCoin
Fugue
Groestl
Myriad-Groestl
Diamond-Groestl
JackpotCoin
Quark
AnimeCoin
TalkCoin
X11/DarkCoin
X13/MaruCoin

ccMiner latest releases:

https://github.com/cbuchner1/ccminer/releases


Have a look at the Google Docs Spreadsheet for configuration and performance data. Please enter new data using this form. We now also have a spreadsheet for scrypt-jane, e.g. Yacoin and the corresponding Data Entry Form. Performance data for scrypt-jane is preliminary, as the feature is under development!

Here is another (somewhat outdated and chaotic) Google Docs spreadsheet with some performance figures and associated configuration settings.

Please carefully inspect the README.txt file before use. Usage is pretty much identical to pooler's cpuminer


previous cudaMiner releases:

cudaminer-2014-02-18.zip [32+64bit version] (7.1 MB) also runs on Maxwell
SHA256 sum: 066e8ffff0de6a3a2d814be4e7fb1f9c59ac6d5378f6710912ccdba61eee00bb

cudaminer-2014-02-09.zip [32+64bit version] (7.1 MB)
SHA256 sum: ef37c97562d98cb95a7a243d8bb378250d9f067b62db239435e6a9975a83a3b8

cudaminer-2014-02-04.zip [32+64bit version] (6.6 MB)
SHA256 sum: 4a38026f662dd06d84f2fe0e5f5098189888de8c0e9947bc24b3cedc4b5f0fdd

cudaminer-2014-02-02.zip [32+64bit version] (6.6 MB)
SHA256 sum: bad402d908862995ec67fd3dddb48a82883176ac7f20cef1f228462f88b04fbb

cudaminer-2013-12-18.zip [32+64bit version] (7.2 MB)
SH256 sum: 4d505804c80bd78fa1c661f74cc5d0e39f92a86f0507abc8ff2aa2b50ffba44b
ATTENTION! Fermi based devices like GTX 560, 570, 580, 590 seem to run quite hot with this release.

cudaminer-2013-12-10.zip [32+64bit version] (10.4 MB)
SHA256 sum: f6a9b1cfcd35867978589c2f36aaef45a16d0f57494777cb14a93366222c195a

cudaminer-2013-12-07.zip [32+64bit version] (9.5 MB)
SHA256 sum: 76dcddcf6d85cbd1ebe4acbb24497bfdae0f3ca9999694c4b152917f4559263a

cudaminer-2013-12-01.zip [32+64bit version] (10.4 MB)
SHA256 sum: dfb4f3a74e534132d397e45aae2f71933a013f557c3be4299e11759c6590b2be

cudaminer-2013-11-20.zip [Update: 32+64bit version] (11.4 MB)
SHA256 sum: 2db068884d0d5683e1b379cf8b4808f55a43b2612547757ce98a8bfe8d2fa0d4

cudaminer-2013-11-15.zip (5.1 MB)
SHA256 sum: 4d4821b0539c24b8882d00caa388e6f7aa8efb2480206e4c9dc2bc95532e3837

cudaminer-2013-11-14.zip (5.4 MB)
SHA256 sum: 5a81f97e183533683373849d73fc30b0b4d287cddb83ef327b0baba006b07c4f

cudaminer-2013-11-01.zip (5.0 MB)
SHA256 sum: 27564fdbc4c41b9d6994a03f8fd2e0a14a1d4a64f0da216b06e8810b604e4ab9

cudaminer-2013-10-10.zip (4.9 MB)
SHA256 sum: 7938965a046b84734daa4332327313b48d198d808a0cf85cb3f0a27e65260c4c

cudaminer-2013-07-13.zip (3.0 MB)
SHA256 sum: d14792ffc8fb5fc910b442d802c480f4f478fa18e2fc95736f525f97a0a9ad52

cudaminer-2013-04-30.zip (3.2 MB)
SHA256 sum: 2d81b52e1051a4f724e75b0e84e231293809437aa060d21b2fd3b8bfc5b711f2

 Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin
If you find this useful, please donate a little. How about the first litecoin you successfully mine with this app? LKS1WDKGED647msBQfLBHV3Ls8sveGncnm      This is my "motivation address".
 Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin Grin

Required dependencies for building on Windows:
pthreads: http://sourceware.org/pthreads-win32/
OpenSSL-Win32: http://slproweb.com/download/Win32OpenSSL-101e.exe
curl-7.29.0: http://curl.haxx.se/download/curl-7.29.0.zip
or in precompiled form for Visual Studio 2010 SP1 cudaminervc2010prerequisites.7z (49.3 MB)

Linux compilation is also possible now:
chmod +x configure autogen.sh     (.zip does not preserve the x bit)
./autogen.sh && ./configure && make

Better grab the sourcecode from github, as the .zip file contains has Windows style line endings in all ASCII files which you would have to convert first.

Christian

