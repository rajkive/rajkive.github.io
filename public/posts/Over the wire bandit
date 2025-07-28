---
author: "Rajshree"
title: "Over the Wire Bandit"
date: "2025-06-18"
draft: false
---

One of the best resources that I've been recommended to learn linux commands is Over the Wire. It's a gamified way to learn different concepts in cybersecurity, one such game is called ***bandit*** which primarily focuses on using different commands to find a text/flag which in our case is the password for next level. 

In order to get started, I had to in through *ssh* with the format username@bandit.overthewire.org on port 2220. 

## Few things to know

This is a simple write-up of levels from 0 to however many I can solve.  I'm giving the answers through my thought process and there is always the case where there are different ways to approach the same question. 

Before you start, there are few things you will need to know, first to use the man page for commands and their arguments. Second, some common commands and arguments to know:
- cat: how view the content in the terminal
- ls -a : to view all the files in a directory, even the hidden ones
- cat ./ : use ./ when dealing with weird file names like "-"
- file : to know the file- type of a particular file

Third, remember that you're not supposed to know everything, that's why research and search around, this way you will learn more!!! 

Also don't forget to keep their website open as they have the description of each level, without it you'll be lost.
## Level 0 --> Level 1
Here we simply had to use the **cat** command to display the text in the file, which contains the password for our next level. 

![l0](/bandit/l0.png)


## Level 1 --> Level 2

Here, I first used the ls -l command to list all the files available, then comes the tricky part. The name of the file is a literal dash, the character "-". As I mentioned earlier, when dealing with such files using the ./ is the best way to go ahead.  The ./ simply means "Look in the current directory."
so the command was something like **./-** and that's it! We got the password for next level.

![l1](/bandit/l1.png)


## Level 2 --> Level 3
In the this level, we're faced with another weird filename, it has spaces in it's name and when you try it, the ./ command won't work and the man page isn't of much help either. This is where the "doing your own research" part comes in. 

The answer is pretty simple, you need to use " " or double quotes.

![l2](/bandit/l2.png)


## Level 3 --> Level 4
This one was a bit tricky for me as you can see in the image. As usual I started using the ls -l command but it did not work, as it's just a long listing format or in other words gives you the mode, number of links, owner, group, size (in bytes), and time of last modification for each file. But ls -a commands is the one which will show you **all** the files. And once you find what you are looking for, simply use the cat command followed by the filename.

![l3](/bandit/l3.png)

## Level 4 --> Level 5
Here they have given a very specific description that the flag is in a human-readable format/filetype only. What this usually means is that we need to find the file type which is in format of "ASCII" characters or text. file command is the way to go for this but there are lot's of file and brute-forcing each one is time consuming and not efficient. Hence we need to parse through the entire directory and for that you need to use the ./* which means "in this directory for all", this will give you an output that looks something like in the image below and you'll have your answer

![l4](/bandit/l4.png)


## Level 5 --> Level 6
This one was a bit tricky as there are multiple ways to find the answer due to the specifications given in the documentation. The method which I used is using the grep method and searching by **du** and **grep** commands with some arguments. As it was given that it has a specific file size, I used du command to search by the file space with -a(all files and not just directories) and -b(bytes) with grep to find the pattern of 1033. And this how I got my answer.

![l5](/bandit/l5.png)


## Level 6 --> Level 7
Here, it's kind of the same as the previous levels. Each file is owned by a user and a group. You can see what user and group owns a file with the ls command and its -l tag. To find the file, we will need to run the command from the root directory so we don't miss anything. I used the command `find / -type f -user bandit7 -group bandit6 -size 33c`  and with a little bit of scrolling, I got the answer. 

```
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c
find: ‘/var/cache/private’: Permission denied
find: ‘/var/cache/apparmor/2425d902.0’: Permission denied
find: ‘/var/cache/apparmor/baad73a1.0’: Permission denied
find: ‘/var/lib/polkit-1’: Permission denied
find: ‘/var/lib/amazon’: Permission denied
/var/lib/dpkg/info/bandit7.password
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/chrony’: Permission denied
find: ‘/var/lib/snapd/void’: Permission denied
find: ‘/var/lib/snapd/cookie’: Permission denied
find: ‘/var/lib/private’: Permission denied
find: ‘/var/lib/ubuntu-advantage/apt-esm/var/lib/apt/lists/partial’: Permission denied


bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

```

I got to know that there is a way to direct the all the error messages/ permission denied message so we don't have to scroll through a lot. You simply need to add `2>/dev/null` at the end of the previous command. It will look something like: 

```
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
```
