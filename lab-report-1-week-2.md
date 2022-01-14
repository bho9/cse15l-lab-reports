# Lab Report 1 Week 2
## How to Download Visual Studio Code

The first step to be able to log into the course-specific account on `ieng6` is to get Visual Studio code.

1. Head over to: https://code.visualstudio.com/
2. Download and install it on the computer. Make sure it is the right version for your operating system.
3. Once that's done, open up Visual Studio Code and it should look like this:

    ![Image](/lab1week2ss/Figure1.png)

## Remotely Connecting

1. If you're on Windows, make sure you have OpenSSH installed. Follow this tutorial if it is not:
[Install OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse). After that, you must find your course-specific `ieng6` account for CSE15L here: https://sdacs.ucsd.edu/~icc/index.php. You might need to change your password for this to work so change it in that website and wait for about 15 or so minutes for the changes to go through.

    **Note:** Your account should look like this: 
    ```
    cs15lwi22zzz@ieng6.ucsd.edu
    ```
    where the `zzz` is replaced by your specific account characters.

2.  Open a terminal in VSCode by clicking `Terminal > New Terminal` located on the top. Type in the terminal:
    ```
    ssh cs15lwi22zzz@ieng6.ucsd.edu
    ```
    Again, where the `zzz` is your specific account's characters. If this is your first time logging in, you should be given a prompt asking about authenticity of host. Just type `yes` and enter.

3. Type your password. Do not worry if nothing shows up. The terminal is just hiding the number of characters. If successful, this should be part of what shows up (the account name shown in the figure below is my specific details, yours could be different), notice how the line where you type commands are now different:

    ![Image](/lab1week2ss/Figure2.png)

## Running Some Commands

1. Now let's try running some commands. Let's start with `ls` which stands for "list files". What you should see are the colored file names being listed separated by spaces:

    ![Image](/lab1week2ss/Figure3.png)

    Yours wouldn't have the "CSE15L" directory because you haven't created the directory yet. So let's do that next. 

2. Type:
    ```
    mkdir CSE15L
    ```
    `mkdir` means "make directory" where you create a new directory and the `CSE15L` argument is the name of the new directory. Press enter and then type `ls` again, you should see the new directory. But now how do we get into it? 
    
3. Type:
    ```
    cd CSE15L
    ```
    `cd` means "change directory" and the `CSE15L` argument is the name of the directory we want to enter. We are now in the `CSE15L` directory. But we want to go back now, what command do we use? You guessed it.

4. Type:
    ```
    cd ../
    ```
    This will take you to the previous directory which should be the "home" or "default" directory. **Note:** If you're inside of a lot of directories and you want to get straight back to the "home" directory without typing this command multiple times, type:
    ```
    cd ~
    ```
    Where `~` means "home" or "default" directory. Here's an example:
    ![Image](/lab1week2ss/Figure4.png)

5. Now we're back in the "home" directory. Let's try one more command. Type:
    ```
    ls -a
    ```
    Where `-a` is an argument for the `ls` command, which in this case is "all" so now we can even see hidden files and directories. The files that start with a `.` are called "dotfiles" which are the hidden files and directories.
    ![Image](/lab1week2ss/Figure5.png)

## Moving Files