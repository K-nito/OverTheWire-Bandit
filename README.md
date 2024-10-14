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

