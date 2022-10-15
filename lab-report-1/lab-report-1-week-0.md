Vadim Victor Kim  
CSE 15L  
09/30/2022

# Lab Report 1

## **1. Installing VScode**

First navigate to vscode website and follow their instructions for installation of Visual Studio Code.

![](Screen%20Shot%202022-10-14%20at%204.35.04%20PM.png)
Click the [Download] button and install the right version for you!


## **2. Remotely Connecting**
To remotely connect in VSCode, you first have to open the terminal. You can do that by pressing Ctrl+` (the key to the left of 1 on top left of your keyboard).

If you are on windows, you have to make sure that you have OpenSSH installed. Navigate to the OpenSSH website and follow their instructions to install it.

If you are on Mac, or already have it installed, you can just proceed with connecting remotely.

To remotely connect you will have to type in “ssh <your username>” where you replace <your username> with your UCSD provided server username.

You will then be prompted to type in your password. If you are having trouble logging in you can follow instructions on [this](https://docs.google.com/document/d/1hs7CyQeh-MdUfM9uv99i8tqfneos6Y8bDU0uhn1wqho/edit) website to change your password. This may take a while to take effect so I hope your lab report is not due soon!

![](Screen%20Shot%202022-10-14%20at%204.37.38%20PM.png)

If you see text similar to the one in the screenshot, you are not connected to the server!

## **3. Trying Some Commands**
Try different commands on the server! Explore the different directories and try to navigate across different files to see what’s out there.
Here are some commands you can try to get the hang of what is going on:
```
cd ~  
cd  
ls -lat  
ls -a  
ls <directory> where <directory> is /home/linux/ieng6/cs15lfa22/cs15lfa22abc, where the abc is one of the other group members’ username  
cp /home/linux/ieng6/cs15lfa22/public/hello.txt ~/  
cat /home/linux/ieng6/cs15lfa22/public/hello.txt  
```

## **4. Moving Files with scp**
Sometimes you might want to move a file to, or from the server. You can do this with the Secure Copy command, or scp. Simply find the path to the file you would like to transfer, and use the scp command on it. 

For example, try moving some provided .java files from server to your device, compiling it, and then moving it back.
![](Screen%20Shot%202022-10-14%20at%205.17.38%20PM.png)

## **5. Setting an SSH Key**
Having to constantly input your credentials when you interact with the server might become very cumbersome when you have to perform a lot of operations. We can avoid that by setting up our ssh key. 
We can create these keys with the “ssh-keygen” program. Simply run it in your terminal on your device and follow it up with the location of where you want it to go on your device when the prompt asks you about it.

![](Screen%20Shot%202022-10-14%20at%205.35.33%20PM.png)

You will now have both the public and the private key generated. You can now add the public key to the server’s .ssh folder, which will add you to a white list of sorts which will allow you to forgo inputting your credentials every time.

## **6. Optimizing Remote Running**
There are plenty of other things you can do to optimize your experience with remote connection. 

One very useful feature of ssh is that you do not have to remotely connect to the terminal before you put in any commands, but you can instead simply add the command you want to run on a specific server at the end of the ssh command in quotation, and it will automatically run it on that server at once.

You can even separate those commands by semi columbus to package a full list of actions into a single line.
![](Screen%20Shot%202022-10-14%20at%205.37.16%20PM.png)
