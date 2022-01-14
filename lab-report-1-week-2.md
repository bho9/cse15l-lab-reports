# Lab Report 1 Week 2
---
## How to Download Visual Studio Code

The first step to be able to log into the course-specific account on `ieng6` is to get Visual Studio code.

1. Head over to: [https://code.visualstudio.com/](https://code.visualstudio.com/)
2. Download and install it on the computer. Make sure it is the right version for your operating system.
3. Once that's done, open up Visual Studio Code and it should look like this:


    ![Image](/lab1week2ss/Figure1.png)

## Remotely Connecting

Some terms to know beforehand:
* Client: The computer you are using right now to read this.
* Server: The remote computer you are going to be connecting to that's stored in a remote location.
1. If you're on Windows, make sure you have OpenSSH installed. Follow this tutorial if it is not:
[Install OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse). After that, you must find your course-specific `ieng6` account for CSE15L here: [https://sdacs.ucsd.edu/~icc/index.php](https://sdacs.ucsd.edu/~icc/index.php). You might need to change your password for this to work so change it in that website and wait for about 15 or so minutes for the changes to go through.

    **Note:** Your account should look like this: 
    ```
    cs15lwi22zzz@ieng6.ucsd.edu
    ```
    where the `zzz` is replaced by your specific account characters.

2.  Open a terminal in VSCode by clicking `Terminal > New Terminal` located on the top. Type in the terminal:
    ```
    ssh cs15lwi22zzz@ieng6.ucsd.edu
    ```
    Again, where the `zzz` is your specific account's characters. `ssh` stands for "secure shell". If this is your first time logging in, you should be given a prompt asking about authenticity of host. Just type `yes` and enter.

3. Type your password. Do not worry if nothing shows up. The terminal is just hiding the number of characters. If successful, this should be part of what shows up (the account name shown in the figure below is my specific details, yours could be different), notice how the line where you type commands are now different:


    ![Image](/lab1week2ss/Figure2.png)

    Now the commands are run on the server you're connected to.

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

**Note:** These commands are Linux commands because the server runs on Linux. If you try these commands on a Windows terminal you will get errors.

## Moving Files

Now we want to add some files, this is essential in working remotely since we're going to need to copy files back and forth between the client and the server. There are many ways to do this but for this section we're going to focus on the command `scp`. This command will always run on the client and it stands for "secure copy" where it will securely copy a file from the client to the server.

1. Let's make a file to store first. Create a file anywhere named `hello.txt`.

2. Open the terminal in that directory where `hello.txt` is stored.

3. Type in the terminal:

    ```
    scp hello.txt cs15lwi22zzz@ieng6.ucsd.edu:~/
    ```
    Again, where `zzz` is your account specific characters. The argument `hello.txt` is the file you want to copy. The username is the server you want to send it to. The `~/` indicates the location that the file will be copied to (which is the home); you can add directories so that it will be placed in that specific directory like `~/CSE15L` to place it in the `CSE15L` folder.
    
    You will be prompted for a password. After that it should show `100%` meaning the file has successfully been copied.

4. Log into the server with ssh again. Now type `ls`. You should see `hello.txt` in the home `~` directory since that's where you selected to copy to.

    ![Image](/lab1week2ss/Figure6.png)

    You may have noticed that in this figure I didn't need to type my password after I used the `scp` command and after I ssh'ed in. That is because I used an SSH key pair so that I don't have to type my password everytime I log in or run a command to send a file to the server. This makes remote working a bit less tedious and time consuming. Let me show you how to add an SSH key pair.

## SSH Keys

The purpose of doing this part is to simplify your workflow. As mentioned before, it can be frustrating having to type your password everytime, especially if your password is long. Even if you store the password in a password manager, you have to open the password manager, copy it, and paste it into the terminal which is still a bit time consuming.

Using SSH keys will make this easier as the `ssh` command can use the key pair to log in instead of your password. Start by opening a terminal.

1. Type:

    ```
    ssh-keygen
    ```

    It should ask you to choose where to save the key. Pick anywhere or just use the defaults. I recommend using the default save location.

    You should be prompted for a passphrase. I highly recommend you use a passphrase instead of empty or a password [(passphrases are said to be more secure)](https://www.zdnet.com/article/fbi-recommends-passphrases-over-password-complexity/).

    If successful it should tell you where the keys are saved, give you a SHA256 key fingerprint, and the key's randomart image. You now have a private key and public key; the private key has no extension while the public key has the `.pub` extention.

    **Keep the private key safe and never share it with anyone.**

2. We need to copy the *public* key (the one with `.pub`) into the `.ssh` directory in the server of your account. First, make the `.ssh` directory in the home directory of the server if there isn't one already.

    ```
    ssh cs15lwi22zzz@ieng6.ucsd.edu
    <Enter password>
    mkdir .ssh
    exit
    ```

    Now we're back on the client.

3. Navigate to or open the terminal in the location where the keys are stored. Type:

    ```
    scp <keyname>.pub cs15lwi22zzz@ieng6.ucsd.edu:~/.ssh/authorized_keys
    ```

    All in one command. Replace `<keyname>` with your key's file name. **Make sure it's the `.pub` file.** The public key should be added.

4. We're not done yet, we still need to add the private key to your computer's ssh-agent. Open a terminal where your private key is stored (or navigate to it using the terminal). Make sure you look up the correct commands for [Windows](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_keymanagement#user-key-generation). MacOS and Linux share the same commands and it's simpy just:

    ```
    ssh-add <keyname>
    ```

    **Without** the `.pub` because this is the private key. If successful it should show you an RSA code or something that looks like gibberish. If not, it's likely the ssh-agent isn't running, so look up how to get it running for your operating system. You can check if it's added by typing:

    ```
    ssh-add -l
    ```

    If something like this shows up, then you're good:

    ![Image](/lab1week2ss/Figure7.png)

Once this is complete you should be able to use `ssh` or `scp` without your password. **Note:** This should only work on those computers where the ssh-agent has your private key.

## Optimizing Remote Running

Now that it's much easier to log in and work on the server, let's try a few things.

1. You can run a command on the server right after ssh-ing and then exit after the command has been executed - all in one line. Simply add quotes to the server commands like this:

    ```
    ssh cs15lwi22zzz@ieng6.ucsd.edu "pwd"
    ```

    Where `pwd` means "print working directory" which is simply printing the path for the directory (in this case, the home directory). It should look something like this:

    ![Image](/lab1week2ss/Figure8.png)

2. You can copy multiple files to the home directory or a directory of your choosing without having to type the same command multiple times for each file. For example, here's how to copy two `.txt` files into the home directory of the server:

    ```
    scp hello.txt hello2.txt cs15lwi22zzz@ieng6.ucsd.edu:~/<optionally add directory paths here>
    ```

3. How about compiling and running a `.java` file on the server all in one line? Again, just use quotation marks and simple add a semicolon inside to separate multiple commands. Let's assume you have a `WhoAmI.java` file in your home directory, where the file contains:

    ```
    public class WhoAmI {
        public static void main(String[] args) 
        {
            System.out.println(System.getProperty("user.name"));
        }
    }
    ```

    Then you just type in the terminal:

    ```
    ssh cs15lwi22zzz@ieng6.ucsd.edu "javac WhoAmI.java; java WhoAmI"
    ```

    All in one line, which should print your username and then exits the server:

    ![Image](/lab1week2ss/Figure9.png)

A handy trick to know is that if you want to get the last, or any other previous commands recently used in the terminal, just press the up-arrow on your keyboard. As you can see, all of these commands do something in the server without requiring you to enter the password every time, and they all simplify having to type multiple commands in the terminal. There are other ways to easily run remote code/commands but these are a few examples.