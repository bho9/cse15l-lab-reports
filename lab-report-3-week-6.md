# Lab Report 3 Week 6
---
## Group Choice 1 - Streamline `ssh` Configuration

The purpose of doing this is to reduce the amount of typing when trying to log into `ieng6`.

I first open the `config` file using TextEdit on MacOS inside the `.ssh` folder and added this in:

![Image](/lab3week6ss/Figure1.png)

After that, I just open a terminal and type:

```
ssh ieng6
```

This is what shows up, logging me into my account in the remote server:

![Image](/lab3week6ss/Figure2.png)

Although this only works if there is a private SSH key already in the ssh agent. If there isn't, I have to add this in:

![Image](/lab3week6ss/Figure3.png)

Where the entry right after `~/.ssh/` is the private SSH key name. If on Windows, use `\` instead of `/`. Upon typing the same ssh terminal command as above, the only difference this time is that it will prompt for the SSH private key passphrase:

![Image](/lab3week6ss/Figure4.png)

The amount of typing and time consumed is now lower (assuming there is already a private key already in the ssh agent so I don't have to type the passphrase) thanks to this.

This should simplify some commands like, for example, using `scp` to copy a file into the server and then running some commands to show that the file has been copied without even logging into the account.

![Image](/lab3week6ss/Figure5.png)

The first command securely copies the file `hello.rtf` into the `CSE15L` directory in my account (that has alias `ieng6`). The second command runs `cd CSE15L` and then `ls` in the server to show the contents in the `CSE15L` directory, so I can check that it has been copied into the right place.