# Lab Report 1 Week 2
## How to Download Visual Studio Code

The first step to be able to log into the course-specific account on `ieng6` is to get Visual Studio code.

1. Head over to: https://code.visualstudio.com/
2. Download and install it on the computer. Make sure it is the right version for your operating system.
3. Once that's done, open up Visual Studio Code and it should look like this:

![Image](/lab1week2ss/Figure1.png)

## Remotely Connecting

Firstly, if you're on Windows, make sure you have OpenSSH installed. Follow this tutorial if it is not:
[Install OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse). After that, you must find your course-specific `ieng6` account for CSE15L here: https://sdacs.ucsd.edu/~icc/index.php. You might need to change your password for this to work so change it in that website and wait for about 15 or so minutes for the changes to go through.

**Note:** Your account should look like this: 
```
cs15lwi22zzz@ieng6.ucsd.edu
```
where the `zzz` is replaced by your specific account characters.

Next up, open a terminal in VSCode by clicking `Terminal > New Terminal` located on the top. Type in the terminal:
```
ssh cs15lwi22zzz@ieng6.ucsd.edu
```
Again, where the `zzz` is your specific account's characters. If this is your first time logging in, you should be given a prompt asking 