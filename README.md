Hi! I'm Karthik Rajkumar, and this markdown file is a documentation of the problems I have to solve in order to advance in OverTheWire's Bandit course.

<h2>Level 0</h2>

The 0th level of the Bandit course is a simple one. Log into the bandit remote server via SSH. This was a bit tricky to me since I had no prior experience with SSH (I knew the meaning and purpose it had, but never worked with it). One youtube video later however caught me up to speed and I managed to log in successfully, via OpenSSH on my Windows machine.

![image](https://github.com/user-attachments/assets/7f0585e5-84a2-4b22-b82f-b7aac0209fa5)

<h2>Level 0 -> 1</h2>

Now I had to access level 1, via a password found in level 0. It was contained in a readme text file, and was easy enough to open via the cat command. I had prior experience using bash commands from a Version Control course i took in my 1st year (I don't think I ever completed it though... haha...).

![image](https://github.com/user-attachments/assets/77e19f21-ddd0-46cf-90b9-7bc86e54d636)

<h2>Level 1 -> 2</h2>

After logging into level 2, the password for the next level was contained in a dashed filename. For a character like this, I had to preceded the filename with a './' to open it.

![image](https://github.com/user-attachments/assets/a2723f56-cd23-4437-b5a4-5edc34ee03c6)

<h2>Level 2 -> 3</h2>

Now the password for the next level was contained in a filename with spaces in it! Easily accessed by just wrapping the name in double quotes when using cat.

![image](https://github.com/user-attachments/assets/16ae4a5d-49ee-44e7-9ebc-589f8836ee1d)

<h2>Level 3 -> 4</h2>

Now there was no file but a directory called "inhere". Moving into the aforementioned directory, I found... nothing. It must be a hidden file then, so I used the ls command with the option -a to list all files, including hidden ones. Reading the hidden file, I got the next level's password.

![image](https://github.com/user-attachments/assets/b4973933-bfc6-4841-8c77-b1c78e4ac11b)

<h2>Level 4 -> 5</h2>

Now there was a bunch of files, but only one of them was human-readable text ; the one with the password. I could cat each file, but that would be tedious... so i decided to use the file command, to see what files were of what type!

![image](https://github.com/user-attachments/assets/5608b9c8-310d-4bdb-8fdf-fa9f88bfc426)

<h2>Level 5 -> 6</h2>

Oh wow. Now there were a BUNCH of directories in the inhere directory, and each sub-directory had a bunch of files! However we know the properties of the file that has the password we need : 
1. Human-readable
2. 1033 bytes in size
3. non-executable

So, utilizing the find command, we can get the file we want. Let's try searching for a file of 1033 bytes in size.

![image](https://github.com/user-attachments/assets/59b0e874-b800-475f-9bce-e0163d898aa1)

Bingo.

<h2>Level 6 -> 7</h2>

The instructions said that the password was stored somewhere in the server. So, i used the following command to search for the file. 

![image](https://github.com/user-attachments/assets/8eac1072-503b-4fa1-a8a9-502d76b46fb8)

Let's break this command down.

<b>find / :</b> The command we use the find files. The slash indicates to search the root directory and all sub-directories for the file.

<b>-size 33c :</b> To specify the file we want is 33 bytes in size.

<b>-user bandit7 :</b> To specify the file we want is owned by user bandit7

<b>-group bandit6 :</b> To specify that the file is owned by group bandit6

<b>2>/dev/null :</b> This part of the command re-directs all error outputs to a folder /dev/null, basically a trash folder where data is discarded. This is done so we don't get a mountain of error outputs we have to sift through.

Now, let's execute the command.

![image](https://github.com/user-attachments/assets/964f6ea1-4d03-48e0-b50e-f5f836b4e783)

Nice.

<h2>Level 7 -> 8</h2>

The password for the next level is stored in the file data.txt next to the word millionth. This data.txt has hundreds of lines! We cannot hope to scroll and try to find it, so let's utilize the strings and grep commands.

strings prints out sequences of printable characters in the targeted file, and grep can find us certain sequences according to the pattern we give it.

![image](https://github.com/user-attachments/assets/d51487b6-164a-4d9e-b7c5-f62fd9e4b399)

the '|' in between the two commands is a pipe. Piping allows us to direct outputs of commands into other commands. This means the Sequences of data.txt procured by the strings commands is sent to the grep command, which gives us the sequence with the word "millionth" in it.

<h2>Level 8 -> 9</h2>

The file data.txt in this level has many sequences of characters, any of which could be the password. However, we're told that the password only repeats once! So, lets utilize the sort and uniq commands this time.

sort, sorts the lines of data.txt. We do this because only then will the uniq command work. The uniq -u command returns us only unique lines in a sorted text file.

![image](https://github.com/user-attachments/assets/9980a89e-8e71-4b70-957b-f198435130e3)

<h2>Level 9 -> 10</h2>

Now we have a data.txt again. This time, it's a jumble of readable characters and binary data. We're told that the password is in one of the readable strings, preceded by a number of "=". For this we need to use strings and grep again.

![image](https://github.com/user-attachments/assets/e88c78f5-7594-4124-b13c-6ce5012e4809)

<h2>Level 10 -> 11</h2>

The data.txt file is containing the password. However, it's encoded in base64. So, we need to use the Base64 command, with the -d option for decoding.

![image](https://github.com/user-attachments/assets/c4f9dd7a-5754-409f-9851-8f0725a8200b)

<h2>Level 11 -> 12</h2>

The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions. This is also the principle of ROT13, a cypher that shifts each letter of a sequence by 13 characters. This means if we apply ROT13 twice, we get the original sequence, since the alphabet is 26 characters long.

We can use the tr command here to apply ROT13.

![image](https://github.com/user-attachments/assets/8b085bce-6480-4985-b5d0-212dccaaa8b5)

The tr command can translate characters. Here, tr [a-z] [n-za-m] shifts each character 13 places to the right. If a character is after n, then it is mapped to the second half of the second argument (a-m).

However, it seems I didn't account for the uppercase characters... Let's fix that.

![image](https://github.com/user-attachments/assets/75830b1f-8106-4565-8227-3f6d9fb22cbf)

Alright!

<h2>Level 12 -> 13</h2>

The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed.

First of all, I might have to make a lot files. So I will create a temporary directory under /tmp to not clutter things up.

![image](https://github.com/user-attachments/assets/fd06faeb-dbee-4c55-a567-2e62d6f4d237)

Then, I'll copy the data.txt file to this temporary directory.

![image](https://github.com/user-attachments/assets/14a9a6a0-e64e-47f0-abe0-2cc607829dbf)

Now let's start actually working on this file. First of all, we know it's a hex dump. So we have to revert this hexdump, using the xxd command with the -r option, for reverting, and send the output into a separate file.

![image](https://github.com/user-attachments/assets/2360dac6-91a8-46f6-bd97-8a9dd6dcaffd)

Now we have this mess... Let's see what it actually is, using the file command.

![image](https://github.com/user-attachments/assets/3b1018ce-51b2-4d1f-a304-40266c591176)

It's gzip compressed data. Let's use the gzip command to unzip it, by using the -d option for decompressing. But first, we have to rename the file to have a .gz extension, otherwise gzip can't recognize it as a gzip compressed file.

![image](https://github.com/user-attachments/assets/62eed3e7-9755-41c8-990a-fee4bd13238a)

Alright, now what file type is it this time?

![image](https://github.com/user-attachments/assets/c61ebeb5-9fd6-4462-8c5c-aa5ef68ca9dc)

It's bzip2, another compression method. For bzip2 compressed data, we need to use bzip -d to decompress it. But once again, we have to rename the file to have a .bz2 extension.

![image](https://github.com/user-attachments/assets/6325e496-89d4-4032-9e98-65c164685246)

What file type now? It's gzip again!

![image](https://github.com/user-attachments/assets/3fdbfd5b-ac0f-449b-ac35-dd0f4e583205)

And what type of file do we have now? Gzip? Bzip2? 

![image](https://github.com/user-attachments/assets/372bb9d8-8db8-4dda-ae02-08416ec13d24)

Neither! It's a tar archive. Let's use tar -xf to extract the data from it. The -f is used to force the command, the -x to signify extraction.

![image](https://github.com/user-attachments/assets/9f282185-fd38-4193-8510-4239657e59f7)

From this point onwards, it's gzip, bzip2 and tar archives within each other. For brevity's sake I am simply showing you the remaining commands I've used.

![image](https://github.com/user-attachments/assets/e825b2ee-81d0-481d-b285-ad5f840db7f0)

<h2>Level 13 -> 14</h2>

This time, there's no data.txt... there's a ssh private key. We can log into remote machines with SSH in two ways ; with a password, or with a key. 
So what we have to do here is log into bandit14 with the ssh key instead of a password. 

But first, we need to get that key onto the computer we are using! And for that, we need the scp command.

scp allows us to transfer files over the internet via ssh.

![image](https://github.com/user-attachments/assets/8dd1047e-46d2-41f8-9041-37d833d87faa)

This is the gist of what this command exactly does:

It connects to port 2220 of bandit13@bandit.labs.overthewire.org, and then searches for a file "sshkey.private" to send to a location in my local machine.

We still require the password we found in the previous level to complete the transfer.

Now that we have the key on our local machine, we can log into bandit14 via key authentication.

![image](https://github.com/user-attachments/assets/a67260c9-241a-4d89-a9db-6da837eff5e2)

<h2>Level 14 -> 15</h2>
