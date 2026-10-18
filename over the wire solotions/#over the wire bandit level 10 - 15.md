#over the wire bandit level 10 -> level 15

#bandit level 10 -> level 11

#goal: The password for the next level is stored in the file data.txt, which contains base64 encoded data

#solotion

1- base64 -d data.txt

#note: if u vim into data.txt u would see the beginning of the line is VGhl which is a giveaway that this file is 64base also the line ends with == , now the -d is decoding option for the base64 file 

2- the password is: pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro

--------------------------------------------

#bandit level 11 -> level 12

#goal: The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

#solotion

1- run: cat data.txt | tr 'N-ZA-Mn-za-m' 'A-Za-z'

#note: tr cant read files that is why we pass it by cat command and then | into tr. now tr needs two sets for it to work look at the map below:

first set (A-Z):

A B C D E F G H I J K L M N O P Q R S T U V W X Y Z

second set (N-ZA-M):

N O P Q R S T U V W X Y Z A B C D E F G H I J K L M

it is kind of confusing but essentially we are shifting by 13 to get the message now what we gain from this challenge is we can use tr 'set1' 'set2' to translate stuff think of set1 as the thing we want to translate and set2 of what the format we want it to be after translating 

2- the password is: GROozWPO8QyN0mGrjUkID0WCYkZiQxrN 

--------------------------------------------

#bandit level 12 -> level 13

#goal: The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)

#solotion

1- mktemp -d 
#note: we need to make temp directory cause we dont have write permission on data.txt

2- cp data.txt "the temporary directory we just created"
#note: for the cp command to work we need write permission which we have now why dont we use mv? cause for mv to work we need write(w) and execute(x) permission on the directory of the data.txt which we dont btw 
3- run: xxd -r data.txt > output 
#to revert the hex into binary, now we saved it into output cause we need to continue the puzzle of decompressing files thats why 

4- file data.txt 
#to know the file type btw this is a core command to get used to

5- mv data.txt data.bz 
# to make the file executable by bzip2 

7- run: bzip2 -d data6.bz 

6- mv data.txt data.gz 
# to make the file executable by gzip

8- run: gzip -d output.gz

9- output: POSIX tar archive (GNU)
run: tar -xvf output
note# if you see output: POSIX tar archive (GNU) after executing file command we need tar. tar is not like bzip2 and gzip which is compression tool tar is essentially stacking the file now the x= is extracting , v= is verbose which means it will print the names of file as they are being unpacked , the f= file it is important and it must be at the end cause after it comes the file name  

#note: this by far the most challenging level i got too i dont know what will be coming ahead lol so after creating the temp directory and cp and then xdd the file it becomes a repeated procces of running bzip2,gzip,tar until u get the ascii file 

10- The password is qQYQiHOBPR8zR61qxYqX45quvihF2uzk

------------------------------------------------------

#bandit level 13 -> level 14

#goal: The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Look at the commands that logged you into previous bandit levels, and find out how to use the key for this level.
If you need help with this level: a hint file can be found in the home directory.
Make sure to read the error messages as they are informative.

#solotion


1- run: scp -P 2220 bandit13@bandit.labs.overthewire.org:~/sshkey.private ./sshkey.private

#note: we run the command from inside our wsl machine now we scp is (secure copy protocol) we need to specify the port with a capital P unlick ssh with a small p and then the user,url then we end with : to tell that this is the server mention end and then ~ this means from home directory we mention the sshkey.private then ./ means to paste it into my home directory on my wsl and we mention the name we want 

2- run chmod 400 sshkey.private 
#note: this will limit the permission to read-only cause it is a private key and also ssh will not let u connect if the permission is to broad 


------------------------------------------------------

#bandit level 14 -> level 15

#goal: The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

#solotion

1- first we connect to the level by running ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220

note# -i means identy file which is the key we got from the previous level 

2- run: cat /etc/bandit_pass/bandit14 | nc localhost 30000

#note: at first i ran the command nc localhost 30000 then it would wait for ur input which is paste the password from the level but as a devops engineer we used piping and redirection both works i just like piping | so this command is passing the password into the nc localhost 30000. now nc is a utility or a way to transmit data without TSL/SSL (transport secure layer),(secure socaket layer) , since it is a game and we dont need to use secure measures now we just simply make a connection to pass the password into the localhost 30000


3- the password is: pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7

