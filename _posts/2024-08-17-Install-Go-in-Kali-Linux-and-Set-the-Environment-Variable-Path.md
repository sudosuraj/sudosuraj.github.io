---
layout: post
title:  Install Go in Kali Linux and Set the Environment Variable Path
author:  sudosuraj
date:  2024-08-17
categories: 
tags:  [linux, go, go-lang, setup]
image:
  path: /assets/img/headers/elliot.jpg
---
## Install Go in Kali Linux and Set the Environment Variable Path.
Hello friend!
I hope you hacking well, in this short tutorial we'll setup go-lang in kali linux so you can easily run go based hacking tools.

Go is expressive, concise, clean, and efficient. Its concurrency mechanisms make it easy to write programs that get the most
out of multicore and networked machines, while its novel type system enables flexible and modular program construction. 
Go compiles quickly to machine code yet has the convenience of garbage collection and the power of run-time reflection. 
It's a fast, statically typed, compiled language that feels like a dynamically typed, interpreted language.

### Download go
Navigate to `https://go.dev/doc/install` and download the zipped folder containing initial go require setup files.

![image](https://github.com/user-attachments/assets/72b82ee9-4eef-4730-a0a7-b4578057084e)

![image](https://github.com/user-attachments/assets/69de1368-04bd-44b6-a191-5b2c6f2575ea)

![image](https://github.com/user-attachments/assets/b3cc85f4-5791-4e00-b172-238c71b21af3)

### Install go
Run the following command to extract the downloadd zip file an to install go-lang.

```
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.23.0.linux-amd64.tar.gz
```

The above command makes sure to delete if the go is already present in the sysem, and install only new one.
NOTE: you may be asked to run command as sudo.

### Setup Go Environment Varialble
After the installation, we need to add the GOROOT and GOPATH in current shell environment variables, so whenever we
try to run specific go tool, it can be run.
To do this, open the `~/.profile` file.
```
nano ~/.profile
```

Add the following bash script at the end of the file:
```
if [ -d "$HOME/go" ]; then
    GOPATH=/home/kali/go
    export GOROOT=/usr/local/go
    PATH=$PATH:$GOROOT/bin/:$GOPATH/bin
fi
```
Now save the profile file.
Open the `~/.bashrc` file and add the following bash script at the end of the file:

```
if [ -f ~/.profile ]; then
    . ~/.profile
fi
```
Now done, we are ready to run all go tools without any error!

You can open the new terminal and run the following commands verify the installation:
```
go version
which go
echo $GOROOt
echo $GOPATH
```
## Final words
I hope this tutorial saved your time, thanks for reding :)
Logging out sudo.
## Find me: 
- [LinkedIn](https://linkedin.com/in/sudosuraj)
- [GitHub](https://github.com/sudosuraz)
- [Bugcrowd](https://bugcrowd.com/sudosuraj)
- [X](https://x.com/sudosuraj)
- [Instagram](https://instagram.com/sudosuraj)

## Contact For Cyber Security Business
- sudosuraj@proton.me
