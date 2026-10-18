


#over the wire bandit level 00 -> level 05

#bandit level 0 -> level 1

#goal: The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. 

#solotion

1- ssh to the instance by running the command: ssh bandit0@bandit.labs.overthewire.org -p 2220

2- run: ls

3- run: cat readme

4- password is: 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR


------------------------------------------

#bandit level 1 -> level 2

#goal: The password for the next level is stored in a file called - located in the home directory 

#solotion

1- run command ls

2- cat ./-

3- password is: PK8fYLZg2hnHSz83plBL1iEPKdD3QToB

------------------------------------------

#bandit level 2 -> level 3

#goal: The password for the next level is stored in a file called --spaces in this filename-- located in the home directory

#solotion

1- run: ls

2- run: cat ./"--spaces in this filename--"

#note: the ./ we put before executing the cat command is cause the file is starting with -

3- the password is: 7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME

------------------------------------------

#bandit level 3 -> level 4

#goal: The password for the next level is stored in a hidden file in the inhere directory.

#solotion

1- run: ls

2- run: cd inhere/

3- run: ls -la

4- run: cat ...Hiding-From-You

5- the password is: xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq

------------------------------------------

#bandit level 4 -> level 5

#goal: The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

#solotion

1- run: ls

2- run: cd inhere/

3- run: cat ./-file07

4- the password is:6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG