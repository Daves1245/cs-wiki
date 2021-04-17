## Linux Basics

### Intro

It was once said that there were three basic necessities for an operating system. An assembler, a filesystem, and a shell. With those three, you can do anything. An assembler turns assembly code into ELF files, so that you can write arbitrary programs. A filesystem so you can store data. And, a shell so that you can interact with the computer. One of the most common shells these days is called "bash". When a computer starts up, the first thing it does is read the harddrive and start some simple services such as the program that handles internet packets. Then, it opens up a shell so that you can type commands in. Nowadays, we have windowing GUIs so it looks prettier than a terminal, but once upon a time, that's the way it was. A shell simply collects characters as you type, and waits until you hit enter. Once you hit enter, it executes exactly what you wrote. That's about it.

### SSH

ssh is a program that will open up a shell on another computer, securely (ssh = S_ecure SH_ell). The other computer has to be running the ssh service in order to handle your request. Let's learn how to use it. A URL is something you already know about, eg, http://www.google.com. A URI is a superset of a URL. A URI has a syntax of the form `username:password@domain:port`. You can connect to an AWS instance with username ubuntu using `ssh ubuntu@IPADDRESS`, where it by-default uses port 22, and you type in the password. If a private key is being used for authentication, do `ssh -i mykey.pem username@IPADDRESS`

### Executable files

An executable file in Linux will either be of the file format ELF, or will be a scripting language (Don’t cite me on that, there might be other things, but those are the two I know of). An ELF file is just machine code with some metadata, simple as that. A scripting language can be something like bash or python. Linux will look for the `#!` characters at the beginning of a file to be the “scripting language” identifier, followed by the scripting program’s filepath. So, an example `connect.sh` file would be

```
#!/bin/bash
ssh my_user@76.207.99.81
```

The file line says to run `/bin/bash`, with the entire file as input. Now, linux won’t know your file is supposed to be an executable until you tell it that it is, and give permission to execute. `chmod` is a command that changes the permissions.

### Services

A service is a program that is expected to run all the time, as a background process. This is in contrast to something like `ssh`, which you will only run specifically when you want to ssh into something. Services include MySQL, which keeps a database running, and Apache, which keeps a website running, or even just a minecraft server counts as a service. In Ubuntu, the program that helps you handle services is called `systemctl`. You can write a command like `sudo systemctl start apache2` to start apache2, for example. `systemctl` will restart a program if it crashes, and you can go pretty in-depth with configuration files to get `systemctl` to act exactly the way you want it to.

### Ports

Your computer will have many things trying to communicate with it, all sending for example TCP packets. By labelling each packet with a port, your computer can organize the information and send it to the correct service that is supposed to handle those packets. Services will commonly use these internet ports on your computer to communicate. For example, MySQL uses port 3306 by default, and ssh uses port 22 (You can of course, tell these programs to use other ports if you desire). If different services within your computer need to communicate, you will commonly access `localhost:port` for example. But, you may also access external computers using their IP address, such as `ssh`ing into another computer, or using `mysql` to access a remote database. Every time Google Chrome visits a webpage, it uses port 80 or 443 to request HTML/CSS/JS/etc files so that it can render the website. Services such as apache2 can handle requests on port 80 or 443, and respond appropriately.

Ports aren't a security vulnerability if protected properly. I can pick any remote IP I want, and send packets with random ports like 1337 or 1234, but the other computer will just ignore them. If I try sending random packets with port 3306 to a computer running mysql, but without providing a proper packet including the mysql password, the computer will still route them to mysql, but the mysql program will ignore them. (I'm simplifying the process of authentication, but you get the idea)
